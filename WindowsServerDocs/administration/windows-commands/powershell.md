---
title: PowerShell
description: Справочная статья по команде PowerShell, которая открывает консоль PowerShell из командной строки.
ms.topic: reference
ms.assetid: 694fc970-0b6c-4046-b1b5-7eb1a0d26609
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 2b84685653f39e83e0d21b974b1d85fed32666d3
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101808429"
---
# <a name="powershell"></a>PowerShell

Windows PowerShell — это оболочка командной строки на основе задач и язык сценариев, разработанный специально для администрирования системы. Созданная на основе .NET Framework служба Windows PowerShell помогает ИТ-специалистам и опытным пользователям в управлении и автоматизации администрирования операционной системы Windows, а также приложений, работающих под управлением Windows.

## <a name="using-powershellexe"></a>Использование PowerShell.exe

Программа командной строки **PowerShell.exe** запускает сеанс Windows PowerShell в окне командной строки. При использовании **PowerShell.exe** можно использовать его необязательные параметры для настройки сеанса. Например, можно запустить сеанс, в котором используется конкретная политика выполнения или одна из которых исключает профиль Windows PowerShell. В противном случае сеанс будет таким же, как и любой сеанс, запущенный в консоли Windows PowerShell.

- Чтобы запустить сеанс Windows PowerShell в окне командной строки, введите команду `PowerShell` . В командную строку добавляется префикс **PS** , указывающий, что вы используете сеанс Windows PowerShell.

- Чтобы запустить сеанс с определенной политикой выполнения, используйте параметр **ExecutionPolicy** и введите:

    ```powershell
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Чтобы запустить сеанс Windows PowerShell без профилей Windows PowerShell, используйте параметр- **Profile** и введите:

    ```powershell
    PowerShell.exe -NoProfile
    ```

- Чтобы начать сеанс, используйте параметр **ExecutionPolicy** и введите:

    ```powershell
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Чтобы просмотреть файл справки PowerShell.exe, введите:

    ```powershell
    PowerShell.exe -help
    PowerShell.exe -?
    PowerShell.exe /?
    ```

- Чтобы завершить сеанс Windows PowerShell в окне командной строки, введите команду `exit` . Типичная Командная строка возвращает.

### <a name="remarks"></a>Комментарии

- Полный список параметров командной строки **PowerShell.exe** см. в разделе [about_PowerShell.Exe](/powershell/module/microsoft.powershell.core/about/about_powershell_exe).

- Дополнительные сведения о других способах запуска Windows PowerShell см. в разделе [Запуск Windows PowerShell](/powershell/scripting/windows-powershell/starting-windows-powershell).

- Windows PowerShell выполняется в варианте установки Server Core в операционных системах Windows Server. Тем не менее функции, требующие графического пользовательского интерфейса, такие как [Интегрированная среда сценариев Windows PowerShell (ISE)](/previous-versions/hh849182(v=technet.10)), и командлеты [Out-GridView](/powershell/module/microsoft.powershell.utility/out-gridview) и for [-Command](/powershell/module/microsoft.powershell.utility/show-command) , не выполняются в установках Server Core.

## <a name="additional-references"></a>Дополнительные ссылки

- [about_PowerShell.Exe](/powershell/module/microsoft.powershell.core/about/about_powershell_exe)

- [about_PowerShell_Ise.exe](/powershell/module/microsoft.powershell.core/about/about_powershell_ise_exe)

- [Windows PowerShell](/powershell/)
