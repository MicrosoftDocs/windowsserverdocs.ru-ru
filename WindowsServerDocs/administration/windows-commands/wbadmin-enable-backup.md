---
title: wbadmin enable backup
description: Справочная статья по команде Wbadmin enable backup, которая создает и включает ежедневное расписание резервного копирования или изменяет существующее расписание резервного копирования.
ms.topic: reference
ms.assetid: c0e57f8a-70fa-4c60-9754-e762e8ad8772
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: c837ad2ae03528a20bd8a1527111b9e2825cb4d3
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804537"
---
# <a name="wbadmin-enable-backup"></a>wbadmin enable backup

Создает и включает ежедневное расписание резервного копирования или изменяет существующее расписание резервного копирования. Если параметры не указаны, отображаются текущие запланированные параметры архивации.

Чтобы настроить или изменить расписание ежедневного резервного копирования с помощью этой команды, необходимо быть членом группы " **Операторы архива** " или " **Администраторы** ". Кроме того, необходимо запустить программу **Wbadmin** из командной строки с повышенными привилегиями, щелкнув правой кнопкой мыши **командную строку** и выбрав команду **Запуск от имени администратора**.

Чтобы просмотреть значение идентификатора диска для дисков, выполните команду [Wbadmin get Disks](wbadmin-get-disks.md) .

## <a name="syntax"></a>Синтаксис

```
wbadmin enable backup [-addtarget:<BackupTarget>] [-removetarget:<BackupTarget>] [-schedule:<TimeToRunBackup>] [-include:<VolumesToInclude>] [-nonRecurseInclude:<ItemsToInclude>] [-exclude:<ItemsToExclude>] [-nonRecurseExclude:<ItemsToExclude>][-systemState] [-hyperv:<HyperVComponentsToExclude>] [-allCritical] [-systemState] [-vssFull | -vssCopy] [-user:<UserName>] [-password:<Password>] [-allowDeleteOldBackups]  [-quiet]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| -аддтаржет | Указывает место хранения резервных копий. Необходимо указать расположение в виде диска, тома или UNC-пути к удаленной общей папке ( `\\<servername>\<sharename>` ). По умолчанию резервная копия будет сохранена в: `\\<servername>\<sharename> WindowsImageBackup <ComputerBackedUp>` . Если указан диск, диск будет отформатирован перед использованием, а все существующие данные на нем будут удалены без возможности восстановления. Если указать общую папку, вы не сможете добавить дополнительные расположения. За один раз можно указать только одну общую папку в качестве места хранения.<p>**Важно.** Если сохранить резервную копию в удаленной общей папке, эта резервная копия будет перезаписана, если вы используете ту же папку для повторного резервного копирования этого же компьютера. Кроме того, если операция резервного копирования завершится сбоем, резервное копирование может оказаться невозможным, поскольку старая резервная копия будет перезаписана, но новая резервная копия не будет использоваться. Это можно избежать, создав вложенные папки в удаленной общей папке для Организации резервных копий. В этом случае вложенные папки должны в два раза превышать пространство родительской папки.<p>В одной команде можно указать только одно расположение. Можно добавить несколько мест хранения резервных копий томов и дисков, выполнив команду еще раз. |
| -ремоветаржет | Указывает место хранения, которое необходимо удалить из существующего расписания резервного копирования. Необходимо указать расположение в качестве идентификатора диска. |
| -Schedule | Указывает время суток для создания резервной копии в формате чч: мм и разделителями-запятыми. |
| -include | Задает разделенный запятыми список элементов, включаемых в резервную копию. Можно включить несколько файлов, папок или томов. Пути к томам можно указать с помощью букв диска тома, точек подключения томов или имен томов на основе GUID. Если используется имя тома на основе GUID, оно должно заканчиваться обратной косой чертой ( `\` ). `*`При указании пути к файлу можно использовать подстановочный знак () в имени файла. |
| -Нонрекурсеинклуде | Указывает нерекурсивный, разделенный запятыми список элементов, включаемых в резервную копию. Можно включить несколько файлов, папок или томов. Пути к томам можно указать с помощью букв диска тома, точек подключения томов или имен томов на основе GUID. Если используется имя тома на основе GUID, оно должно заканчиваться обратной косой чертой ( `\` ). `*`При указании пути к файлу можно использовать подстановочный знак () в имени файла. Следует использовать, только если используется параметр **-backupTarget** . |
| — исключить | Задает разделенный запятыми список элементов, исключаемых из резервной копии. Можно исключить файлы, папки или тома. Пути к томам можно указать с помощью букв диска тома, точек подключения томов или имен томов на основе GUID. Если используется имя тома на основе GUID, оно должно заканчиваться обратной косой чертой ( `\` ). `*`При указании пути к файлу можно использовать подстановочный знак () в имени файла. |
| -Нонрекурсиксклуде | Указывает нерекурсивный, разделенный запятыми список элементов, исключаемых из резервной копии. Можно исключить файлы, папки или тома. Пути к томам можно указать с помощью букв диска тома, точек подключения томов или имен томов на основе GUID. Если используется имя тома на основе GUID, оно должно заканчиваться обратной косой чертой ( `\` ). `*`При указании пути к файлу можно использовать подстановочный знак () в имени файла. |
| -Hyperv | Задает разделенный запятыми список компонентов, включаемых в резервную копию. Идентификатор может быть именем компонента или GUID компонента (с фигурными скобками или без них). |
| -systemState | Создает резервную копию, которая включает в себя состояние системы в дополнение к любым другим элементам, указанным с помощью параметра **-include** . Состояние системы содержит файлы загрузки (Boot.ini, НДТЛДР, NTDetect.com), реестр Windows, включая параметры COM, SYSVOL (групповые политики и сценарии входа в систему), Active Directory и NTDS. DIT на контроллерах домена и, если установлена служба сертификатов, хранилище сертификатов. Если на сервере установлена роль веб-сервера, будет включена служба IIS метакаталога. Если сервер входит в состав кластера, служба кластеров также включается информация. |
| -allCritical | Указывает, что все критические тома (тома, содержащие состояние операционной системы) будут включены в резервные копии. Этот параметр полезен при создании резервной копии для полного восстановления системы или состояния системы. Его следует использовать, только если указан **-backupTarget** ; в противном случае команда завершится ошибкой. Можно использовать с параметром **-include** .<p>**Совет.** Целевой том для резервного копирования критических томов может быть локальным диском, но не может быть любым из томов, входящих в резервную копию. |
| -Вссфулл | Выполняет полное резервное копирование с помощью служба теневого копирования томов (VSS). Выполняется резервное копирование всех файлов. журнал каждого файла обновляется с учетом того, что была создана резервная копия, а журналы предыдущих резервных копий могут быть усечены. Если этот параметр не используется, команда [Wbadmin start backup](wbadmin-start-backup.md) создает резервную копию копии, но журнал резервных копий файлов не обновляется.<p>**Внимание!** Не используйте этот параметр, если вы используете продукт, отличный от cистема архивации данных Windows Server, для резервного копирования приложений, которые находятся на томах, включенных в текущую резервную копию. Это может привести к нарушению добавочного, разностного или другого типа резервных копий, создаваемых другим продуктом резервного копирования, так как журнал, на котором они основаны, определяет, сколько данных может отсутствовать в резервной копии, и может выполнить полное резервное копирование необязательно. |
| -Всскопи | Выполняет резервное копирование с помощью VSS. Выполняется резервное копирование всех файлов, но журнал резервных копий файлов не обновляется, поэтому вы сохраняете все данные, на которые были внесены изменения, удалены и т. д., а также любые файлы журнала приложений. Использование этого типа резервного копирования не влияет на последовательность добавочных и разностных резервных копий, которые могут происходить независимо от этой резервной копии. Это значение по умолчанию.<p>**Предупреждение:** Резервную копию нельзя использовать для добавочных или разностных резервных копий или восстановления. |
| пользователь | Указывает пользователя с разрешением на запись в место хранения резервных копий (если это удаленная общая папка). Пользователь должен быть членом группы " **Администраторы** " или " **Операторы резервного копирования** " на компьютере, на котором выполняется резервное копирование. |
| -password | Указывает пароль для имени пользователя, предоставленного параметром **-User**. |
| -Алловделетеолдбаккупс | Перезаписывает все резервные копии, созданные до обновления компьютера. |
| -quiet | Выполняет команду без запроса пользователю. |

## <a name="examples"></a>Примеры

Чтобы запланировать ежедневное резервное копирование в 9:00 AM и 6:00 PM для жестких дисков E:, Д:\маунтпоинт и `\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\` , а также для сохранения файлов на диске с именем DiskID, введите:

```
wbadmin enable backup -addtarget:DiskID -schedule:09:00,18:00 -include:E:,D:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
```

Чтобы запланировать ежедневное резервное копирование папки Д:\документс в 12:00 AM и 7:00 PM в сетевую папку `\\backupshare\backup1` , используя сетевые учетные данные для **оператора Backup**, Аарен екелунд (аекел), кто имеет пароль *$3hM9 ^ 5lp* и кто является членом домена контосоеаст, который используется для проверки подлинности доступа к сетевой папке, введите:

```
wbadmin enable backup –addtarget:\\backupshare\backup1 –include: D:\documents –user:CONTOSOEAST\aekel –password:$3hM9^5lp –schedule:00:00,19:00
```

Чтобы запланировать ежедневное резервное копирование тома T: и папку Д:\документс с 1:00 AM на диск H:, за исключением папки `d:\documents\~tmp` и выполнение полной архивации с помощью Служба теневого копирования томов, введите:

```
wbadmin enable backup –addtarget:H: –include T:,D:\documents –exclude D:\documents\~tmp –vssfull –schedule:01:00
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда Wbadmin](wbadmin.md)

- [Команда Wbadmin enable backup](wbadmin-enable-backup.md)

- [Команда Wbadmin start backup](wbadmin-start-backup.md)

- [Wbadmin get Disks, команда](wbadmin-get-disks.md)
