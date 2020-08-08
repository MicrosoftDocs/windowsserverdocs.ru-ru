---
title: Управление видимостью средства в решении
description: Управление видимостью средства в решении Windows Admin Center SDK (проект Хонолулу)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: df939bb1a87c9ded77431661dcabd7faf607bb6e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945007"
---
# <a name="control-your-tools-visibility-in-a-solution"></a>Управление видимостью средства в решении #

>Область применения. Windows Admin Center, ознакомительная версия Windows Admin Center

Иногда требуется исключить (или скрыть) расширение или средство из списка Доступные инструменты. Например, если средство предназначено только для Windows Server 2016 (не более старых версий), может потребоваться, чтобы пользователь, который подключается к серверу Windows Server 2012 R2, мог видеть ваше средство. (Представьте себе взаимодействие с пользователем. щелкните его, дождитесь загрузки средства, чтобы получить сообщение о том, что его функции недоступны для подключения.) Можно определить, следует ли отображать (или скрывать) функцию в manifest.jsфайле средства.

## <a name="options-for-deciding-when-to-show-a-tool"></a>Параметры для принятия решения о том, когда следует показывать средство ##

Существует три разных параметра, которые можно использовать для определения того, должно ли средство отображаться и доступно для конкретного сервера или подключения к кластеру.

* localhost
* Инвентаризация (массив свойств)
* скрипт

### <a name="localhost"></a>LocalHost ###

Свойство localHost объекта conditions содержит логическое значение, которое может быть вычислено, чтобы определить, имеет ли подключающийся узел localHost (тот же компьютер, на котором установлена центр администрирования Windows). Передавая значение свойству, вы указываете, когда (условие) для отображения средства. Например, если нужно, чтобы средство отображалось только при подключении пользователя к локальному узлу, настройте его следующим образом:

``` json
"conditions": [
{
    "localhost": true
}]
```

Кроме того, если нужно, чтобы средство отображалось только в том случае, если узел подключения *не является* localhost:

``` json
"conditions": [
{
    "localhost": false
}]
```

Вот как выглядят параметры конфигурации, чтобы отображалось только средство, если подключенный узел не является localhost:

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!windowsClients"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.windows-client"
        ],
        "conditions": [
        {
            "localhost": true
        }
        ]
    }
    ]
}
```

### <a name="inventory-properties"></a>Свойства инвентаризации ###

Пакет SDK включает предварительно проверенный набор свойств инвентаризации, который можно использовать для построения условий, чтобы определить, когда должно быть доступно средство. Массив "Inventory" имеет девять различных свойств:

| Имя свойства | Ожидаемый тип значения |
| ------------- | ------------------- |
| компутермануфактурер | строка |
| оператингсистемску | число |
| operatingSystemVersion | version_string (например: "10,1. *") |
| productType | число |
| клустерфкдн | строка |
| ишипервролеинсталлед | Логическое |
| ишипервповершеллинсталлед | Логическое |
| исманажементтулсаваилабле | Логическое |
| исвмфинсталлед | Логическое |

Каждый объект в массиве инвентаризации должен соответствовать следующей структуре JSON:

``` json
"<property name>": {
    "type": "<expected type>",
    "operator": "<defined operator to use>",
    "value": "<expected value to evaluate using the operator>"
}
```

#### <a name="operator-values"></a>Значения операторов ####

| Оператор | Описание |
| -------- | ----------- |
| gt | больше чем |
| ge | больше или равно |
| lt | меньше чем |
| le | меньше или равно |
| eq | равно |
| ne | не равно |
| is | проверяется, является ли значение истинным |
| not | проверяется, является ли значение ложным |
| contains | элемент существует в строке |
| notContains | элемент не существует в строке |

#### <a name="data-types"></a>Типы данных ####

Доступные параметры для свойства "Type":

| Тип | Description |
| ---- | ----------- |
| version | номер версии (например: 10,1. *) |
| число | числовое значение |
| строка | Строковое значение |
| Логическое | true или false |

#### <a name="value-types"></a>Типы значений ####

Свойство "value" принимает следующие типы:

* строка
* число
* Логическое

Правильно сформированный набор условий инвентаризации выглядит следующим образом:

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!servers"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.server"
        ],
        "conditions": [
        {
            "inventory": {
            "operatingSystemVersion": {
                "type": "version",
                "operator": "gt",
                "value": "6.3"
            },
            "operatingSystemSKU": {
                "type": "number",
                "operator": "eq",
                "value": "8"
            }
            }
        }
        ]
    }
    ]
}
```

### <a name="script"></a>Скрипт ###

Наконец, можно запустить пользовательский скрипт PowerShell для обнаружения доступности и состояния узла. Все скрипты должны возвращать объект со следующей структурой:

``` ps
@{
    State = 'Available' | 'NotSupported' | 'NotConfigured';
    Message = '<Message to explain the reason of state such as not supported and not configured.>';
    Properties =
        @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}
```
Свойство State — это важное значение, которое будет управлять принятием решения о показе или скрытии расширения в списке инструментов.  Допустимые значения:

| Значение | Описание |
| ---- | ----------- |
| Доступно | Расширение должно отображаться в списке инструментов. |
| NotSupported | Расширение не должно отображаться в списке инструментов. |
| NotConfigured | Это значение заполнителя для будущей работы, в ходе которого пользователю предлагается дополнительная настройка, прежде чем средство станет доступным.  В настоящее время это значение приведет к отображению средства и является функциональным аналогом "доступно". |

Например, если требуется загрузить средство, только если на удаленном сервере установлен BitLocker, сценарий будет выглядеть следующим образом:

``` ps
$response = @{
    State = 'NotSupported';
    Message = 'Not executed';
    Properties = @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}

if (Get-Module -ListAvailable -Name servermanager) {
    Import-module servermanager;
    $isInstalled = (Get-WindowsFeature -name bitlocker).Installed;
    $isGood = $isInstalled;
}

if($isGood) {
    $response.State = 'Available';
    $response.Message = 'Everything should work.';
}

$response
```

Конфигурация точки входа с использованием параметра скрипта выглядит следующим образом:

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!windowsClients"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.windows-client"
        ],
        "conditions": [
        {
            "localhost": true,
            "inventory": {
            "operatingSystemVersion": {
                "type": "version",
                "operator": "eq",
                "value": "10.0.*"
            },
            "operatingSystemSKU": {
                "type": "number",
                "operator": "eq",
                "value": "4"
            }
            },
            "script": "$response = @{ State = 'NotSupported'; Message = 'Not executed'; Properties = @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' }, @{Name='Prop2'; Value = 12345678; Type='number'; }; }; if (Get-Module -ListAvailable -Name servermanager) { Import-module servermanager; $isInstalled = (Get-WindowsFeature -name bitlocker).Installed; $isGood = $isInstalled; }; if($isGood) { $response.State = 'Available'; $response.Message = 'Everything should work.'; }; $response"
        }
        ]
    }
    ]
}
```

## <a name="supporting-multiple-requirement-sets"></a>Поддержка нескольких наборов требований ##

Можно использовать более одного набора требований, чтобы определить, когда следует отображать средство, определив несколько блоков «требования».

Например, чтобы отобразить средство, если "сценарий A" или "сценарий б" имеет значение true, определите два блока требований: Если значение равно true (то есть все условия в блоке требований соблюдены), средство отображается.

``` json
"entryPoints": [
{
    "requirements": [
    {
        "solutionIds": [
            …"scenario A"…
        ],
        "connectionTypes": [
            …"scenario A"…
        ],
        "conditions": [
            …"scenario A"…
        ]
    },
    {
        "solutionIds": [
            …"scenario B"…
        ],
        "connectionTypes": [
            …"scenario B"…
        ],
        "conditions": [
            …"scenario B"…
        ]
    }
    ]
}

```

## <a name="supporting-condition-ranges"></a>Поддержка диапазонов условий ##

Кроме того, можно определить ряд условий, определив несколько блоков "Condition" с одним и тем же свойством, но с разными операторами.

Если одно и то же свойство определено с разными операторами, оно отображается, пока значение находится между двумя условиями.

Например, это средство отображается, если операционная система является версией между 6.3.0 и 10.0.0:

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
             "msft.sme.server-manager!servers"
        ],
        "connectionTypes": [
             "msft.sme.connection-type.server"
        ],
        "conditions": [
        {
            "inventory": {
                "operatingSystemVersion": {
                    "type": "version",
                    "operator": "gt",
                    "value": "6.3.0"
                },
            }
        },
        {
            "inventory": {
                "operatingSystemVersion": {
                    "type": "version",
                    "operator": "lt",
                    "value": "10.0.0"
                }
            }
        }
        ]
    }
    ]
}

```
