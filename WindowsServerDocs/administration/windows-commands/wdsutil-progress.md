---
title: wdsutil progress
description: Справочная статья с ходом выполнения WDSUTIL, которая отображает ход выполнения команды.
ms.topic: reference
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e9bd24479cd2d6ab538e8a7810f9dab28e27db54
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101825601"
---
# <a name="wdsutil-progress"></a>WDSUTIL/прогресс

Отображает ход выполнения команды. **/Прогресс** можно использовать с любыми другими выполняемыми командами WDSUTIL. Если вы хотите включить подробное ведение журнала для этой команды, необходимо указать **/verbose** и **/прогресс** непосредственно после **WDSUTIL**.

## <a name="syntax"></a>Синтаксис

```
wdsutil /progress <commands>
```

## <a name="examples"></a>Примеры

Чтобы инициализировать сервер и отобразить ход выполнения, введите:

```
wdsutil /verbose /progress /Initialize-Server /Server:MyWDSServer /RemInst:C:\RemoteInstall
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)