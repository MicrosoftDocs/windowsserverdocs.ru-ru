---
title: Роли, службы ролей и компоненты, отсутствующие в контейнерах Server Core — Windows Server, версия 1803
description: Сведения о ролях и функциях, удаленных из образа контейнера Server Core для Windows Server.
ms.mktglfcycl: manage
ms.sitesec: library
author: pronichkin
ms.author: artemp
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.topic: conceptual
ms.openlocfilehash: 058a976a20e09cf46b57ec39af6c7f5b0cc30fdf
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947170"
---
# <a name="roles-role-services-and-features-not-in-server-core-containers---windows-server-version-1803"></a>Роли, службы ролей и компоненты, отсутствующие в контейнерах Server Core — Windows Server, версия 1803

> Применяется к: Windows Server версии 1803

В Windows Server версии 1803 мы [уменьшили общий размер образа контейнера Server Core до **1,58 Гб**](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/). Мы сделали это, оптимизируя архитектуру и удалив вещи, которые не нужны в [контейнере Server Core](/virtualization/windowscontainers/about/). Некоторые были вещи, которые не работали в контейнерах, некоторые были роли и функции, которые никто не использовал.

> [!IMPORTANT]
> Мы удалили их из образа **контейнера** Server Core, а не [самого ядра сервера](server-core-roles-and-services.md).

Ниже приведен полный список функций и ролей, удаленных из образа контейнера Server Core.

<div style='font-size:9.0pt'>

<br>адцертификатесервицесроле
<br>AuthManager
<br>Bitlocker-Utilities
<br>BitLocker
<br>BITS
<br>BITSExtensions-Upload
<br>ккффилтер
<br>цертификатинроллментполицисервер
<br>цертификатинроллментсервер
<br>цертификатесервицес
<br>ClientForNFS-Infrastructure
<br>Контейнеры
<br>корефилесервер
<br>DataCenterBridging-LLDP-средства
<br>DataCenterBridging
<br>Dedup-Core
<br>девицехеалсаттестатионсервице
<br>DFSN-Server
<br>DFSR-Infrastructure-Сервередитион
<br>DirectoryServices — Адам
<br>DirectoryServices-DomainController
<br>DiskIo-QoS
<br>енханцедстораже
<br>FailoverCluster-AdminPak
<br>FailoverCluster-AutomationServer
<br>FailoverCluster-CmdInterface
<br>FailoverCluster-FullServer
<br>FailoverCluster-PowerShell
<br>File-Services
<br>филесервервссажент
<br>FRS-Infrastructure
<br>FSRM-Infrastructure-службы
<br>FSRM-Infrastructure
<br>харденедфабриценкриптионтаск
<br>хостгуардиан
<br>HostGuardianService-Package
<br>IdentityServer-SecurityTokenService
<br>ипамклиентфеатуре
<br>ипамсерверфеатуре
<br>iSCSITargetServer-PowerShell
<br>iSCSITargetServer
<br>искситаржетсторажепровидерс
<br>iSNS_Service
<br>Лицензирование
<br>LightweightServer
<br>Microsoft-Hyper-V-Management-Clients
<br>Microsoft-Hyper-V — автономный режим
<br>Microsoft-Hyper-V-Online
<br>Microsoft-Hyper-V
<br>Microsoft-Windows-FCI-Client-Package
<br>Microsoft-Windows-GroupPolicy-Серверадминтулс-Update
<br>Microsoft-Windows-подсистема — Linux
<br>MSRDC-Infrastructure
<br>мултипасио
<br>NetworkController
<br>нетворкконтроллертулс
<br>нетворкдевицеенроллментсервицес
<br>нетворклоадбаланЦингфуллсервер
<br>нетворквиртуализатион
<br>онлинеревокатионсервицес
<br>P2P-PnrpOnly
<br>Относительно
<br>Печать — пользовательский интерфейс пользователя
<br>Printing-LPDPrintService
<br>Printing-Server-Foundation-Features
<br>Печать — роль сервера
<br>QWAVE
<br>расраутингпротоколс
<br>Удаленный рабочий стол — службы
<br>RemoteAccess
<br>ремотеакцессмгмттулс
<br>ремотеакцессповершелл
<br>ремотеакцесссервер
<br>ресумекэйфилтер
<br>RightsManagementServices-Role
<br>ригхтсманажементсервицес
<br>RMS-Federation
<br>Сбмгр — пользовательский интерфейс
<br>ServerCore-Drivers-General-WOW64
<br>ServerCore-Drivers-General
<br>ServerForNFS-Infrastructure
<br>ServerManager-Core-RSAT-Feature-Tools
<br>сервермедиафаундатион
<br>ServerMigration
<br>сессиондиректори
<br>сетупандбутевентколлектион
<br>шиелдедвмтулсадминпакк
<br>SMB1Protocol-Server
<br>смбдирект
<br>смбхашженератион
<br>SmbWitness
<br>SNMP
<br>софтварелоадбаланцер
<br>Хранилище-реплика — Админпакк
<br>Storage-Replica
<br>TPM-КОМАНДНОМ PSH-командлеты
<br>UpdateServices-Database
<br>UpdateServices-Services
<br>UpdateServices-WidDatabase
<br>UpdateServices
<br>вмхостажент
<br>Волумеактиватион — полная роль
<br>Веб-приложение-прокси
<br>Доступ к данным
<br>вебенроллментсервицес
<br>Windows-Defender
<br>WindowsServerBackup
<br>виндовссторажеманажементсервице
<br>винсрунтиме
<br>вмиснмппровидер
<br>WorkFolders-Server
<br>WSS-Product-Package

</div>