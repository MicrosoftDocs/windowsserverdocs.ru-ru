---
title: bitsadmin setclientcertificatebyid
description: Справочная статья по команде битсадмин сетклиентцертификатебид, которая указывает идентификатор сертификата клиента, используемого для проверки подлинности клиента в запросе HTTPS (SSL).
ms.topic: article
ms.assetid: 8585a7a1-7472-437b-b04a-a11925782a3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e46219a52eda48ddb3e203730e6275fb5e534020
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893264"
---
# <a name="bitsadmin-setclientcertificatebyid"></a>bitsadmin setclientcertificatebyid

Указывает идентификатор сертификата клиента, который будет использоваться для проверки подлинности клиента в запросе HTTPS (SSL).

## <a name="syntax"></a>Синтаксис

```
bitsadmin /setclientcertificatebyid <job> <store_location> <store_name> <hexadecimal_cert_id>
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| -------------- | -------------- |
| задание | Отображаемое имя задания или идентификатор GUID. |
| store_location | Определяет расположение системного хранилища, используемого для поиска сертификата, в том числе:<ul><li>CURRENT_USER</li><li>LOCAL_MACHINE</li><li>CURRENT_SERVICE</li><li>Обслуживание</li><li>ПОЛЬЗОВАТЕЛИ</li><li>CURRENT_USER_GROUP_POLICY</li><li>LOCAL_MACHINE_GROUP_POLICY</li><li>LOCAL_MACHINE_ENTERPRISE.</li></ul> |
| store_name | Имя хранилища сертификатов, включая:<ul><li>ЦЕНТР сертификации (сертификаты центра сертификации)</li><li>MY (личные сертификаты)</li><li>Корневой каталог (корневые сертификаты)</li><li>SPC (сертификат издателя программного обеспечения).</li></ul> |
| hexadecimal_cert_id | Шестнадцатеричное число, представляющее хэш сертификата. |

## <a name="examples"></a>Примеры

Чтобы указать идентификатор сертификата клиента, который будет использоваться для проверки подлинности клиента в запросе HTTPS (SSL) для задания с именем *мидовнлоаджоб*:

```
bitsadmin /setclientcertificatebyid myDownloadJob BG_CERT_STORE_LOCATION_CURRENT_USER MY A106B52356D3FBCD1853A41B619358BD
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Команда битсадмин](bitsadmin.md)
