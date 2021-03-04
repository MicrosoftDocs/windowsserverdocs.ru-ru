---
title: Использование команды verbose
description: Справочная статья для verbose, которая отображает подробные выходные данные для указанной команды.
ms.topic: reference
ms.assetid: fcf30ae7-818f-4e7e-a083-a1812682032b
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8db245b0bce452b9d01734b5dd766087dbe17f3b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101826100"
---
# <a name="using-the-verbose-command"></a>Использование команды verbose

Отображает подробные выходные данные для указанной команды. Вы можете использовать **/verbose** с любыми другими выполняемыми командами WDSUTIL. Обратите внимание, что необходимо указать **/verbose** и **/прогресс** непосредственно после **WDSUTIL**.

## <a name="syntax"></a>Синтаксис

```
wdsutil /verbose <commands>
```

## <a name="examples"></a>Примеры

Чтобы удалить утвержденные компьютеры из базы данных автоматического добавления и отобразить подробные выходные данные, введите:

```
wdsutil /Verbose /progress /Delete-AutoAddDevices /Server:MyWDSServer /DeviceType:ApprovedDevices
```