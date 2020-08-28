---
title: bitsadmin
description: Справочная статья по команде битсадмин, которая представляет собой средство командной строки, используемое для создания, загрузки и передачи заданий и отслеживания хода выполнения.
ms.topic: reference
ms.assetid: 4853036e-1df8-45ad-8be6-cfb097b8dd27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3744d45265b0b0ae7143d1e37c5e53511a23e26a
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034613"
---
# <a name="bitsadmin"></a>bitsadmin

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10

Битсадмин — это средство командной строки, используемое для создания, загрузки и передачи заданий, а также для отслеживания хода выполнения. Средство битсадмин использует параметры для указания выполняемой работы. `bitsadmin /?` `bitsadmin /help` Для получения списка параметров можно вызвать метод или.

Для большинства параметров требуется `<job>` параметр, для которого задано отображаемое имя задания или идентификатор GUID. Отображаемое имя задания не обязательно должно быть уникальным. Параметры **/CREATE** и **/List** возвращают идентификатор GUID задания.

По умолчанию можно получить доступ к сведениям о собственных заданиях. Для доступа к сведениям о заданиях другого пользователя необходимо иметь права администратора. Если задание было создано в состоянии с повышенными привилегиями, необходимо запустить **битсадмин** из окна с повышенными привилегиями; в противном случае у вас будет доступ к заданию только для чтения.

Многие из параметров соответствуют методам в [интерфейсах BITS](/windows/win32/bits/bits-interfaces). Дополнительные сведения, которые могут быть связаны с использованием параметра, см. в соответствующем методе.

Используйте следующие параметры для создания задания, задания и получения свойств задания, а также для наблюдения за состоянием задания. Примеры, демонстрирующие использование некоторых из этих параметров для выполнения задач, см. в разделе [битсадмин examples](bitsadmin-examples.md).

## <a name="available-switches"></a>Доступные параметры

- [битсадмин/AddFile](bitsadmin-addfile.md)
- [битсадмин/аддфилесет](bitsadmin-addfileset.md)
- [битсадмин/аддфилевисранжес](bitsadmin-addfilewithranges.md)
- [битсадмин/Cache](bitsadmin-cache.md)
- [битсадмин/Cache/Delete](bitsadmin-cache-and-delete.md)
- [битсадмин/Cache/делетеурл](bitsadmin-cache-and-deleteurl.md)
- [битсадмин/Cache/жетекспиратионтиме](bitsadmin-cache-and-getexpirationtime.md)
- [битсадмин/Cache/жетлимит](bitsadmin-cache-and-getlimit.md)
- [битсадмин/Cache/Help](bitsadmin-cache-and-help.md)
- [битсадмин/Cache/info](bitsadmin-cache-and-info.md)
- [битсадмин/Cache/List](bitsadmin-cache-and-list.md)
- [битсадмин/Cache/сетекспиратионтиме](bitsadmin-cache-and-setexpirationtime.md)
- [битсадмин/Cache/сетлимит](bitsadmin-cache-and-setlimit.md)
- [битсадмин/Cache/Clear](bitsadmin-cache-clear.md)
- [битсадмин/канцел](bitsadmin-cancel.md)
- [битсадмин/комплете](bitsadmin-complete.md)
- [битсадмин/CREATE](bitsadmin-create.md)
- [битсадмин/ексамплес](bitsadmin-examples.md)
- [битсадмин/жетаклфлагс](bitsadmin-getaclflags.md)
- [битсадмин/жетбитестотал](bitsadmin-getbytestotal.md)
- [битсадмин/жетбитестрансферред](bitsadmin-getbytestransferred.md)
- [битсадмин/жетклиентцертификате](bitsadmin-getclientcertificate.md)
- [битсадмин/жеткомплетионтиме](bitsadmin-getcompletiontime.md)
- [битсадмин/жеткреатионтиме](bitsadmin-getcreationtime.md)
- [битсадмин/жеткустомхеадерс](bitsadmin-getcustomheaders.md)
- [битсадмин/жетдескриптион](bitsadmin-getdescription.md)
- [битсадмин/жетдисплайнаме](bitsadmin-getdisplayname.md)
- [битсадмин/жетеррор](bitsadmin-geterror.md)
- [битсадмин/жетерроркаунт](bitsadmin-geterrorcount.md)
- [битсадмин/жетфилестотал](bitsadmin-getfilestotal.md)
- [битсадмин/жетфилестрансферред](bitsadmin-getfilestransferred.md)
- [битсадмин/жеселпертокенфлагс](bitsadmin-gethelpertokenflags.md)
- [битсадмин/жеселпертокенсид](bitsadmin-gethelpertokensid.md)
- [битсадмин/жесттпмесод](bitsadmin-gethttpmethod.md)
- [битсадмин/жетмаксдовнлоадтиме](bitsadmin-getmaxdownloadtime.md)
- [битсадмин/жетминретриделай](bitsadmin-getminretrydelay.md)
- [битсадмин/жетмодификатионтиме](bitsadmin-getmodificationtime.md)
- [битсадмин/жетнопрогресстимеаут](bitsadmin-getnoprogresstimeout.md)
- [битсадмин/жетнотификмдлине](bitsadmin-getnotifycmdline.md)
- [битсадмин/жетнотифифлагс](bitsadmin-getnotifyflags.md)
- [битсадмин/жетнотифинтерфаце](bitsadmin-getnotifyinterface.md)
- [битсадмин/жетовнер](bitsadmin-getowner.md)
- [битсадмин/жетпиркачингфлагс](bitsadmin-getpeercachingflags.md)
- [битсадмин/жетприорити](bitsadmin-getpriority.md)
- [битсадмин/жетпроксибипасслист](bitsadmin-getproxybypasslist.md)
- [битсадмин/жетпроксилист](bitsadmin-getproxylist.md)
- [битсадмин/жетпроксюсаже](bitsadmin-getproxyusage.md)
- [битсадмин/жетреплидата](bitsadmin-getreplydata.md)
- [битсадмин/жетреплифиленаме](bitsadmin-getreplyfilename.md)
- [битсадмин/жетреплипрогресс](bitsadmin-getreplyprogress.md)
- [битсадмин/жетсекуритифлагс](bitsadmin-getsecurityflags.md)
- [битсадмин/жетстате](bitsadmin-getstate.md)
- [битсадмин/жеттемпораринаме](bitsadmin-gettemporaryname.md)
- [битсадмин/жеттипе](bitsadmin-gettype.md)
- [битсадмин/жетвалидатионстате](bitsadmin-getvalidationstate.md)
- [битсадмин/Help](bitsadmin-help.md)
- [битсадмин/info](bitsadmin-info.md)
- [битсадмин/List](bitsadmin-list.md)
- [битсадмин/листфилес](bitsadmin-listfiles.md)
- [битсадмин/макекустомхеадерсвритеонли](bitsadmin-makecustomheaderswriteonly.md)
- [битсадмин/монитор](bitsadmin-monitor.md)
- [битсадмин/новрап](bitsadmin-nowrap.md)
- [битсадмин/пиркачинг](bitsadmin-peercaching.md)
- [битсадмин/пиркачинг/жетконфигуратионфлагс](bitsadmin-peercaching-and-getconfigurationflags.md)
- [битсадмин/пиркачинг/Help](bitsadmin-peercaching-and-help.md)
- [битсадмин/пиркачинг/сетконфигуратионфлагс](bitsadmin-peercaching-and-setconfigurationflags.md)
- [битсадмин/Пирс](bitsadmin-peers.md)
- [битсадмин/Пирс/Clear](bitsadmin-peers-and-clear.md)
- [битсадмин/Пирс/Дисковер](bitsadmin-peers-and-discover.md)
- [битсадмин/Пирс/Help](bitsadmin-peers-and-help.md)
- [битсадмин/Пирс/List](bitsadmin-peers-and-list.md)
- [битсадмин/равретурн](bitsadmin-rawreturn.md)
- [битсадмин/ремовеклиентцертификате](bitsadmin-removeclientcertificate.md)
- [битсадмин/ремовекредентиалс](bitsadmin-removecredentials.md)
- [битсадмин/реплацеремотепрефикс](bitsadmin-replaceremoteprefix.md)
- [битсадмин/Reset](bitsadmin-reset.md)
- [битсадмин/Resume](bitsadmin-resume.md)
- [битсадмин/сетаклфлаг](bitsadmin-setaclflag.md)
- [битсадмин/сетклиентцертификатебид](bitsadmin-setclientcertificatebyid.md)
- [битсадмин/сетклиентцертификатебинаме](bitsadmin-setclientcertificatebyname.md)
- [битсадмин/сеткредентиалс](bitsadmin-setcredentials.md)
- [битсадмин/сеткустомхеадерс](bitsadmin-setcustomheaders.md)
- [битсадмин/сетдескриптион](bitsadmin-setdescription.md)
- [битсадмин/сетдисплайнаме](bitsadmin-setdisplayname.md)
- [битсадмин/сеселпертокен](bitsadmin-sethelpertoken.md)
- [битсадмин/сеселпертокенфлагс](bitsadmin-sethelpertokenflags.md)
- [битсадмин/сесттпмесод](bitsadmin-sethttpmethod.md)
- [битсадмин/сетмаксдовнлоадтиме](bitsadmin-setmaxdownloadtime.md)
- [битсадмин/сетминретриделай](bitsadmin-setminretrydelay.md)
- [битсадмин/сетнопрогресстимеаут](bitsadmin-setnoprogresstimeout.md)
- [битсадмин/сетнотификмдлине](bitsadmin-setnotifycmdline.md)
- [битсадмин/сетнотифифлагс](bitsadmin-setnotifyflags.md)
- [битсадмин/сетпиркачингфлагс](bitsadmin-setpeercachingflags.md)
- [битсадмин/сетприорити](bitsadmin-setpriority.md)
- [битсадмин/сетпроксисеттингс](bitsadmin-setproxysettings.md)
- [битсадмин/сетреплифиленаме](bitsadmin-setreplyfilename.md)
- [битсадмин/сетсекуритифлагс](bitsadmin-setsecurityflags.md)
- [битсадмин/сетвалидатионстате](bitsadmin-setvalidationstate.md)
- [битсадмин/суспенд](bitsadmin-suspend.md)
- [битсадмин/такеовнершип](bitsadmin-takeownership.md)
- [битсадмин/Трансфер](bitsadmin-transfer.md)
- [битсадмин/утил](bitsadmin-util.md)
- [битсадмин/утил/енаблеаналитикчаннел](bitsadmin-util-and-enableanalyticchannel.md)
- [битсадмин/утил/жетиепрокси](bitsadmin-util-and-getieproxy.md)
- [битсадмин/утил/Help](bitsadmin-util-and-help.md)
- [битсадмин/утил/репаирсервице](bitsadmin-util-and-repairservice.md)
- [битсадмин/утил/сетиепрокси](bitsadmin-util-and-setieproxy.md)
- [битсадмин/утил/Version](bitsadmin-util-and-version.md)
- [битсадмин/ВРАП](bitsadmin-wrap.md)
