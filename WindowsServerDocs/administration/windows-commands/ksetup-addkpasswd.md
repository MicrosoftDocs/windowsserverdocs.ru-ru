---
title: ksetup addkpasswd
description: Справочная статья по команде ksetup аддкпассвд, которая добавляет адрес сервера пароля Kerberos (кпассвд) для области.
ms.topic: reference
ms.assetid: d3196995-1b38-48ff-ba08-911cfab77317
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 62123fc8a04006078c42894ee53f11346dec0e59
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037952"
---
# <a name="ksetup-addkpasswd"></a>ksetup addkpasswd

Добавляет адрес сервера пароля Kerberos (кпассвд) для области.

## <a name="syntax"></a>Синтаксис

```
ksetup /addkpasswd <realmname> [<kpasswdname>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<realmname>` | Указывает DNS-имя в верхнем регистре, например CORP. CONTOSO.COM и указывается в качестве области по умолчанию или **области =** при запуске **ksetup** . |
| `<kpasswdname>` | Указывает сервер паролей Kerberos. Оно называется без учета регистра, полное доменное имя, например mitkdc.contoso.com. Если имя KDC пропущено, для размещения Кдкс может использоваться DNS. |

#### <a name="remarks"></a>Remarks

- Если область Kerberos, в которой выполняется проверка подлинности на рабочей станции, поддерживает протокол Kerberos для изменения пароля, можно настроить клиентский компьютер под управлением операционной системы Windows для использования сервера паролей Kerberos.

- Можно добавить дополнительные имена KDC по одному.

### <a name="examples"></a>Примеры

Для настройки корпоративной сети. Чтобы использовать в качестве сервера паролей CONTOSO.COM-сервер, отличный от Windows KDC, введите:

```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```

Чтобы убедиться, что имя KDC задано, введите `ksetup` и просмотрите выходные данные, выполняя поиск текста **кпассвд =**. Если текст не отображается, это означает, что сопоставление не было настроено.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup делкпассвд, команда](ksetup-delkpasswd.md)
