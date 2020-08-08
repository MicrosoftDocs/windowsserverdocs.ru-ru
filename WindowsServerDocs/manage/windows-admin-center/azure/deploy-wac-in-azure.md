---
title: Развертывание шлюза центра администрирования Windows в Azure
description: Развертывание шлюза центра администрирования Windows в Azure
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: b4ae232d47398800ecae8500cff6726128f22b83
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971991"
---
# <a name="deploy-windows-admin-center-in-azure"></a>Развертывание Windows Admin Center в Azure

## <a name="deploy-using-script"></a>Развертывание с помощью скрипта

Вы можете скачать [Deploy-WACAzVM.ps1](https://aka.ms/deploy-wacazvm) , которые будут запускаться из [Azure Cloud Shell](https://shell.azure.com) , чтобы настроить шлюз центра администрирования Windows в Azure. Этот сценарий может создать всю среду, включая группу ресурсов.

[Переход к шагам по развертыванию вручную](#deploy-manually-on-an-existing-azure-virtual-machine)

### <a name="prerequisites"></a>Предварительные требования

* Настройте учетную запись в [Azure Cloud Shell](https://shell.azure.com). Если вы впервые используете Cloud Shell, вам будет предложено связать или создать учетную запись хранения Azure с Cloud Shell.
* В Cloud Shell **PowerShell** перейдите к домашнему каталогу:```PS Azure:\> cd ~```
* Чтобы передать ```Deploy-WACAzVM.ps1``` файл, перетащите его с локального компьютера в любое место в окне Cloud Shell.

При указании собственного сертификата:

* Отправьте сертификат в [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis). Сначала создайте хранилище ключей на портале Azure, а затем отправьте сертификат в хранилище ключей. Кроме того, для создания сертификата можно использовать портал Azure.

### <a name="script-parameters"></a>Параметры скрипта

* **ResourceGroupName** -[строка] указывает имя группы ресурсов, в которой будет создана виртуальная машина.

* **Name** -[строка] указывает имя виртуальной машины.

* **Credential** -[PSCredential] указывает учетные данные для виртуальной машины.

* **Мсипас** -[строка] задает локальный путь к MSI-файлу центра администрирования Windows при развертывании центра администрирования Windows на существующей виртуальной машине. По умолчанию используется версия из, если она не https://aka.ms/WACDownload указана.

* **VaultName** -[строка] указывает имя хранилища ключей, которое содержит сертификат.

* **CertName** -[строка] указывает имя сертификата, используемого для установки MSI.

* **Женератесслцерт** -[Switch] true, если MSI должен создавать самозаверяющий SSL-сертификат.

* **Номер_порта** -[int] указывает номер порта SSL для службы центра администрирования Windows. По умолчанию имеет значение 443, если не указано.

* **Опенпортс** -[int []] указывает открытые порты для виртуальной машины.

* **Location** — [строка] указывает расположение виртуальной машины.

* **Size** -[строка] задает размер виртуальной машины. По умолчанию используется значение "Standard_DS1_v2", если не указано.

* **Image** -[строка] указывает образ виртуальной машины. По умолчанию используется значение "Win2016Datacenter", если не указано.

* **VirtualNetworkName** -[строка] указывает имя виртуальной сети для виртуальной машины.

* **SubnetName** -[строка] указывает имя подсети для виртуальной машины.

* **Секуритиграупнаме** -[строка] указывает имя группы безопасности для виртуальной машины.

* **ПублиЦипаддресснаме** -[строка] указывает имя общедоступного IP-адреса виртуальной машины.

* **Инсталлваконли** -[Switch] задайте значение true, если ВАК должен быть установлен на уже существующей виртуальной машине Azure.

Существует два разных варианта развертывания MSI и сертификат, используемый для установки MSI. MSI может быть скачан из aka.ms/WACDownload или при развертывании на существующей виртуальной машине можно предоставить путь к файлу MSI локально на виртуальной машине. Сертификат можно найти либо в Azure Key Vault, либо в виде самозаверяющего сертификата, который будет создан MSI.

### <a name="script-examples"></a>Примеры сценариев

Сначала определите общие переменные, необходимые для параметров скрипта.

```PowerShell
$ResourceGroupName = "wac-rg1"
$VirtualNetworkName = "wac-vnet"
$SecurityGroupName = "wac-nsg"
$SubnetName = "wac-subnet"
$VaultName = "wac-key-vault"
$CertName = "wac-cert"
$Location = "westus"
$PublicIpAddressName = "wac-public-ip"
$Size = "Standard_D4s_v3"
$Image = "Win2016Datacenter"
$Credential = Get-Credential
```

#### <a name="example-1-use-the-script-to-deploy-wac-gateway-on-a-new-vm-in-a-new-virtual-network-and-resource-group-use-the-msi-from-akamswacdownload-and-a-self-signed-cert-from-the-msi"></a>Пример 1. Использование скрипта для развертывания шлюза ВАК на новой виртуальной машине в новой виртуальной сети и группе ресурсов. Используйте MSI из aka.ms/WACDownload и самозаверяющий сертификат из MSI.

```PowerShell
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm1"
    Credential = $Credential
    VirtualNetworkName = $VirtualNetworkName
    SubnetName = $SubnetName
    GenerateSslCert = $true
}
./Deploy-WACAzVM.ps1 @scriptParams
```

#### <a name="example-2-same-as-1-but-using-a-certificate-from-azure-key-vault"></a>Пример 2. то же, что и #1, но с использованием сертификата из Azure Key Vault.

```PowerShell
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm2"
    Credential = $Credential
    VirtualNetworkName = $VirtualNetworkName
    SubnetName = $SubnetName
    VaultName = $VaultName
    CertName = $CertName
}
./Deploy-WACAzVM.ps1 @scriptParams
```

#### <a name="example-3-using-a-local-msi-on-an-existing-vm-to-deploy-wac"></a>Пример 3. Использование локального MSI-файла на существующей виртуальной машине для развертывания ВАК.

```PowerShell
$MsiPath = "C:\Users\<username>\Downloads\WindowsAdminCenter<version>.msi"
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm3"
    Credential = $Credential
    MsiPath = $MsiPath
    InstallWACOnly = $true
    GenerateSslCert = $true
}
./Deploy-WACAzVM.ps1 @scriptParams
```

### <a name="requirements-for-vm-running-the-windows-admin-center-gateway"></a>Требования к виртуальной машине, на которой работает шлюз центра администрирования Windows

Порт 443 (HTTPS) должен быть открыт.
Используя те же переменные, определенные для сценария, можно использовать приведенный ниже код в Azure Cloud Shell для обновления группы безопасности сети.

```powershell
$nsg = Get-AzNetworkSecurityGroup -Name $SecurityGroupName -ResourceGroupName $ResourceGroupName
$newNSG = Add-AzNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name ssl-rule -Description "Allow SSL" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 443
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $newNSG
```

### <a name="requirements-for-managed-azure-vms"></a>Требования к управляемой виртуальной машине Azure

Порт 5985 (WinRM через HTTP) должен быть открыт и иметь активный прослушиватель.
Вы можете использовать приведенный ниже код в Azure Cloud Shell для обновления управляемых узлов. ```$ResourceGroupName```и ```$Name``` используют те же переменные, что и скрипт развертывания, но необходимо использовать ```$Credential``` конкретные для УПРАВЛЯЕМОЙ виртуальной машины.

```powershell
Enable-AzVMPSRemoting -ResourceGroupName $ResourceGroupName -Name $Name
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any} -Credential $Credential
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {winrm create winrm/config/Listener?Address=*+Transport=HTTP} -Credential $Credential
```

## <a name="deploy-manually-on-an-existing-azure-virtual-machine"></a>Развертывание вручную на существующей виртуальной машине Azure

Перед установкой центра администрирования Windows на требуемой виртуальной машине шлюза Установите SSL-сертификат, который будет использоваться для связи по протоколу HTTPS, или используйте самозаверяющий сертификат, созданный центром администрирования Windows. Однако при попытке подключения из браузера будет выдано предупреждение, если выбрать второй вариант. Чтобы обойти это предупреждение в границе, щелкните **сведения > перейти на веб-страницу** или в Chrome, выбрав **Дополнительно > перейдите к [веб-страница]**. Рекомендуется использовать самозаверяющие сертификаты только для тестовых сред.

> [!NOTE]
> Эти инструкции предназначены для установки в Windows Server с возможностями рабочего стола, а не для установки Server Core.

1. [Скачайте центр администрирования Windows](https://aka.ms/windowsadmincenter) на локальный компьютер.

2. Установите подключение к виртуальной машине по удаленному рабочему столу, а затем скопируйте MSI с локального компьютера и вставьте его в ВИРТУАЛЬную машину.

3. Дважды щелкните MSI-файл, чтобы начать установку, и следуйте инструкциям мастера. Обратите внимание на такие моменты:

   - По умолчанию установщик использует рекомендованный порт 443 (HTTPS). Если вы хотите выбрать другой порт, обратите внимание, что этот порт также необходимо открыть в брандмауэре.

   - Если на виртуальной машине уже установлен SSL-сертификат, убедитесь, что выбран этот параметр, и введите отпечаток.

4. Запустите службу центра администрирования Windows (запустите C:/Program Files/Windows Admin Center/sme.exe).

[Дополнительные сведения о развертывании центра администрирования Windows.](../deploy/install.md)

### <a name="configure-the-gateway-vm-to-enable-https-port-access"></a>Настройте виртуальную машину шлюза, чтобы разрешить доступ к портам HTTPS:

1. Перейдите к виртуальной машине в портал Azure и выберите **сети**.

2. Выберите **Добавить правило входящего трафика** и выберите **HTTPS** в разделе **Служба**.

> [!NOTE]
> Если выбран порт, отличный от 443 по умолчанию, выберите **Настраиваемый** в разделе Служба и введите порт, выбранный на шаге 3 в разделе **диапазоны портов**.

### <a name="accessing-a-windows-admin-center-gateway-installed-on-an-azure-vm"></a>Доступ к шлюзу центра администрирования Windows, установленному на виртуальной машине Azure

На этом этапе вы можете получить доступ к центру администрирования Windows из современного браузера (ребра или Chrome) на локальном компьютере, перейдя к DNS-имени виртуальной машины шлюза.

> [!NOTE]
> Если вы выбрали порт, отличный от 443, вы можете получить доступ к центру администрирования Windows, перейдя по \<DNS name of your VM\> адресу https://:\<custom port\>

При попытке доступа к центру администрирования Windows браузер запрашивает учетные данные для доступа к виртуальной машине, на которой установлен центр администрирования Windows. Здесь необходимо ввести учетные данные, которые входят в локальную группу "Пользователи" или "Локальные администраторы" виртуальной машины.

Чтобы добавить другие виртуальные машины в виртуальной сети, убедитесь, что служба удаленного управления Windows выполняется на целевых виртуальных машинах, выполнив следующую команду в PowerShell или в командной строке на целевой виртуальной машине:`winrm quickconfig`

Если вы еще не присоединились к доменной виртуальной машине Azure, виртуальная машина ведет себя как сервер в Рабочей группе, поэтому необходимо убедиться, что учетная запись [используется в качестве центра администрирования Windows в Рабочей группе](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup).