---
title: Управление виртуальными машинами Windows с помощью PowerShell Direct
description: Содержит инструкции по использованию PowerShell Direct для управления виртуальными машинами без полагаться на сетевое или удаленное подключение к ним.
manager: dongill
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc09093ba2d
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 654767901607207ff1dea74201e1b7ede3c38ae0
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997472"
---
# <a name="manage-windows-virtual-machines-with-powershell-direct"></a>Управление виртуальными машинами Windows с помощью PowerShell Direct

>Область применения: Windows 10, Windows Server 2016, Windows Server 2019

PowerShell Direct можно использовать для удаленного управления виртуальной машиной Windows 10, Windows Server 2016 или Windows Server 2019 с узла Windows 10, Windows Server 2016 или Windows Server 2019 Hyper-V. PowerShell Direct позволяет управлять Windows PowerShell внутри виртуальной машины независимо от конфигурации сети или параметров удаленного управления на узле Hyper-V или виртуальной машине. Это позволяет администраторам Hyper-V автоматизировать управление и настройку виртуальных машин с помощью сценариев.

Запустить PowerShell Direct можно двумя способами:

- Создание и выход из прямого сеанса PowerShell с помощью командлетов PSSession

- Выполните сценарий или команду с помощью командлета Invoke-Command.

Если вы управляете виртуальными машинами более ранних версий, используйте средство "Подключение к виртуальной машине" (VMConnect) или [настройте для этой машины виртуальную сеть](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816585(v=ws.10)).

## <a name="create-and-exit-a-powershell-direct-session-using-pssession-cmdlets"></a>Создание и выход из прямого сеанса PowerShell с помощью командлетов PSSession

1. На узле Hyper-V откройте Windows PowerShell от имени администратора.

2. Используйте командлет [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession?view=powershell-7) для подключения к виртуальной машине. Чтобы создать сеанс с помощью имени или GUID виртуальной машины, выполните одну из следующих команд:

    ```
    Enter-PSSession -VMName <VMName>
    ```

    ```
    Enter-PSSession -VMGUID <VMGUID>
    ```

3. Введите свои учетные данные для виртуальной машины.
4. Выполните все необходимые команды. Эти команды выполняются на виртуальной машине, в которой был создан сеанс.

5.  Когда все будет готово, завершите сеанс с помощью команды [Exit-PSSession](/powershell/module/microsoft.powershell.core/exit-pssession?view=powershell-7) .

    ```
    Exit-PSSession
    ```

## <a name="run-script-or-command-with-invoke-command-cmdlet"></a>Выполнение скрипта или команды с помощью командлета Invoke-Command
Выполнить предварительно определенный набор команд на виртуальной машине можно с помощью командлета [Invoke-Command](/powershell/module/Microsoft.PowerShell.Core/Invoke-Command). Ниже приведен пример использования командлета Invoke-Command, где PSTest — это имя виртуальной машины, а сценарий, который требуется запустить,(foo.ps1) находится в папке сценария (script) на диске C:

```
Invoke-Command -VMName PSTest  -FilePath C:\script\foo.ps1
```

Чтобы выполнить одну команду, используйте параметр **-ScriptBlock**:

```
Invoke-Command -VMName PSTest  -ScriptBlock { cmdlet }
```

## <a name="whats-required-to-use-powershell-direct"></a>Что необходимо для использования PowerShell Direct?
Чтобы создать сеанс PowerShell Direct на виртуальной машине:

-   Виртуальная машина должна работать на узле локально и быть загружена.

-   Необходимо войти в учетную запись администратора Hyper-V на хост-компьютере.

-   Необходимо указать действительные учетные данные пользователя для виртуальной машины.

-   Операционная система узла должна работать под управлением Windows 10 или Windows Server 2016 или более поздней версии.

-   Виртуальная машина должна работать под управлением Windows 10 или Windows Server 2016 или более поздней.

С помощью командлета [Get-VM](/powershell/module/hyper-v/get-vm) можно проверить, что используемые учетные данные имеют роль администратора Hyper-V, и получить список виртуальных машин, запущенных локально на узле и загруженных.

## <a name="see-also"></a>См. также:
[Enter-PSSession](/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) 
 [Exit-PSSession](/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) 
 [Invoke-Command](/powershell/module/Microsoft.PowerShell.Core/Invoke-Command)