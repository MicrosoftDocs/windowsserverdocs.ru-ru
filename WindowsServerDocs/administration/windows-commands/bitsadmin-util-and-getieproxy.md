---
title: bitsadmin util и getieproxy
description: Справочная статья по команде битсадмин util and жетиепрокси, которая получает сведения об использовании прокси-сервера для данной учетной записи службы.
ms.topic: reference
ms.assetid: 6d50c7e3-f4eb-4ca5-9f0c-4ed396087db6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87a67dbdf1495b3cb8398fdbc0cc3cfed1c4e577
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033262"
---
# <a name="bitsadmin-util-and-getieproxy"></a>bitsadmin util и getieproxy

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Возвращает сведения об использовании прокси-сервера для данной учетной записи службы. Эта команда показывает значение для каждого использования прокси-сервера, а не только использование прокси-сервера, указанного для учетной записи службы. Дополнительные сведения о настройке использования прокси-сервера для конкретных учетных записей служб см. в описании команды [битсадмин util и сетиепрокси](bitsadmin-util-and-setieproxy.md) .

## <a name="syntax"></a>Синтаксис

```
bitsadmin /util /getieproxy <account> [/conn <connectionname>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ---------- |
| account | Указывает учетную запись службы, параметры прокси которой необходимо получить. Ниже перечислены возможные значения.<ul><li>ЛОКАЛЬ</li><li>   NETWORKSERVICE</li><li>LocalService.</li></ul> |
| connectionName | Необязательный элемент. Используется с параметром **/conn** для указания используемого подключения модема. Если параметр **/conn** не указан, служба BITS использует подключение по локальной сети. |

## <a name="examples"></a>Примеры

Чтобы отобразить сведения об использовании прокси-сервера для учетной записи сетевой службы, выполните следующие действия.

```
bitsadmin /util /getieproxy NETWORKSERVICE
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [битсадмин util, команда](bitsadmin-util.md)

- [Команда битсадмин](bitsadmin.md)
