---
title: Создание поставщика соединений для расширения решения
description: Разработка расширения решения Windows Admin Center SDK (проект Хонолулу) — создание поставщика подключения
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: ec11b8a6b9129348ec2405548c21fa9d6ec5deff
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952689"
---
# <a name="create-a-connection-provider-for-a-solution-extension"></a>Создание поставщика соединений для расширения решения

>Область применения. Windows Admin Center, ознакомительная версия Windows Admin Center

Поставщики подключений играют важную роль в том, как центр администрирования Windows определяет и взаимодействует с подключаемыми объектами или целями. В основном поставщик соединений выполняет действия во время соединения, например обеспечение доступности целевого объекта и его доступность, а также обеспечение наличия у подключающегося пользователя разрешений на доступ к целевой службе.

По умолчанию центр администрирования Windows поставляется со следующими поставщиками подключений:

* Сервер
* Клиент Windows
* Отказоустойчивый кластер
* Кластер ХЦИ

Чтобы создать собственный настраиваемый поставщик соединений, выполните следующие действия.

* Добавить сведения о поставщике подключения в```manifest.json```
* Определение поставщика состояния подключения
* Реализация поставщика соединений на уровне приложения

## <a name="add-connection-provider-details-to-manifestjson"></a>Добавление сведений о поставщике подключения в manifest.js

Теперь мы рассмотрим, что необходимо знать для определения поставщика подключения в ```manifest.json``` файле проекта.

### <a name="create-entry-in-manifestjson"></a>Создать запись в manifest.jsна

```manifest.json```Файл находится в папке \срк и содержит, помимо прочего, определения точек входа в проект. Типы точек входа включают средства, решения и поставщики подключений. Мы будем определять поставщик соединений.

Пример записи поставщика подключения в manifest.jsв:

``` json
    {
      "entryPointType": "connectionProvider",
      "name": "addServer",
      "path": "/add",
      "displayName": "resources:strings:addServer_displayName",
      "icon": "sme-icon:icon-win-server",
      "description": "resources:strings:description",
      "connectionType": "msft.sme.connection-type.server",
      "connectionTypeName": "resources:strings:addServer_connectionTypeName",
      "connectionTypeUrlName": "server",
      "connectionTypeDefaultSolution": "msft.sme.server-manager!servers",
      "connectionTypeDefaultTool": "msft.sme.server-manager!overview",
      "connectionStatusProvider": {
        "powerShell": {
          "script": "## Get-My-Status ##\nfunction Get-Status()\n{\n# A function like this would be where logic would exist to identify if a node is connectable.\n$status = @{label = $null; type = 0; details = $null; }\n$caption = \"MyConstCaption\"\n$productType = \"MyProductType\"\n# A result object needs to conform to the following object structure to be interpreted properly by the Windows Admin Center shell.\n$result = @{ status = $status; caption = $caption; productType = $productType; version = $version }\n# DO FANCY LOGIC #\n# Once the logic is complete, the following fields need to be populated:\n$status.label = \"Display Thing\"\n$status.type = 0 # This value needs to conform to the LiveConnectionStatusType enum. >= 3 represents a failure.\n$status.details = \"success stuff\"\nreturn $result}\nGet-Status"
        },
        "displayValueMap": {
          "wmfMissing-label": "resources:strings:addServer_status_wmfMissing_label",
          "wmfMissing-details": "resources:strings:addServer_status_wmfMissing_details",
          "unsupported-label": "resources:strings:addServer_status_unsupported_label",
          "unsupported-details": "resources:strings:addServer_status_unsupported_details"
        }
      }
    },
```

Точка входа типа "Конннектионпровидер" указывает оболочке центра администрирования Windows, что настраиваемый элемент является поставщиком, который будет использоваться решением для проверки состояния подключения. Точки входа поставщика подключения содержат ряд важных свойств, определенных ниже.

| Свойство | Описание |
| -------- | ----------- |
| Параметр entrypointtype | Это обязательное свойство. Существует три допустимых значения: "инструмент", "решение" и "connectionProvider". |
| name | Определяет поставщика соединений в области решения. Это значение должно быть уникальным в полном экземпляре центра администрирования Windows (а не только в решении). |
| path | Представляет URL-путь для пользовательского интерфейса "Добавить подключение", если он будет настроен решением. Это значение должно быть сопоставлено с маршрутом, настроенным в файле App-Routing. Module. TS. Если точка входа решения настроена для использования Рутнавигатионбехавиор подключений, этот маршрут загрузит модуль, используемый оболочкой, для вывода пользовательского интерфейса добавления подключения. Дополнительные сведения доступны в разделе по Рутнавигатионбехавиор. |
| displayName | Введенное здесь значение отображается в правой части оболочки под черной панелью центра администрирования Windows, когда пользователь загружает страницу соединений решения. |
| icon | Представляет значок, используемый в раскрывающемся меню решения для представления решения. |
| description | Введите краткое описание точки входа. |
| connectionType | Представляет тип соединения, который будет загружен поставщиком. Введенное здесь значение также будет использоваться в точке входа решения, чтобы указать, что решение может загрузить эти подключения. Введенное здесь значение также будет использоваться в точках входа инструментов, чтобы указать, что средство совместимо с этим типом. Введенное здесь значение также будет использоваться в объекте Connection, который отправляется в вызов RPC в окне "Добавление окна" на шаге реализации уровня приложения. |
| коннектионтипенаме | Используется в таблице соединений для представления соединения, использующего поставщик соединений. Это должно быть имя типа во множественном числе. |
| коннектионтипеурлнаме | Используется при создании URL-адреса, представляющего загруженное решение, после подключения центра администрирования Windows к экземпляру. Эта запись используется после соединений и перед целевым объектом. В этом примере "коннектионексампле" — это значение, которое отображается в URL-адресе:`http://localhost:6516/solutionexample/connections/connectionexample/con-fake1.corp.contoso.com` |
| коннектионтипедефаултсолутион | Представляет компонент по умолчанию, который должен быть загружен поставщиком соединений. Это значение является сочетанием: <br>[a] имя пакета расширения, определенного в верхней части манифеста; <br>[b] восклицательный знак (!); <br>[c] имя точки входа решения.    <br>Для проекта с именем "MSFT. Эксперт. mySample-Extension" и точкой входа решения с именем "example" это значение будет "MSFT. Эксперт. Солутионексампле-Extension! example". |
| коннектионтипедефаулттул | Представляет инструмент по умолчанию, который должен быть загружен при успешном соединении. Это значение свойства состоит из двух частей, аналогичных Коннектионтипедефаултсолутион. Это значение является сочетанием: <br>[a] имя пакета расширения, определенного в верхней части манифеста; <br>[b] восклицательный знак (!); <br>[c] имя точки входа для средства, которое должно быть загружено изначально. <br>Для проекта с именем "MSFT. Эксперт. Солутионексампле-Extension" и точкой входа решения с именем "example" это значение будет "MSFT. Эксперт. Солутионексампле-Extension! example". |
| коннектионстатуспровидер | См. раздел "определение поставщика состояния подключения". |

## <a name="define-connection-status-provider"></a>Определение поставщика состояния подключения

Поставщик состояния соединения — это механизм, с помощью которого целевой объект проверяется как подключенный и доступный, также гарантируя, что подключающийся пользователь имеет разрешение на доступ к целевому объекту. В настоящее время существует два типа поставщиков состояний подключения: PowerShell и Релативегатевайурл.

*   <strong>Поставщик состояния подключения PowerShell</strong> — определяет, находится ли целевой объект в сети и доступен с помощью скрипта PowerShell. Результат должен возвращаться в объекте с одним свойством Status, определенным ниже.
*   <strong>Поставщик состояния подключения релативегатевайурл</strong> — определяет, находится ли целевой объект в сети и доступен с вызовом RESTful. Результат должен возвращаться в объекте с одним свойством Status, определенным ниже.

### <a name="define-status"></a>Определение состояния

Поставщики состояния соединения необходимы для возврата объекта с одним свойством ```status``` , которое соответствует следующему формату:

``` json
{
    status: {
        label: string;
        type: int;
        details: string;
    }
}
```

Свойства состояния:

* <strong>Метка</strong> — метка, описывающая тип возвращаемого значения состояния. Обратите внимание, что значения для метки могут быть сопоставлены во время выполнения. Сведения о сопоставлении значений в среде выполнения см. в записи ниже.

* <strong>Type</strong> — тип возвращаемого значения состояния. Тип имеет следующие значения перечисления. Для любого значения 2 или более поздней версии платформа не будет переходить к подключенному объекту, и в пользовательском интерфейсе отобразится сообщение об ошибке.

   Типов

  | Значение | Описание |
  | ----- | ----------- |
  | 0 | Миграция по сети |
  | 1 | Предупреждение |
  | 2 | Не авторизовано |
  | 3 | Error |
  | 4 | Аварий |
  | 5 | Неизвестно |

* <strong>Сведения</strong> — дополнительные сведения, описывающие тип возвращаемого значения состояния.

### <a name="powershell-connection-status-provider-script"></a>Скрипт поставщика состояния подключения PowerShell

Сценарий PowerShell для поставщика состояния подключения определяет, находится ли целевой объект в сети и доступен с помощью скрипта PowerShell. Результат должен возвращаться в объекте с одним свойством Status. Ниже приведен пример сценария.

Пример сценария PowerShell:

```PowerShell
## Get-My-Status ##

function Get-Status()
{
    # A function like this would be where logic would exist to identify if a node is connectable.
    $status = @{label = $null; type = 0; details = $null; }
    $caption = "MyConstCaption"
    $productType = "MyProductType"

    # A result object needs to conform to the following object structure to be interperated properly by the Windows Admin Center shell.
    $result = @{ status = $status; caption = $caption; productType = $productType; version = $version }

    # DO FANCY LOGIC #

    # Once the logic is complete, the following fields need to be populated:
    $status.label = "Display Thing"
    $status.type = 0 # This value needs to conform to the LiveConnectionStatusType enum. >= 3 represents a failure.
    $status.details = "success stuff"

    return $result
}

Get-Status
```

### <a name="define-relativegatewayurl-connection-status-provider-method"></a>Определение метода поставщика состояния соединения Релативегатевайурл

Метод поставщика состояния соединения ```RelativeGatewayUrl``` вызывает API-интерфейс для определения того, находится ли целевой объект в сети и доступен. Результат должен возвращаться в объекте с одним свойством Status. Ниже приведен пример записи поставщика подключения в manifest.jsРелативегатевайурл on.

``` json
    {
      "entryPointType": "connectionProvider",
      "name": "addServer",
      "path": "/add/server",
      "displayName": "resources:strings:addServer_displayName",
      "icon": "sme-icon:icon-win-server",
      "description": "resources:strings:description",
      "connectionType": "msft.sme.connection-type.server",
      "connectionTypeName": "resources:strings:addServer_connectionTypeName",
      "connectionTypeUrlName": "server",
      "connectionTypeDefaultSolution": "msft.sme.server-manager!servers",
      "connectionTypeDefaultTool": "msft.sme.server-manager!overview",
      "connectionStatusProvider": {
        "relativeGatewayUrl": "<URL here post /api>",
        "displayValueMap": {
          "wmfMissing-label": "resources:strings:addServer_status_wmfMissing_label",
          "wmfMissing-details": "resources:strings:addServer_status_wmfMissing_details",
          "unsupported-label": "resources:strings:addServer_status_unsupported_label",
          "unsupported-details": "resources:strings:addServer_status_unsupported_details"
        }
      }
    },
```

Примечания об использовании Релативегатевайурл:

* "Релативегатевайурл" указывает, куда получить состояние подключения из URL-адреса шлюза. Этот URI является относительным от/АПИ. Если $connectionName найден в URL-адресе, он будет заменен именем соединения.
* Все свойства Релативегатевайурл должны быть выполнены для шлюза узла, что можно сделать, создав расширение шлюза.

### <a name="map-values-in-runtime"></a>Отображение значений в среде выполнения

Значения Label и Details в объекте возврата состояния можно форматировать во время настройки, включая ключи и значения в свойстве "Дефаултвалуемап" поставщика.

Например, если добавить значение ниже, то каждый раз, когда "defaultConnection_test" отображается как значение для метки или сведений, центр администрирования Windows автоматически заменит ключ настроенным строковым значением ресурса.

``` json
    "defaultConnection_test": "resources:strings:addServer_status_defaultConnection_label"
```

## <a name="implement-connection-provider-in-application-layer"></a>Реализация поставщика соединений на уровне приложения

Теперь мы создадим поставщик соединений на уровне приложения, создав класс TypeScript, реализующий OnInit. Класс содержит следующие функции:

| Функция | Описание |
| -------- | ----------- |
| Конструктор (частный Аппконтекстсервице: Аппконтекстсервице, частный маршрут: Активатедрауте) |  |
| общедоступная Нгонинит () |  |
| общедоступная OnSubmit () | Содержит логику обновления оболочки при попытке добавления соединения |
| Открытый OnCancel () | Содержит логику обновления оболочки при отмене попытки добавления соединения |

### <a name="define-onsubmit"></a>Определение OnSubmit

```onSubmit```выдает вызов RPC обратно в контекст приложения, чтобы уведомить оболочку о добавлении подключения. Базовый вызов использует "Упдатедата" следующим образом:

``` ts
this.appContextService.rpc.updateData(
    EnvironmentModule.nameOfShell,
    '##',
    <RpcUpdateData>{
        results: {
            connections: connections,
            credentials: this.useCredentials ? this.creds : null
        }
    }
);
```

Результатом является свойство Connection, которое представляет собой массив объектов, соответствующих следующей структуре:

``` ts

/**
 * The connection attributes class.
 */
export interface ConnectionAttribute {

    /**
     * The id string of this attribute
     */
    id: string;

    /**
     * The value of the attribute. used for attributes that can have variable values such as Operating System
     */
    value?: string | number;
}

/**
 * The connection class.
 */
export interface Connection {

    /**
     * The id of the connection, this is unique per connection
     */
    id: string;

    /**
     * The type of connection
     */
    type: string;

    /**
     * The name of the connection, this is unique per connection type
     */
    name: string;

    /**
     * The property bag of the connection
     */
    properties?: ConnectionProperties;

    /**
     * The ids of attributes identified for this connection
     */
    attributes?: ConnectionAttribute[];

    /**
     * The tags the user(s) have assigned to this connection
     */
    tags?: string[];
}

/**
 * Defines connection type strings known by core
 * Be careful that these strings match what is defined by the manifest of @msft-sme/server-manager
 */
export const connectionTypeConstants = {
    server: 'msft.sme.connection-type.server',
    cluster: 'msft.sme.connection-type.cluster',
    hyperConvergedCluster: 'msft.sme.connection-type.hyper-converged-cluster',
    windowsClient: 'msft.sme.connection-type.windows-client',
    clusterNodesProperty: 'nodes'
};
```

### <a name="define-oncancel"></a>Определить OnCancel

```onCancel```отменяет попыток "Добавить подключение", передавая пустой массив соединений:

``` ts
this.appContextService.rpc.updateData(EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
```

## <a name="connection-provider-example"></a>Пример поставщика подключения

Ниже приведен полный класс TypeScript для реализации поставщика соединений. Обратите внимание, что строка "connectionType" соответствует параметру "connectionType", как определено в поставщике соединений в manifest.json.

``` ts
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';
import { AppContextService } from '@msft-sme/shell/angular';
import { Connection, ConnectionUtility } from '@msft-sme/shell/core';
import { EnvironmentModule } from '@msft-sme/shell/dist/core/manifest/environment-modules';
import { RpcUpdateData } from '@msft-sme/shell/dist/core/rpc/rpc-base';
import { Strings } from '../../generated/strings';

@Component({
  selector: 'add-example',
  templateUrl: './add-example.component.html',
  styleUrls: ['./add-example.component.css']
})
export class AddExampleComponent implements OnInit {
  public newConnectionName: string;
  public strings = MsftSme.resourcesStrings<Strings>().SolutionExample;
  private connectionType = 'msft.sme.connection-type.example'; // This needs to match the connectionTypes value used in the manifest.json.

  constructor(private appContextService: AppContextService, private route: ActivatedRoute) {
    // TODO:
  }

  public ngOnInit() {
    // TODO
  }

  public onSubmit() {
    let connections: Connection[] = [];

    let connection = <Connection> {
      id: ConnectionUtility.createConnectionId(this.connectionType, this.newConnectionName),
      type: this.connectionType,
      name: this.newConnectionName
    };

    connections.push(connection);

    this.appContextService.rpc.updateData(
      EnvironmentModule.nameOfShell,
      '##',
      <RpcUpdateData> {
        results: {
          connections: connections,
          credentials: null
        }
      }
    );
  }

  public onCancel() {
    this.appContextService.rpc.updateData(
      EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
  }
}

```
