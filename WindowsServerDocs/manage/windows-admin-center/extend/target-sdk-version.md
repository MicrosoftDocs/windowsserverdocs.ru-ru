---
title: Нацеливание на другую версию пакета SDK для Windows Admin Center
description: Назначение другой версии пакета SDK для Windows Admin Center (проект Хонолулу)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3d6b08e69d69a37b31b616994b3bdb67666cb2bb
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766937"
---
# <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>Нацеливание на другую версию пакета SDK для Windows Admin Center

>Область применения. Windows Admin Center, ознакомительная версия Windows Admin Center

Обновление расширения с помощью изменений пакета SDK и изменение платформы — это просто.  Мы используем [теги NPM](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk) для организации выпуска новых функций в версии пакета SDK.

Вы можете выбрать три версии пакета SDK:

* ```latest``` — Этот пакет SDK соответствует текущему общедоступному выпуску центра администрирования Windows
* ```insider``` — Этот пакет SDK соответствует текущему предварительному выпуску центра администрирования Windows (доступен в предварительной версии Windows Server Insider Preview).
* ```next``` — Этот пакет SDK содержит самые последние функции

> [!NOTE]
> Узнайте больше о различных [версиях](../overview.md) центра администрирования Windows, доступных для загрузки.

## <a name="targeting-sdk-version-on-a-new-project"></a>Целевая версия пакета SDK для нового проекта

При создании нового расширения можно включить ```--version``` параметр, предназначенный для другой версии пакета SDK:

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| Значение | Объяснение | Пример |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Название вашей компании (с пробелами) | ```Contoso Inc``` |
| ```{!Tool Name}``` | Имя средства (с пробелами) | ```Manage Foo Works``` |
| ```{!version}``` | Версия пакета SDK | ```latest``` |

Ниже приведен пример создания нового расширения для нацеливания ```insider``` :

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## <a name="targeting-sdk-version-on-an-existing-project"></a>Целевая версия пакета SDK для существующего проекта

Чтобы изменить существующий проект для другой версии пакета SDK, измените следующую строку в следующей строке ```package.json``` :

```
"@microsoft/windows-admin-center-sdk": "latest",
```
В этом примере замените ```latest``` требуемой версией пакета SDK, например ```insider``` :

```
"@microsoft/windows-admin-center-sdk": "insider",
```

Затем выполните команду ```npm install``` , чтобы обновить ссылки в рамках проекта.