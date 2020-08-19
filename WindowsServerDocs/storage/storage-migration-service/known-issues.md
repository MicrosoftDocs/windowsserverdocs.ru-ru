---
title: Известные проблемы со службой миграции хранилища
description: Известные проблемы и устранение неполадок службы миграции хранилища, например получение журналов для служба поддержки Майкрософт.
author: nedpyle
ms.author: nedpyle
manager: tiaascs
ms.date: 07/29/2020
ms.topic: article
ms.openlocfilehash: 0dc49603099427fb00507db021c391500a7c42f2
ms.sourcegitcommit: 3d59c2aaebcd190b20d24bc8a449eee0681b6a3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/19/2020
ms.locfileid: "88583319"
---
# <a name="storage-migration-service-known-issues"></a>Известные проблемы со службой миграции хранилища

Этот раздел содержит ответы на известные проблемы, возникающие при использовании [службы миграции хранилища](overview.md) для миграции серверов.

Служба миграции хранилища выпускается в два этапа: служба в Windows Server и пользовательский интерфейс в центре администрирования Windows. Служба доступна в Windows Server, долгосрочном канале обслуживания, а также на Windows Server, полугодовой канал; Хотя центр администрирования Windows доступен для загрузки отдельно. Мы также периодически включаем изменения в накопительные обновления для Windows Server, выпущенные с помощью Центр обновления Windows.

Например, Windows Server версии 1903 включает новые функции и исправления для службы миграции хранилища, которые также доступны для Windows Server 2019 и Windows Server версии 1809 путем установки [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534).

## <a name="how-to-collect-log-files-when-working-with-microsoft-support"></a><a name="collecting-logs"></a> Как получать файлы журналов при работе с служба поддержки Майкрософт

Служба миграции хранилища содержит журналы событий для службы Orchestrator и прокси-службы. Сервер Orchestrator всегда содержит оба журнала событий, а целевые серверы с установленной службой прокси содержат журналы прокси-сервера. Эти журналы находятся в папке:

- Журналы приложений и служб \ Microsoft \ Windows \ Сторажемигратионсервице
- Журналы приложений и служб \ Microsoft \ Windows \ Сторажемигратионсервице-proxy

Если необходимо собрать эти журналы для просмотра в автономном режиме или для отправки в служба поддержки Майкрософт, в GitHub доступен сценарий PowerShell с открытым кодом:

 [Вспомогательная служба службы миграции хранилища](https://aka.ms/smslogs)

Ознакомьтесь с ФАЙЛОМ README для использования.

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>Служба миграции хранилища не отображается в центре администрирования Windows, если управление Windows Server 2019 не выполняется.

При использовании версии 1809 центра администрирования Windows для управления Windows Server 2019 Orchestrator не отображается параметр средства для службы миграции хранилища.

Расширение "Служба миграции хранилища центра администрирования Windows" привязано к версии только для Windows Server 2019 версии 1809 или более поздних операционных систем. Если вы используете ее для управления более старыми операционными системами Windows Server или предварительными версиями Insider Preview, это средство не будет отображаться. В этом весь замысел.

Чтобы разрешить, используйте или обновите до Windows Server 2019 Build 1809 или более поздней версии.

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>Сбой проверки прямую миграцию службы миграции хранилища с ошибкой "отказано в доступе для политики фильтрации токенов на конечном компьютере"

При выполнении проверки прямую миграцию появляется сообщение об ошибке "ошибка: доступ запрещен для политики фильтрации маркеров на конечном компьютере". Это происходит даже в том случае, если указаны правильные учетные данные локального администратора для исходного и конечного компьютеров.

Эта проблема была исправлена в обновлении [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) .

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-or-windows-server-2019-essentials-edition"></a>Служба переноса хранилища не входит в ознакомительную версию Windows Server 2019 или Windows Server 2019 Essentials

При использовании центра администрирования Windows для подключения к [ознакомительному выпуску Windows server 2019](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) или windows Server 2019 Essentials нет возможности управлять службой миграции хранилища. Служба миграции хранилища также не входит в роли и компоненты.

Эта проблема вызвана проблемой обслуживания в ознакомительной версии Windows Server 2019 и Windows Server 2019 Essentials.

Чтобы обойти эту ошибку для ознакомительной версии, установите розничную, MSDN, OEM или корпоративную лицензию Windows Server 2019 и не активируйте ее. Без активации все выпуски Windows Server работают в режиме оценки 180 дней.

Мы устранили эту ошибку в более позднем выпуске Windows Server.

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>Истекло время ожидания для службы миграции хранилища при скачивании CSV-файла ошибки переноса

При использовании Windows Admin Center или PowerShell для загрузки подробных сведений об ошибках операций перемещения — только журнал CSV, появляется сообщение об ошибке:

```
Transfer Log - Please check file sharing is allowed in your firewall. : This request operation sent to net.tcp://localhost:28940/sms/service/1/transfer did not receive a reply within the configured timeout (00:01:00). The time allotted to this operation may have been a portion of a longer timeout. This may be because the service is still processing the operation or because the service was unable to send a reply message. Please consider increasing the operation timeout (by casting the channel/proxy to IContextChannel and setting the OperationTimeout property) and ensure that the service is able to connect to the client.
```

Эта проблема вызвана очень большим количеством переданных файлов, которые не могут быть отфильтрованы по умолчанию в течение минуты времени ожидания, разрешенного службой миграции хранилища.

Чтобы обойти эту ошибку, сделайте следующее:

1. На компьютере Orchestrator измените файл *% systemroot% \SMS\Microsoft.StorageMigration.Service.exe.config* с помощью Notepad.exe, чтобы изменить значение "SendTimeout" с 1 минуты по умолчанию на 10 минут.

    ```
    <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:10:00"
    ```

2. Перезапустите службу "Служба миграции хранилища" на компьютере Orchestrator.

3. На компьютере Orchestrator запустите Regedit.exe

4. Найдите и выберите следующий подраздел реестра.

    `HKEY_LOCAL_MACHINE\Software\Microsoft\SMSPowershell`

5. В меню "Правка" выберите пункт "Создать", а затем выберите "Значение DWORD".

6. Введите "Вкфоператионтимеаутинминутес" в качестве имени DWORD и нажмите клавишу ВВОД.

7. Щелкните правой кнопкой мыши "Вкфоператионтимеаутинминутес" и выберите команду "Изменить".

8. В поле Базовые данные щелкните "десятичное число"

9. В поле данные значения введите "10", а затем нажмите кнопку ОК.

10. Закройте редактор реестра.

11. Попытайтесь снова скачать CSV-файл с ошибками.

Мы планируем изменить это поведение в более позднем выпуске Windows Server 2019.

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>Предупреждения проверки для прокси-сервера назначения и права администратора учетных данных

При проверке задания перемещения отображаются следующие предупреждения.

```
The credential has administrative privileges.
Warning: Action isn't available remotely.
The destination proxy is registered.
Warning: The destination proxy wasn't found.
```

Если вы не установили прокси-службу службы миграции хранилища на конечный компьютер с Windows Server 2019, или на целевом компьютере установлена ОС Windows Server 2016 или Windows Server 2012 R2, это поведение предназначено для разработки. Мы рекомендуем перейти на компьютер под Windows Server 2019 с установленным прокси-сервером, чтобы значительно повысить производительность переноса.

## <a name="certain-files-dont-inventory-or-transfer-error-5-access-is-denied"></a>Некоторые файлы не переносятся или передаются, ошибка 5 "доступ запрещен"

При инвентаризации или передаче файлов из источника на конечные компьютеры файлы, с которых пользователь удалил разрешения для группы "Администраторы", не смогут выполнить миграцию. Проверка службы миграции хранилища — Отладка прокси показывает:

```
Log Name: Microsoft-Windows-StorageMigrationService-Proxy/Debug
Source: Microsoft-Windows-StorageMigrationService-Proxy
Date: 2/26/2019 9:00:04 AM
Event ID: 10000
Task Category: None
Level: Error
Keywords:
User: NETWORK SERVICE
Computer: srv1.contoso.com
Description:

02/26/2019-09:00:04.860 [Error] Transfer error for \\srv1.contoso.com\public\indy.png: (5) Access is denied.
Stack Trace:
at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.OpenFile(String fileName, DesiredAccess desiredAccess, ShareMode shareMode, CreationDisposition creationDisposition, FlagsAndAttributes flagsAndAttributes)
at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile(String path)
at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetTargetFile(FileInfo file)
at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.InitializeSourceFileInfo()
     at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.Transfer()
at Microsoft.StorageMigration.Proxy.Service.Transfer.FileTransfer.TryTransfer()
```

Эта проблема вызвана дефектом кода в службе миграции хранилища, в котором не были вызваны права на резервное копирование.

Чтобы устранить эту проблему, установите [Центр обновления Windows 2 апреля 2019 г. — KB4490481 (сборка ос 17763,404)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481) на компьютере Orchestrator и конечном компьютере, если прокси-служба установлена там. Убедитесь, что исходная учетная запись миграции пользователя является локальным администратором на исходном компьютере и службой миграции хранилища Orchestrator. Убедитесь, что учетная запись миграции конечного пользователя является локальным администратором на конечном компьютере и службой миграции хранилища Orchestrator.

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>Несоответствие хэшей DFSR при использовании службы миграции хранилища для предзаполнения данных

При использовании службы миграции хранилища для переноса файлов в новое место назначения и последующей настройки репликация DFS для репликации этих данных с помощью существующего сервера через предварительно заполненную репликацию или репликация DFS клонирование базы данных все файлы будут испытывать несоответствие хэша и повторно реплицироваться. Все потоки данных, потоки безопасности, размеры и атрибуты вполне соответствуют друг другу после использования службы миграции хранилища для их переноса. При проверке файлов с помощью ICACLS или репликация DFS журнала отладки клонирования базы данных выясняется:

### <a name="source-file"></a>Исходный файл
```
  icacls d:\test\Source:

  icacls d:\test\thatcher.png /save out.txt /t thatcher.png
  D:AI(A;;FA;;;BA)(A;;0x1200a9;;;DD)(A;;0x1301bf;;;DU)(A;ID;FA;;;BA)(A;ID;FA;;;SY)(A;ID;0x1200a9;;;BU)
```

### <a name="destination-file"></a>Целевой файл

```
  icacls d:\test\thatcher.png /save out.txt /t thatcher.png
  D:AI(A;;FA;;;BA)(A;;0x1301bf;;;DU)(A;;0x1200a9;;;DD)(A;ID;FA;;;BA)(A;ID;FA;;;SY)(A;ID;0x1200a9;;;BU)**S:PAINO_ACCESS_CONTROL**
```
### <a name="dfsr-debug-log"></a>Журнал отладки DFSR

```
   20190308 10:18:53.116 3948 DBCL  4045 [WARN] DBClone::IDTableImportUpdate Mismatch record was found.

   Local ACL hash:1BCDFE03-A18BCE01-D1AE9859-23A0A5F6
   LastWriteTime:20190308 18:09:44.876
   FileSizeLow:1131654
   FileSizeHigh:0
   Attributes:32

   Clone ACL hash:**DDC4FCE4-DDF329C4-977CED6D-F4D72A5B**
   LastWriteTime:20190308 18:09:44.876
   FileSizeLow:1131654
   FileSizeHigh:0
   Attributes:32
```

Эта проблема устранена с помощью обновления [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) .

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transferring-from-windows-server-2008-r2"></a>Ошибка "не удалось передать хранилище на любую из конечных точек" при передаче из Windows Server 2008 R2

При попытке передачи данных с исходного компьютера Windows Server 2008 R2 передача данных не происходит и возникает ошибка:

```
Couldn't transfer storage on any of the endpoints.
0x9044
```

Эта ошибка возникает, если на компьютере под Windows Server 2008 R2 не установлено полное обновление со всеми критически важными и важными обновлениями Центр обновления Windows. Особенно важно, чтобы компьютер под управлением Windows Server 2008 R2 обновлялся в целях безопасности, так как эта операционная система не содержит улучшений безопасности более новых версий Windows Server.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>Ошибка "не удалось переместить хранилище на любую из конечных точек" и "проверить, подключено ли исходное устройство к сети."

При попытке пересылки данных с исходного компьютера некоторые или все общие папки не передаются, за которыми возникает ошибка:

```
Couldn't transfer storage on any of the endpoints.
0x9044
```

При проверке сведений о переносе SMB отображается ошибка:

```
Check if the source device is online - we couldn't access it.
```

Просмотр журнала событий Сторажемигратионсервице/Admin показывает:

```
Couldn't transfer storage.

Job: Job1
ID:
State: Failed
Error: 36931
Error Message:

Guidance: Check the detailed error and make sure the transfer requirements are met. The transfer job couldn't transfer any source and destination computers. This could be because the orchestrator computer couldn't reach any source or destination computers, possibly due to a firewall rule, or missing permissions.
```

При проверке журнала Сторажемигратионсервице-proxy/Debug отображаются следующие сведения:

```
07/02/2019-13:35:57.231 [Error] Transfer validation failed. ErrorCode: 40961, Source endpoint is not reachable, or doesn't exist, or source credentials are invalid, or authenticated user doesn't have sufficient permissions to access it.
at Microsoft.StorageMigration.Proxy.Service.Transfer.TransferOperation.Validate()
at Microsoft.StorageMigration.Proxy.Service.Transfer.TransferRequestHandler.ProcessRequest(FileTransferRequest fileTransferRequest, Guid operationId)
```

Это был дефект кода, который был бы манифестом, если у учетной записи миграции нет разрешений по крайней мере на чтение для общих ресурсов SMB. Эта проблема была впервые исправлена в накопительном обновлении [4520062](https://support.microsoft.com/help/4520062/windows-10-update-kb4520062).

## <a name="error-0x80005000-when-running-inventory"></a>Ошибка 0x80005000 при выполнении инвентаризации

После установки [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) и попытки запустить инвентаризацию происходит сбой инвентаризации с ошибками:

```
EXCEPTION FROM HRESULT: 0x80005000

Log Name:      Microsoft-Windows-StorageMigrationService/Admin
Source:        Microsoft-Windows-StorageMigrationService
Date:          9/9/2019 5:21:42 PM
Event ID:      2503
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      FS02.TailwindTraders.net
Description:
Couldn't inventory the computers.
Job: foo2
ID: 20ac3f75-4945-41d1-9a79-d11dbb57798b
State: Failed
Error: 36934
Error Message: Inventory failed for all devices
Guidance: Check the detailed error and make sure the inventory requirements are met. The job couldn't inventory any of the specified source computers. This could be because the orchestrator computer couldn't reach it over the network, possibly due to a firewall rule or missing permissions.

Log Name:      Microsoft-Windows-StorageMigrationService/Admin
Source:        Microsoft-Windows-StorageMigrationService
Date:          9/9/2019 5:21:42 PM
Event ID:      2509
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      FS02.TailwindTraders.net
Description:
Couldn't inventory a computer.
Job: foo2
Computer: FS01.TailwindTraders.net
State: Failed
Error: -2147463168
Error Message:
Guidance: Check the detailed error and make sure the inventory requirements are met. The inventory couldn't determine any aspects of the specified source computer. This could be because of missing permissions or privileges on the source or a blocked firewall port.

Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
Source:        Microsoft-Windows-StorageMigrationService-Proxy
Date:          2/14/2020 1:18:21 PM
Event ID:      10000
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      2019-rtm-orc.ned.contoso.com
Description:
02/14/2020-13:18:21.097 [Erro] Failed device discovery stage SystemInfo with error: (0x80005000) Unknown error (0x80005000)
```

Эта ошибка вызвана дефектом кода в службе миграции хранилища при предоставлении учетных данных миграции в виде имени участника-пользователя (UPN), например " meghan@contoso.com ". Службе Orchestrator Migration Service не удается правильно проанализировать этот формат, что приводит к сбою уточняющего запроса домена, добавленного для поддержки миграции кластера в KB4512534 и 19H1.

Чтобы обойти эту ошибку, укажите учетные данные в формате домен \ пользователь, например "Контосо\мегхан".

## <a name="error-serviceerror0x9006-or-the-proxy-isnt-currently-available-when-migrating-to-a-windows-server-failover-cluster"></a>Ошибка "ServiceError0x9006" или "прокси-сервер в настоящее время недоступен". При переходе на отказоустойчивый кластер Windows Server

При попытке перемещения данных на кластеризованный файловый сервер появляются следующие ошибки:

```
Make sure the proxy service is installed and running, and then try again. The proxy isn't currently available.
0x9006
ServiceError0x9006,Microsoft.StorageMigration.Commands.UnregisterSmsProxyCommand
```

Эта ошибка возникает, если ресурс файлового сервера перемещен с исходного узла владельца кластера Windows Server 2019 на новый узел, а функция прокси-сервера службы миграции хранилища не установлена на этом узле.

Чтобы избежать этого, переместите целевой ресурс файлового сервера обратно на исходный узел кластера владельца, который использовался при первой настройке пар передачи.

В качестве альтернативного решения:

1. Установите компонент прокси-сервера службы миграции хранилища на всех узлах кластера.
2. Выполните следующую команду PowerShell для службы миграции хранилища на компьютере Orchestrator:

   ```PowerShell
   Register-SMSProxy -ComputerName <destination server> -Force
   ```
## <a name="error-dll-was-not-found-when-running-inventory-from-a-cluster-node"></a>Ошибка "DLL не найдена" при выполнении инвентаризации с узла кластера

При попытке выполнить инвентаризацию с помощью службы миграции хранилища и нацеливания на общий источник файлового сервера отказоустойчивого кластера Windows Server появляется следующее сообщение об ошибке:

```
DLL not found
[Error] Failed device discovery stage VolumeInfo with error: (0x80131524) Unable to load DLL 'Microsoft.FailoverClusters.FrameworkSupport.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)
```

Чтобы обойти эту ошибку, установите "средства управления отказоустойчивыми кластерами" (RSAT-Cluster-Management) на сервере, на котором выполняется служба миграции хранилища Orchestrator.

## <a name="error-there-are-no-more-endpoints-available-from-the-endpoint-mapper-when-running-inventory-against-a-windows-server-2003-source-computer"></a>Ошибка "при выполнении инвентаризации с исходным компьютером Windows Server 2003 больше нет доступных конечных точек"

При попытке запустить инвентаризацию с помощью службы миграции хранилища Orchestrator на исходном компьютере Windows Server 2003 появляется следующее сообщение об ошибке:

```
There are no more endpoints available from the endpoint mapper
```

Эта проблема решена с помощью обновления [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818) .

## <a name="uninstalling-a-cumulative-update-prevents-storage-migration-service-from-starting"></a>Удаление накопительного обновления предотвращает запуск службы миграции хранилища

Удаление накопительных обновлений Windows Server может препятствовать запуску службы миграции хранилища. Чтобы устранить эту проблему, можно создать резервную копию и удалить базу данных службы миграции хранилища:

1. Откройте командную строку с повышенными привилегиями, в которой вы являетесь членом группы администраторов на сервере Orchestrator службы миграции хранилища, и выполните следующую команду:

     ```DOS
     TAKEOWN /d y /a /r /f c:\ProgramData\Microsoft\StorageMigrationService

     MD c:\ProgramData\Microsoft\StorageMigrationService\backup

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService\* /grant Administrators:(GA)

     XCOPY c:\ProgramData\Microsoft\StorageMigrationService\* .\backup\*

     DEL c:\ProgramData\Microsoft\StorageMigrationService\* /q

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService  /GRANT networkservice:F /T /C

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService /GRANT networkservice:(GA) /T /C
     ```

2. Запустите службу миграции хранилища, которая создаст новую базу данных.

## <a name="error-clusctl_resource_netname_repair_vco-failed-against-netname-resource-and-windows-server-2008-r2-cluster-cutover-fails"></a>Ошибка "сбой CLUSCTL_RESOURCE_NETNAME_REPAIR_VCO для ресурса netName" и кластера Windows Server 2008 R2, сбой прямую миграцию

При попытке выполнить операцию вырезания источника кластера Windows Server 2008 R2 на этапе "Переименование исходного компьютера" зависает. появится следующая ошибка:

```
Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
Source:        Microsoft-Windows-StorageMigrationService-Proxy
Date:          10/17/2019 6:44:48 PM
Event ID:      10000
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      WIN-RNS0D0PMPJH.contoso.com
Description:
10/17/2019-18:44:48.727 [Erro] Exception error: 0x1. Message: Control code CLUSCTL_RESOURCE_NETNAME_REPAIR_VCO failed against netName resource 2008r2FS., stackTrace:    at Microsoft.FailoverClusters.Framework.ClusterUtils.NetnameRepairVCO(SafeClusterResourceHandle netNameResourceHandle, String netName)
at Microsoft.FailoverClusters.Framework.ClusterUtils.RenameFSNetName(SafeClusterHandle ClusterHandle, String clusterName, String FsResourceId, String NetNameResourceId, String newDnsName, CancellationToken ct)
at Microsoft.StorageMigration.Proxy.Cutover.CutoverUtils.RenameFSNetName(NetworkCredential networkCredential, Boolean isLocal, String clusterName, String fsResourceId, String nnResourceId, String newDnsName, CancellationToken ct)    [d:\os\src\base\dms\proxy\cutover\cutoverproxy\CutoverUtils.cs::RenameFSNetName::1510]
```

Эта проблема вызвана отсутствием API в более ранних версиях Windows Server. Сейчас нет способа перенести кластеры Windows Server 2008 и Windows Server 2003. Вы можете выполнять инвентаризацию и перенос без проблем в кластерах Windows Server 2008 R2, а затем вручную выполнять прямую миграцию путем изменения имени и IP-адреса ресурса исходного файлового сервера кластера вручную, а затем изменяя NetName конечного кластера и IP-адрес в соответствии с исходным источником.

## <a name="cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer-when-using-static-ips"></a>Прямую миграцию зависает на "38% сопоставлении сетевых интерфейсов на исходном компьютере..." При использовании статических IP-адресов

При попытке выполнить вырезание с исходного компьютера с установленным исходным компьютером на использование нового статического (не DHCP) IP-адреса в одном или нескольких сетевых интерфейсах на этапе «вырезание на уровне "38% сопоставлений сетевых интерфейсов на исходном компьютере" зависает. в журнале событий службы миграции хранилища появится следующая ошибка:

```
Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Admin
Source:        Microsoft-Windows-StorageMigrationService-Proxy
Date:          11/13/2019 3:47:06 PM
Event ID:      20494
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      orc2019-rtm.corp.contoso.com
Description:
Couldn't set the IP address on the network adapter.

Computer: fs12.corp.contoso.com
Adapter: microsoft hyper-v network adapter
IP address: 10.0.0.99
Network mask: 16
Error: 40970
Error Message: Unknown error (0xa00a)

Guidance: Confirm that the Netlogon service on the computer is reachable through RPC and that the credentials provided are correct.
```

Проверка исходного компьютера показывает, что исходный IP-адрес не меняется.

Эта проблема не возникает, если выбран параметр "использовать DHCP" на экране "Настройка прямую миграцию" центра администрирования Windows, только если указан новый статический IP-адрес.

Существует два решения этой проблемы.

1. Эта проблема впервые была решена обновлением [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818) . Эта ошибка кода не позволила использовать статические IP-адреса.

2. Если вы не указали IP-адрес шлюза по умолчанию в сетевых интерфейсах исходного компьютера, эта проблема будет возникать даже при обновлении KB4537818. Чтобы обойти эту ошибку, задайте допустимый IP-адрес по умолчанию для сетевых интерфейсов с помощью приложения "Сетевые подключения" (NCPA.CPL) или командлета PowerShell Set-NetRoute.

## <a name="slower-than-expected-re-transfer-performance"></a>Медленнее, чем ожидаемая производительность повторной пересылки

После завершения перемещения и последующей повторной пересылки одних и тех же данных вы можете не заметить значительного улучшения времени на перемещение, даже если на исходном сервере изменились небольшие данные.

Это ожидаемое поведение при передаче очень большого количества файлов и вложенных папок. Размер данных не важен. Мы сначала внесли улучшения в это поведение в [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) и продолжаем оптимизировать производительность обмена. Чтобы еще больше настроить производительность, ознакомьтесь с [оптимизацией инвентаризации и производительности перемещения](https://docs.microsoft.com/windows-server/storage/storage-migration-service/faq#optimizing-inventory-and-transfer-performance).

## <a name="data-does-not-transfer-user-renamed-when-migrating-to-or-from-a-domain-controller"></a>Данные не передаются, пользователь переименован при миграции на контроллер домена или с него

После запуска перемещения с контроллера домена или на него выполните следующие действия.

 1. Данные не переносятся, и в месте назначения не создаются общие папки.
 2. В центре администрирования Windows отображается красный символ ошибки без сообщения об ошибке
 3. Для одного или нескольких пользователей AD и локальных групп домена изменилось имя и (или) пред-Windows 2000 атрибут входа

 4. Вы увидите событие 3509 в службе миграции хранилища Orchestrator:

    ```
    Log Name:      Microsoft-Windows-StorageMigrationService/Admin
    Source:        Microsoft-Windows-StorageMigrationService
    Date:          1/10/2020 2:53:48 PM
    Event ID:      3509
    Task Category: None
    Level:         Error
    Keywords:
    User:          NETWORK SERVICE
    Computer:      orc2019-rtm.corp.contoso.com
    Description:
    Couldn't transfer storage for a computer.

    Job: dctest3
    Computer: dc02-2019.corp.contoso.com
    Destination Computer: dc03-2019.corp.contoso.com
    State: Failed
    Error: 53251
    Error Message: Local accounts migration failed with error System.Exception: -2147467259
        at Microsoft.StorageMigration.Service.DeviceHelper.MigrateSecurity(IDeviceRecord sourceDeviceRecord, IDeviceRecord destinationDeviceRecord, TransferConfiguration config, Guid proxyId, CancellationToken cancelToken)
    ```

    Это ожидаемое поведение, если вы попытались выполнить миграцию из или в контроллер домена с помощью службы миграции хранилища и использовали параметр "Миграция пользователей и групп" для переименования или повторного использования учетных записей. Вместо выбора параметра "не передавать пользователей и группы". Миграция контроллера домена [не поддерживается при использовании службы миграции хранилища](faq.md). Так как контроллер домена не имеет локальных пользователей и групп, служба миграции хранилища обрабатывает эти субъекты безопасности так, как если бы они переводились между двумя рядовыми серверами и пытаются настроить списки управления доступом, что приведет к ошибкам, а также искаженным или скопированным учетным записям.

Если вы уже выполнили перемещение один или несколько раз:

 1. Используйте следующую команду AD PowerShell для контроллера домена, чтобы найти измененных пользователей или группы (при изменении Сеарчбасе в соответствии с различающимся именем домена):

    ```PowerShell
    Get-ADObject -Filter 'Description -like "*storage migration service renamed*"' -SearchBase 'DC=<domain>,DC=<TLD>' | ft name,distinguishedname
    ```

 2. Для всех пользователей, возвращенных с их исходным именем, измените их имя для входа в систему (пред-Windows 2000), чтобы удалить суффикс случайных символов, добавленный службой миграции хранилища, чтобы он мог войти в систему.

 3. Для всех групп, возвращенных с их исходным именем, измените их имя группы (пред-Windows 2000), чтобы удалить суффикс случайных символов, добавленный службой миграции хранилища.

 4. Для всех отключенных пользователей или групп с именами, которые теперь содержат суффикс, добавленный службой миграции хранилища, эти учетные записи можно удалить. Вы можете подтвердить, что учетные записи пользователей были добавлены позже, так как они будут содержать только группу "Пользователи домена" и будут иметь созданную дату и время, соответствующие времени начала переноса службы миграции хранилища.

    Если вы хотите использовать службу миграции хранилища с контроллерами домена для целей переноса, убедитесь, что на странице Параметры переноса в центре администрирования Windows всегда выбран параметр "не передавать пользователей и группы".

## <a name="error-53-failed-to-inventory-all-specified-devices-when-running-inventory"></a>Ошибка 53, "не удалось выполнить инвентаризацию всех указанных устройств" при выполнении инвентаризации,

При попытке запустить инвентаризацию вы получаете следующее:

```
Failed to inventory all specified devices

Log Name:      Microsoft-Windows-StorageMigrationService/Admin
Source:        Microsoft-Windows-StorageMigrationService
Date:          1/16/2020 8:31:17 AM
Event ID:      2516
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      ned.corp.contoso.com
Description:
Couldn't inventory files on the specified endpoint.
Job: ned1
Computer: ned.corp.contoso.com
Endpoint: hithere
State: Failed
File Count: 0
File Size in KB: 0
Error: 53
Error Message: Endpoint scan failed
Guidance: Check the detailed error and make sure the inventory requirements are met. This could be because of missing permissions on the source computer.

Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Debug
Source:        Microsoft-Windows-StorageMigrationService-Proxy
Date:          1/16/2020 8:31:17 AM
Event ID:      10004
Task Category: None
Level:         Critical
Keywords:
User:          NETWORK SERVICE
Computer:      ned.corp.contoso.com
Description:
01/16/2020-08:31:17.031 [Crit] Consumer Task failed with error:The network path was not found.
. StackTrace=   at Microsoft.Win32.RegistryKey.Win32ErrorStatic(Int32 errorCode, String str)
    at Microsoft.Win32.RegistryKey.OpenRemoteBaseKey(RegistryHive hKey, String machineName, RegistryView view)
    at Microsoft.StorageMigration.Proxy.Service.Transfer.FileDirUtils.GetEnvironmentPathFolders(String ServerName, Boolean IsServerLocal)
    at Microsoft.StorageMigration.Proxy.Service.Discovery.ScanUtils.<ScanSMBEndpoint>d__3.MoveNext()
    at Microsoft.StorageMigration.Proxy.EndpointScanOperation.Run()
    at Microsoft.StorageMigration.Proxy.Service.Discovery.EndpointScanRequestHandler.ProcessRequest(EndpointScanRequest scanRequest, Guid operationId)
    at Microsoft.StorageMigration.Proxy.Service.Discovery.EndpointScanRequestHandler.ProcessRequest(Object request)
    at Microsoft.StorageMigration.Proxy.Common.ProducerConsumerManager`3.Consume(CancellationToken token)

01/16/2020-08:31:10.015 [Erro] Endpoint Scan failed. Error: (53) The network path was not found.
Stack trace:
    at Microsoft.Win32.RegistryKey.Win32ErrorStatic(Int32 errorCode, String str)
    at Microsoft.Win32.RegistryKey.OpenRemoteBaseKey(RegistryHive hKey, String machineName, RegistryView view)
```

На этом этапе служба миграции хранилища пытается выполнить удаленный доступ к реестру для определения конфигурации исходного компьютера, но она отклоняется исходным сервером, сообщающим, что путь реестра не существует. Для этого могут быть следующие причины:

 - Служба удаленного реестра не запущена на исходном компьютере.
 - брандмауэр не разрешает подключение удаленного реестра к исходному серверу из Orchestrator.
 - У учетной записи миграции источника отсутствуют разрешения на удаленный реестр для подключения к исходному компьютеру.
 - Учетная запись миграции источника не имеет разрешений на чтение в реестре исходного компьютера, в разделе "HKEY_LOCAL_MACHINE \Софтваре\микрософт\виндовс Нт\куррентверсион" или в разделе "HKEY_LOCAL_MACHINE \Систем\куррентконтролсет\сервицес\ланмансервер"

## <a name="cutover-hangs-on-38-mapping-network-interfaces-on-the-source-computer"></a>Прямую миграцию зависает на "38% сопоставлении сетевых интерфейсов на исходном компьютере..."

При попытке выполнить вырезание с исходного компьютера повышена блокировка на этапе "38% сопоставления сетевых интерфейсов на исходном компьютере..." в журнале событий службы миграции хранилища появится следующая ошибка:

```
Log Name:      Microsoft-Windows-StorageMigrationService-Proxy/Admin
Source:        Microsoft-Windows-StorageMigrationService-Proxy
Date:          1/11/2020 8:51:14 AM
Event ID:      20505
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      nedwardo.contosocom
Description:
Couldn't establish a CIM session with the computer.

Computer: 172.16.10.37
User Name: nedwardo\MsftSmsStorMigratSvc
Error: 40970
Error Message: Unknown error (0xa00a)

Guidance: Confirm that the Netlogon service on the computer is reachable through RPC and that the credentials provided are correct.
```

Эта проблема вызвана групповая политика, которая устанавливает следующее значение реестра на исходном компьютере: "HKEY_LOCAL_MACHINE \Софтваре\микрософт\виндовс\куррентверсион\полиЦиес\систем\локалаккаунттокенфилтерполици = 0"

Этот параметр не входит в стандартную групповая политика. это надстройка, настроенная с помощью [набора средств обеспечения соответствия требованиям корпорации Майкрософт](https://www.microsoft.com/download/details.aspx?id=55319):

- Windows Server 2012 R2: "компьютер \ конфигурация Темплатес\скм: передайте хэш-Митигатионс\аппли ограничения UAC в локальные учетные записи при входе в сеть"

- Не закладывает сервер 2016: "компьютер \ конфигурация Темплатес\мс безопасность Гуиде\аппли UAC ограничения для локальных учетных записей при входе в сеть"

Его также можно задать с помощью параметров групповая политика с пользовательским параметром реестра. С помощью средства GPRESULT можно определить, какая политика применяет этот параметр к исходному компьютеру.

Служба миграции хранилища временно включает параметр [LocalAccountTokenFilterPolicy](https://support.microsoft.com/help/951016/description-of-user-account-control-and-remote-restrictions-in-windows) в процессе вырезания, а затем удаляет его после завершения процесса. Когда групповая политика применяет конфликтующий объект групповая политика (GPO), он переопределяет службу миграции хранилища и предотвращает вырезание.

Чтобы обойти эту ошибку, используйте один из следующих вариантов.

1. Временно переместите исходный компьютер из подразделения Active Directory, который применяет этот конфликтующий объект групповой политики.
2. Временно отключите объект групповой политики, который применяет эту конфликтующую политику.
3. Временно создайте новый объект групповой политики, который задает для этого параметра значение отключено и применяется к конкретному подразделению исходных серверов с более высоким приоритетом, чем любые другие объекты групповой политики.

## <a name="inventory-or-transfer-fail-when-using-credentials-from-a-different-domain"></a>Сбой инвентаризации или перемещения при использовании учетных данных из другого домена

При попытке запуска инвентаризации или переноса с помощью службы миграции хранилища и нацеливания на Windows Server с использованием учетных данных миграции из домена, не являющегося целевым сервером, появляются следующие ошибки.
```
Exception from HRESULT:0x80131505

The server was unable to process the request due to an internal error

04/28/2020-11:31:01.169 [Error] Failed device discovery stage SystemInfo with error: (0x490) Could not find computer object 'myserver' in Active Directory    [d:\os\src\base\dms\proxy\discovery\discoveryproxy\DeviceDiscoveryOperation.cs::TryStage::1042]
```

Анализ журналов дополнительно показывает, что учетная запись миграции и сервер, на котором выполняется миграция, находятся в разных доменах:

```
06/25/2020-10:11:16.543 [Info] Creating new job=NedJob user=**CONTOSO**\ned
[d:\os\src\base\dms\service\StorageMigrationService.IInventory.cs::CreateJob::133]
```

```
GetOsVersion(fileserver75.**corp**.contoso.com)    [d:\os\src\base\dms\proxy\common\proxycommon\CimSessionHelper.cs::GetOsVersion::66] 06/25/2020-10:20:45.368 [Info] Computer 'fileserver75.corp.contoso.com': OS version
```

Эта проблема вызвана дефектом кода в службе миграции хранилища. Чтобы обойти эту ошибку, используйте учетные данные миграции из того же домена, к которому принадлежат исходный и конечный компьютеры. Например, если исходный и конечный компьютеры принадлежат домену "corp.contoso.com" в лесу "contoso.com", используйте "корп\мяккаунт", чтобы выполнить миграцию, а не учетные данные "контосо\мяккаунт".

## <a name="inventory-fails-with-element-not-found"></a>Сбой инвентаризации с "элемент не найден"

Рассмотрим следующий сценарий.

У вас есть исходный сервер с именем узла DNS и Active Directory именем более 15 символов Юникода, например "иамаверилонгкомпутернаме". Операционная система Windows не позволяла установить в качестве устаревшего NetBIOS-имя, которое будет задано как длинное, и предупреждать о том, что имя NetBIOS было усечено до 15 символов Юникода (например, "иамаверилонгком"). При попытке выполнить инвентаризацию этого компьютера вы получаете в центре администрирования Windows и журнале событий:

```DOS
"Element not found"
========================

Log Name:      Microsoft-Windows-StorageMigrationService/Admin
Source:        Microsoft-Windows-StorageMigrationService
Date:          4/10/2020 10:49:19 AM
Event ID:      2509
Task Category: None
Level:         Error
Keywords:
User:          NETWORK SERVICE
Computer:      WIN-6PJAG3DHPLF.corp.contoso.com
Description:
Couldn't inventory a computer.

Job: longnametest
Computer: iamaverylongcomputername.corp.contoso.com
State: Failed
Error: 1168
Error Message:

Guidance: Check the detailed error and make sure the inventory requirements are met. The inventory couldn't determine any aspects of the specified source computer. This could be because of missing permissions or privileges on the source or a blocked firewall port.
```

Эта проблема вызвана дефектом кода в службе миграции хранилища. В настоящее время единственным решением является переименование компьютера с тем же именем, что и у NetBIOS-имени, а затем с помощью команды [NETDOM ComputerName/Add](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc835082(v=ws.11)) добавьте альтернативное имя компьютера, которое использовалось до начала инвентаризации. Служба миграции хранилища поддерживает миграцию альтернативных имен компьютеров.

## <a name="see-also"></a>См. также

- [Обзор службы миграции хранилища](overview.md)
