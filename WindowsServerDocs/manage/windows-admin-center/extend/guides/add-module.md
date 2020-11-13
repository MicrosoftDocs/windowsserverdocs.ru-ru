---
title: Добавление модуля в расширение средства
description: Разработка расширения инструмента Windows Admin Center SDK (Project Хонолулу). Добавление модуля в расширение средства
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 06331c23730cfdbf1752961f7867b0bebf45cacb
ms.sourcegitcommit: 01b3140f79f5614ce566e8036474feefafbeddc3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/13/2020
ms.locfileid: "94581418"
---
# <a name="add-a-module-to-a-tool-extension"></a>Добавление модуля в расширение средства

>Область применения. Windows Admin Center, ознакомительная версия Windows Admin Center

В этой статье мы добавим пустой модуль в расширение инструмента, созданное с помощью интерфейса командной строки центра администрирования Windows.

## <a name="prepare-your-environment"></a>Подготовка среды

Если вы еще этого не сделали, следуйте указаниям в [подсказке](../develop-tool.md) по разработке средства (или [решения](../develop-solution.md)) для подготовки среды и создания нового пустого расширения инструмента.

## <a name="use-the-angular-cli-to-create-a-module-and-component"></a>Использование угловой панели CLI для создания модуля (и компонента)

Если вы не знакомы с Angular, настоятельно рекомендуется прочитать документацию на веб-сайте Angular.Io, чтобы ознакомиться с Angular и NgModule. Дополнительные сведения о NgModule см. здесь: https://angular.io/guide/ngmodule

* Дополнительные сведения о создании нового модуля в Angular CLI: https://github.com/angular/angular-cli/wiki/generate-module
* Дополнительные сведения о создании нового компонента в Angular CLI: https://github.com/angular/angular-cli/wiki/generate-component


Откройте командную строку, измените каталог на .\срк\апп в проекте, а затем выполните следующие команды, заменив ```{!ModuleName}``` именем модуля (пробелы удалены):

```
cd .\src\app
ng generate module {!ModuleName}
ng generate component {!ModuleName}
```

| Значение | Объяснение | Пример |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | Имя модуля (пробелы удалены) | ```ManageFooWorksPortal``` |

Пример использования:
```
cd .\src\app
ng generate module ManageFooWorksPortal
ng generate component ManageFooWorksPortal
```


## <a name="add-routing-information"></a>Добавление сведений о маршрутизации

Если вы не знакомы с Angular, настоятельно рекомендуется ознакомиться с маршрутизацией и навигацией в Angular. В следующих разделах рассматриваются необходимые элементы маршрутизации, которые позволяют Windows Admin Center переходить к вашему расширению и между представлениями в вашем расширении в ответ на действия пользователя. Подробнее см. здесь: https://angular.io/guide/router

Используйте то же имя модуля, которое использовалось на предыдущем шаге.

### <a name="add-content-to-new-routing-file"></a>Добавление содержимого в новый файл маршрутизации

* Перейдите к папке модуля, созданной с помощью ``` ng generate ``` на предыдущем шаге.

* Создайте новый файл ```{!module-name}.routing.ts```, следуя этому соглашению об именовании:

    | Значение | Объяснение | Пример имени файла |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | Имя модуля (нижний регистр, пробелы заменены на тире) | ```manage-foo-works-portal.routing.ts``` |

* Добавьте это содержимое в только что созданный файл:

    ``` ts
    import { NgModule } from '@angular/core';
    import { RouterModule, Routes } from '@angular/router';
    import { {!ModuleName}Component } from './{!module-name}.component';

    const routes: Routes = [
        {
            path: '',
            component: {!ModuleName}Component,
            // if the component has child components that need to be routed to, include them in the children array.
            children: [
                {
                    path: '',
                    redirectTo: 'base',
                    pathMatch: 'full'
                }
            ]
    }];

    @NgModule({
        imports: [
            RouterModule.forChild(routes)
        ],
        exports: [
            RouterModule
        ]
    })
    export class Routing { }
    ```

* Замените значения в только что созданном файле необходимыми значениями:

    | Значение | Объяснение | Пример |
    | ----- | ----------- | ------- |
    | ```{!ModuleName}``` | Имя модуля (пробелы удалены) | ```ManageFooWorksPortal``` |
    | ```{!module-name}``` | Имя модуля (нижний регистр, пробелы заменены на тире) | ```manage-foo-works-portal``` |

### <a name="add-content-to-new-module-file"></a>Добавление содержимого в новый файл модуля

Откройте файл ```{!module-name}.module.ts```, соответствующий этому соглашению об именовании:

| Значение | Объяснение | Пример имени файла |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Имя модуля (нижний регистр, пробелы заменены на тире) | ```manage-foo-works-portal.module.ts``` |

* Добавьте содержимое в файл:

    ``` ts
    import { Routing } from './{!module-name}.routing';
    ```

* Замените значения в только что созданном содержимом необходимыми значениями:

    | Значение | Объяснение | Пример |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | Имя модуля (нижний регистр, пробелы заменены на тире) | ```manage-foo-works-portal``` |

* Измените оператор imports, чтобы выполнить импорт маршрутизации:

    | Исходное значение | Новое значение |
    | -------------- | --------- |
    | ```imports: [ CommonModule ]``` | ```imports: [ CommonModule, Routing ]``` |

* Убедитесь, что операторы ```import``` упорядочены в алфавитном порядке по источнику.

### <a name="add-content-to-new-component-typescript-file"></a>Добавить содержимое в файл typescript нового компонента

Откройте файл ```{!module-name}.component.ts```, соответствующий этому соглашению об именовании:

| Значение | Объяснение | Пример имени файла |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Имя модуля (нижний регистр, пробелы заменены на тире) | ```manage-foo-works-portal.component.ts``` |

Измените содержимое в файле на следующее:

``` ts
constructor() {
    // TODO
}

public ngOnInit() {
    // TODO
}
```
### <a name="update-app-routingmodulets"></a>Обновление App-Routing. Module. TS

Откройте файл ```app-routing.module.ts``` и измените путь по умолчанию, чтобы загрузить только что созданный модуль.  Найдите запись для ```path: ''``` и обновите,  ```loadChildren``` чтобы загрузить модуль вместо модуля по умолчанию:

| Значение | Объяснение | Пример |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | Имя модуля (пробелы удалены) | ```ManageFooWorksPortal``` |
| ```{!module-name}``` | Имя модуля (нижний регистр, пробелы заменены на тире) | ```manage-foo-works-portal``` |

``` ts
    {
        path: '',
        loadChildren: 'app/{!module-name}/{!module-name}.module#{!ModuleName}Module'
    },
```
Ниже приведен пример обновленного пути по умолчанию.
``` ts
    {
        path: '',
        loadChildren: 'app/manage-foo-works-portal/manage-foo-works-portal.module#ManageFooWorksPortalModule'
    },
```


## <a name="build-and-side-load-your-extension"></a>Сборка и загрузка на стороне вашего расширения

Теперь вы добавили модуль в расширение.  Затем вы можете [создать и загрузить](../develop-tool.md#build-and-side-load-your-extension) свои расширения в центре администрирования Windows, чтобы увидеть результаты.
