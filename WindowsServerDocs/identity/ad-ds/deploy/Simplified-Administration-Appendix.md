---
description: 'Дополнительные сведения: упрощенное приложение для администрирования'
ms.assetid: c911d6c6-98c6-4532-b1db-5724e1ceb96c
title: Приложение по упрощенному администрированию
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 21b379b8138e95b70ebae91b34b8955e20715b3b
ms.sourcegitcommit: 6fbe337587050300e90340f9aa3e899ff5ce1028
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/16/2020
ms.locfileid: "97599697"
---
# <a name="simplified-administration-appendix"></a>Приложение по упрощенному администрированию

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

-   [Диалоговое окно "Добавление серверов диспетчер сервера" (Active Directory)](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_AddServers)

-   [Состояние диспетчер сервера удаленного сервера](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_ServerMgrStatus)

-   [Загрузка модуля Windows PowerShell](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_PSLoadModule)

-   [Исправления выдачи RID для предыдущих операционных систем](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_Rid)

-   [Ntdsutil.exe установить из изменений носителя](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)

## <a name="server-manager-add-servers-dialog-active-directory"></a><a name="BKMK_AddServers"></a>Диалоговое окно "Добавление серверов диспетчер сервера" (Active Directory)

Диалоговое окно **Добавление серверов** позволяет выполнять поиск Active Directory для серверов, по операционной системе, с использованием подстановочных знаков и по расположению. Диалоговое окно также позволяет использовать DNS-запросы по полному доменному имени или имени префикса. Эти поисковые запросы используют собственные протоколы DNS и LDAP, реализованные с помощью .NET, а не AD Windows PowerShell для шлюза управления AD через протокол SOAP. Это означает, что контроллеры домена, на которые осуществляется обращение диспетчер сервера, могут даже работать под управлением Windows Server 2003. Кроме того, можно импортировать файл с именами серверов для целей подготовки.

Active Directory Поиск использует следующие фильтры LDAP:

```
(&(ObjectCategory=computer)

(&(ObjectCategory=computer)(cn=dc*)(OperatingSystemVersion=6.2*))

(&(ObjectCategory=computer)(OperatingSystemVersion=6.1*))

(&(ObjectCategory=computer)(OperatingSystemVersion=6.0*))

(&(ObjectCategory=computer)(|(OperatingSystemVersion=5.2*)(OperatingSystemVersion=5.1*)))

```

Active Directory поиска возвращает следующие атрибуты:

```
( dnsHostName )( operatingSystem )( cn )

```

## <a name="server-manager-remote-server-status"></a><a name="BKMK_ServerMgrStatus"></a>Состояние диспетчер сервера удаленного сервера
Диспетчер сервера проверяет доступность удаленного сервера с помощью протокола маршрутизации адресов. Любые серверы, не отвечающие на запросы ARP, не перечисляются, даже если они находятся в пуле.

Если служба ARP отвечает, то для возврата сведений о состоянии серверу устанавливаются подключения DCOM и WMI. Если RPC, DCOM и WMI недостижимы, диспетчер сервера не сможет полностью управлять сервером.

## <a name="windows-powershell-module-loading"></a><a name="BKMK_PSLoadModule"></a>Загрузка модуля Windows PowerShell
Windows PowerShell 3,0 реализует динамическую загрузку модулей. Использование командлета **Import-Module** , как правило, больше не требуется; Вместо этого при простом вызове командлета, псевдонима или функции автоматически загружается модуль.

Чтобы просмотреть загруженные модули, используйте командлет **Get-Module** .

```
Get-Module

```

![Упрощенное администрирование](media/Simplified-Administration-Appendix/ADDS_PSGetModule.gif)

Чтобы просмотреть все установленные модули с экспортированными функциями и командлетами, используйте:

```
Get-Module -ListAvailable

```

Главным случаем использования команды **Import-Module** является необходимость доступа к виртуальному диску "AD:" Windows PowerShell и еще не загружен модуль. Например, с помощью следующих команд:

```
import-module activedirectory
cd ad:
dir

```

## <a name="rid-issuance-hotfixes-for-previous-operating-systems"></a><a name="BKMK_Rid"></a>Исправления выдачи RID для предыдущих операционных систем
Ознакомьтесь с [обновлением, которое позволяет обнаруживать и предотвращать слишком большое потребление глобального пула RID на контроллере домена, работающем под Windows Server 2008 R2](https://support.microsoft.com/kb/2618669).

## <a name="ntdsutilexe-install-from-media-changes"></a><a name="BKMK_IFM"></a>Ntdsutil.exe установить из изменений носителя
Windows Server 2012 добавляет два дополнительных параметра в программу командной строки Ntdsutil.exe для меню **ifm (создание носителя IFM)** . Они позволяют создавать хранилища IFM без предварительного выполнения автономного дефрагментации экспортированного NTDS. Файл базы данных DIT. Если место на диске не является расширенным, это экономит время на создание IFM.

В следующей таблице описаны два новых пункта меню:

|Menu Item|Объяснение|
|--|--|
|Создание полной Нодефраг% s|Создание носителя IFM без дефрагментации полного контроллера домена AD или экземпляра AD/LDS в папке% s|
|Создание полного SYSVOL Нодефраг% s|Создание носителя IFM с SYSVOL и без дефрагментации для полного контроллера домена AD в папке% s|

![Снимок экрана окна терминала, в котором показан процесс создания носителя IFM.](media/Simplified-Administration-Appendix/ADDS_PSIFM.png)

![Снимок экрана: окно терминала, в котором показан носитель IFM, успешно создан.](media/Simplified-Administration-Appendix/ADDS_PSIFMComplete.gif)
