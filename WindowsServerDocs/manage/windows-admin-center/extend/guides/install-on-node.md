---
title: Установка полезных данных расширения на управляемом узле
description: Инструкции по установке полезных данных расширения на управляемый узел
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6a8675ff481f908feeeef4f97be0f1889b117291
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944976"
---
# <a name="install-extension-payload-on-a-managed-node"></a>Установка полезных данных расширения на управляемом узле

>Область применения. Windows Admin Center, ознакомительная версия Windows Admin Center

## <a name="setup"></a>Настройка

> [!NOTE]
> Для выполнения этой инструкции потребуется сборка 1.2.1904.02001 или более поздняя версия. Чтобы проверить номер сборки, откройте центр администрирования Windows и щелкните вопросительный знак в правом верхнем углу.

Создайте [расширение средства](../develop-tool.md) для центра администрирования Windows, если это еще не сделано. Закончив, запишите значения, используемые при создании расширения:

| Значение | Объяснение | Пример |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Название вашей компании (с пробелами) | ```Contoso``` |
| ```{!Tool Name}``` | Имя средства (с пробелами) | ```InstallOnNode``` |

В папке расширения средства создайте ```Node``` папку ( ```{!Tool Name}\Node``` ). Все, что помещено в эту папку, будет скопировано на управляемый узел при использовании этого API. Добавьте файлы, необходимые для вашего варианта использования.

Также создайте ```{!Tool Name}\Node\installNode.ps1``` скрипт. Этот скрипт будет запущен на управляемом узле после копирования всех файлов из ```{!Tool Name}\Node``` папки на управляемый узел. Добавьте любую дополнительную логику для вашего варианта использования. Пример ```{!Tool Name}\Node\installNode.ps1``` файла:

``` ps1
# Add logic for installing payload on managed node
echo 'Success'
```

> [!NOTE]
> ```{!Tool Name}\Node\installNode.ps1```имеет определенное имя, которое будет искать API. Изменение имени этого файла приведет к ошибке.


## <a name="integration-with-ui"></a>Интеграция с пользовательским интерфейсом

Обновите ```\src\app\default.component.ts``` следующее:

``` ts
import { Component } from '@angular/core';
import { AppContextService } from '@microsoft/windows-admin-center-sdk/angular';
import { Observable } from 'rxjs';

@Component({
  selector: 'default-component',
  templateUrl: './default.component.html',
  styleUrls: ['./default.component.css']
})

export class DefaultComponent {
  constructor(private appContextService: AppContextService) { }

  public response: any;
  public loading = false;

  public installOnNode() {
    this.loading = true;
    this.post('{!Company Name}.{!Tool Name}', '1.0.0',
      this.appContextService.activeConnection.nodeName).subscribe(
        (response: any) => {
          console.log(response);
          this.response = response;
          this.loading = false;
        },
        (error) => {
          console.log(error);
          this.response = error;
          this.loading = false;
        }
      );
  }

  public post(id: string, version: string, targetNode: string): Observable<any> {
    return this.appContextService.node.post(targetNode,
      `features/extensions/${id}/versions/${version}/install`);
  }

}
```
Обновите заполнители значениями, которые использовались при создании расширения:
``` ts
this.post('contoso.install-on-node', '1.0.0',
      this.appContextService.activeConnection.nodeName).subscribe(
        (response: any) => {
          console.log(response);
          this.response = response;
          this.loading = false;
        },
        (error) => {
          console.log(error);
          this.response = error;
          this.loading = false;
        }
      );
```

Также обновите ```\src\app\default.component.html``` до:
``` html
<button (click)="installOnNode()">Click to install</button>
<sme-loading-wheel *ngIf="loading" size="large"></sme-loading-wheel>
<p *ngIf="response">{{response}}</p>
```
И наконец ```\src\app\default.module.ts``` :
``` ts
import { CommonModule } from '@angular/common';
import { NgModule } from '@angular/core';

import { LoadingWheelModule } from '@microsoft/windows-admin-center-sdk/angular';
import { DefaultComponent } from './default.component';
import { Routing } from './default.routing';

@NgModule({
  imports: [
    CommonModule,
    LoadingWheelModule,
    Routing
  ],
  declarations: [DefaultComponent]
})
export class DefaultModule { }

```

## <a name="creating-and-installing-a-nuget-package"></a>Создание и установка пакета NuGet

Последний шаг — создание пакета NuGet с добавленными файлами, а затем Установка этого пакета в центре администрирования Windows.

Если пакет расширения ранее не создавался, следуйте руководству по работе с [расширениями публикации](../publish-extensions.md) .
> [!IMPORTANT]
> В nuspec-файле для этого расширения важно, ```<id>``` чтобы значение совпадало с именем в проекте ```manifest.json``` и совпадало с тем, ```<version>``` что было добавлено в ```\src\app\default.component.ts``` . Кроме того, добавьте запись в раздел ```<files>``` :
>
> ```<file src="Node\**\*.*" target="Node" />```.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="https://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
  <metadata>
    <id>contoso.install-on-node</id>
    <version>1.0.0</version>
    <authors>Contoso</authors>
    <owners>Contoso</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <projectUrl>https://msft-sme.myget.org/feed/windows-admin-center-feed/package/nuget/contoso.sme.install-on-node-extension</projectUrl>
    <licenseUrl>http://YourLicenseLink</licenseUrl>
    <iconUrl>http://YourLogoLink</iconUrl>
    <description>Install on node extension by Contoso</description>
    <copyright>(c) Contoso. All rights reserved.</copyright>
  </metadata>
    <files>
    <file src="bundle\**\*.*" target="ux" />
    <file src="package\**\*.*" target="gateway" />
    <file src="Node\**\*.*" target="Node" />
  </files>
</package>
```

После создания этого пакета добавьте путь к этому каналу. В центре администрирования Windows перейдите в раздел Параметры > расширения > каналы и добавьте путь к месту существования этого пакета. После установки расширения вы сможете нажать кнопку, ```install``` и API будет вызван.