---
title: Добавление категорий верхнего уровня в панель запуска (операционная система Macintosh)
description: Узнайте, как добавлять категории верхнего уровня на панель запуска на компьютере, работающем под управлением операционной системы Macintosh.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: ee2173c3-e464-4001-9f43-6d926a575092
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 09cbae3e6643e9ebd729c06646647b361374c787
ms.sourcegitcommit: d2224cf55c5d4a653c18908da4becf94fb01819e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2020
ms.locfileid: "97711629"
---
# <a name="add-top-level-categories-to-the-launchpad-macintosh-operating-system"></a>Добавление категорий верхнего уровня в панель запуска (операционная система Macintosh)

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

На компьютерах под управлением операционной системы Macintosh можно добавить в панель запуска категории верхнего уровня. Чтобы создать надстройку панели запуска, которая добавляет категории верхнего уровня, можно использовать сочетание информации с этой страницы и из раздела «инструкции. Добавление задач и категорий» на панель запуска. в [пакете SDK для Windows Server Solutions](https://go.microsoft.com/fwlink/?LinkID=248648).

 В следующем примере показано, каким образом можно назначить запись панели запуска категорией верхнего уровня в LAUNCHPAD-файле.

```

<?xml version="1.0" encoding="utf-8" ?>
<LaunchPad resFile="Localizable">
   <Category id="Microsoft.Launchpad.HomeCategory" name="SampleAddin"  image="SampleImage01.png">
      <Task id="Microsoft.Launchpad.SampleAddin.Pictures"
          name="Pictures"
           src="smb://%ServerAddress%/Pictures"
         image="SampleImage02.png"/>
   </Category>
</LaunchPad>
```

 Для назначения записи категорией верхнего уровня для атрибута Id элемента Category необходимо назначить значение «Microsoft.Launchpad.HomeCategory».

## <a name="see-also"></a>См. также:
 [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)