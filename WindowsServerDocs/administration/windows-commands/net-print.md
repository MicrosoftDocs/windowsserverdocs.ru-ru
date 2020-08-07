---
title: net print
description: Справочная статья по команде net print. Эта команда устарела и не гарантируется, что она будет поддерживаться в будущих выпусках Windows.
ms.topic: article
ms.assetid: f59b2015-4698-415d-9a74-09566c466f40
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16e685c4fb616272baace3554e5ca96bd7a82617
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886077"
---
# <a name="net-print"></a>net print

> [!IMPORTANT]
> Эта команда устарела. Однако многие из этих задач можно выполнять с помощью [команды прнжобс](prnjobs.md), [инструментарий управления Windows (WMI) (WMI)](/windows/win32/wmisdk/wmi-start-page), [Принтманажемент в PowerShell](/powershell/module/printmanagement)или [ресурсов скриптов для](https://gallery.technet.microsoft.com/ScriptCenter/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=printing&f%5B0%5D.Text=Printing)ИТ-специалистов.

Отображает сведения об указанной очереди печати или указанном задании печати или управляет указанным заданием печати.

## <a name="syntax"></a>Синтаксис

```
net print {\\<computername>\<sharename> | \\<computername> <jobnumber> [/hold | /release | /delete]} [help]
```

### <a name="parameters"></a>Параметры

| Параметры | Описание |
| ---------- | ----------- |
| `\\<computername>\<sharename>` | Указывает (по имени) компьютер и очередь печати, сведения о которых требуется отобразить. |
| `\\<computername>` | Указывает (по имени) компьютер, на котором размещено задание печати, которое требуется контролировать. Если компьютер не указан, предполагается, что используется локальный компьютер. Требуется `<jobnumber>` параметр. |
| `<jobnumber>` | Указывает номер задания печати, которое требуется контролировать. Этот номер назначается компьютером, на котором размещена очередь печати, в которой отправляется задание печати. После того как компьютер назначает номер заданию печати, этот номер не назначается никаким другим заданиям печати в любой очереди, размещенной на этом компьютере. Требуется при использовании `\\<computername>` параметра. |
| `[/hold | /release | /delete]` | Указывает действие, выполняемое с заданием печати. Если указать номер задания, но не указывать никаких действий, будут отображены сведения о задании печати.<ul><li>**/холд** — задерживает задание, позволяя другим заданиям печати обходить его до выпуска.</li><li>**/Release** — освобождает Отложенное задание печати.</li><li>**/Delete** — удаляет задание печати из очереди печати.</li></ul> |
| help | Отображение справки в командной строке. |

#### <a name="remarks"></a>Remarks

- `net print\\<computername>`Команда отображает сведения о заданиях печати в общей очереди принтера. Ниже приведен пример отчета для всех заданий печати в очереди для общего принтера с именем *Laser*:

    ```
    printers at \\PRODUCTION
    Name              Job #      Size      Status
    -----------------------------
    LASER Queue       3 jobs               *printer active*
    USER1          84        93844      printing
    USER2          85        12555      Waiting
    USER3          86        10222      Waiting
    ```

- Ниже приведен пример отчета для задания печати.

    ```
    Job #            35
    Status           Waiting
    Size             3096
    remark
    Submitting user  USER2
    Notify           USER2
    Job data type
    Job parameters
    additional info
    ```

### <a name="examples"></a>Примеры

Чтобы получить список содержимого очереди печати *дотматрикс* на * \\ рабочем* компьютере, введите:

```
net print \\Production\Dotmatrix
```

Чтобы отобразить сведения о задании с номером *35* на * \\ рабочем* компьютере, введите:

```
net print \\Production 35
```

Чтобы отложить задание с номером *263* на * \\ рабочем* компьютере, введите:

```
net print \\Production 263 /hold
```

Чтобы освободить задание с номером *263* на * \\ рабочем* компьютере, введите:

```
net print \\Production 263 /release
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Справочник по командам печати](print-command-reference.md)

- [Команда прнжобс](prnjobs.md)

- [Инструментарий управления Windows (WMI)](/windows/win32/wmisdk/wmi-start-page)

- [Принтманажемент в PowerShell](/powershell/module/printmanagement)

- [Ресурсы сценариев для ИТ-специалистов](https://gallery.technet.microsoft.com/ScriptCenter/site/search?f%5B0%5D.Type=RootCategory&f%5B0%5D.Value=printing&f%5B0%5D.Text=Printing)
