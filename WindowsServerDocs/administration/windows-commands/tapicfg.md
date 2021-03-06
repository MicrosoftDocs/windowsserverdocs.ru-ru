---
title: tapicfg
description: Справочная статья по командам Tapicfg, которая создает, удаляет или отображает раздел каталога приложений TAPI или задает раздел каталога приложений TAPI по умолчанию.
ms.topic: reference
ms.assetid: c0e642ce-5d98-4edb-9a65-1dff09aef4e1
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: eadce4f145e57f0e6cf6e7ac1291e42bdd92b82d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101805347"
---
# <a name="tapicfg"></a>tapicfg

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Создает, удаляет или отображает раздел каталога приложений TAPI или задает раздел каталога приложений TAPI по умолчанию. Клиенты TAPI 3,1 могут использовать сведения из этого раздела каталога приложений со службой локатора службы каталогов для поиска и взаимодействия с каталогами TAPI. Кроме того, с помощью программы **Tapicfg** можно создавать и удалять точки подключения службы, которые позволяют клиентам TAPI эффективно размещать разделы каталога приложений TAPI в домене.

Это средство командной строки можно запустить на любом компьютере, входящем в домен.

## <a name="syntax"></a>Синтаксис

```
tapicfg install
tapicfg remove
tapicfg publishscp
tapicfg removescp
tapicfg show
tapicfg makedefault
```

### <a name="parameters"></a>Параметры

| Параметры | Описание |
|--|--|
| [tapicfg install](tapicfg-install.md) | Создает раздел каталога приложений TAPI. |
| [tapicfg remove](tapicfg-remove.md) | Удаляет раздел каталога приложений TAPI.|
| [tapicfg publishscp](tapicfg-publishscp.md) | Создает точку подключения службы для публикации раздела каталога приложений TAPI. |
| [tapicfg removescp](tapicfg-removescp.md) | Удаляет точку подключения службы для раздела каталога приложений TAPI. |
| [tapicfg show](tapicfg-show.md) | Отображает имена и расположение разделов каталога приложений TAPI в домене. |
| [tapicfg makedefault](tapicfg-makedefault.md) | Задает раздел каталога приложений TAPI по умолчанию для домена. |

#### <a name="remarks"></a>Комментарии

- Необходимо быть членом группы **"Администраторы предприятия** " в Active Directory, чтобы выполнить команду **Tapicfg Install** (для создания раздела каталога приложений TAPI) или **Tapicfg Remove** (удалить раздел каталога приложений TAPI).

- Введенный пользователем текст (например, имена разделов каталога приложений TAPI, серверов и доменов) с международными или Юникод-символами отображается правильно, только если установлены соответствующие шрифты и языковая поддержка.

- Вы по-прежнему можете использовать в организации серверы службы локатора Интернета (ILS), если для поддержки определенных приложений требуется ILS, так как клиенты TAPI, работающие под управлением Windows XP или ОС Windows Server 2003, могут запрашивать серверы ILS или разделы каталога приложений TAPI.

- Для создания или удаления точек подключения службы можно использовать **Tapicfg** . Если раздел каталога приложений TAPI переименовывается по какой-либо причине (например, при переименовании домена, в котором он находится), необходимо удалить существующую точку подключения службы и создать новую, содержащую новое DNS-имя публикуемого раздела каталога приложений TAPI. В противном случае клиенты TAPI не смогут выполнить обнаружение раздела каталога приложений TAPI и получить к нему доступ. Точку подключения службы также можно удалить в целях обслуживания или безопасности (например, если нежелательно предоставлять доступ к данным TAPI в конкретном разделе каталога приложений TAPI).

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [tapicfg install](tapicfg-install.md)

- [tapicfg remove](tapicfg-remove.md)

- [tapicfg publishscp](tapicfg-publishscp.md)

- [tapicfg removescp](tapicfg-removescp.md)

- [tapicfg show](tapicfg-show.md)

- [tapicfg makedefault](tapicfg-makedefault.md)
