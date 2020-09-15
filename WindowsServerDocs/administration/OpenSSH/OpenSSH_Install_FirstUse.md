---
title: Установка OpenSSH для Windows Server
description: Установка клиента OpenSSH и сервера для Windows Server с помощью параметров Windows или Windows PowerShell.
ms.date: 09/27/2019
ms.topic: conceptual
ms.author: damaerte
author: maertendmsft
ms.openlocfilehash: 2496ee056dec9fc5b39578d889d8279574e76ba5
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078411"
---
# <a name="installation-of-openssh-for-windows-server-2019-and-windows-10"></a>Установка OpenSSH для Windows Server 2019 и Windows 10

Клиент OpenSSH и сервер OpenSSH являются отдельными устанавливаемыми компонентами в Windows Server 2019 и Windows 10 1809.
Пользователи с этими версиями Windows могут установить и настроить OpenSSH, используя приведенные ниже инструкции.

> [!NOTE]
> Пользователи, которые получили OpenSSH из репозитория PowerShell на сайте GitHub (https://github.com/PowerShell/OpenSSH-Portable) должны использовать инструкции из репозитория, а __не эти инструкции__.

## <a name="installing-openssh-from-the-settings-ui-on-windows-server-2019-or-windows-10-1809"></a>Установка OpenSSH через пользовательский интерфейс настройки в Windows Server 2019 или Windows 10 версии 1809

Клиент и сервер OpenSSH устанавливаются в Windows 10 версии 1809 как отдельные компоненты.

Чтобы установить OpenSSH, откройте раздел **Параметры** и последовательно выберите **Приложения** > **Приложения и возможности** > **Управление дополнительными компонентами**.

Просмотрите этот список и выясните, установлен ли клиент OpenSSH. Если нет, то выберите пункт **Добавить компонент** в верхней части страницы, а затем:

* чтобы установить клиент OpenSSH, найдите элемент **Клиент OpenSSH** и щелкните **Установить**;
* чтобы установить сервер OpenSSH, найдите элемент **Сервер OpenSSH** и щелкните **Установить**.

После завершения установки вернитесь в раздел **Приложения** > **Приложения и возможности** > **Управление дополнительными компонентами**, где теперь должны появиться компоненты OpenSSH.

> [!NOTE]
> Установка сервера OpenSSH создаст и включит правило брандмауэра с именем OpenSSH-Server-in-TCP. Правило разрешает входящий трафик SSH через порт 22.

## <a name="installing-openssh-with-powershell"></a>Установка OpenSSH с помощью PowerShell

Чтобы установить OpenSSH с помощью PowerShell, запустите PowerShell от имени администратора.
Убедитесь, что функции OpenSSH доступны для установки, выполнив следующие действия.

```powershell
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

# This should return the following output:

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent
```

Затем установите компонент сервера и (или) клиента.

```powershell
# Install the OpenSSH Client
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

# Both of these should return the following output:

Path          :
Online        : True
RestartNeeded : False
```

## <a name="uninstalling-openssh"></a>Удаление OpenSSH

Чтобы удалить OpenSSH через раздел **Параметры** в ОС Windows, откройте этот раздел и последовательно выберите **Приложения** > **Приложения и возможности** > **Управление дополнительными компонентами**.
В списке установленных компонентов выберите компонент **Клиент OpenSSH** или **Сервер OpenSSH** и щелкните **Удалить**.

Чтобы удалить OpenSSH с помощью PowerShell, выполните одну из следующих команд:

```powershell
# Uninstall the OpenSSH Client
Remove-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Uninstall the OpenSSH Server
Remove-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

После удаления OpenSSH может потребоваться перезагрузка Windows, если служба использовалась в момент удаления.


## <a name="initial-configuration-of-ssh-server"></a>Начальная настройка сервера SSH

Чтобы настроить только что установленный сервер OpenSSH для использования в ОС Windows, запустите PowerShell от имени администратора и выполните следующие команды, чтобы запустить службу SSHD:

```powershell
Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup.
Get-NetFirewallRule -Name *ssh*
# There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled
# If the firewall does not exist, create one
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
```

## <a name="initial-use-of-ssh"></a>Начальное использование SSH

После установки сервера OpenSSH в Windows вы можете быстро проверить его работу с помощью PowerShell на любом устройстве Windows, где установлен клиент SSH.
В PowerShell запустите следующую команду:

```powershell
Ssh username@servername
```

Первое подключение к любому серверу сопровождается сообщением примерно такого содержания:

```
The authenticity of host 'servername (10.00.00.001)' can't be established.
ECDSA key fingerprint is SHA256:(<a large string>).
Are you sure you want to continue connecting (yes/no)?
```

В качестве ответа принимаются значения yes (да) или no (нет).
Ответ "Да" приведет к добавлению этого сервера в список известных узлов SSH в локальной системе.

После этого появится запрос на ввод пароля. В целях безопасности пароль не будет отображаться по мере ввода.

После успешного подключения вы увидите командную оболочку, которая выглядит примерно так:

```
domain\username@SERVERNAME C:\Users\username>
```

По умолчанию для сервера OpenSSH в ОС Windows используется командная оболочка Windows.

