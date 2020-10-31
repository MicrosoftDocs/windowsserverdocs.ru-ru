---
ms.assetid: 7e195f5b-b194-40f3-a26d-5cf4ade5fc4d
title: Командлеты Windows PowerShell для резервного копирования и восстановления ЦС
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 1a36e72858e5ea2ae95cc0f1730e5906b3c85866
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93070736"
---
# <a name="ca-backup-and-restore-windows-powershell-cmdlets"></a>Командлеты Windows PowerShell для резервного копирования и восстановления ЦС

> Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
>
> **Автор** : Джастин Тернер, старший инженер по расширению поддержки с группой Windows
>
> [!NOTE]
> Этот материал создан инженером службы поддержки клиентов Майкрософт и предназначен для опытных администраторов и архитекторов систем, которым нужны более глубокие технические сведения о функциях и решениях в Windows Server 2012 R2, а не обычная информация, доступная в статьях на сайте TechNet. Однако он не был отредактирован согласно требованиям сайта, поэтому некоторые формулировки могут быть не такими выверенными, как на станицах TechNet.

## <a name="overview"></a>Обзор
Модуль Адксадминистратион Windows PowerShell появился в Window Server 2012.  В этот модуль в Windows Server 2012 R2 были добавлены два новых командлета для поддержки резервного копирования и восстановления центра сертификации.

-   Backup-CARoleService

-   Restore-CARoleService

## <a name="backup-caroleservice"></a>Backup-CARoleService
**Таблица SEQ таблица \\ \* арабский 17: командлеты Backup и RESTORE Windows PowerShell**

**Командлет Адксадминистратион: Backup-Каролесервице**

|Аргументы — требуются аргументы **полужирного шрифта**|Описание|
|------------------------------------------------|---------------|
|**-Path**|-Строка — место для сохранения резервной копии<br />— Это единственный безымянный параметр.<br />-Позиционированный параметр<p>**Пример** .<p>Backup-Каролесервице.-путь c:\adcsbackup1<p>Backup-CARoleService c:\adcsbackup2|
|-Кэйонли|— Резервное копирование сертификата ЦС без базы данных;<p>**Пример** .<p>Backup-CARoleService c:\adcsbackup3 — Кэйонли|
|-Password|— Указывает пароль для защиты сертификатов ЦС и закрытых ключей.<br />— Должна быть защищенной строкой<br />-Недопустимо с параметром-Датабасеонли<p>Пример<p>Backup-CARoleService c:\adcsbackup4-Password (чтение-хост-запрос "пароль:"-AsSecureString)<p>Backup-CARoleService c:\adcsbackup5-Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText-Force)|
|-Датабасеонли|— Резервное копирование базы данных без сертификата ЦС;<p>Backup-CARoleService c:\adcsbackup6 — Датабасеонли|
|-Force|1. позволяет перезаписать резервную копию, которая существует в расположении, указанном в параметре-Path.<p>Backup-CARoleService c:\adcsbackup1-Force|
|-Добавочное|-Выполнить добавочное резервное копирование<p>Backup-CARoleService c:\adcsbackup7 — добавочный|
|-Киплог|1. указывает команде на необходимость сохранения файлов журнала. Если параметр не указан, файлы журнала усекаются по умолчанию, за исключением случая добавочного сценария.<p>Backup-CARoleService c:\adcsbackup7 — Киплог|

### <a name="-password-secure-string"></a>-Password <Secure String>
Если используется параметр-Password, указанный пароль должен быть защищенной строкой.  Используйте командлет **Read-Host** для запуска интерактивного запроса на ввод безопасного пароля или используйте командлет **ConvertTo-SecureString** , чтобы указать пароль в строке.

Ознакомьтесь со следующими примерами.

**Указание защищенной строки для параметра пароля с помощью командлета Read-Host**

```powershell
Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)
```

**Указание защищенной строки для параметра Password с помощью ConvertTo-SecureString**

```powershell
Backup-CARoleService c:\adcsbackup5 -Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force)
```

## <a name="restore-caroleservice"></a>Restore-CARoleService
**Командлет Адксадминистратион: Restore-Каролесервице**

|Аргументы — требуются аргументы **полужирного шрифта**|Описание|
|------------------------------------------------|---------------|
|**-Path**|-Строка — расположение для восстановления резервной копии<br />— Это единственный безымянный параметр.<br />-Позиционированный параметр<p>**Пример** .<p>Restore-Каролесервице.-path c:\adcsbackup1 — Force<p>Restore-CARoleService c:\adcsbackup2-Force|
|-Кэйонли|— Восстановить сертификат ЦС без базы данных;<br />— Необходимо указать, если резервная копия была сделана с параметром-Кэйонли<p>**Пример** .<p>Restore-CARoleService c:\adcsbackup3-Кэйонли-Force|
|-Password|— Указывает пароль сертификатов ЦС и закрытых ключей.<br />— Должна быть защищенной строкой<p>**Пример** .<p>Restore-CARoleService c:\adcsbackup4-Password (чтение-хост-запрос "пароль:"-AsSecureString)-Force<p>Restore-CARoleService c:\adcsbackup5-Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText-Force) — Force|
|-Датабасеонли|Восстановление базы данных без сертификата ЦС<p>Restore-CARoleService c:\adcsbackup6 — Датабасеонли|
|-Force|— Позволяет перезаписать существующие ключи<br />— Необязательный параметр, но при восстановлении на месте, скорее всего, требуется<p>Restore-CARoleService c:\adcsbackup1-Force|

### <a name="issues"></a>Проблемы
Резервная копия, не защищенная паролем, создается в случае сбоя функции ConvertTo-SecureString при использовании Backup-CARoleService с параметром-password.

![Резервное копирование и восстановление ЦС](media/CA-Backup-and-Restore-Windows-PowerShell-cmdlets/GTR_ADDS_BackupCARole.gif)

**Таблица SEQ таблица, \\ \* Арабская 18. распространенные ошибки**

|Действие|Ошибка|Комментировать|
|----------|---------|-----------|
|**Restore-Каролесервице К:\адксбаккуп**|Restore-CARoleService: процесс не может получить доступ к файлу, так как он используется другим процессом. (Exception from HRESULT:<p>0x80070020|Прежде чем запускать командлет Restore-CARoleService, закройте Active Directory службы сертификатов.|
|**Restore-Каролесервице К:\адксбаккуп**|Restore-CARoleService: Каталог не пуст. (Исключение из HRESULT: 0x80070091)|Используйте параметр-Force для перезаписи существующих ключей|
|**Backup-Каролесервице К:\адксбаккуп-пароль (чтение-хост-запрос "пароль:"-AsSecureString)-Датабасеонли**|Backup-CARoleService: не удается разрешить набор параметров с использованием указанных именованных параметров.|Параметр-Password используется только для защиты паролем закрытых ключей и, следовательно, является недопустимым, если архивация не выполняется|
|**Restore-Каролесервице C:\ADCSBack15-Password (чтение-хост-запрос "пароль:"-AsSecureString)-Датабасеонли**|Restore-CARoleService: не удается разрешить набор параметров с использованием указанных именованных параметров.|Параметр-Password используется только для защиты паролем закрытых ключей и поэтому является недопустимым, если вы не восстанавливаете их.|
|**Restore-Каролесервице C:\ADCSBack14-Password (чтение-хост-запрос "пароль:"-AsSecureString)**|Restore-CARoleService: системе не удается найти указанный файл. (Исключение из HRESULT: 0x80070002)|Указанный путь не содержит допустимой резервной копии базы данных.  Возможно, путь является недопустимым или резервная копия была сделана с параметром-Кэйсонли?|

## <a name="additional-resources"></a>Дополнительные ресурсы
[Руководство по переносу служб сертификатов Active Directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee126170(v=ws.10))

[Резервное копирование базы данных и закрытого ключа ЦС](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee126140(v=ws.10)#BKMK_BackUpDB)

[Восстановление базы данных и конфигурации ЦС на сервере назначения](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee126140(v=ws.10)#BKMK_RestoreCA)

## <a name="try-this-backup-the-ca-in-your-lab-using-windows-powershell"></a>Попробуйте сделать это: Создайте резервную копию центра сертификации в лаборатории с помощью Windows PowerShell

1.  Используйте команды на этом занятии, чтобы создать резервную копию базы данных ЦС и закрытого ключа, защищенных паролем.

2.  Подождите, пока не будет восстановлен ЦС.

