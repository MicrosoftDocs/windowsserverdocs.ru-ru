---
title: bitsadmin examples
description: Примеры, демонстрирующие использование средства битсадмин для выполнения наиболее распространенных задач.
ms.topic: reference
ms.assetid: cb8f8374-ba6e-4a68-85a1-9a95b8215354
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/31/2018
ms.openlocfilehash: e1fcf545efee765b5130c616ddee53b25f03d0d3
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89030492"
---
# <a name="bitsadmin-examples"></a>bitsadmin examples

В следующих примерах показано, как использовать это `bitsadmin` средство для выполнения наиболее распространенных задач.

## <a name="transfer-a-file"></a>Перенос файла

Чтобы создать задание, добавить файлы, активировать задание в очереди на перемещение и завершить задание:

`bitsadmin /transfer myDownloadJob /download /priority normal https://downloadsrv/10mb.zip c:\\10mb.zip`

Битсадмин сохраняет сведения о ходе выполнения в окне MS-DOS до тех пор, пока не завершится перемещение или не произойдет ошибка.

## <a name="create-a-download-job"></a>Создание задания скачивания

Чтобы создать задание загрузки с именем *мидовнлоаджоб*, выполните следующие действия.

```
bitsadmin /create myDownloadJob
```

Битсадмин возвращает идентификатор GUID, однозначно определяющий задание. Используйте идентификатор GUID или имя задания в последующих вызовах. Следующий текст — пример выходных данных.

### <a name="sample-output"></a>Пример выходных данных

`created job {C775D194-090F-431F-B5FB-8334D00D1CB6}`

## <a name="add-files-to-the-download-job"></a>Добавление файлов в задание скачивания

Чтобы добавить файл в задание, выполните следующие действия.

```
bitsadmin /addfile myDownloadJob https://downloadsrv/10mb.zip c:\\10mb.zip
```

Повторите этот вызов для каждого файла, который нужно добавить. Если несколько заданий используют *мидовнлоаджоб* в качестве имени, необходимо использовать идентификатор GUID задания, чтобы однозначно идентифицировать его для завершения.

## <a name="activate-the-download-job"></a>Активация задания скачивания

После создания нового задания служба BITS автоматически приостанавливает задание. Чтобы активировать задание в очереди на перемещение, выполните следующие действия.

```
bitsadmin /resume myDownloadJob
```

Если несколько заданий используют *мидовнлоаджоб* в качестве имени, необходимо использовать идентификатор GUID задания, чтобы однозначно идентифицировать его для завершения.

## <a name="determine-the-progress-of-the-download-job"></a>Определение хода выполнения задания загрузки

Параметр **/info** возвращает состояние задания и число переданных файлов и байтов. Если состояние отображается как, то `TRANSFERRED` это означает, что служба BITS успешно передала все файлы в задании. Кроме того, можно добавить аргумент **/verbose** , чтобы получить полные сведения о задании, а также выполнить **/List** или **/монитор** , чтобы получить все задания в очереди на перемещение.

Чтобы вернуть состояние задания, выполните следующие действия.

```
bitsadmin /info myDownloadJob /verbose
```

Если несколько заданий используют *мидовнлоаджоб* в качестве имени, необходимо использовать идентификатор GUID задания, чтобы однозначно идентифицировать его для завершения.

## <a name="complete-the-download-job"></a>Завершение задания скачивания

Чтобы завершить задание после изменения состояния `TRANSFERRED` :

```
bitsadmin /complete myDownloadJob
```

Необходимо запустить параметр, `/complete` чтобы файлы в задании стали доступны. Если несколько заданий используют *мидовнлоаджоб* в качестве имени, необходимо использовать идентификатор GUID задания, чтобы однозначно идентифицировать его для завершения.

## <a name="monitor-jobs-in-the-transfer-queue-using-the-list-switch"></a>Мониторинг заданий в очереди на перемещение с помощью параметра/List

Чтобы получить состояние задания и число файлов и байт, переданных для всех заданий в очереди передачи, выполните следующие действия.

```
bitsadmin /list
```

### <a name="sample-output"></a>Пример выходных данных

```
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN

Listed 2 job(s).
```

## <a name="monitor-jobs-in-the-transfer-queue-using-the-monitor-switch"></a>Мониторинг заданий в очереди на перемещение с помощью параметра/монитор

Чтобы получить сведения о состоянии задания и количестве файлов и байт, переданных для всех заданий в очереди передачи, обновляют данные каждые 5 секунд:

```
bitsadmin /monitor
```

> [!NOTE]
> Чтобы прервать обновление, нажмите клавиши CTRL + C.

### <a name="sample-output"></a>Пример выходных данных

```
MONITORING BACKGROUND COPY MANAGER(5 second refresh)
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN
{0B138008-304B-4264-B021-FD04455588FF} job3 TRANSFERRED 1 / 1 100379370 / 100379370
```

## <a name="monitor-jobs-in-the-transfer-queue-using-the-info-switch"></a>Мониторинг заданий в очереди на перемещение с помощью параметра/info

Чтобы вернуть состояние задания и число переданных файлов и передано байт:

```
bitsadmin /info
```

### <a name="sample-output"></a>Пример выходных данных

```
GUID: {482FCAF0-74BF-469B-8929-5CCD028C9499} DISPLAY: myDownloadJob
TYPE: DOWNLOAD STATE: TRANSIENT_ERROR OWNER: domain\user
PRIORITY: NORMAL FILES: 0 / 1 BYTES: 0 / UNKNOWN
CREATION TIME: 12/17/2002 1:21:17 PM MODIFICATION TIME: 12/17/2002 1:21:30 PM
COMPLETION TIME: UNKNOWN
NOTIFY INTERFACE: UNREGISTERED NOTIFICATION FLAGS: 3
RETRY DELAY: 600 NO PROGRESS TIMEOUT: 1209600 ERROR COUNT: 0
PROXY USAGE: PRECONFIG PROXY LIST: NULL PROXY BYPASS LIST: NULL
ERROR FILE:    https://downloadsrv/10mb.zip -> c:\10mb.zip
ERROR CODE:    0x80072ee7 - The server name or address could not be resolved
ERROR CONTEXT: 0x00000005 - The error occurred while the remote file was being
processed.
DESCRIPTION:
JOB FILES:
0 / UNKNOWN WORKING https://downloadsrv/10mb.zip -> c:\10mb.zip
NOTIFICATION COMMAND LINE: none
```

## <a name="delete-jobs-from-the-transfer-queue"></a>Удаление заданий из очереди на перемещение

Чтобы удалить все задания из очереди на перемещение, используйте параметр/Reset:

```
bitsadmin /reset
```

### <a name="sample-output"></a>Пример выходных данных

```
{DC61A20C-44AB-4768-B175-8000D02545B9} canceled.
{BB6E91F3-6EDA-4BB4-9E01-5C5CBB5411F8} canceled.
2 out of 2 jobs canceled.
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
