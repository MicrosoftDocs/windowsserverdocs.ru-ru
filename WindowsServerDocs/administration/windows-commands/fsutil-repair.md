---
title: fsutil repair
description: Справочная статья по команде fsutil Repair, которая служит для администрирования и мониторинга операций восстановления с самостоятельным восстановлением NTFS.
manager: dmoss
ms.author: toklima
author: toklima
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
ms.topic: reference
ms.date: 10/16/2017
ms.openlocfilehash: 9c26f2be8e586205271ba1d150bb2378cc8b2045
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037332"
---
# <a name="fsutil-repair"></a>fsutil repair

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

Администрирование и мониторинг операций восстановления с самостоятельным восстановлением NTFS. Самовосстанавливающаяся система NTFS пытается исправить повреждения файловой системы NTFS в режиме «в сети» без необходимости запуска **Chkdsk.exe** . Дополнительные сведения см. в разделе [Самостоятельное восстановление NTFS](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc771388(v=ws.10)).

## <a name="syntax"></a>Синтаксис

```
fsutil repair [enumerate] <volumepath> [<logname>]
fsutil repair [initiate] <volumepath> <filereference>
fsutil repair [query] <volumepath>
fsutil repair [set] <volumepath> <flags>
fsutil repair [wait][<waittype>] <volumepath>

```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| перечислить | Перечисление всех записей журнала повреждений тома. |
| `<logname>` | Может быть `$corrupt` , набор подтвержденных повреждений в томе или `$verify` набор потенциальных, непроверенных повреждений в томе. |
| инициализаци | Инициирует самостоятельную восстановление файловой системы NTFS. |
| `<filereference>` | Указывает идентификатор файла, относящийся к тому NTFS (номер ссылки на файл). Ссылка на файл включает номер сегмента файла. |
| query | Запрашивает состояние автоматического восстановления тома NTFS. |
| set | Задает состояние тома с самовосстановлением. |
| `<flags>` | Указывает метод восстановления, используемый при установке состояния тома с самовосстановлением.<p>Этому параметру можно присвоить три значения:<ul><li>**0x01** — включает общее восстановление.</li><li>**0x09** — предупреждает о возможной потере данных без восстановления.</li><li>**0x00** — отключает восстановление с самовосстановлением NTFS.</li></ul> |
| Состояние | Запрашивает состояние повреждения системы или для заданного тома. |
| wait | Ожидает завершения восстановления. Если файловая система NTFS обнаружила проблему на томе, на котором выполняется восстановление, этот параметр позволяет системе ожидать завершения восстановления, прежде чем запускать все ожидающие сценарии. |
| `[waittype {0|1}]` | Указывает, следует ли ожидать завершения текущего восстановления или ожидать завершения всех операций по восстановлению. Для параметра *столбцы waittype* можно задать следующие значения:<ul><li>**0** — ожидание завершения всех исправлений. (значение по умолчанию)</li><li>**1** — ожидание завершения текущего восстановления.</li></ul> |

### <a name="examples"></a>Примеры

Чтобы перечислить подтвержденные повреждения тома, введите:

```
fsutil repair enumerate C: $Corrupt
```

Чтобы включить восстановление с самовосстановлением на диске C, введите:

```
fsutil repair set c: 1
```

Чтобы отключить восстановление с самовосстановлением на диске C, введите:

```
fsutil repair set c: 0
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [fsutil](fsutil.md)

- [Самостоятельное Восстановление NTFS](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc771388(v=ws.10))
