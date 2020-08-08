---
title: Добавление iFrame в расширение средства
description: Разработка расширения инструмента Windows Admin Center SDK (Project Хонолулу) — Добавление iFrame к расширению инструмента
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: da145d4ef3a58af51846d395081fb643af7c78ac
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945111"
---
# <a name="add-an-iframe-to-a-tool-extension"></a>Добавление iFrame в расширение средства

>Область применения. Windows Admin Center, ознакомительная версия Windows Admin Center

В этой статье мы добавим iFrame к новому, пустому расширению инструмента, созданному с помощью интерфейса командной строки центра администрирования Windows.

## <a name="prepare-your-environment"></a>Подготовка среды ##

Если вы еще этого не сделали, следуйте указаниям в [подсказке по разработке расширения](../develop-tool.md) для подготовки среды и созданию нового пустого расширения инструмента.

## <a name="add-a-module-to-your-project"></a>Добавление модуля в проект ##

Добавьте новый [пустой модуль](add-module.md) в проект, в который мы добавим IFRAME на следующем шаге.

## <a name="add-an-iframe-to-your-module"></a>Добавление iFrame в модуль ##

Теперь мы добавим iFrame к новому пустому модулю, который мы только что создали.

В \срк\апп \, перейдите в папку модуля, а затем откройте файл ```{!module-name}.component.html``` и найдите следующее соглашение об именовании:

| Значение | Объяснение | Пример имени файла |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Имя модуля (нижний регистр, пробелы заменены на тире) | ```manage-foo-works-portal.component.html``` |

Добавьте следующее содержимое в HTML-файл:

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

Вот и вы добавили iFrame к своему расширению.  Затем вы можете [создать и загрузить](../develop-tool.md#build-and-side-load-your-extension) свои расширения в центре администрирования Windows, чтобы увидеть результаты.

> [!Note]
> Параметры политики безопасности содержимого (CSP) могут препятствовать отрисовке некоторых сайтов в iFrame в центре администрирования Windows. Подробнее об этом можно узнать [здесь](https://content-security-policy.com/).
