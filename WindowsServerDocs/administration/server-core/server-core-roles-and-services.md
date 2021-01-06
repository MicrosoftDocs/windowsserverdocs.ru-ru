---
title: Роли, службы ролей и компоненты, входящие в Windows Server — Server Core
description: Какие роли и компоненты включены в вариант установки Server Core Windows Server?
ms.mktglfcycl: manage
ms.sitesec: library
author: pronichkin
ms.author: artemp
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.topic: conceptual
ms.openlocfilehash: a30e282647c6fb58bd9f5aaa0e24c5e840ac5351
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947150"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>Роли, службы ролей и компоненты, входящие в Windows Server — Server Core

> Область применения: Windows Server 2019, Windows Server 2016 и Windows Server (половина ежегодного канала)

Как правило, мы говорим о [том, что *не* входит в Server Core](server-core-removed-roles.md) . Теперь мы попробуем использовать другой подход и поможем  узнать, какие компоненты *установлены по умолчанию*. Следующие роли, службы ролей и компоненты находятся *в* варианте установки Server Core Windows Server. Используйте эти сведения, чтобы определить, работает ли параметр Server Core для вашей среды. Так как это большой список, рассмотрите возможность поиска конкретной роли или интересующего вас компонента. Если поиск не возвращает искомый объект, он не включается в ядро сервера.

Например, если выполнить поиск по запросу "узел удаленный рабочий стол сеансов", вы не найдете его на этой странице. Это обусловлено тем, что узел сеансов удаленных рабочих столов не включен в образ Server Core.

Помните, что вы [всегда можете взглянуть](server-core-removed-roles.md) на то, что *не* входит в комплект. Это еще один способ взглянуть на вещи.

## <a name="roles-included-in-server-core"></a>Роли, входящие в Server Core
Вариант установки Server Core включает следующие роли сервера.

| Роль                                            | Имя                           | Установлено по умолчанию? |
|-------------------------------------------------|--------------------------------|-----------------------|
| Службы сертификатов Active Directory           | AD-Certificate                 | Нет                     |
| Доменные службы Active Directory                | AD-Domain-Services             | Нет                     |
| службы федерации Active Directory;            | ADFS-Federation                | Нет                     |
| Службы Active Directory облегченного доступа к каталогам (AD LDS) | ADLDS                          | Нет                     |
| Службы управления правами Active Directory (AD RMS)     | AD RMS                          | Нет                     |
| Подтверждение работоспособности устройств                       | девицехеалсаттестатионсервице | Нет                     |
| DHCP-сервер                                     | DHCP                           | Нет                     |
| DNS-сервер                                      | DNS                            | Нет                     |
| Файловые службы и службы хранилища                       | FileAndStorage-Services        | Y                     |
| Служба защиты узла                           | хостгуардиансервицероле        | N                     |
| Hyper-V                                         | Hyper-V                        | Нет                     |
| Службы печати и документов                     | Print-Services                 | Нет                     |
| Удаленный доступ                                   | RemoteAccess                   | Нет                     |
| Службы удаленных рабочих столов                         | Удаленный рабочий стол — службы        | Нет                     |
| Службы активации корпоративных лицензий                      | волумеактиватион               | Нет                     |
| Веб-сервер  IIS                                  | Web-Server                     | Нет                     |
| Режим Windows Server Essentials            | серверессентиалсроле           | Нет                     |
| Службы Windows Server Update Services                  | UpdateServices                 | Нет                     |

## <a name="role-services-included-in-server-core"></a>Службы ролей, входящие в Server Core
Вариант установки Server Core включает следующие службы ролей.

| Роль                                  | Служба роли                                                   | Имя                    | Установлено по умолчанию? |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Службы сертификатов Active Directory | Центр сертификации                                        | ADCS-CERT-Authority     | Нет                     |
|                                       | Веб-служба политик регистрации сертификатов                      | ADCS-регистрация-Web-POL     | Нет                     |
|                                       | Веб-служба регистрации сертификатов                             | ADCS-регистрация — Web-SVC     | Нет                     |
|                                       | Служба регистрации в центре сертификации через Интернет                         | ADCS — веб-регистрация     | Нет                     |
|                                       | Служба подачи заявок на сетевые устройства                              | ADCS — регистрация устройства  | Нет                     |
|                                       | Сетевой ответчик                                               | ADCS-Online-CERT        | Нет                     |
| Active Directory Rights Management    | Сервер управления правами Active Directory                      | ADRMS-Server            | Нет                     |
|                                       | Поддержка федерации удостоверений                                    | ADRMS-Identity          | Нет                     |
| Файловые службы и службы хранилища             | Файловые службы и службы iSCSI                                        | File-Services           | Нет                     |
|                                       | Файловый сервер                                                    | FS-FileServer           | Нет                     |
|                                       | Служба BranchCache для сетевых файлов                                  | FS-BranchCache          | Нет                     |
|                                       | дедупликация данных;                                             | FS — дедупликация данных   | Нет                     |
|                                       | Пространства имен DFS                                                 | FS-DFS-Namespace        | Нет                     |
|                                       | Репликация DFS                                                | FS-DFS-репликация      | Нет                     |
|                                       | File Server Resource Manager                                   | Диспетчер ресурсов (FS)     | Нет                     |
|                                       | Служба агента VSS файлового сервера                                  | Агент FS-VSS-Agent            | Нет                     |
|                                       | Целевой сервер iSCSI                                            | iSCSITarget — сервер      | Нет                     |
|                                       | Поставщик хранилища цели iSCSI (поставщики оборудования VDS и VSS) | iSCSITarget-VSS-VDS     | Нет                     |
|                                       | Сервер для NFS                                                 | FS-NFS-служба          | Нет                     |
|                                       | рабочие папки                                                   | FS-SyncShareService     | Нет                     |
|                                       | Службы хранилища                                               | Storage-Services        | Y                     |
| Службы печати и документов           | Сервер печати                                                   | Print-Server            | Нет                     |
|                                       | Служба LPD                                                    | Print-LPD-Service       | Нет                     |
| Удаленный доступ                         | DirectAccess и VPN (RAS)                                     | DirectAccess — VPN        | Нет                     |
|                                       | Маршрутизация                                                        | Маршрутизация                 | Нет                     |
|                                       | Прокси-сервер веб-приложения                                          | Веб-приложение-прокси   | Нет                     |
| Службы удаленных рабочих столов               | Посредник подключений к удаленному рабочему столу                               | RDS-Connection-Broker   | Нет                     |
|                                       | Лицензирование удаленных рабочих столов                                       | RDS-Licensing           | Нет                     |
|                                       | Узел виртуализации удаленных рабочих столов                             | RDS-Virtualization      | Нет                     |
| Веб-сервер (IIS)                      | Веб-сервер                                                     | Web-WebServer           | Нет                     |
|                                       | Общие функции HTTP                                           | Web-Common-HTTP         | Нет                     |
|                                       | Документ по умолчанию                                               | Web-Default-doc         | Нет                     |
|                                       | Просмотр каталогов                                             | Web-dir-Просмотр        | Нет                     |
|                                       | Ошибки HTTP                                                    | Web-HTTP — ошибки         | Нет                     |
|                                       | Статическое содержимое                                                 | Веб-статические — содержимое      | Нет                     |
|                                       | Перенаправление HTTP                                               | Web-HTTP — перенаправление       | Нет                     |
|                                       | Публикация WebDAV                                              | Web-DAV-публикация      | Нет                     |
|                                       | Исправность и диагностика                                         | Web-Health              | Нет                     |
|                                       | Ведение журнала HTTP                                                   | Web-HTTP — ведение журнала        | Нет                     |
|                                       | Настраиваемое ведение журнала                                                 | Веб — настраиваемое ведение журнала      | Нет                     |
|                                       | Средства ведения журнала                                                  | Веб-журналы — библиотеки       | Нет                     |
|                                       | Ведение журнала ODBC                                                   | Web-ODBC — ведение журнала        | Нет                     |
|                                       | Монитор запросов                                              | Веб-запрос — монитор     | Нет                     |
|                                       | Трассировка                                                        | Web-HTTP — трассировка        | Нет                     |
|                                       | Производительность                                                    | Web-Performance         | Нет                     |
|                                       | Сжатие статического содержимого                                     | Web-stat-Compression    | Нет                     |
|                                       | Функция сжатия динамического содержимого                                    | Web-Дин — сжатие     | Нет                     |
|                                       | Безопасность                                                       | Web-Security            | Нет                     |
|                                       | Фильтрация запросов                                              | Web-Filtering           | Нет                     |
|                                       | Обычная проверка подлинности                                           | Web-Basic-auth          | Нет                     |
|                                       | централизованная поддержка SSL-сертификатов                            | Web-CertProvider        | Нет                     |
|                                       | Проверка подлинности с сопоставлением сертификата клиента                      | Web-Client-auth         | Нет                     |
|                                       | Дайджест-проверка подлинности                                          | Web-Digest-auth         | Нет                     |
|                                       | Аутентификация IIS с сопоставлением сертификата клиента                  | Web-CERT-auth           | Нет                     |
|                                       | Ограничения IP-адресов и доменов                                     | Web-IP — безопасность         | Нет                     |
|                                       | Авторизация URL-адресов                                              | Web-URL — проверка подлинности            | Нет                     |
|                                       | Проверка подлинности Windows                                         | Веб-Windows — проверка подлинности        | Нет                     |
|                                       | Разработка приложений                                        | Веб-App-dev             | Нет                     |
|                                       | Расширяемость .NET 3.5                                         | Web-NET-ext             | Нет                     |
|                                       | Расширяемость .NET 4,6                                         | Web — NET-Ext45           | Нет                     |
|                                       | Инициализация приложений                                     | Web-AppInit             | Нет                     |
|                                       | ASP                                                            | Web — ASP                 | Нет                     |
|                                       | ASP.NET 3.5                                                    | Web-ASP-NET             | Нет                     |
|                                       | ASP.NET 4,6                                                    | Web-ASP-Net45           | Нет                     |
|                                       | CGI                                                            | Веб-CGI                 | Нет                     |
|                                       | Расширения ISAPI                                               | Web-ISAPI-ext           | Нет                     |
|                                       | Фильтры ISAPI                                                  | Веб-ISAPI-фильтр        | Нет                     |
|                                       | Включения на стороне сервера                                           | Web-Includes            | Нет                     |
|                                       | Протокол WebSocket                                             | Web-WebSockets          | Нет                     |
|                                       | FTP-сервер                                                     | Веб-FTP — сервер          | Нет                     |
|                                       | Служба FTP                                                    | Веб-FTP — служба         | Нет                     |
|                                       | Расширяемость FTP                                              | Web-FTP-ext             | Нет                     |
|                                       | Средства управления                                               | Веб-управление — средства          | Нет                     |
|                                       | Совместимость управления IIS 6                                 | Веб-управление-совместимость         | Нет                     |
|                                       | Совместимость метабазы IIS 6                                   | Web-Metabase            | Нет                     |
|                                       | Инструменты для работы со сценариев IIS 6                                          | Web-Лгци — создание сценариев      | Нет                     |
|                                       | Совместимость с WMI IIS 6                                        | Веб-WMI                 | Нет                     |
|                                       | Сценарии и средства управления IIS                               | Веб-сценарии — средства     | Нет                     |
|                                       | Служба Management Service                                             | Веб-управление — служба        | Нет                     |
| Службы Windows Server Update Services        | Подключение WID                                               | UpdateServices-WidDB    | Нет                     |
|                                       | Службы WSUS                                                  | UpdateServices-Services | Нет                     |
|                                       | Подключение SQL Server                                        | UpdateServices-DB       | Нет                     |

## <a name="features-included-in-server-core"></a>Компоненты, входящие в Server Core
Вариант установки Server Core включает следующие функции.

| Компонент                                                | Имя                               | Установлено по умолчанию? |
|--------------------------------------------------------|------------------------------------|-----------------------|
| Компоненты .NET Framework 3.5                            | NET-Framework-компоненты             | Нет                     |
| .NET Framework 3,5 (включает .NET 2,0 и 3,0)       | NET-Framework-Core                 | удален             |
| Активация по протоколам HTTP                                        | NET-HTTP-Activation                | Нет                     |
| Не-HTTP активация                                    | NET-non-HTTP-активные                 | Нет                     |
| Функции .NET Framework 4,6                            | NET-Framework-45-функции          | Y                     |
| .NET Framework 4.6                                     | NET-Framework-45-Core              | Y                     |
| ASP.NET 4,6                                            | NET-Framework-45-ASPNET            | Нет                     |
| Службы WCF                                           | NET-WCF-Services45                 | Y                     |
| Активация по протоколам HTTP                                        | NET-WCF-HTTP-Activation45          | Нет                     |
| Активация очереди сообщений (MSMQ)                      | NET-WCF-MSMQ-Activation45          | Нет                     |
| Активация именованного канала                                  | NET-WCF-pipe-Activation45          | Нет                     |
| Активация TCP                                         | NET-WCF-TCP-Activation45           | Нет                     |
| Совместное использование TCP-порта                                       | NET-WCF-TCP-PortSharing45          | Y                     |
| Фоновая интеллектуальная служба передачи (BITS)         | BITS                               | Нет                     |
| Облегченный сервер загрузки                                         | BITS-Compact-Server                | Нет                     |
| Шифрование диска BitLocker                             | BitLocker                          | Нет                     |
| BranchCache                                            | BranchCache                        | Нет                     |
| Клиент для NFS                                         | NFS-Client                         | Нет                     |
| Контейнеры                                             | Контейнеры                         | Нет                     |
| Data Center Bridging                                   | Центр обработки данных — мосты               | Нет                     |
| Enhanced Storage;                                       | енханцедстораже                    | Нет                     |
| Отказоустойчивая кластеризация                                    | Failover-Clustering                | Нет                     |
| Управление групповой политикой                                | Консоль управления групповыми политиками                               | Нет                     |
| Качество обслуживания ввода-вывода                                 | DiskIo-QoS                         | Нет                     |
| Внедряемое веб-ядро служб IIS                                  | Веб-ВХК                            | Нет                     |
| Сервер управления IP-адресами (IPAM)                    | IPAM                               | Нет                     |
| Службы iSNS-сервера                                    | ISNS                               | Нет                     |
| Расширение IIS OData для управления                         | манажементодата                    | Нет                     |
| Media Foundation                                       | Server-Media-Foundation            | Нет                     |
| служба очередей сообщений                                        | MSMQ                               | Нет                     |
| Службы очереди сообщений                               | MSMQ-Services                      | Нет                     |
| Сервер службы очередей сообщений                                 | MSMQ-Server                        | Нет                     |
| Интеграция служб каталогов                          | MSMQ-Directory                     | Нет                     |
| Поддержка HTTP                                           | Поддержка MSMQ-HTTP                  | Нет                     |
| Триггеры очереди сообщений                               | MSMQ-Triggers                      | Нет                     |
| Служба маршрутизации                                        | MSMQ-Routing                       | Нет                     |
| DCOM-прокси очереди сообщений                             | MSMQ — DCOM                          | Нет                     |
| Multipath I/O;                                          | Multipath-IO                       | Нет                     |
| Соединитель MultiPoint                                   | MultiPoint-Connector               | Нет                     |
| Службы соединителя MultiPoint                          | MultiPoint-Connector — службы      | Нет                     |
| MultiPoint Manager и панель мониторинга MultiPoint            | MultiPoint-Tools                   | Нет                     |
| Network Load Balancing                                 | NLB                                | Нет                     |
| Протокол PNRP                          | ПРОТОКОЛА                               | Нет                     |
| qWave;                 | qWave                              | Нет                     |
| Протокол удаленного разностного сжатия                        | КОМПОНЕНТА                                | Нет                     |
| Средства удаленного администрирования сервера                     | RSAT                               | Нет                     |
| Средства администрирования компонентов                           | Средства для RSAT-Feature-Tools                 | Нет                     |
| Служебные программы шифрование диска BitLocker Administration  | RSAT-Feature-Tools-BitLocker       | Нет                     |
| Средства DataCenterBridging LLDP                          | RSAT-DataCenterBridging-LLDP-средства | Нет                     |
| Средства отказоустойчивости кластеров                              | RSAT-Clustering                    | Нет                     |
| Модуль отказоустойчивого кластера для Windows PowerShell         | PowerShell для кластеризации RSAT         | Нет                     |
| Сервер автоматизации отказоустойчивого кластера                     | RSAT — кластеризация — Аутоматионсервер   | Нет                     |
| Интерфейс командной строки отказоустойчивого кластера                     | RSAT — кластеризация — Кмдинтерфаце       | Нет                     |
| Клиент управления IP-адресами (IPAM)                    | IPAM — клиент-функция                | Нет                     |
| Средства экранированной виртуальной машины                                      | RSAT-экранированные-VM-Tools             | Нет                     |
| Модуль реплики хранилища для Windows PowerShell          | RSAT-Storage-реплика               | Нет                     |
| Средства администрирования ролей                              | RSAT-Role-Tools                    | Нет                     |
| Средства AD DS и AD LDS                                 | RSAT-AD-Tools                      | Нет                     |
| Модуль Active Directory для Windows PowerShell         | RSAT-AD-PowerShell                 | Нет                     |
| Средства AD DS                                            | RSAT — ДОБАВЛЯЕТ                          | Нет                     |
| Центр администрирования Active Directory                 | RSAT-AD-Админцентер                | Нет                     |
| Средства Snap-Ins и Command-Line AD DS                  | RSAT — ADDS-Tools                    | Нет                     |
| Средства Snap-Ins и Command-Line AD LDS                 | RSAT-ADLDS                         | Нет                     |
| Средства управления Hyper-V                               | RSAT-Hyper-V-Tools                 | Нет                     |
| Модуль Hyper-V для Windows PowerShell                  | PowerShell для Hyper-V                 | Нет                     |
| Средства Windows Server Update Services                   | UpdateServices-RSAT                | Нет                     |
| API и командлеты PowerShell                             | UpdateServices — API                 | Нет                     |
| Средства DHCP-сервера                                      | RSAT — DHCP                          | Нет                     |
| Средства DNS-сервера                                       | RSAT-DNS-Server                    | Нет                     |
| Средства управления удаленным доступом                         | RSAT-RemoteAccess                  | Нет                     |
| модуль удаленного доступа для Windows PowerShell.            | RSAT-RemoteAccess-PowerShell       | Нет                     |
| RPC через HTTP-прокси;                                    | RPC-over-HTTP-proxy                | Нет                     |
| Коллекция событий установки и загрузки                        | Настройка и загрузка — сбор событий    | Нет                     |
| простые службы TCP/IP;                                 | Simple-TCPIP                       | Нет                     |
| Поддержка протоколов общего доступа к файлам SMB 1.0 и CIFS                      | FS — SMB1                            | Y                     |
| Ограничение пропускной способности SMB                                    | FS — СМББВ                           | Нет                     |
| служба SNMP;                                           | SNMP-Service                       | Нет                     |
| Поставщик WMI SNMP                                      | SNMP-WMI-provider                  | Нет                     |
| Клиент Telnet                                          | Telnet-Client                      | Нет                     |
| Средства экранирования виртуальных машин для управления структурой               | фабрикшиелдедтулс                | Нет                     |
| Функции защитника Windows                              | Windows-Defender-функции          | Y                     |
| Защитник Windows                                       | Windows-Defender                   | Y                     |
| Внутренняя база данных Windows                              | Внутренние базы данных Windows          | Нет                     |
| Windows PowerShell                                     | повершеллрут                     | Y                     |
| Windows PowerShell 5.1                                 | PowerShell                         | Y                     |
| Подсистема Windows PowerShell 2,0                          | PowerShell — v2                      | удален             |
| Служба настройки требуемого состояния Windows PowerShell | DSC-Service                        | Нет                     |
| Windows PowerShell Web Access                          | WindowsPowerShellWebAccess         | Нет                     |
| Служба активации процессов Windows                     | WAS                                | Нет                     |
| Модель процесса                                          | WAS — модель обработки                  | Нет                     |
| Среда .NET 3,5                                   | WAS – NET-Environment;                | Нет                     |
| API-интерфейсы конфигурации                                     | WAS-config-API                    | Нет                     |
| Система архивации данных Windows Server                                  | Windows-Server-Backup              | Нет                     |
| Средства миграции Windows Server                         | Миграция                          | Нет                     |
| Управление хранилищем на основе стандартов Windows             | виндовссторажеманажементсервице    | Нет                     |
| Расширение IIS WinRM                                    | WinRM-IIS-Ext                      | Нет                     |
| WINS-сервер                                            | WINS                               | Нет                     |
| Поддержка WoW64                                          | WoW64-Support                      | Y                     |
|                                                        |                                    |                       |
