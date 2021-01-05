---
title: Переход с Windows Server Essentials на Windows Server 2012 R2 Standard
description: Узнайте, как перейти с Windows Server Essentials на Windows Server 2012 R2 Standard.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: a14689e3-2310-4229-bd3e-dafc0e739e02
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 4838101de3ed9daa1150e208d7aa0a938c95041e
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810351"
---
# <a name="transition-from-windows-server-essentials-to-windows-server-2012-r2-standard"></a>Переход с Windows Server Essentials на Windows Server 2012 R2 Standard

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server 2016 — это готовая к использованию в облаке операционная система, которая поддерживает текущие рабочие нагрузки и предоставляет новые технологии, упрощающие переход к облачным вычислениям. Содержимое Windows Server 2016 поможет вам приступить к работе.

 Windows Server Essentials поддерживает до 25 пользователей и устройств 50. Если потребности вашего бизнеса превышают ограничение, можно выполнить переход на промежуточную лицензию с Windows Server Essentials на Windows Server 2012 R2 Standard, чтобы остаться в соответствии с лицензиями.

 После перехода на Windows Server 2012 R2 Standard ограничения учетной записи пользователя и устройств удаляются, но функции, которые являются уникальными для Windows Server Essentials (такие как панель мониторинга, удаленный Веб-доступ и резервная копия клиентских компьютеров), по-прежнему остаются доступными. Из-за ограничений технического характера данные компоненты поддерживают не более 100 учетных записей и 200 устройств. Компонент архивации данных клиентского компьютера будет поддерживать резервное копирование данных с клиентских компьютеров количеством не более 75.

> [!IMPORTANT]
>   Для Windows Server 2012 R2 Standard требуется клиентская лицензия (CAL) для каждого пользователя или устройства в вашей среде. Это отличается от Windows Server Essentials, который не использует модель CAL и не поставляется с клиентскими лицензиями. При переходе с Windows Server Essentials на Windows Server 2012 R2 Standard необходимо приобрести соответствующее число и тип клиентских лицензий для вашей среды (большинство клиентов приобрели клиентские лицензии пользователя).

## <a name="before-the-transition"></a>Перед переходом

-   Перед переходом с Windows Server Essentials на Windows Server 2012 R2 Standard необходимо полностью создать резервную копию данных сервера.

    > [!IMPORTANT]
    >  Без полной резервной копии сервера будет невозможно восстановить состояние сервера до перехода.

-   Кроме того, убедитесь, что вы прочитали и понимаете лицензионное соглашение (EULA) для Windows Server 2012 R2 Standard. Чтобы просмотреть лицензионное соглашение, выполните следующие действия.

    1.  Откройте окно командной строки от имени администратора.

    2.  Выполните следующую команду:

        ```console
        dism /online /set-edition:ServerStandard /geteula: <eula path>
        ```

        Где *путь лицензионного соглашения* представляет расположение, в которое необходимо сохранить файл лицензионного соглашения; Пример: C:\ ws8std_eula. RTF). Обязательно укажите в качестве расширения имени файла ".rtf".

    3.  Откройте папку, в которой сохранен файл, и дважды щелкните его, чтобы открыть.

## <a name="transition-to--windows-server-2012-r2-standard"></a>Переход на Windows Server 2012 R2 Standard
 После того как вы решили перейти с Windows Server Essentials на Windows Server 2012 R2 Standard, выполните следующие два действия.

1. Приобретите лицензию для Windows Server 2012 R2 Standard и соответствующее число лицензий пользователей и/или клиентов устройств для вашей среды.

    Лицензию на Windows Server 2012 R2 Standard можно приобрести в розничной розетке, на распространителе или с помощью [партнера Майкрософт](https://pinpoint.microsoft.com/SelectCulture.aspx).

   > [!NOTE]
   >  Если изначально вы приобрели Windows Server 2012 R2 Standard и преддали вам права на переход на более раннюю версию для установки одного из двух виртуальных экземпляров в качестве Windows Server Essentials, вам не нужно приобретать никаких дополнительных.
   >
   >  Если вы приобрели Windows Server 2012 R2 Standard через канал корпоративного лицензирования, вы можете скачать ISO-образ и ключ продукта для Windows Server 2012 R2 Standard из центра поддержки корпоративных лицензий (VLSC).
   >
   >  Если вы приобрели Windows Server 2012 R2 Standard из любого другого канала, вы можете скачать ISO-образ и ознакомительный ключ продукта для Windows Server Essentials из [центра оценки TechNet](https://technet.microsoft.com/evalcenter/jj659306.aspx). Далее описано, как выполнить переход, чтобы преобразовать пробную версию продукта в полную лицензионную версию, обеспечиваемую поддержкой.

2. Откройте Windows PowerShell с правами администратора и выполните следующую команду:

    ```console
    dism /online /set-edition:ServerStandard /accepteula /productkey: <Product Key>
    ```

    Где *ключ продукта* — это ключ продукта для вашей копии Windows Server 2012 R2 Standard).

    Для завершения перехода сервер перезагрузится.

   После перехода компоненты Windows Server Essentials остаются на сервере и поддерживаются до 100 пользователей и 200 устройств.

## <a name="additional-references"></a>Дополнительные ссылки


-   [Перенос данных сервера в Windows Server Essentials](Migrate-Server-Data-to-Windows-Server-Essentials.md)

