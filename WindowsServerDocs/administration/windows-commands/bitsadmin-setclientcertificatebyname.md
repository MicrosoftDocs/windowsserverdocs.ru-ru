---
title: bitsadmin setclientcertificatebyname
description: Справочная статья по команде битсадмин сетклиентцертификатебинаме, которая указывает имя субъекта сертификата клиента, используемого для проверки подлинности клиента в запросе HTTPS (SSL).
ms.topic: reference
ms.assetid: f308a6d9-d0da-48be-ae41-eced14b3cccb
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 5a0d7e6566391248c22a18f7af048f1fc3d0579f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101821048"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>bitsadmin setclientcertificatebyname

Указывает имя субъекта сертификата клиента, используемого для проверки подлинности клиента в запросе HTTPS (SSL).

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setclientcertificatebyname <job> <store_location> <store_name> <subject_name>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| store_location | Определяет расположение системного хранилища, используемого для поиска сертификата. Ниже перечислены возможные значения.<ul><li>1 (CURRENT_USER)</li><li>2 (LOCAL_MACHINE)</li><li>3 (CURRENT_SERVICE)</li><li>4 (СЛУЖБЫ)</li><li>5 (ПОЛЬЗОВАТЕЛИ)</li><li>6 (CURRENT_USER_GROUP_POLICY)</li><li>7 (LOCAL_MACHINE_GROUP_POLICY)</li><li>8 (LOCAL_MACHINE_ENTERPRISE)</li></ul> |
| store_name | Имя хранилища сертификатов. Ниже перечислены возможные значения.<ul><li>ЦЕНТР сертификации (сертификаты центра сертификации)</li><li>MY (личные сертификаты)</li><li>Корневой каталог (корневые сертификаты)</li><li>SPC (сертификат издателя программного обеспечения)</li></ul> |
| subject_name | Имя сертификата. |

## <a name="examples"></a>Примеры

Чтобы указать имя сертификата клиента, *мойсертификат* для использования при проверке подлинности клиента в запросе HTTPS (SSL) для задания с именем *мидовнлоаджоб*:

```
bitsadmin /setclientcertificatebyname myDownloadJob 1 MY myCertificate
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
