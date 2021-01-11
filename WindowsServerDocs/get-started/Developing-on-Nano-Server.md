---
title: Разработка на базе сервера Nano Server
description: Удаленное взаимодействие и сеансы CIM в PowerShell
manager: DonGill
ms.date: 09/06/2017
ms.topic: how-to
ms.assetid: 57079470-a1c1-4fdc-af15-1950d3381860
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: b2f192f45a624c3c6ad26b80a075911abeddfb53
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947580"
---
# <a name="developing-for-nano-server"></a>Разработка на базе сервера Nano Server

>Область применения. Windows Server 2016

> [!IMPORTANT]
> Начиная с Windows Server версии 1709, сервер Nano Server будет доступен только в качестве [базового образа ОС контейнера](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image). Его описание см. в статье об [изменениях сервера Nano Server](nano-in-semi-annual-channel.md).

В этих разделах поясняются важные отличия PowerShell на сервере Nano Server, а также даются рекомендации по разработке собственных командлетов PowerShell для использования на сервере Nano.

- [PowerShell на сервере Nano Server](PowerShell-on-Nano-Server.md)
- [Разработка командлетов PowerShell для сервера Nano Server](Developing-PowerShell-Cmdlets-for-Nano-Server.md)

## <a name="using-windows-powershell-remoting"></a>Использование удаленного взаимодействия Windows PowerShell
Для управления сервером Nano Server с помощью удаленного взаимодействия Windows PowerShell вам следует добавить IP-адрес сервера Nano Server в список доверенных узлов на компьютере управления, добавить учетную запись, которую вы используете, в группу администраторов сервера Nano Server и включить CredSSP, если вы планируете использовать эту функцию.

> [!NOTE]
> Если целевой сервер Nano Server и ваш компьютер управления находятся в одном лесу доменных служб Active Directory (или в лесах с отношением доверия), не следует добавлять сервер Nano Server в список доверенных узлов, так как вы можете подключиться к серверу, используя его полное доменное имя, например: PS C:\> Enter-PSSession -ComputerName nanoserver.contoso.com -Credential (Get-Credential)


Чтобы добавить сервер Nano Server в список доверенных узлов, выполните следующую команду в командной строке Windows PowerShell с повышенными привилегиями:

`Set-Item WSMan:\localhost\Client\TrustedHosts <IP address of Nano Server>`

Чтобы запустить удаленный сеанс Windows PowerShell, запустите локальный сеанс Windows PowerShell с повышенными привилегиями и выполните следующие команды:


```
$ip = \<IP address of Nano Server>
$user = $ip\Administrator
Enter-PSSession -ComputerName $ip -Credential $user
```


Теперь вы можете выполнять команды Windows PowerShell на сервере Nano Server в обычном режиме.

> [!NOTE]
> В этом выпуске сервера Nano Server доступны не все команды Windows PowerShell. Чтобы просмотреть доступные команды, выполните команду `Get-Command -CommandType Cmdlet`.

Чтобы остановить удаленный сеанс, выполните команду `Exit-PSSession`.

## <a name="using-windows-powershell-cim-sessions-over-winrm"></a>Использование сеансов Windows PowerShell CIM через WinRM
Сеансы и экземпляры CIM можно использовать в Windows PowerShell для выполнения команд WMI через службу удаленного управления Windows (WinRM).

Запустите сеанс CIM, выполнив следующие команды в командной строке Windows PowerShell:


```
$ip = <IP address of the Nano Server\>
$ip\Administrator
$cim = New-CimSession -Credential $user -ComputerName $ip
```


В рамках запущенного сеанса можно выполнять различные команды WMI, например:


```
Get-CimInstance -CimSession $cim -ClassName Win32_ComputerSystem | Format-List *
Get-CimInstance -CimSession $Cim -Query SELECT * from Win32_Process WHERE name LIKE 'p%'
```

