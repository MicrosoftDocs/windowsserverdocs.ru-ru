---
title: irftp
description: Справочная статья по команде ирфтп, которая отправляет файлы по инфракрасной связи.
ms.topic: reference
ms.assetid: e15c60a7-546d-4e9f-9871-43aaa1b569d6
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 23a366f398e62d23fd09f774eb0e236a9fb9c689
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101816013"
---
# <a name="irftp"></a>irftp

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Отправляет файлы по инфракрасной связи.

> [!IMPORTANT]
> Убедитесь, что устройства, предназначенные для связи по инфракрасной связи, имеют включенные функции инфракрасной связи и работают правильно. Кроме того, убедитесь, что между устройствами установлена связь по инфракрасной связи.

## <a name="syntax"></a>Синтаксис

```
irftp [<drive>:\] [[<path>] <filename>] [/h][/s]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<drive>:\` | Указывает диск, содержащий файлы, которые необходимо отправить через инфракрасную связь. |
| `[path]<filename>` | Указывает расположение и имя файла или набора файлов, которые требуется отправить через инфракрасную связь. Если указать набор файлов, необходимо указать полный путь для каждого файла. |
| /h | Указывает скрытый режим. Если используется скрытый режим, файлы отправляются без отображения диалогового окна беспроводная связь. |
| /s | Открывает диалоговое окно **беспроводная связь** , позволяющее выбрать файл или набор файлов, которые требуется отправить, без использования командной строки для указания диска, пути и имен файлов. Диалоговое окно **беспроводная связь** также открывается при использовании этой команды без параметров. |

### <a name="examples"></a>Примеры

Чтобы отправить *c:\example.txt* по инфракрасной связи, введите:

```
irftp c:\example.txt
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
