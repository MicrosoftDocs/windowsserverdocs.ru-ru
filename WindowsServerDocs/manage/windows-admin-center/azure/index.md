---
title: Подключение Windows Server к гибридным службам Azure
description: Вы можете полностью или частично перенести локальные развертывания Windows Server в облако с помощью гибридных служб Azure.
ms.technology: manage
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 05/31/2019
ms.openlocfilehash: b82d2eaa9283d99993102f1656262e2eda86cfff
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "79323326"
---
# <a name="connecting-windows-server-to-azure-hybrid-services"></a>Подключение Windows Server к гибридным службам Azure

Вы можете полностью или частично перенести локальные развертывания Windows Server в облако с помощью гибридных служб Azure. В этих облачных службах предоставляется ряд полезных функций для переноса локальных ресурсов в Azure и централизованного управления с помощью Azure.

![Схема со стрелками, обозначающими перенос локальных ресурсов в Azure и централизованное управление с помощью Azure](../media/azure-services/hybrid-framing.png)

Используя гибридные службы Azure в Windows Admin Center, вы можете выполнять такие задачи:

- [защита виртуальных машин, использование облачного резервного копирования и аварийного восстановления (HA/DR)](#back-up-and-protect-your-on-premises-servers-and-vms);  
- [увеличение локальной емкости с помощью хранилища и вычислительных ресурсов в Azure, а также упрощение сетевого подключения к Azure](#extend-on-premises-capacity-with-azure);
- [централизованный мониторинг, администрирование, настройка и защита приложений, сети и инфраструктуры с помощью облачных служб Azure для управления](#centrally-manage-your-hybrid-environment-from-azure).  

Большинство гибридных служб Azure можно установить, скачав приложение и выполнив вручную некоторые настройки. Но многие службы интегрированы непосредственно в Windows Admin Center, что упрощает их установку и обеспечивает серверное представление служб. В Windows Admin Center также предоставляются удобные интеллектуальные гиперссылки на портал Azure. Они позволяют просматривать данные о подключенных ресурсах Azure и использовать централизованное представление гибридной среды.

## <a name="discover-integrated-services-in-the-azure-hybrid-services-tool"></a>Поиск интегрированных служб в средстве для работы с гибридными службами Azure

Средство для работы с гибридными службами Azure в [Windows Admin Center](../overview.md) объединяет все интегрированные службы Azure в единый центр, в котором можно легко определить все доступные службы Azure, которые повышают эффективность вашей локальной или гибридной среды.  

![Снимок экрана Windows Admin Center, на котором показано средство для работы с гибридными службами Azure](../media/azure-services/ahs-discover.png)

Если вы подключаетесь к серверу, на котором уже включены службы Azure, средство для работы с гибридными службами Azure выполняет роль единой консоли для просмотра всех включенных служб на этом сервере. Вы можете легко получить доступ к соответствующему инструменту в Windows Admin Center, перейти на портал Azure для более детального управления этими службами Azure или ознакомиться с дополнительной документацией.  

![Снимок экрана Windows Admin Center, на котором показаны службы Azure, уже установленные на сервере](../media/azure-services/ahs-dayN.png)

Средство для работы с гибридными службами Azure предоставляет следующие возможности:

- резервное копирование Windows Server из Windows Admin Center с [помощью службы Azure Backup](azure-backup.md);
- защита виртуальных машин Hyper-V из Windows Admin Center с помощью [Azure Site Recovery](azure-site-recovery.md);
- синхронизация файлового сервера с облаком при помощи функции [Синхронизация файлов Azure](azure-file-sync.md);
- управление обновлениями операционной системы для всех серверов Windows как в локальной среде, так и в облаке с помощью службы [Управление обновлениями Azure](azure-update-management.md);
- мониторинг серверов в локальной среде или в облаке и настройка оповещений с помощью [Azure Monitor](azure-monitor.md);
- применение политик управления к локальным серверам с помощью Политики Azure и [Azure Arc для серверов](https://docs.microsoft.com/azure/azure-arc/servers/overview);
- защита серверов и расширенная защита от угроз с помощью [Центра безопасности Azure](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration);
- подключение локальных серверов к виртуальной сети Azure с помощью [сетевого адаптера Azure](https://aka.ms/WACNetworkAdapter).
- применение структуры локальной сети к виртуальным машинам Azure с помощью [расширенной сети Azure](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409).

## <a name="back-up-and-protect-your-on-premises-servers-and-vms"></a>Резервное копирование и защита локальных серверов и виртуальных машин

- **Резервное копирование серверов Windows Server с помощью службы [Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview)**  
Резервное копирование серверов Windows Server в Azure поможет вам обеспечить защиту от случайного или злонамеренного удаления и повреждения данных, а также от программ-шантажистов.  
Дополнительные сведения см. в статье о [резервном копирование серверов с помощью службы Azure Backup](azure-backup.md).

- **Защита виртуальных машин Hyper-V с помощью [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)**  
Вы можете реплицировать рабочие нагрузки, выполняемые на виртуальных машинах, чтобы защитить важную для предприятия инфраструктуру в случае сбоя. Windows Admin Center упрощает процесс настройки и репликации виртуальных машин на серверах или в кластерах Hyper-V, позволяя без лишних усилий повысить устойчивость используемой среды с помощью службы аварийного восстановления Azure Site Recovery.  
Дополнительные сведения см. в статье о [защите виртуальных машин с помощью Azure Site Recovery и Windows Admin Center](azure-site-recovery.md).

- **Использование синхронной или асинхронной репликации на основе блоков для виртуальной машины в Azure с помощью [реплики хранилища](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-overview)**  
Вы можете настроить репликацию на основе блоков или томов между серверами, выполняя репликацию хранилища на сервер-получатель или виртуальную машину. С помощью Windows Admin Center вы можете создать виртуальную машину Azure, предназначенную для целевого объекта репликации, а также выбрать нужные размеры и правильно настроить хранилище на новой виртуальной машине Azure.  
См. сведения о [межсерверной репликации с использованием реплики хранилища](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-ui).  

## <a name="extend-on-premises-capacity-with-azure"></a>Увеличение локальной емкости с помощью Azure

### <a name="extend-storage-capacity"></a>Увеличение емкости хранилища

- **Синхронизация файлового сервера с облаком с помощью [Синхронизации файлов Azure](https://aka.ms/afs)**  
Синхронизируйте файлы на этом сервере с общими папками Azure. Сохраняйте все свои файлы локально или используйте распределение между уровнями в облаке для освобождения места, и кэшируйте только самые используемые файлы на сервере, размещая холодные данные в облачном хранилище. Используя возможность резервного копирования данных в облаке, можно не беспокоиться о резервном копировании данных на локальном сервере. Кроме того, благодаря многосайтовой синхронизации можно синхронизировать набор файлов на нескольких серверах.
См. сведения о [синхронизации файлового сервера с облаком с помощью Синхронизации файлов Azure](azure-file-sync.md).

- **Перенос хранилища на виртуальную машину в Azure с помощью [службы миграции хранилища](https://docs.microsoft.com/windows-server/storage/storage-migration-service/overview)**  
Используйте средство согласно пошаговым инструкциям, чтобы получить доступ к данным инвентаризации на серверах Windows и Linux и перенести эти данные на новую виртуальную машину Azure. С помощью Windows Admin Center вы можете создать виртуальную машину Azure для определенного задания, правильно настроив размер и параметры для получения данных с исходного сервера.  
См. сведения об [использовании службы миграции хранилища для переноса сервера](https://docs.microsoft.com/windows-server/storage/storage-migration-service/migrate-data).

### <a name="extend-compute-capacity"></a>Увеличение емкости вычислительных ресурсов

- **Создание виртуальной машины Azure в Windows Admin Center**  
В Windows Admin Center на странице *Все подключения* щелкните **Добавить** и **Создать** в разделе **Виртуальная машина Azure**. В этом пошаговом средстве создания вы даже можете присоединить виртуальную машину Azure к домену и настроить хранилище.

- **Использование Azure для достижения кворума на отказоустойчивом кластере с помощью [облака-свидетеля](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)**  
Чтобы не инвестировать в дополнительное оборудование для достижения кворума на кластере с двумя узлами, можете использовать учетную запись хранения Azure в качестве кластера-свидетеля для кластера Azure Stack HCI или другого отказоустойчивого кластера.  
Дополнительные сведения см. в статье [Развертывание облака-свидетеля для отказоустойчивого кластера](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness).  

### <a name="simplify-network-connectivity-between-your-on-premises-and-azure-networks"></a>Упрощение сетевого подключения между локальной сетью и сетью Azure

- **Подключение локальных серверов к виртуальной сети Azure с помощью [сетевого адаптера Azure](https://aka.ms/WACNetworkAdapter)**  
Используйте Windows Admin Center, чтобы упростить настройку VPN-подключения "точка — сеть" между локальным сервером и виртуальной сетью Azure.  

- **Применение структуры локальной сети к виртуальным машинам Azure с помощью [расширенной сети Azure](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409)**  
С помощью Windows Admin Center вы можете настроить VPN-подключение "сеть — сеть" и перенести локальные IP-адреса в виртуальную сеть Azure, чтобы упростить миграцию рабочих нагрузок в Azure без нарушения зависимостей от IP-адресов.

## <a name="centrally-manage-your-hybrid-environment-from-azure"></a>Централизованное управление гибридной средой в Azure

- **Мониторинг и получение оповещений по электронной почте для всех серверов в среде с помощью [Azure Monitor для виртуальных машин](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)**  
Служба Azure Monitor (другое название — Virtual Machines Insights) позволяет отслеживать работоспособность и события сервера, создавать оповещения по электронной почте, получить комплексное представление о производительности сервера в вашей среде и визуализировать приложения, системы и службы, подключенные к конкретному серверу. В Windows Admin Center также можно настроить отправку на электронную почту оповещений по умолчанию о событиях, связанных с работоспособностью сервера и кластера.  
Дополнительные сведения см. в статье о том, как [подключить серверы к Azure Monitor и настроить уведомления по электронной почте](azure-monitor.md).

- **Централизованное управление обновлениями операционной системы для всех серверов Windows Server с помощью службы [Управление обновлениями Azure](https://docs.microsoft.com/azure/automation/automation-update-management)**  
Вы можете управлять обновлениями и исправлениями для нескольких серверов и виртуальных машин централизованно, а не на каждом из серверов. С помощью службы "Управление обновлениями Azure" можно быстро оценить состояние доступных обновлений, запланировать установку необходимых обновлений и проверить результаты развертывания, чтобы убедиться, что обновления применены успешно. При этом неважно, где размещены ваши серверы — на виртуальных машинах Azure, у других поставщиков облачных служб или в локальной среде.  
Дополнительные сведения см. в статье о [настройке серверов для службы "Управление обновлениями Azure"](azure-update-management.md).

- **Усиленная защита и расширенная защита от угроз с помощью [Центра безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)**  
Центр безопасности Azure — это единая система управления безопасностью инфраструктуры, которая усиливает защиту центров обработки данных и обеспечивает расширенную защиту от угроз для гибридных рабочих нагрузок в облаке Azure, другом облаке или локальной среде. С помощью Windows Admin Center вы можете без труда настроить и подключить свои серверы к Центру безопасности Azure.  
См. сведения об [интеграции Центра безопасности Azure с Windows Admin Center (предварительная версия)](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration).  

- **Применение политик и обеспечение соответствия требованиям в гибридной среде с помощью [Azure Arc для серверов](https://docs.microsoft.com/azure/azure-arc/servers/overview) и [Политики Azure](https://docs.microsoft.com/azure/governance/policy/overview)**  
Выполняйте инвентаризацию, упорядочение и администрирование локальных серверов в Azure. Вы можете управлять серверами с помощью Политики Azure, контролировать доступ с помощью RBAC и включать дополнительные службы управления в Azure.  

## <a name="clusters-versus-stand-alone-servers-and-vms"></a>Сравнение кластеров с изолированными серверами и виртуальными машинами

Гибридные службы Azure работают с серверами Windows Server в следующих конфигурациях:

- изолированные физические серверы и виртуальные машины;
- кластеры, в том числе гиперконвергентные кластеры, сертифицированные в рамках программ [Azure Stack HCI](../../../azure-stack-hci/index.md) и [Windows Server Software-Defined (WSSD)](https://www.microsoft.com/cloud-platform/software-defined-datacenter).

### <a name="services-for-stand-alone-servers-and-vms"></a>Службы для изолированных серверов и виртуальных машин

Это полный список служб Azure, которые предоставляют функциональные возможности для изолированных серверов и виртуальных машин:

- резервное копирование Windows Server из Windows Admin Center с [помощью службы Azure Backup](azure-backup.md);
- защита виртуальных машин Hyper-V из Windows Admin Center с помощью [Azure Site Recovery](azure-site-recovery.md);
- синхронизация файлового сервера с облаком при помощи функции [Синхронизация файлов Azure](azure-file-sync.md);
- управление обновлениями операционной системы для всех серверов Windows как в локальной среде, так и в облаке с помощью службы [Управление обновлениями Azure](azure-update-management.md);
- мониторинг серверов в локальной среде или в облаке и настройка оповещений с помощью [Azure Monitor](azure-monitor.md);
- применение политик управления к локальным серверам с помощью Политики Azure и [Azure Arc для серверов](https://docs.microsoft.com/azure/azure-arc/servers/overview);
- защита серверов и расширенная защита от угроз с помощью [Центра безопасности Azure](https://docs.microsoft.com/azure/security-center/windows-admin-center-integration);
- подключение локальных серверов к виртуальной сети Azure с помощью [сетевого адаптера Azure](https://aka.ms/WACNetworkAdapter).
- применение структуры локальной сети к виртуальным машинам Azure с помощью [расширенной сети Azure](https://go.microsoft.com/fwlink/?linkid=2109517&clcid=0x409).

### <a name="services-for-clusters"></a>Службы кластеров

Следующие службы Azure обеспечивают комплексную поддержку функций кластеров:

- [Мониторинг гиперконвергентного кластера с помощью Azure Monitor](../../../storage/storage-spaces/configure-azure-monitor.md)
- [Защита виртуальных машин с помощью Azure Site Recovery](azure-site-recovery.md)
- [Развертывание облака-свидетеля для кластера](../../../failover-clustering/deploy-cloud-witness.md)  

## <a name="other-azure-integrated-abilities-of-windows-admin-center"></a>Другие возможности Windows Admin Center, обеспечиваемые интеграцией с Azure

- **[Добавление подключений виртуальных машин Azure](manage-azure-vms.md) в Windows Admin Center**  
С помощью Windows Admin Center можно управлять как виртуальными машинами Azure, так и локальными компьютерами. Настроив в шлюзе Windows Admin Center подключение к виртуальной сети Azure, можно управлять виртуальными машинами в Azure с помощью простых совместимых инструментов, предоставляемых в Windows Admin Center.  
Дополнительные сведения см. в статье о [настройке Windows Admin Center для управления виртуальными машинами в Azure](manage-azure-vms.md).

- **Добавление уровня безопасности для Windows Admin Center в виде проверки подлинности [Azure Active Directory (Azure AD)](https://azure.microsoft.com/services/active-directory/)**  
Вы можете добавить еще один уровень безопасности для Windows Admin Center, настроив для пользователей, которым требуется доступ к шлюзу, обязательную проверку подлинности с помощью удостоверения Azure Active Directory (Azure AD). Проверка подлинности Azure AD также позволяет воспользоваться такими функциями безопасности Azure AD, как условный доступ и многофакторная проверка подлинности.  
См. сведения о [настройке аутентификации Azure AD для Windows Admin Center](../configure/user-access-control.md#azure-active-directory).  

- **Управление ресурсами Azure непосредственно через [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) из Windows Admin Center**  
Используйте Azure Cloud Shell, чтобы получить возможности Bash или PowerShell в Windows Admin Center и обеспечить простой доступ к задачам управления Azure.  
См. сведения об [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).


## <a name="see-also"></a>См. также статью

- [Подключение Windows Admin Center к Azure](azure-integration.md)
- [Развертывание Windows Admin Center в Azure](deploy-wac-in-azure.md)
