---
title: ход выполнения WDSUTIL
description: Справочная статья с ходом выполнения WDSUTIL, которая отображает ход выполнения команды.
ms.topic: reference
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 4a7ddc18db35b110c8b5c513f798e3408aafd93f
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730695"
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