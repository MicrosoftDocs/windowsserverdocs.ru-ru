---
title: Замена URL-адресов конечных точек при покупке или ознакомлении для модуля интеграции Microsoft 365 в рамках поддержки по соглашению с торговым посредником интернет-служб Майкрософт
description: Узнайте, как заменить URL-адреса конечных точек, используемые модулем интеграции Windows Server Essentials Microsoft 365.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 9860a6b9-baea-4bf0-9a9f-6f1a288f996e
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 4d01b7dbea4566bae962c73220c389c3a4e2c19a
ms.sourcegitcommit: e00e789dff216dbade861e61365f078b758a5720
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2020
ms.locfileid: "97755370"
---
# <a name="replace-microsoft-365-integration-module-buy-try-endpoint-url-in-support-of-microsoft-online-service-reseller-agreement"></a>Замена URL-адресов конечных точек при покупке или ознакомлении для модуля интеграции Microsoft 365 в рамках поддержки по соглашению с торговым посредником интернет-служб Майкрософт

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_O365"></a>
 Если вы являетесь партнером по соглашению торгового посредника Microsoft Online Service (МОСРА), чтобы обеспечить обработку транзакций регистрации клиентов через портал, необходимо заменить URL-адреса конечных точек, используемые модулем интеграции Windows Server Essentials Microsoft 365.

 Модуль интеграции использует следующие четыре URL-адреса конечных точек.

1.  Конечная точка приобретения подписки Microsoft 365 корпоративный.

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\

    -   Тип = REG-SZ

    -   Имя раздела = MOSRASTDBUY

    -   Значение = *xxxxx*, где xxxxx - URL-адрес покупки подписки Enterprise. Например, значение = http://syndicatepartner.office365.com/enterprisebuy.html

2.  Конечная точка пробной версии подписки Microsoft 365 корпоративный.

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\

    -   Тип = REG-SZ

    -   Имя раздела = MOSRASTDTRY

    -   Значение = *xxxxx*, где xxxxx - URL-адрес покупки подписки Enterprise. Например, значение = http://syndicatepartner.office365.com/enterprisetry.html

3.  Конечная точка приобретения подписки на Microsoft 365 малого бизнеса Premium.

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\

    -   Тип = REG-SZ

    -   Имя раздела = MOSRALITEBUY

    -   Значение = *xxxxx*, где xxxxx - URL-адрес покупки подписки Enterprise. Например, значение = http://syndicatepartner.office365.com/smallbizbuy.html

4.  Конечная точка пробной версии подписки Small Business Premium Microsoft 365.

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\

    -   Тип = REG-SZ

    -   Имя раздела = MOSRALITETRY

    -   Значение = *xxxxx*, где xxxxx - URL-адрес покупки подписки Enterprise. Например, значение = http://syndicatepartner.office365.com/smallbiztry.html

#### <a name="to-add-an-endpoint-url-key-to-the-registry"></a>Добавление раздела реестра со значением URL-адреса конечной точки

1.  На компьютере-образце нажмите кнопку **Пуск**, введите команду **regedit** и нажмите клавишу ВВОД.

2.  В левой области разверните разделы **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server** и **MSO**.

3.  Если раздел MSO не существует, щелкните правой кнопкой мыши **Windows Server**, выберите пункт **Создать**, щелкните **Раздел**, а затем введите **MSO** в качестве имени раздела.

4.  Щелкните правой кнопкой мыши раздел MSO и выберите пункт **Строковый параметр**. Введите одно из приведенных ниже имен конечной точки в качестве имени строки.

    -   MOSRASTDBUY

    -   MOSRASTDTRY

    -   MOSRALITEBUY

    -   MOSRALITETRY

5.  Щелкните правой кнопкой мыши новую строку в правой области и выберите команду **Изменить**.

6.  Введите URL-адрес конечной точки в текстовое поле **Значение** и нажмите кнопку **OK**.

7.  Повторите шаги 4-6 для каждого имени строки из указанных в шаге 4.

## <a name="see-also"></a>См. также:

 [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)

