---
title: Добавление информации о зарегистрированном партнере, заключившем партнерское соглашение об использовании интернет-служб Майкрософт
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 9bd191d6-ecc5-4230-a88e-f3fc281cb956
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c1d6d9b056c4ccc5b6961023e1f0c22034321960
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181580"
---
# <a name="add-microsoft-online-service-partner-agreement-partner-of-record-information"></a>Добавление информации о зарегистрированном партнере, заключившем партнерское соглашение об использовании интернет-служб Майкрософт

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_3rdLevelDomanNames"></a>
 Если вы являетесь партнером Microsoft Online Service Partner Agreement (МОСПА) для Office 365, чтобы обеспечить правильную компенсацию при порождении запроса на подписку из Windows Server Essentials с помощью модуля интеграции Office 365, необходимо создать раздел реестра, содержащий идентификатор партнера-записи (пор ID). Указанная ниже информация считывается и передается поставщику услуг через URL-адреса регистрации Office 365.

-   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO

-   Тип = строковый параметр

-   Имя раздела = Partner

-   Значение = xxxxx, где xxxxx - POR ID партнера

#### <a name="to-add-the-por-id-key-to-the-registry"></a>Добавление раздела POR ID в реестр

1.  На компьютере-образце нажмите кнопку **Пуск**, введите команду **regedit** и нажмите клавишу ВВОД.

2.  В левой области последовательно разверните узлы **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft** и **Windows Server**.

3.  Щелкните правой кнопкой мыши узел **Windows Server**, выберите команду **Создать** и щелкните пункт **Раздел**.

4.  В качестве имени раздела введите **MSO**.

5.  Щелкните правой кнопкой мыши созданный раздел и выберите пункт **Строковый параметр**.

6.  В качестве имени строки введите **Partner** и нажмите клавишу ВВОД.

7.  Щелкните правой кнопкой мыши строку **Partner** в правой области и выберите команду **Изменить**.

8.  Введите идентификатор POR ID в текстовое поле **Значение** и нажмите кнопку **ОК**.

## <a name="see-also"></a>См. также:

 [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)

