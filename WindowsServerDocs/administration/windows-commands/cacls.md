---
title: cacls
description: Справочный раздел команды cacls, которая отображает или изменяет избирательные списки управления доступом (DACL) для указанных файлов.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b5bdbaaa-4557-48b8-80df-e75ee0d2f27d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d827199ea319bd41511f9abadfde8c6e8949976e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82726026"
---
# <a name="cacls"></a>cacls

>[!IMPORTANT]
> Эта команда устарела. Взамен рекомендуется использовать [icacls](icacls.md) .  

Отображает или изменяет избирательные списки управления доступом (DACL) для указанных файлов.  

## <a name="syntax"></a>Синтаксис

```  
cacls <filename> [/t] [/m] [/l] [/s[:sddl]] [/e] [/c] [/g user:<perm>] [/r user [...]] [/p user:<perm> [...]] [/d user [...]]  
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| `<filename>` | Обязательный. Отображает списки управления доступом для указанных файлов. |
| /t | Изменяет списки управления доступом для указанных файлов в текущем каталоге и во всех подкаталогах. |
| /m | Изменяет списки управления доступом томов, подключенных к каталогу. |
| /l | Работает с самой символьной ссылкой вместо целевого объекта. |
| /s: SDDL | Заменяет списки управления доступом указанными в строке SDDL. Этот параметр недопустим для использования с параметрами **/e**, **/g**, **/r**, **/p**или **/d** . |
| /e | Измените список управления доступом вместо его замены. |
| /C | Продолжить после ошибок "отказано в доступе". |
| `/g user:<perm>` | Предоставляет указанные права доступа пользователя, включая следующие допустимые значения разрешения:<ul><li>**n** — нет</li><li>чтение с **r**</li><li>**w** — запись</li><li>**c** — изменение (запись)</li><li>**f** — полный доступ</li></ul> |
| /r пользователь [...] | Отозвать права доступа указанного пользователя. Допустимо только при использовании с параметром **/e** . |
| `[/p user:<perm> [...]` | Замените права доступа указанного пользователя, включая следующие допустимые значения для разрешения:<ul><li>**n** — нет</li><li>чтение с **r**</li><li>**w** — запись</li><li>**c** — изменение (запись)</li><li>**f** — полный доступ</li></ul> |
| [/d пользователь [...] | Запрет указанного доступа пользователя. |
| /? | Отображение справки в командной строке. |

#### <a name="sample-output"></a>Пример выходных данных

| Вывод | Запись управления доступом (ACE) применяется к |
-------- | ------------------------------------- |
| OI | Объект наследует. Эту папку и файлы. |
| CI | Контейнер наследует. Эта папка и вложенные папки. |
| IO | Только наследовать. ACE не применяется к текущему файлу или каталогу. |
| Нет выходного сообщения | Только в этой папке. |
| Oi ЭЛЕМЕНТ | Эта папка, вложенные папки и файлы. |
| Oi ЭЛЕМЕНТ IO | Только для вложенных папок и файлов. |
| ЭЛЕМЕНТ IO | Только во вложенных папках. |
| Oi IO | Только файлы. |

#### <a name="remarks"></a>Примечания

- Можно использовать подстановочные знаки (**?** и **&#42;**) для указания нескольких файлов.

- Можно указать более одного пользователя.  

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [icacls](icacls.md)