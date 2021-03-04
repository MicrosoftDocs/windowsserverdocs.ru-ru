---
title: ksetup addkdc
description: Справочная статья по команде ksetup аддкдк, которая содержит сведения о центр распространения ключей (KDC) для данной области Kerberos.
ms.topic: reference
ms.assetid: 98bfc23a-14c4-401c-bcb3-9903c5cdde64
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 818864510b03afd09b7388cdd08aef9cadabf425
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101815723"
---
# <a name="ksetup-addkdc"></a>ksetup addkdc

Добавляет адрес центр распространения ключей (KDC) для данной области Kerberos.

Сопоставление сохраняется в реестре в разделе **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\LSA\Kerberos\Domains** и компьютер необходимо перезапустить, прежде чем будет использоваться новый параметр сферы.

> [!NOTE]
> Чтобы развернуть данные конфигурации области Kerberos на нескольких компьютерах, необходимо явно использовать оснастку " **шаблоны конфигурации безопасности** " и "распределение политик" на отдельных компьютерах. Эту команду нельзя использовать.

## <a name="syntax"></a>Синтаксис

```
ksetup /addkdc <realmname> [<KDCname>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<realmname>` | Указывает DNS-имя в верхнем регистре, например CORP. CONTOSO.COM. Это значение также отображается как область по умолчанию при выполнении **ksetup** , а — область, в которую необходимо добавить другой KDC. |
| `<KDCname>` | Задает нечувствительное к регистру полное доменное имя, например mitkdc.contoso.com. Если имя KDC не указано, DNS обнаружит Кдкс. |

### <a name="examples"></a>Примеры

Чтобы настроить сервер KDC, отличный от Windows, и область, которую Рабочая станция должна использовать, введите:

```
ksetup /addkdc CORP.CONTOSO.COM mitkdc.contoso.com
```

Чтобы задать для пароля учетной записи локального компьютера значение p@sswrd1 % на том же компьютере, что и в предыдущем примере, а затем перезапустить компьютер, введите:

```
ksetup /setcomputerpassword p@sswrd1%
```

Чтобы проверить имя области по умолчанию для компьютера или убедиться, что эта команда работала правильно, введите:

```
ksetup
```
Проверьте реестр, чтобы убедиться, что сопоставление выполнено должным образом.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда ksetup](ksetup.md)

- [ksetup сеткомпутерпассворд, команда](ksetup-setcomputerpassword.md)
