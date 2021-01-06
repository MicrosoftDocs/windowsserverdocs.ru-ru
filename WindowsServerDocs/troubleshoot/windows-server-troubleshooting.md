---
title: Устранение неполадок Windows Server
description: Ссылки на статьи по устранению неполадок, связанных с Windows Server
ms.date: 1/24/2020
author: kaushika-msft
ms.author: kaushika
ms.topic: troubleshooting
ms.openlocfilehash: d438f8c2a0e17e13e01c198a55c7dfd3f234da14
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97949660"
---
# <a name="troubleshooting-windows-server-components"></a>Устранение неполадок компонентов Windows Server

> [!TIP]
> Ищете дополнительные сведения о предыдущих версиях Windows Server? Ознакомьтесь с другими нашими [библиотеками Windows Server](/previous-versions/windows/) на сайте docs.microsoft.com.
>
> Кроме того, вы можете найти нужную информацию [на этом сайте](/search/index?dataSource=previousVersions&search=Windows+Server).

Корпорация Майкрософт регулярно выпускает оба обновления для Windows Server. Необходимо вовремя обновлять серверы, чтобы они могли получать будущие обновления, в том числе обновления безопасности. Полный список выпущенных обновлений см. в разделе [Журнал обновлений Windows 10 и Windows Server 2016](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history).

Этот раздел содержит дополнительные разделы по устранению неполадок и ссылки, которые помогут устранить проблемы с Windows Server. Будут добавлены дополнительные разделы по мере их появления.

## <a name="troubleshoot-activation"></a>Устранение неполадок активации

- [Устранение неполадок с активацией корпоративных лицензий Windows](../get-started/activation-troubleshooting-guide.md)
- [Рекомендации по устранению неполадок KMS](../get-started/activation-troubleshoot-kms-general.md)
- [Параметры Slmgr.vbs для получения сведений об активации корпоративных лицензий](../get-started/activation-slmgr-vbs-options.md)
- [Разрешение кодов ошибок активации Windows](../get-started/activation-error-codes.md)
- [Известные проблемы с активацией KMS](../get-started/activation-troubleshoot-kms-issues.md)
- [Известные проблемы с активацией MAK](../get-started/activation-troubleshoot-mak-issues.md)
- [Рекомендации по устранению проблем с активацией, связанных с DNS](../get-started/common-troubleshooting-procedures-kms-dns.md)
- [Перестроение файла Tokens.dat](../get-started/activation-rebuild-tokens-dat-file.md)
- [Устранение неполадок клиентов ADBA](../get-started/activation-troubleshoot-adba-clients.md)

## <a name="troubleshoot-startup-and-restart"></a>Устранение неполадок при запуске и перезапуске

- [Дополнительные способы устранения неполадок загрузки Windows](/windows/client-management/troubleshoot-windows-startup)
- [Как определить размер файла подкачки для 64-разрядных версий Windows](/windows/client-management/determine-appropriate-page-file-size)
- [Создание ядра или завершение аварийного дампа](/windows/client-management/generate-kernel-or-complete-crash-dump)
- [Общие сведения о файле подкачки](/windows/client-management/introduction-page-file)
- [Настройка параметров системного сбоя и восстановления в Windows](/windows/client-management/system-failure-recovery-options)
- [Дополнительные способы устранения неполадок при загрузке Windows](/windows/client-management/advanced-troubleshooting-boot-problems)
- [Дополнительные способы устранения проблем с зависанием компьютера с Windows](/windows/client-management/troubleshoot-windows-freeze)
- [Дополнительные способы устранения STOP-ошибок или ошибок типа "синий экран"](/windows/client-management/troubleshoot-stop-errors)
- [Дополнительные способы устранения STOP-ошибки 7B или ошибки типа "Inaccessible_Boot_Device"](/windows/client-management/troubleshoot-inaccessible-boot-device)
- [Расширенное устранение неполадок для события с ИДЕНТИФИКАТОРом 41 "система была перезагружена без аккуратного завершения работы"](/windows/client-management/troubleshoot-event-id-41-restart)
- [При обновлении драйвера сетевого адаптера Broadcom появляется сообщение о фатальной ошибке](/windows/client-management/troubleshoot-stop-error-on-broadcom-driver-update)

## <a name="troubleshoot-ad-forest-recovery"></a>Устранение неполадок восстановления леса AD

- [Восстановление леса AD — вопросы и ответы](../identity/ad-ds/manage/ad-forest-recovery-faq.md)

## <a name="troubleshoot-ad-replication"></a>Устранение неполадок репликации AD

- [Устранение неполадок с репликацией Active Directory](../identity/ad-ds/manage/troubleshoot/troubleshooting-active-directory-replication-problems.md)
- [Диагностика виртуализированного контроллера домена](../identity/ad-ds/manage/virtual-dc/virtualized-domain-controller-troubleshooting.md)
- [Устранение неполадок с развертыванием контроллера домена](../identity/ad-ds/deploy/troubleshooting-domain-controller-deployment.md)
- [Настройка компьютера для устранения неполадок](../identity/ad-ds/manage/troubleshoot/configuring-a-computer-for-troubleshooting.md)

## <a name="troubleshoot-ad-fs"></a>Устранение неполадок AD FS

- [Устранение неполадок в службах федерации Active Directory](../identity/ad-fs/troubleshooting/ad-fs-tshoot-overview.md)
- [AD FS устранение неполадок — аудит событий и ведение журнала](../identity/ad-fs/troubleshooting/ad-fs-tshoot-logging.md)
- [Устранение неполадок AD FS. Подключение SQL](../identity/ad-fs/troubleshooting/ad-fs-tshoot-sql.md)
- [Устранение неполадок AD FS — выдача утверждений](../identity/ad-fs/troubleshooting/ad-fs-tshoot-claims-issuance.md)
- [Обнаружение циклов устранения неполадок AD FS](../identity/ad-fs/troubleshooting/ad-fs-tshoot-loop.md)
- [Устранение неполадок AD FS — сертификаты](../identity/ad-fs/troubleshooting/ad-fs-tshoot-certs.md)
- [Устранение неполадок AD FS — Fiddler](../identity/ad-fs/troubleshooting/ad-fs-tshoot-fiddler.md)
- [AD FS устранение неполадок — Fiddler-WS-Federation](../identity/ad-fs/troubleshooting/ad-fs-tshoot-fiddler-ws-fed.md)
- [AD FS устранение неполадок — правила утверждений](../identity/ad-fs/troubleshooting/ad-fs-tshoot-claims-rules.md)
- [Устранение неполадок AD FS — встроенная проверка подлинности Windows](../identity/ad-fs/troubleshooting/ad-fs-tshoot-iwa.md)
- [Устранение неполадок AD FS в Azure AD](../identity/ad-fs/troubleshooting/ad-fs-tshoot-azure.md)
- [Вопросы и ответы по AD FS](../identity/ad-fs/overview/ad-fs-faq.md)
- [Анализатор данных диагностики справки AD FS](../identity/ad-fs/troubleshooting/ad-fs-diagnostics-analyzer.md)

## <a name="troubleshoot-aovpn"></a>Устранение неполадок Аовпн

- [Устранение неполадок постоянно подключенного VPN-профиля](../remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-troubleshooting.md)

## <a name="troubleshoot-converged-nic"></a>Устранение неполадок с согласованным сетевым адаптером

- [Устранение неполадок конфигураций Объединенных сетевых адаптеров](../networking/technologies/conv-nic/cnic-app-troubleshoot.md)

## <a name="troubleshoot-dfsr"></a>Устранение неполадок DFSR

- [Репликация DFS. Вопросы и ответы](../storage/dfs-replication/dfsr-faq.md)

## <a name="troubleshoot-directaccess"></a>Устранение неполадок DirectAccess

- [Диагностика DirectAccess](../remote/remote-access/directaccess/troubleshooting-directaccess.md)

## <a name="troubleshoot-disk-management"></a>Устранение неполадок в управлении дисками

- [Диагностика с помощью оснастки "Управление дисками"](../storage/disk-management/troubleshooting-disk-management.md)

## <a name="troubleshoot-dns"></a>Устранение неполадок DNS

- [Устранение неполадок системы доменных имен (DNS)](../networking/dns/troubleshoot/troubleshoot-dns-data-collection.md)
- [Устранение неполадок DNS-клиентов](../networking/dns/troubleshoot/troubleshoot-dns-client.md)
- [Отключение кэширования на стороне клиента DNS на DNS-клиентах](../networking/dns/troubleshoot/disable-dns-client-side-caching.md)
- [Устранение неполадок DNS-серверов](../networking/dns/troubleshoot/troubleshoot-dns-server.md)

## <a name="troubleshoot-failover-cluster"></a>Устранение неполадок отказоустойчивого кластера

- [Устранение неполадок отказоустойчивого кластера с помощью отчетов об ошибках Windows](../failover-clustering/troubleshooting-using-wer-reports.md)
- [Часто задаваемые вопросы об обновлении с поддержкой кластера](../failover-clustering/cluster-aware-updating-faq.md)
- [Устранение неполадок с кластером с идентификатором события 1135](./troubleshooting-cluster-event-id-1135.md)
- [Возникла проблема с узлами, удаляемыми из активного членства отказоустойчивого кластера](./problem-nodes-failover-cluster.md)
- [Узлы, удаляемые из состава отказоустойчивого кластера в VMWare ESX](./nodes-failover-cluster-vmware.md)
- [IaaS with SQL AlwaysOn - Tuning Failover Cluster Network Thresholds](./iaas-sql-failover-cluster.md) (IaaS с SQL AlwaysOn — настройка пороговых значений сети отказоустойчивого кластера)

## <a name="troubleshoot-dhcp"></a>Устранение неполадок DHCP

- [Руководство по устранению неполадок для протокола DHCP](./troubleshoot-dhcp-issue.md)
- [Основы DHCP (протокол динамического конфигурирования узлов)](./dynamic-host-configuration-protocol-basics.md)
- [Общие рекомендации по устранению неполадок с DHCP](./general-guidance-to-troubleshoot-dhcp.md)
- [Использование автоматической адресации TCP/IP без DHCP-сервера](./how-to-use-automatic-tcpip-addressing-without-a-dh.md)
- [Устранение неполадок на клиенте DHCP](./troubleshoot-problems-on-dhcp-client.md)
- [Устранение неполадок на сервере DHCP](./troubleshoot-problems-on-dhcp-server.md)

## <a name="troubleshoot-fsrm"></a>Устранение неполадок в FSRM

- [Устранение неполадок в диспетчере ресурсов файлового сервера](../storage/fsrm/troubleshooting-file-server-resource-manager.md)

## <a name="troubleshoot-guarded-fabric"></a>Устранение неполадок защищенной структуры

- [Устранение неполадок с помощью средства диагностики защищенной структуры](../security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-diagnostics.md)
- [Устранение неполадок службы защиты узла](../security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hgs.md)
- [Устранение неполадок службы защиты узла](../security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hosts.md)

## <a name="troubleshoot-multi-site-ras"></a>Устранение неполадок удаленного доступа к нескольким сайтам

- [Диагностика при активации многосайтового развертывания](../remote/remote-access/ras/multisite/troubleshoot/troubleshooting-enabling-multisite.md)
- [Устранение неполадок при добавлении точек входа](../remote/remote-access/ras/multisite/troubleshoot/troubleshooting-adding-entry-points.md)
- [Устранение неполадок задания контроллера домена для точки входа](../remote/remote-access/ras/multisite/troubleshoot/troubleshooting-setting-the-entry-point-domain-controller.md)
- [Диагностическая информация об URL-адресах веб-пробы](../remote/remote-access/ras/multisite/troubleshoot/troubleshooting-web-probe-urls.md)

## <a name="troubleshoot-nano-server"></a>Устранение неполадок Nano Server

- [Устранение неполадок сервера Nano Server](../get-started/troubleshooting-nano-server.md)

## <a name="troubleshoot-nic-teaming"></a>Устранение неполадок объединения сетевых карт

- [Диагностика объединения сетевых адаптеров](../networking/technologies/nic-teaming/troubleshooting-nic-teaming.md)

## <a name="troubleshoot-otp-authentication"></a>Устранение неполадок проверки подлинности OTP

- [Диагностика проблем с проверкой подлинности](../remote/remote-access/ras/otp/troubleshoot/troubleshooting-authentication-issues.md)
- [Диагностика включения OTP](../remote/remote-access/ras/otp/troubleshoot/troubleshooting-enabling-otp.md)

## <a name="troubleshoot-qos"></a>Устранение неполадок качества обслуживания

- [Часто задаваемые вопросы о QoS](../networking/technologies/qos/qos-policy-faq.md)

## <a name="troubleshoot-s2d"></a>Устранение неполадок S2D

- [Устранение неполадок Локальные дисковые пространства](../storage/storage-spaces/troubleshooting-storage-spaces.md)
- [Локальные дисковые пространства-часто задаваемые вопросы](../storage/storage-spaces/storage-spaces-direct-faq.md)
- [Локальные дисковые пространства работоспособности и операционные состояния](../storage/storage-spaces/storage-spaces-states.md)
- [Сбор диагностических данных с помощью Локальные дисковые пространства](../storage/storage-spaces/data-collection.md)
- [Управление работоспособностью памяти хранилища (NVDIMM-N) в Windows](../storage/storage-spaces/storage-class-memory-health.md)

## <a name="troubleshoot-sdn"></a>Устранение неполадок SDN

- [Устранение неполадок SDN](../networking/sdn/troubleshoot/troubleshoot-software-defined-networking.md)
- [Диагностика стека программно-конфигурируемой сети Windows Server](../networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack.md)

## <a name="troubleshoot-rds-session-connectivity"></a>Устранение неполадок подключения к сеансу RDS

- [Устранение неполадок с подключениями к удаленному рабочему столу](../remote/remote-desktop-services/troubleshoot/rdp-error-general-troubleshooting.md)
- [Клиенты не могут подключиться и получить ошибку "класс не зарегистрирован"](../remote/remote-desktop-services/troubleshoot/rdp-error-class-not-registered.md)
- [Клиенты не могут подключиться и видеть ошибку "нет доступных лицензий"](../remote/remote-desktop-services/troubleshoot/rdp-error-no-licenses-available.md)
- [Пользователь не может пройти проверку подлинности или проходит ее дважды](../remote/remote-desktop-services/troubleshoot/cannot-authenticate-or-must-authenticate-twice.md)
- [При подключении пользователь получает удаленный рабочий стол служба в настоящий момент занята сообщением](../remote/remote-desktop-services/troubleshoot/remote-desktop-service-currently-busy.md)
- [Клиент удаленного рабочего стола отключается и не может повторно подключиться к тому же сеансу](../remote/remote-desktop-services/troubleshoot/rdp-client-disconnects-cannot-reconnect-same-session.md)
- [Удаленный ноутбук отключается от беспроводной сети](../remote/remote-desktop-services/troubleshoot/remote-laptop-disconnects-wireless-network.md)
- [Низкая производительность или проблемы с приложениями во время подключения к удаленному рабочему столу](../remote/remote-desktop-services/troubleshoot/poor-performance-or-application-problems.md)

## <a name="troubleshoot-shielded-vm"></a>Устранение неполадок экранированной виртуальной машины

- [Устранение неполадок экранированных виртуальных машин](../security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms.md)

## <a name="troubleshoot-software-restriction-policies"></a>Устранение неполадок политик ограниченного использования программ

- [Устранение неполадок политик ограниченного использования программ](../identity/software-restriction-policies/troubleshoot-software-restriction-policies.md)

## <a name="troubleshoot-storage-migration"></a>Устранение неполадок при миграции хранилища

- [Известные проблемы со службой миграции хранилища](../storage/storage-migration-service/known-issues.md)
- [Служба миграции хранилища: часто задаваемые вопросы](../storage/storage-migration-service/faq.md)

## <a name="troubleshoot-storage-replica"></a>Устранение неполадок реплики хранилища

- [Известные проблемы с репликой хранилища](../storage/storage-replica/storage-replica-known-issues.md)
- [Часто задаваемые вопросы о реплике хранилища](../storage/storage-replica/storage-replica-frequently-asked-questions.md)

## <a name="troubleshoot-user-profiles"></a>Устранение неполадок профилей пользователей

- [Устранение проблем с профилями пользователей с помощью событий](../storage/folder-redirection/troubleshoot-user-profiles-events.md)

## <a name="troubleshoot-vrss"></a>Устранение неполадок vRSS

- [Часто задаваемые вопросы по vRSS](../networking/technologies/vrss/vrss-faq.md)

## <a name="troubleshoot-webproxy"></a>Устранение неполадок WebProxy

- [Диагностика прокси-службы веб-приложения](../remote/remote-access/web-application-proxy/troubleshooting-web-application-proxy.md)

## <a name="troubleshoot-windows-admin-center"></a>Устранение неполадок в Windows Admin Center

- [Windows Admin Center: общие действия по устранению неполадок](../manage/windows-admin-center/support/troubleshooting.md)
- [Windows Admin Center — известные проблемы](../manage/windows-admin-center/support/known-issues.md)
- [Вопросы и ответы: Windows Admin Center](../manage/windows-admin-center/understand/faq.md)