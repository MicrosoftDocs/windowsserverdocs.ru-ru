---
title: nslookup set
description: Справочная статья по команде nslookup set, которая изменяет параметры конфигурации, влияющие на поведение уточняющих запросов.
ms.topic: reference
ms.assetid: 1fe5b36d-e93e-468b-abca-43b0204b32d1
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bb86fa6fbba54e39acf08f521544be66d2ea6836
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101809562"
---
# <a name="nslookup-set"></a>nslookup set

> Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Изменяет параметры конфигурации, влияющие на работу функций Lookup.

## <a name="syntax"></a>Синтаксис

```
set all [class | d2 | debug | domain | port | querytype | recurse | retry | root | search | srchlist | timeout | type | vc] [options]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| [nslookup set all](nslookup-set-all.md) | Список всех текущих параметров. |
| [nslookup set class](nslookup-set-class.md) | Изменяет класс запроса, который указывает группу протоколов для информации. |
| [nslookup set d2](nslookup-set-d2.md) | Включает или выключает режим подробной отладки. |
| [nslookup set debug](nslookup-set-debug.md) | Полностью отключает режим отладки. |
| [nslookup set domain](nslookup-set-domain.md) | Изменяет доменное имя DNS по умолчанию на указанное имя. |
| [nslookup set port](nslookup-set-port.md) | Изменяет порт сервера доменных имен (DNS) по умолчанию TCP/UDP на указанное значение.
| [nslookup set querytype](nslookup-set-querytype.md) | Изменяет тип записи ресурса для запроса. |
| [nslookup set recurse](nslookup-set-recurse.md) | Указывает серверу доменных имен (DNS) запрашивать другие серверы, если не удается найти какие-либо сведения. |
| [nslookup set retry](nslookup-set-retry.md) | Задает число повторных попыток. |
| [nslookup set root](nslookup-set-root.md) | Изменяет имя корневого сервера, используемого для запросов. |
| [nslookup set search](nslookup-set-search.md) | Добавляет доменные имена DNS в списке поиска доменов DNS в запрос, пока не будет получен ответ. |
| [nslookup set srchlist](nslookup-set-srchlist.md) | Изменяет доменное имя службы доменных имен (DNS) по умолчанию и список поиска. |
| [nslookup set timeout](nslookup-set-timeout.md) | Изменяет начальное число секунд ожидания ответа на запрос поиска. |
| [nslookup set type](nslookup-set-type.md) | Изменяет тип записи ресурса для запроса. |
| [nslookup set vc](nslookup-set-vc.md) | Указывает, следует ли использовать виртуальный канал при отправке запросов на сервер. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
