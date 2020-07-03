---
title: nslookup ls
description: Справочная статья по команде nslookup Ls, которая содержит сведения о домене DNS.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f15f06fe-67e7-41a9-93b5-192ab14ab380
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c0c0aeb01cdffb1f2b779178f0298e1f120348e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936577"
---
# <a name="nslookup-ls"></a>nslookup ls

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Выводит сведения о DNS-домене.

## <a name="syntax"></a>Синтаксис

```
ls [<option>] <DNSdomain> [{[>] <filename>|[>>] <filename>}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<option>` | К допустимым параметрам относятся:<ul><li>**-t:** Перечисляет все записи указанного типа. Дополнительные сведения см. в разделе [nslookup set QueryType](nslookup-set-querytype.md).</li><li>**-а.** Выводит список псевдонимов компьютеров в домене DNS. Этот параметр аналогичен **-t CNAME**</li><li>**-d:** Список всех записей для домена DNS. Этот параметр аналогичен **-t Any**</li><li>**-h:** Выводит сведения о ЦП и операционной системе для DNS-домена. Этот параметр аналогичен **-t HINFO** .</li><li>**-s:** Выводит список хорошо известных служб компьютеров в домене DNS. Этот параметр аналогичен **-t WKS**. |
| `<DNSdomain>` | Указывает домен DNS, сведения о котором требуется получить. |
| `<filename>` | Указывает имя файла, используемого для сохранения выходных данных. `>` `>>` Чтобы перенаправить выходные данные обычным способом, можно использовать символы больше () и Double больше (). |
| /? | Отображение справки в командной строке. |
| /help | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Выход по умолчанию этой команды включает в себя имена компьютеров и связанные с ними IP-адреса.

- Если выходные данные направляются в файл, то для каждых 50 записей, полученных с сервера, добавляются хэш-метки.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [nslookup set querytype](nslookup-set-querytype.md)
