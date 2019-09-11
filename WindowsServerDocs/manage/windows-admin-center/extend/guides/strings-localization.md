---
title: Строки и локализация в центре администрирования Windows
description: Сведения о том, как подготовить строки для локализации в пакете SDK для Windows Admin Center (проект Хонолулу)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4cc624dcc985f13f97b7bbc767de6bbb9c72217a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869714"
---
# <a name="strings-and-localization-in-windows-admin-center"></a>Строки и локализация в центре администрирования Windows #

>Область применения. Windows Admin Center, ознакомительная версия Windows Admin Center

Давайте подробно рассмотрим пакет SDK для расширений центра администрирования Windows и поговорим о строках и локализации.

Чтобы включить локализацию всех строк, отображаемых на уровне представления, воспользуйтесь файлом strings. resjson в разделе/СРК/ресаурцес/стрингс — он уже настроен. Если необходимо добавить новую строку в расширение, добавьте ее в этот файл RESJSON в качестве новой записи. Существующая структура имеет следующий формат:

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

Для строк можно использовать любой формат, но имейте в виду, что процесс создания (процесс, который принимает RESJSON и выводит используемый класс TypeScript) преобразует символ подчеркивания (_) в точки (.).

Например, эта запись:
``` ts
"HelloWorld_cim_title": "CIM Component",
```
Создает следующую структуру метода доступа:
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```

## <a name="add-other-languages-for-localization"></a>Добавить другие языки для локализации ## 

Для локализации на другие языки необходимо создать файл strings. resjson для каждого языка. Эти файлы должны быть местами в ```\loc\output\{!ExtensionName}\{!LanguageFolder}\strings.resjson```. Доступные языки с соответствующими папками:

| Язык      | Папка      |
| ------------- |-------------|
| Čeština | cs-CZ |
| Deutsch | de-DE |
| Английский | en-US |
| Español | es-ES |
| Français | fr-FR | 
| Magyar | hu-HU | 
| Italiano | it-IT |
| 日本語 | ja-JP | 
| 한국어 | ko-KR | 
| Nederlands | nl-NL |
| Polski | pl-PL |
| Português (Brasil) | pt-BR |
| Português (Portugal) | pt-PT |
| Русский | ru-RU |
| Svenska | sv-SE |
| Türkçe    | tr-TR |
| 中文(简体) | zh-CN |
| 中文(繁體) | zh-TW |
> [!NOTE]
> Если потребности в структуре файлов различаются в LOC/Output, необходимо настроить Локалеоффсет для задачи gulp "Generate-RESJSON-JSON-локализованный", которая находится в gulpfile. js. Это смещение является глубоким для папки loc, в которой он должен начинать поиск файлов strings. resjson.

Каждый файл strings. resjson будет отформатирован так же, как упоминалось ранее в верхней части этого раздела. 

Например, чтобы включить локализацию для Espaсol, включите следующую запись в ```\loc\output\HelloWorld\es-ES\strings.resjson```: 
```json
"HelloWorld_cim_title": "CIM Componente",
```
В любое время, когда вы добавили локализованные строки, для их появления необходимо запустить gulp. Выполните:
``` cmd
gulp generate 
```

Чтобы убедиться, что строки созданы, перейдите к ```\src\app\assets\strings\{!LanguageFolder}\strings.resjson```. Недавно добавленная запись появится в этом файле.
Теперь при переключении языка в центре администрирования Windows вы увидите локализованные строки в расширении. 
