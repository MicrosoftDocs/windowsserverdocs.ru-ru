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
ms.openlocfilehash: 94ecc52522a05dfd8cd961c2bf66316a449f4b95
ms.sourcegitcommit: 960010e0636953601aea7c88cb1370d46e2b8212
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101883460"
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
| Службы сертификатов Active Directory           | AD-Certificate                 | N                     |
| Доменные службы Active Directory                | AD-Domain-Services             | N                     |
| Службы федерации Active Directory (AD FS)            | ADFS-Federation                | N                     |
| Службы Active Directory облегченного доступа к каталогам (AD LDS) | ADLDS                          | N                     |
| Службы управления правами Active Directory (AD RMS)     | AD RMS                          | N                     |
| Подтверждение работоспособности устройств                       | девицехеалсаттестатионсервице | N                     |
| DHCP-сервер                                     | DHCP                           | N                     |
| DNS-сервер                                      | DNS                            | N                     |
| Файловые службы и службы хранилища                       | FileAndStorage-Services        | Да                     |
| Служба защиты узла                           | хостгуардиансервицероле        | N                     |
| Hyper-V                                         | Hyper-V                        | N                     |
| Службы печати и документов                     | Print-Services                 | N                     |
| Удаленный доступ                                   | RemoteAccess                   | N                     |
| Службы удаленных рабочих столов                         | Удаленный рабочий стол — службы        | N                     |
| Службы активации корпоративных лицензий                      | волумеактиватион               | N                     |
| Веб-сервер  IIS                                  | Web-Server                     | N                     |
| Режим Windows Server Essentials            | серверессентиалсроле           | N                     |
| Службы WSUS                  | UpdateServices                 | N                     |

## <a name="role-services-included-in-server-core"></a>Службы ролей, входящие в Server Core
Вариант установки Server Core включает следующие службы ролей.

| Роль                                  | Служба роли                                                   | Имя                    | Установлено по умолчанию? |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Службы сертификатов Active Directory | Центр сертификации                                        | ADCS-CERT-Authority     | N                     |
|                                       | Веб-служба политик регистрации сертификатов                      | ADCS-регистрация-Web-POL     | N                     |
|                                       | Веб-служба регистрации сертификатов                             | ADCS-регистрация — Web-SVC     | N                     |
|                                       | Служба регистрации в центре сертификации через Интернет                         | ADCS — веб-регистрация     | N                     |
|                                       | Служба подачи заявок на сетевые устройства                              | ADCS — регистрация устройства  | N                     |
|                                       | Сетевой ответчик                                               | ADCS-Online-CERT        | N                     |
| Active Directory Rights Management    | Сервер управления правами Active Directory                      | ADRMS-Server            | N                     |
|                                       | Поддержка федерации удостоверений                                    | ADRMS-Identity          | N                     |
| Файловые службы и службы хранилища             | Файловые службы и службы iSCSI                                        | File-Services           | N                     |
|                                       | Файловый сервер                                                    | FS-FileServer           | N                     |
|                                       | Служба BranchCache для сетевых файлов                                  | FS-BranchCache          | N                     |
|                                       | дедупликация данных;                                             | FS — дедупликация данных   | N                     |
|                                       | Пространства имен DFS                                                 | FS-DFS-Namespace        | N                     |
|                                       | Репликация DFS                                                | FS-DFS-репликация      | N                     |
|                                       | File Server Resource Manager                                   | Диспетчер ресурсов (FS)     | N                     |
|                                       | Служба агента VSS файлового сервера                                  | Агент FS-VSS-Agent            | N                     |
|                                       | Целевой сервер iSCSI                                            | iSCSITarget — сервер      | N                     |
|                                       | Поставщик хранилища цели iSCSI (поставщики оборудования VDS и VSS) | iSCSITarget-VSS-VDS     | N                     |
|                                       | Сервер для NFS                                                 | FS-NFS-служба          | N                     |
|                                       | рабочие папки                                                   | FS-SyncShareService     | N                     |
|                                       | Службы хранилища                                               | Storage-Services        | Да                     |
| Службы печати и документов           | Сервер печати                                                   | Print-Server            | N                     |
|                                       | Служба LPD                                                    | Print-LPD-Service       | N                     |
| Удаленный доступ                         | DirectAccess и VPN (RAS)                                     | DirectAccess — VPN        | N                     |
|                                       | Маршрутизация                                                        | Маршрутизация                 | N                     |
|                                       | Прокси-сервер веб-приложения                                          | Веб-приложение-прокси   | N                     |
| Службы удаленных рабочих столов               | Брокер подключение к удаленному рабочему столу *                               | RDS-Connection-Broker   | N                     |
|                                       | Лицензирование удаленных рабочих столов                                       | RDS-Licensing           | N                     |
|                                       | Узел виртуализации удаленных рабочих столов                             | RDS-Virtualization      | N                     |
| Веб-сервер (IIS)                      | Веб-сервер                                                     | Web-WebServer           | N                     |
|                                       | Общие функции HTTP                                           | Web-Common-HTTP         | N                     |
|                                       | Документ по умолчанию                                               | Web-Default-doc         | N                     |
|                                       | Просмотр каталогов                                             | Web-dir-Просмотр        | N                     |
|                                       | Ошибки HTTP                                                    | Web-HTTP — ошибки         | N                     |
|                                       | Статическое содержимое                                                 | Веб-статические — содержимое      | N                     |
|                                       | Перенаправление HTTP                                               | Web-HTTP — перенаправление       | N                     |
|                                       | Публикация WebDAV                                              | Web-DAV-публикация      | N                     |
|                                       | Исправность и диагностика                                         | Web-Health              | N                     |
|                                       | Ведение журнала HTTP                                                   | Web-HTTP — ведение журнала        | N                     |
|                                       | Настраиваемое ведение журнала                                                 | Веб — настраиваемое ведение журнала      | N                     |
|                                       | Средства ведения журнала                                                  | Веб-журналы — библиотеки       | N                     |
|                                       | Ведение журнала ODBC                                                   | Web-ODBC — ведение журнала        | N                     |
|                                       | Монитор запросов                                              | Веб-запрос — монитор     | N                     |
|                                       | Трассировка                                                        | Web-HTTP — трассировка        | N                     |
|                                       | Производительность                                                    | Web-Performance         | N                     |
|                                       | Сжатие статического содержимого                                     | Web-stat-Compression    | N                     |
|                                       | Функция сжатия динамического содержимого                                    | Web-Дин — сжатие     | N                     |
|                                       | Безопасность                                                       | Web-Security            | N                     |
|                                       | Фильтрация запросов                                              | Web-Filtering           | N                     |
|                                       | Обычная проверка подлинности                                           | Web-Basic-auth          | N                     |
|                                       | централизованная поддержка SSL-сертификатов                            | Web-CertProvider        | N                     |
|                                       | Проверка подлинности с сопоставлением сертификата клиента                      | Web-Client-auth         | N                     |
|                                       | Дайджест-проверка подлинности                                          | Web-Digest-auth         | N                     |
|                                       | Аутентификация IIS с сопоставлением сертификата клиента                  | Web-CERT-auth           | N                     |
|                                       | Ограничения IP-адресов и доменов                                     | Web-IP — безопасность         | N                     |
|                                       | Авторизация URL-адресов                                              | Web-URL — проверка подлинности            | N                     |
|                                       | Проверка подлинности Windows                                         | Веб-Windows — проверка подлинности        | N                     |
|                                       | Разработка приложений                                        | Веб-App-dev             | N                     |
|                                       | Расширяемость .NET 3.5                                         | Web-NET-ext             | N                     |
|                                       | Расширяемость .NET 4,6                                         | Web — NET-Ext45           | N                     |
|                                       | Инициализация приложений                                     | Web-AppInit             | N                     |
|                                       | ASP                                                            | Web — ASP                 | N                     |
|                                       | ASP.NET 3.5                                                    | Web-ASP-NET             | N                     |
|                                       | ASP.NET 4,6                                                    | Web-ASP-Net45           | N                     |
|                                       | CGI                                                            | Веб-CGI                 | N                     |
|                                       | Расширения ISAPI                                               | Web-ISAPI-ext           | N                     |
|                                       | Фильтры ISAPI                                                  | Веб-ISAPI-фильтр        | N                     |
|                                       | Включения на стороне сервера                                           | Web-Includes            | N                     |
|                                       | Протокол WebSocket                                             | Web-WebSockets          | N                     |
|                                       | FTP-сервер                                                     | Веб-FTP — сервер          | N                     |
|                                       | Служба FTP                                                    | Веб-FTP — служба         | N                     |
|                                       | Расширяемость FTP                                              | Web-FTP-ext             | N                     |
|                                       | Средства управления                                               | Веб-управление — средства          | N                     |
|                                       | Совместимость управления IIS 6                                 | Веб-управление-совместимость         | N                     |
|                                       | Совместимость метабазы IIS 6                                   | Web-Metabase            | N                     |
|                                       | Инструменты для работы со сценариев IIS 6                                          | Web-Лгци — создание сценариев      | N                     |
|                                       | Совместимость с WMI IIS 6                                        | Веб-WMI                 | N                     |
|                                       | Сценарии и средства управления IIS                               | Веб-сценарии — средства     | N                     |
|                                       | Служба Management Service                                             | Веб-управление — служба        | N                     |
| Службы WSUS        | Подключение WID                                               | UpdateServices-WidDB    | N                     |
|                                       | Службы WSUS                                                  | UpdateServices-Services | N                     |
|                                       | Подключение SQL Server                                        | UpdateServices-DB       | N                     |

## <a name="features-included-in-server-core"></a>Компоненты, входящие в Server Core
Вариант установки Server Core включает следующие функции.

| Функция                                                | Имя                               | Установлено по умолчанию? |
|--------------------------------------------------------|------------------------------------|-----------------------|
| Компоненты .NET Framework 3.5                            | NET-Framework-компоненты             | N                     |
| Платформа .NET Framework 3,5 (включает .NET 2,0 и 3,0)       | NET-Framework-Core                 | удален             |
| Активация по протоколам HTTP                                        | NET-HTTP-Activation                | N                     |
| Не-HTTP активация                                    | NET-non-HTTP-активные                 | N                     |
| Функции платформа .NET Framework 4,6                            | NET-Framework-45-функции          | Да                     |
| .NET Framework 4.6                                     | NET-Framework-45-Core              | Да                     |
| ASP.NET 4,6                                            | NET-Framework-45-ASPNET            | N                     |
| Службы WCF                                           | NET-WCF-Services45                 | Да                     |
| Активация по протоколам HTTP                                        | NET-WCF-HTTP-Activation45          | N                     |
| Активация очереди сообщений (MSMQ)                      | NET-WCF-MSMQ-Activation45          | N                     |
| Активация именованного канала                                  | NET-WCF-pipe-Activation45          | N                     |
| Активация TCP                                         | NET-WCF-TCP-Activation45           | N                     |
| Совместное использование TCP-порта                                       | NET-WCF-TCP-PortSharing45          | Да                     |
| Фоновая интеллектуальная служба передачи (BITS)         | BITS                               | N                     |
| Облегченный сервер загрузки                                         | BITS-Compact-Server                | N                     |
| Шифрование диска BitLocker                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| Клиент для NFS                                         | NFS-Client                         | N                     |
| Контейнеры                                             | Контейнеры                         | N                     |
| Data Center Bridging                                   | Центр обработки данных — мосты               | N                     |
| Enhanced Storage;                                       | енханцедстораже                    | N                     |
| Отказоустойчивая кластеризация                                    | Failover-Clustering                | N                     |
| Управление групповой политикой                                | Консоль управления групповыми политиками                               | N                     |
| Качество обслуживания ввода-вывода                                 | DiskIo-QoS                         | N                     |
| Внедряемое веб-ядро служб IIS                                  | Веб-ВХК                            | N                     |
| Сервер управления IP-адресами (IPAM)                    | IPAM                               | N                     |
| Службы iSNS-сервера                                    | ISNS                               | N                     |
| Расширение IIS OData для управления                         | манажементодата                    | N                     |
| Media Foundation                                       | Server-Media-Foundation            | N                     |
| служба очередей сообщений                                        | MSMQ                               | N                     |
| Службы очереди сообщений                               | MSMQ-Services                      | N                     |
| Сервер службы очередей сообщений                                 | MSMQ-Server                        | N                     |
| Интеграция служб каталогов                          | MSMQ-Directory                     | N                     |
| Поддержка HTTP                                           | Поддержка MSMQ-HTTP                  | N                     |
| Триггеры очереди сообщений                               | MSMQ-Triggers                      | N                     |
| Служба маршрутизации                                        | MSMQ-Routing                       | N                     |
| DCOM-прокси очереди сообщений                             | MSMQ — DCOM                          | N                     |
| Multipath I/O;                                          | Multipath-IO                       | N                     |
| Соединитель MultiPoint                                   | MultiPoint-Connector               | N                     |
| Службы соединителя MultiPoint                          | MultiPoint-Connector — службы      | N                     |
| MultiPoint Manager и панель мониторинга MultiPoint            | MultiPoint-Tools                   | N                     |
| Network Load Balancing                                 | NLB                                | N                     |
| Протокол PNRP                          | ПРОТОКОЛА                               | N                     |
| qWave;                 | qWave                              | N                     |
| Протокол удаленного разностного сжатия                        | КОМПОНЕНТА                                | N                     |
| Средства удаленного администрирования сервера                     | RSAT                               | N                     |
| Средства администрирования компонентов                           | Средства для RSAT-Feature-Tools                 | N                     |
| Служебные программы шифрование диска BitLocker Administration  | RSAT-Feature-Tools-BitLocker       | N                     |
| Средства DataCenterBridging LLDP                          | RSAT-DataCenterBridging-LLDP-средства | N                     |
| Средства отказоустойчивости кластеров                              | RSAT-Clustering                    | N                     |
| Модуль отказоустойчивого кластера для Windows PowerShell         | PowerShell для кластеризации RSAT         | N                     |
| Сервер автоматизации отказоустойчивого кластера                     | RSAT — кластеризация — Аутоматионсервер   | N                     |
| Интерфейс командной строки отказоустойчивого кластера                     | RSAT — кластеризация — Кмдинтерфаце       | N                     |
| Клиент управления IP-адресами (IPAM)                    | IPAM — клиент-функция                | N                     |
| Средства экранированной виртуальной машины                                      | RSAT-экранированные-VM-Tools             | N                     |
| Модуль реплики хранилища для Windows PowerShell          | RSAT-Storage-реплика               | N                     |
| Средства администрирования ролей                              | RSAT-Role-Tools                    | N                     |
| Средства AD DS и AD LDS                                 | RSAT-AD-Tools                      | N                     |
| Модуль Active Directory для Windows PowerShell         | RSAT-AD-PowerShell                 | N                     |
| Средства AD DS                                            | RSAT — ДОБАВЛЯЕТ                          | N                     |
| Центр администрирования Active Directory                 | RSAT-AD-Админцентер                | N                     |
| Средства Snap-Ins и Command-Line AD DS                  | RSAT — ADDS-Tools                    | N                     |
| Средства Snap-Ins и Command-Line AD LDS                 | RSAT-ADLDS                         | N                     |
| Средства управления Hyper-V                               | RSAT-Hyper-V-Tools                 | N                     |
| Модуль Hyper-V для Windows PowerShell                  | PowerShell для Hyper-V                 | N                     |
| Средства Windows Server Update Services                   | UpdateServices-RSAT                | N                     |
| API и командлеты PowerShell                             | UpdateServices — API                 | N                     |
| Средства DHCP-сервера                                      | RSAT — DHCP                          | N                     |
| Средства DNS-сервера                                       | RSAT-DNS-Server                    | N                     |
| Средства управления удаленным доступом                         | RSAT-RemoteAccess                  | N                     |
| модуль удаленного доступа для Windows PowerShell.            | RSAT-RemoteAccess-PowerShell       | N                     |
| RPC через HTTP-прокси;                                    | RPC-over-HTTP-proxy                | N                     |
| Коллекция событий установки и загрузки                        | Настройка и загрузка — сбор событий    | N                     |
| простые службы TCP/IP;                                 | Simple-TCPIP                       | N                     |
| Поддержка протоколов общего доступа к файлам SMB 1.0 и CIFS                      | FS — SMB1                            | Да                     |
| Ограничение пропускной способности SMB                                    | FS — СМББВ                           | N                     |
| служба SNMP;                                           | SNMP-Service                       | N                     |
| Поставщик WMI SNMP                                      | SNMP-WMI-provider                  | N                     |
| Клиент Telnet                                          | Telnet-Client                      | N                     |
| Средства экранирования виртуальных машин для управления структурой               | фабрикшиелдедтулс                | N                     |
| Функции защитника Windows                              | Windows-Defender-функции          | Да                     |
| Защитник Windows                                       | Windows-Defender                   | Да                     |
| Внутренняя база данных Windows                              | Внутренние базы данных Windows          | N                     |
| Windows PowerShell                                     | повершеллрут                     | Да                     |
| Windows PowerShell 5.1                                 | PowerShell                         | Да                     |
| Подсистема Windows PowerShell 2,0                          | PowerShell — v2                      | удален             |
| Служба настройки требуемого состояния Windows PowerShell | DSC-Service                        | N                     |
| Windows PowerShell Web Access                          | WindowsPowerShellWebAccess         | N                     |
| Служба активации процессов Windows                     | WAS                                | N                     |
| Модель процесса                                          | WAS — модель обработки                  | N                     |
| Среда .NET 3,5                                   | WAS – NET-Environment;                | N                     |
| API-интерфейсы конфигурации                                     | WAS-config-API                    | N                     |
| Система архивации данных Windows Server                                  | Windows-Server-Backup              | N                     |
| Средства миграции Windows Server                         | Миграция                          | N                     |
| Управление хранилищем на основе стандартов Windows             | виндовссторажеманажементсервице    | N                     |
| Расширение IIS WinRM                                    | WinRM-IIS-Ext                      | N                     |
| WINS-сервер                                            | WINS                               | N                     |
| Поддержка WoW64                                          | WoW64-Support                      | Да                     |
|                                                        |                                    |                       |

* Службы, обозначенные символом *, больше не доступны в Server Core, начиная с Server 2019 1803.
