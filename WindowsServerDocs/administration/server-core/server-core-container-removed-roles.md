---
title: Роли, службы ролей и компоненты, отсутствующие в контейнерах Server Core — Windows Server, версия 1803
description: Сведения о ролях и функциях, удаленных из образа контейнера Server Core для Windows Server.
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.openlocfilehash: 2092e330af479ae0cbdb1da88ba87cf233307b59
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993257"
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
<br>BitLocker — служебные программы
<br>BitLocker
<br>BITS
<br>Битсекстенсионс — отправка
<br>ккффилтер
<br>цертификатинроллментполицисервер
<br>цертификатинроллментсервер
<br>цертификатесервицес
<br>Клиентфорнфс — инфраструктура
<br>Контейнеры
<br>корефилесервер
<br>DataCenterBridging-LLDP-средства
<br>DataCenterBridging
<br>Дедупликация — ядро
<br>девицехеалсаттестатионсервице
<br>ДФСН — сервер
<br>DFSR-Infrastructure-Сервередитион
<br>DirectoryServices — Адам
<br>DirectoryServices — DomainController
<br>Дискио — качество обслуживания
<br>енханцедстораже
<br>Фаиловерклустер — пакет AdminPak
<br>Фаиловерклустер — Аутоматионсервер
<br>Фаиловерклустер — Кмдинтерфаце
<br>Фаиловерклустер — Фуллсервер
<br>Фаиловерклустер-PowerShell
<br>Файловые службы
<br>филесервервссажент
<br>Инфраструктура FRS
<br>FSRM-Infrastructure-службы
<br>FSRM — инфраструктура
<br>харденедфабриценкриптионтаск
<br>хостгуардиан
<br>HostGuardianService-Package
<br>IdentityServer — SecurityTokenService
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
<br>МСРДК — инфраструктура
<br>мултипасио
<br>нетворкконтроллер
<br>нетворкконтроллертулс
<br>нетворкдевицеенроллментсервицес
<br>нетворклоадбаланЦингфуллсервер
<br>нетворквиртуализатион
<br>онлинеревокатионсервицес
<br>P2P-Пнрпонли
<br>Относительно
<br>Печать — пользовательский интерфейс пользователя
<br>Печать — Лпдпринтсервице
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
<br>Ригхтсманажементсервицес — роль
<br>ригхтсманажементсервицес
<br>RMS — Федерация
<br>Сбмгр — пользовательский интерфейс
<br>ServerCore-Drivers-General-WOW64
<br>ServerCore-Drivers-General
<br>Серверфорнфс — инфраструктура
<br>ServerManager-Core-RSAT-Feature-Tools
<br>сервермедиафаундатион
<br>ServerMigration
<br>сессиондиректори
<br>сетупандбутевентколлектион
<br>шиелдедвмтулсадминпакк
<br>SMB1Protocol — сервер
<br>смбдирект
<br>смбхашженератион
<br>смбвитнесс
<br>SNMP
<br>софтварелоадбаланцер
<br>Хранилище-реплика — Админпакк
<br>Хранилище — реплика
<br>TPM-КОМАНДНОМ PSH-командлеты
<br>UpdateServices — база данных
<br>UpdateServices — службы
<br>UpdateServices — Виддатабасе
<br>UpdateServices
<br>вмхостажент
<br>Волумеактиватион — полная роль
<br>Веб-приложение-прокси
<br>Доступ к данным
<br>вебенроллментсервицес
<br>Защитник Windows
<br>Архивы
<br>виндовссторажеманажементсервице
<br>винсрунтиме
<br>вмиснмппровидер
<br>Воркфолдерс — сервер
<br>WSS-Product-Package

</div>