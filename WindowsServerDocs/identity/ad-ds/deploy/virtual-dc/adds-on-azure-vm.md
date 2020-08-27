---
title: Установка служб домен Active Directory на виртуальной машине Azure
description: Создание нового Active Directory леса на виртуальной машине в виртуальной машине Azure.
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 04/11/2019
ms.topic: article
ms.openlocfilehash: 98725e194226f048de5bc8332c02ec54c7525ee1
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/26/2020
ms.locfileid: "88940124"
---
# <a name="install-a-new-active-directory-forest-using-azure-cli"></a>Установка нового леса Active Directory с помощью Azure CLI

AD DS могут выполняться на виртуальной машине Azure так же, как и во многих локальных экземплярах. В этой статье описывается развертывание нового леса AD DS на двух новых контроллерах домена в группе доступности Azure с помощью портал Azure и Azure CLI. Многие клиенты считают это руководство полезным при создании лаборатории или подготовке к развертыванию контроллеров домена в Azure.

## <a name="components"></a>Components

* Группа ресурсов для размещения всех элементов.
* [Виртуальная сеть Azure](/azure/virtual-network/virtual-networks-overview.md), подсеть, группа безопасности сети и правило, разрешающие доступ к виртуальным машинам по протоколу RDP.
* [Группа доступности](/azure/virtual-machines/windows/regions-and-availability#availability-sets) виртуальных машин Azure для размещения двух контроллеров домена домен Active Directory служб (AD DS) в.
* Для запуска AD DS и DNS на двух виртуальных машинах Azure.

### <a name="items-that-are-not-covered"></a>Неохваченные элементы

* [Создание VPN-подключения типа "сеть — сеть](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) " из локального расположения
* [Защита сетевого трафика в Azure](/azure/security/azure-security-network-security-best-practices.md)
* [Проектирование топологии сайта](../../plan/designing-the-site-topology.md)
* [Размещение роли хозяина операций планирования](../../plan/planning-operations-master-role-placement.md)
* [Развертывание Azure AD Connect для синхронизации удостоверений в Azure AD](/azure/active-directory/hybrid/how-to-connect-install-express)

## <a name="build-the-test-environment"></a>Создание тестовой среды

Для создания среды используется [портал Azure](https://portal.azure.com) и [Azure CLI](/cli/azure/overview?view=azure-cli-latest) .

Azure CLI используется для создания ресурсов Azure и управления ими из командной строки или с помощью скриптов. В этом руководстве содержатся сведения об использовании Azure CLI для развертывания виртуальных машин под Windows Server 2019. После завершения развертывания подключитесь к серверам и установите AD DS.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free), прежде чем начинать работу.

### <a name="using-azure-cli"></a>Использование Azure CLI

Следующий сценарий автоматизирует процесс создания двух виртуальных машин Windows Server 2019 с целью создания контроллеров домена для нового Active Directory леса в Azure. Администратор может изменить приведенные ниже переменные в соответствии со своими потребностями, а затем завершить их как одну операцию. Скрипт создает необходимую группу ресурсов, группу безопасности сети и правило трафика для удаленный рабочий стол, виртуальной сети и подсети, а также группы доступности. Затем все виртуальные машины создаются с использованием диска данных объемом 20 ГБ с отключенным кэшированием для AD DS для установки.

Приведенный ниже скрипт можно запустить непосредственно из портал Azure. Если вы решили установить и использовать CLI локально, для выполнения инструкций в этом руководстве вам понадобится Azure CLI 2.0.4 или более поздней версии. Чтобы узнать версию, выполните команду `az --version`. Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0](/cli/azure/install-azure-cli?view=azure-cli-latest).

| Имя переменной | Цель |
| :---: | :--- |
| AdminUsername | Имя пользователя, которое должно быть настроено на каждой виртуальной машине в качестве локального администратора. |
| AdminPassword | Пароль с открытым текстом, настроенный для каждой виртуальной машины в качестве пароля локального администратора. |
| ResourceGroupName | Имя, используемое для группы ресурсов. Не следует дублировать существующее имя. |
| Расположение | Имя расположения Azure, в которое вы хотите выполнить развертывание. Вывод списка поддерживаемых регионов для текущей подписки с помощью `az account list-locations` . |
| VNetName | Имя для назначения виртуальной сети Azure не должно дублировать существующее имя. |
| внетаддресс | Область IP-адресов, используемая для сетей Azure. Не должен дублировать существующий диапазон. |
| SubnetName | Имя для назначения IP-подсети. Не следует дублировать существующее имя. |
| субнетаддресс | Адрес подсети для контроллеров домена. Должна быть подсетью в виртуальной сети. |
| Группа доступности | Имя группы доступности, к которой будут присоединяться виртуальные машины контроллера домена. |
| VMSize | Размер стандартной виртуальной машины Azure доступен в расположении для развертывания. |
| датадисксизе | Размер диска данных, на который устанавливается AD DS, в ГБ. |
| DomainController1 | Имя первого контроллера домена. |
| DC1IP | IP-адрес для первого контроллера домена. |
| DomainController2 | Имя второго контроллера домена. |
| DC2IP | IP-адрес для второго контроллера домена. |

```azurecli
#Update based on your organizational requirements
Location=westus2
ResourceGroupName=ADonAzureVMs
NetworkSecurityGroup=NSG-DomainControllers
VNetName=VNet-AzureVMsWestUS2
VNetAddress=10.10.0.0/16
SubnetName=Subnet-AzureDCsWestUS2
SubnetAddress=10.10.10.0/24
AvailabilitySet=DomainControllers
VMSize=Standard_DS1_v2
DataDiskSize=20
AdminUsername=azureuser
AdminPassword=ChangeMe123456
DomainController1=AZDC01
DC1IP=10.10.10.11
DomainController2=AZDC02
DC2IP=10.10.10.12

# Create a resource group.
az group create --name $ResourceGroupName \
                --location $Location

# Create a network security group
az network nsg create --name $NetworkSecurityGroup \
                      --resource-group $ResourceGroupName \
                      --location $Location

# Create a network security group rule for port 3389.
az network nsg rule create --name PermitRDP \
                           --nsg-name $NetworkSecurityGroup \
                           --priority 1000 \
                           --resource-group $ResourceGroupName \
                           --access Allow \
                           --source-address-prefixes "*" \
                           --source-port-ranges "*" \
                           --direction Inbound \
                           --destination-port-ranges 3389

# Create a virtual network.
az network vnet create --name $VNetName \
                       --resource-group $ResourceGroupName \
                       --address-prefixes $VNetAddress \
                       --location $Location \

# Create a subnet
az network vnet subnet create --address-prefix $SubnetAddress \
                              --name $SubnetName \
                              --resource-group $ResourceGroupName \
                              --vnet-name $VNetName \
                              --network-security-group $NetworkSecurityGroup

# Create an availability set.
az vm availability-set create --name $AvailabilitySet \
                              --resource-group $ResourceGroupName \
                              --location $Location

# Create two virtual machines.
az vm create \
    --resource-group $ResourceGroupName \
    --availability-set $AvailabilitySet \
    --name $DomainController1 \
    --size $VMSize \
    --image Win2019Datacenter \
    --admin-username $AdminUsername \
    --admin-password $AdminPassword \
    --data-disk-sizes-gb $DataDiskSize \
    --data-disk-caching None \
    --nsg $NetworkSecurityGroup \
    --private-ip-address $DC1IP \
    --no-wait

az vm create \
    --resource-group $ResourceGroupName \
    --availability-set $AvailabilitySet \
    --name $DomainController2 \
    --size $VMSize \
    --image Win2019Datacenter \
    --admin-username $AdminUsername \
    --admin-password $AdminPassword \
    --data-disk-sizes-gb $DataDiskSize \
    --data-disk-caching None \
    --nsg $NetworkSecurityGroup \
    --private-ip-address $DC2IP

```

## <a name="dns-and-active-directory"></a>DNS и Active Directory

Если виртуальные машины Azure, созданные в рамках этого процесса, будут расширением существующей локальной инфраструктуры Active Directory, перед развертыванием необходимо изменить параметры DNS в виртуальной сети, чтобы они включали локальные DNS-серверы. Этот шаг важен, чтобы позволить вновь созданным контроллерам домена в Azure Разрешать локальные ресурсы и выполнять репликацию. Дополнительные сведения о DNS, Azure и настройке параметров можно найти в разделе [разрешение имен разделов, использующих собственный DNS-сервер](/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#name-resolution-that-uses-your-own-dns-server).

После повышения уровня новых контроллеров домена в Azure им необходимо назначить основной и дополнительный DNS-серверы для виртуальной сети, а все локальные DNS-серверы будут понижены до третьего и более поздних. Дополнительные сведения об изменении DNS-серверов можно найти в статье [Создание, изменение и удаление виртуальной сети](/azure/virtual-network/manage-virtual-network#change-dns-servers).

Сведения о расширении локальной сети в Azure можно найти в статье [Создание VPN-подключения типа "сеть — сеть](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)".

## <a name="configure-the-vms-and-install-active-directory-domain-services"></a>Настройка виртуальных машин и установка служб домен Active Directory

После завершения выполнения скрипта перейдите к [портал Azure](https://portal.azure.com), а затем — к **виртуальным машинам**.

### <a name="configure-the-first-domain-controller"></a>Настройка первого контроллера домена

Подключитесь к AZDC01 с помощью учетных данных, указанных в сценарии.

* Инициализируйте и отформатируйте диск данных как F:
   * Откройте меню "Пуск" и выберите " **Управление компьютером** ".
   * Переход к **Storage**  >  **управлению дисками** хранилища
   * Инициализация диска как MBR
   * Создайте новый простой том и назначьте букву диска F: при желании можно указать метку тома.
* Установка домен Active Directory служб с помощью диспетчер сервера
* Повышение уровня контроллера домена как первого в новом лесу
   * На странице "параметры контроллера домена" оставьте установленный сервер службы доменных имен (DNS) и глобальный каталог (GC).
   * Укажите пароль режима восстановления служб каталогов в соответствии с требованиями Организации
   * Измените пути с C: так, чтобы они указывали на диск F:, созданный при появлении запроса на расположение.
   * Проверьте выбор, сделанный в мастере, и нажмите кнопку **Далее** .

> [!NOTE]
> Проверка предварительных требований выдаст предупреждение о том, что физическому сетевому адаптеру не назначены статические IP-адреса, вы можете спокойно проигнорировать его, так как в виртуальной сети Azure назначены статические адреса.

* Выбор **установки**

Когда мастер завершит процесс установки, виртуальная машина перезагружается.

После завершения перезагрузки виртуальной машины Войдите в систему с использованием учетных данных, которые использовались ранее, но на этот раз как член созданного домена.

   > [!NOTE]
   > Первый вход в систему после повышения роли контроллера домена может занять больше времени, чем обычная, и это нормально. Возьмите кружки в чай, кафе, воды или другие напитки по своему усмотрению.

[Виртуальные сети Azure теперь поддерживают IPv6](/azure/virtual-network/virtual-networks-faq#do-vnets-support-ipv6) , но если вы хотите установить для виртуальных машин предпочитаемый протокол IPv4 по протоколу IPv6, сведения о том, как выполнить эту задачу, можно найти в статье базы знаний [руководство по настройке IPv6 в Windows для опытных пользователей](https://support.microsoft.com/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users).

### <a name="configure-the-second-domain-controller"></a>Настройка второго контроллера домена

Подключитесь к AZDC02 с помощью учетных данных, указанных в сценарии.

* Инициализируйте и отформатируйте диск данных как F:
   * Откройте меню "Пуск" и выберите " **Управление компьютером** ".
   * Переход к **Storage**  >  **управлению дисками** хранилища
   * Инициализация диска как MBR
   * Создайте новый простой том и назначьте букву диска F: (при желании можно указать метку тома).
* Установка домен Active Directory служб с помощью диспетчер сервера
* Повышение уровня контроллера домена
   * Добавление контроллера домена в существующий домен — CONTOSO.com
   * Укажите учетные данные для выполнения операции
   * Измените пути с C: так, чтобы они указывали на диск F:, созданный при появлении запроса на расположение.
   * Проверка сервера доменных имен (DNS) и глобального каталога (GC) на странице параметров контроллера домена
   * Укажите пароль режима восстановления служб каталогов в соответствии с требованиями Организации
   * Проверьте выбор, сделанный в мастере, и нажмите кнопку **Далее** .

> [!NOTE]
> Проверка предварительных требований выдаст предупреждение о том, что для физического сетевого адаптера не назначены статические IP-адреса. Вы можете спокойно проигнорировать это, так как статические IP-адреса назначены в виртуальной сети Azure.

* Выбор **установки**

Когда мастер завершит процесс установки, виртуальная машина перезагружается.

После завершения перезагрузки виртуальной машины Войдите в систему с использованием учетных данных, которые использовались ранее, но на этот раз как член домена CONTOSO.com.

[Виртуальные сети Azure теперь поддерживают IPv6](/azure/virtual-network/virtual-networks-faq#do-vnets-support-ipv6) , но если вы хотите установить для виртуальных машин предпочитаемый протокол IPv4 по протоколу IPv6, сведения о том, как выполнить эту задачу, можно найти в статье базы знаний [руководство по настройке IPv6 в Windows для опытных пользователей](https://support.microsoft.com/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users).

### <a name="configure-dns"></a>Настройка DNS

После повышения уровня новых контроллеров домена в Azure им необходимо назначить основной и дополнительный DNS-серверы для виртуальной сети, а все локальные DNS-серверы будут понижены до третьего и более поздних. Дополнительные сведения об изменении DNS-серверов можно найти в статье [Создание, изменение и удаление виртуальной сети](/azure/virtual-network/manage-virtual-network#change-dns-servers).

### <a name="wrap-up"></a>Заключение

На этом этапе среда имеет пару контроллеров домена, и мы настроили виртуальную сеть Azure, чтобы дополнительные серверы можно было добавить в среду. Задачи, выполняемые после установки служб домен Active Directory, например настройка сайтов и служб, аудит, резервное копирование и обеспечение безопасности встроенной учетной записи администратора, должны быть завершены на этом этапе.

## <a name="removing-the-environment"></a>Удаление среды

Чтобы удалить среду, после завершения тестирования созданная ранее группа ресурсов может быть удалена. На этом шаге удаляются все компоненты, которые являются частью этой группы ресурсов.

### <a name="remove-using-the-azure-portal"></a>Удалить с помощью портал Azure

В портал Azure перейдите к группе **ресурсов** и выберите созданную группу ресурсов (в нашем примере это адоназуревмс), а затем выберите **Удалить группу ресурсов**. Процесс запрашивает подтверждение перед удалением всех ресурсов, содержащихся в группе ресурсов.

### <a name="remove-using-the-azure-cli"></a>Удалить с помощью Azure CLI

В Azure CLI выполните следующую команду:

```azurecli
az group delete --name ADonAzureVMs
```

## <a name="next-steps"></a>Дальнейшие действия

* [Безопасная виртуализация доменных служб Active Directory (AD DS)](../../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)
* [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect-get-started-express)
* [Резервное копирование и восстановление](/azure/virtual-machines/windows/backup-recovery)
* [VPN-подключение типа "сеть — сеть"](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [Мониторинг](/azure/virtual-machines/windows/monitor)
* [Безопасность и политика](/azure/virtual-machines/windows/security-policy)
* [Обслуживание и обновления](/azure/virtual-machines/windows/maintenance-and-updates)
