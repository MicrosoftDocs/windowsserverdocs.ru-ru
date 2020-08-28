---
title: Использование команды Progress
description: Справочная статья о ходе выполнения, которая отображает ход выполнения команды.
ms.topic: reference
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 33e0494133523748b599ab9e3673d4f786e044df
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038312"
---
# <a name="using-the-progress-command"></a>Использование команды Progress

Отображает ход выполнения команды. **/Прогресс** можно использовать с любыми другими выполняемыми командами WDSUTIL. Обратите внимание, что необходимо указать **/verbose** и **/прогресс** непосредственно после **WDSUTIL**.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL /progress <commands>
```

## <a name="examples"></a>Примеры

Чтобы инициализировать сервер и отобразить ход выполнения, введите:
```
WDSUTIL /Verbose /Progress /Initialize-Server /Server:MyWDSServer /RemInst:C:\RemoteInstall
```