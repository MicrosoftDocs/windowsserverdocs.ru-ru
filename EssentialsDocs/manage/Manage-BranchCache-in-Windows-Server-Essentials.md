---
title: Управление BranchCache в Windows Server Essentials
description: Узнайте о службе BranchCache и о том, как она может помочь оптимизировать использование Интернета, повысить производительность сетевых приложений и снизить объем трафика в глобальной сети.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: f6e05aec-d07c-4e0b-94ab-f20279e9ffd1
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: efa4abc7da2c0949444ffa87514500561c9840ba
ms.sourcegitcommit: e00e789dff216dbade861e61365f078b758a5720
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2020
ms.locfileid: "97755280"
---
# <a name="manage-branchcache-in-windows-server-essentials"></a>Управление BranchCache в Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

BranchCache помогает оптимизировать использование Интернета, повысить производительность сетевых приложений и снизить объем трафика в глобальной сети (WAN), когда сервер Windows Server Essentials находится удаленно из офиса или если клиентские компьютеры, подключенные к локальному серверу, используют облачные ресурсы, такие как библиотеки SharePoint Online.

 Если служба BranchCache включена, то когда клиентский компьютер запрашивает содержимое с удаленного сервера Windows Server Essentials, содержимое кэшируется в локальном офисе. После этого остальные компьютеры в этом офисе могут получать данные локально, а не загружать их с сервера по глобальной сети. Это может увеличить производительность сетевых приложений и снизить нагрузку на глобальную сеть.

 Независимо от того, является ли сервер Windows Server Essentials локальным или удаленным, BranchCache может увеличить время отклика для общих папок сервера и веб-содержимого, размещенного на сервере (например, в библиотеках SharePoint Online).

 Поскольку для развертывания BranchCache не нужно дополнительное оборудование или изменение топологии сети, эта служба представляет собой простое решение для оптимизации использования пропускной способности и сокращения времени отклика служб и приложений, доступ к которым осуществляется по глобальной сети.

## <a name="branchcache-scenarios"></a>Сценарии использования BranchCache
 Существует три основных сценария использования BranchCache с удаленным сервером.

-   Сервер Windows Server Essentials размещается в Microsoft Azure.

-   Сервер Windows Server Essentials размещается в центре обработки данных стороннего поставщика услуг.

-   Сервер Windows Server Essentials находится в другом офисе в другом физическом расположении.

## <a name="distributed-cache-mode"></a>Режим распределенного кэша
 В Windows Server Essentials функция BranchCache реализована в *режиме распределенного кэша*— один из двух режимов кэширования, доступных в BranchCache. В режиме распределенного кэша кэш содержимого в филиале распределяется между клиентскими компьютерами. Поскольку в этом случае дополнительное оборудование и изменение топологии не требуются, этот режим больше подходит для небольших офисов, где для доступа к облачным службам, таким как SharePoint Online, используется удаленный сервер или локальный сервер. При включении BranchCache в Windows Server Essentials реализуется режим распределенного кэша.

> [!NOTE]
>  В крупных филиалах с несколькими подсетями или большим количеством сотрудников, работающих с сетевыми приложениями, может быть целесообразно реализовать BranchCache в *режиме размещенного кэша*. В режиме размещенного кэша кэш содержимого размещается в филиале на одном или нескольких серверах размещенного кэша.

## <a name="requirements"></a>Требования
 Чтобы использовать BranchCache в Windows Server Essentials, сервер и клиентские компьютеры должны соответствовать следующим требованиям.

-   Сервер должен работать под управлением операционной системы Windows Server Essentials или Windows Server 2012 R2 Standard или Windows Server 2012 R2 Datacenter с ролью Windows Server Essentials.

     На сервере Windows Server 2012 R2 Standard или Windows Server 2012 R2 Datacenter Server служба BranchCache добавляется при добавлении роли Windows Server Essentials Experience. Чтобы включить BranchCache, необходимо войти на панель мониторинга Windows Server Essentials с учетными данными администратора домена.

-   Клиентские компьютеры должны работать под управлением операционной системы Windows 7 Корпоративная, Windows 7 Максимальная, Windows 8 Корпоративная или Windows 8.1 Enterprise.

-   В режиме распределенного кэша все клиентские компьютеры должны находиться в одной подсети.

    > [!NOTE]
    >  Если клиентские компьютеры подключены к серверу Windows Server Essentials без присоединения к домену, они исключаются из кэширования по умолчанию. Чтобы включить в кэширование клиентский компьютер, который не присоединен к домену, выполните командлет [Enable-BCDistributed](https://technet.microsoft.com/library/hh848398.aspx) Windows PowerShell на этом компьютере. Дополнительные сведения см. в разделе [Командлеты BranchCache в Windows PowerShell](https://technet.microsoft.com/library/hh848392.aspx).


## <a name="turn-branchcache-on"></a>Включение BranchCache
 Чтобы включить BranchCache в режиме распределенного кэша, просто нажмите кнопку на панели мониторинга Windows Server Essentials. Кэширование начинается немедленно и процесс полностью прозрачен.

#### <a name="to-turn-on-branchcache-in-windows-server-essentials"></a>Включение BranchCache в Windows Server Essentials

1.  Войдите на сервер Windows Server Essentials с помощью учетной записи администратора.

2.  На панели мониторинга Windows Server Essentials щелкните **Параметры**.

     Откроется мастер настройки параметров.

3.  Щелкните **BranchCache**.

4.  На странице **Параметры BranchCache** нажмите кнопку **Включить**.

## <a name="use-windows-powershell-to-turn-branchcache-on-or-off"></a>Включение и отключение BranchCache с помощью Windows PowerShell
 С помощью Windows PowerShell можно проверять состояние BranchCache (включено или отключено) и включать или отключать BranchCache.

#### <a name="to-turn-branchcache-on-or-off-using-windows-powershell"></a>Включение и отключение BranchCache с помощью Windows PowerShell

1.  На сервере откройте Windows PowerShell от имени администратора. На **начальной** странице щелкните правой кнопкой мыши **Windows PowerShell**, а затем выберите **Запуск от имени администратора** и нажмите кнопку **Да**.

2.  В командной строке введите один из следующих командлетов.

    -   Чтобы проверить состояние BranchCache (служба включена или отключена), введите:

        ```powershell
        Get-WSSBranchCacheStatus
        ```

    -   Чтобы включить BranchCache, введите:

        ```powershell
        Enable-WSSBranchCache
        ```

    -   Чтобы отключить BranchCache, введите:

        ```powershell
        Disable-WSSBranchCache
        ```

## <a name="additional-references"></a>Дополнительные ссылки

-   [Обзор BranchCache](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831696(v=ws.11))

-   [Управление Windows Server Essentials](Manage-Windows-Server-Essentials.md)