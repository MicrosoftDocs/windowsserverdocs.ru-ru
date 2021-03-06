---
title: tpmvscmgr
description: Справочная статья по тпмвскмгр — это программа командной строки, которая позволяет пользователям с правами администратора создавать и удалять виртуальные смарт-карты TPM на компьютере.
ms.topic: reference
ms.assetid: 8b2c8ff4-5c5d-446d-99e7-4daa1b36a163
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: de6308697ec84300392b15a85f7bc011606990c1
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101804967"
---
# <a name="tpmvscmgr"></a>tpmvscmgr

Программа командной строки тпмвскмгр позволяет пользователям с правами администратора создавать и удалять виртуальные смарт-карты TPM на компьютере.

## <a name="syntax"></a>Синтаксис

```
tpmvscmgr create [/name] [/adminkey DEFAULT | PROMPT | RANDOM] [/PIN DEFAULT | PROMPT] [/PUK DEFAULT | PROMPT] [/generate] [/machine] [/?]
```

```
tpmvscmgr destroy [/instance <instanceID>] [/?]
```

### <a name="create-parameters"></a>Создание параметров

Команда **CREATE** настраивает новые виртуальные смарт-карты в системе пользователя. Он также возвращает идентификатор экземпляра вновь созданной карточки для последующего обращения, если требуется удаление. Идентификатор экземпляра имеет формат **ROOT\SMARTCARDREADER\000n** , где **n** начинается с 0 и увеличивается на 1 каждый раз при создании новой виртуальной смарт-карты.

| Параметр | Описание |
|--|--|
| /Name | Обязательный элемент. Указывает имя новой виртуальной смарт-карты. |
| /админкэй | Указывает требуемый ключ администратора, который можно использовать для сброса ПИН-кода карточки, если пользователь забывает ПИН-код. Для этого может потребоваться выполнение следующих задач:<ul><li>**Default** — задает значение по умолчанию *010203040506070801020304050607080102030405060708*.</li><li>**Prompt** — предлагает пользователю ввести значение для ключа администратора.</li><li>**Случайным образом** — случайный параметр для ключа администратора карточки, которая не возвращается пользователю. При этом создается карточка, которая может быть неуправляемой с помощью средств управления смарт-картой. При использовании параметра RANDOM ключ администратора должен быть задан в виде шестнадцатеричных символов 48.</li></ul> |
| /пин | Указывает требуемое значение ПИН-кода пользователя.<ul><li>**Default** — задает ПИН-код по умолчанию 12345678.</li><li>**Prompt** — предлагает пользователю ввести ПИН-код в командной строке. ПИН-код должен содержать не менее восьми символов, а также цифр, символов и специальных символов.</li></ul> |
| /пук | Указывает требуемое значение ключа разблокировки ПИН-кода (PUK). Значение PUK-кода должно быть не менее восьми символов и может содержать цифры, символы и специальные символы. Если параметр не указан, карточка создается без PUK-кода. Эти способы могут быть следующими:<ul><li>**Default** — задает PUK-код по умолчанию *12345678*.</li><li>**Prompt** — предложит пользователю ввести PUK-код в командной строке.</li></ul> |
| /женерате | Создает файлы в хранилище, необходимые для функционирования виртуальной смарт-карты. Если вы не используете параметр **/женерате** , это похоже на то, что вы создали карточку без базовой файловой системы. Карта без файловой системы может управляться только системой управления смарт-картой, такой как Microsoft Configuration Manager. |
| /machine | Позволяет указать имя удаленного компьютера, на котором может быть создана виртуальная смарт-карта. Его можно использовать только в среде домена и полагается на DCOM. Для выполнения команды при создании виртуальной смарт-карты на другом компьютере пользователь, выполняющий эту команду, должен быть членом локальной группы администраторов на удаленном компьютере. |
| /? | Отображает справку для этой команды. |

### <a name="destroy-parameters"></a>Параметры уничтожения

Команда **destroy** безопасно удаляет виртуальную смарт-карту с компьютера пользователя.

> [!WARNING]
> Если виртуальная смарт-карта удалена, ее невозможно восстановить.

| Параметр | Описание |
|--|--|
| /instance | Указывает идентификатор экземпляра виртуальной смарт-карты, которую нужно удалить. InstanceID был создан в виде выходных данных tpmvscmgr.exe при создании карточки. Параметр **/инстанце** является обязательным полем для команды **destroy** . |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Для буквенно-цифровых входов разрешено использовать полный набор символов ASCII 127.

## <a name="examples"></a>Примеры

Чтобы создать виртуальную смарт-карту, которая впоследствии может управляться средством управления смарт-картой, запущенным с другого компьютера, введите:

```
tpmvscmgr.exe create /name VirtualSmartCardForCorpAccess /AdminKey DEFAULT /PIN PROMPT
```

Кроме того, вместо использования ключа администратора по умолчанию можно создать ключ администратора в командной строке. Следующая команда показывает, как создать ключ администратора.

```
tpmvscmgr.exe create /name VirtualSmartCardForCorpAccess /AdminKey PROMPT /PIN PROMPT
```

Чтобы создать неуправляемую виртуальную смарт-карту, которую можно использовать для регистрации сертификатов, введите:

```
tpmvscmgr.exe create /name VirtualSmartCardForCorpAccess /AdminKey RANDOM /PIN PROMPT /generate
```

Виртуальная смарт-карта создается с помощью случайного ключа администратора. Ключ автоматически удаляется после создания карты. Это означает, что если пользователь забыл ПИН-код или хочет изменить ПИН-код, пользователь должен удалить карту и создать ее снова.

Чтобы удалить карточку, введите:

```
tpmvscmgr.exe destroy /instance <instance ID>
```

Где `<instanceID>` — значение, печатаемое на экране при создании карты пользователем. В частности, для первой созданной карты ИДЕНТИФИКАТОРом экземпляра является *ROOT\SMARTCARDREADER\0000*.

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
