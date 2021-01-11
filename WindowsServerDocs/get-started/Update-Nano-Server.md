---
title: Обновление сервера Nano Server
description: 'Сведения по таким темам: Обновление сервера Nano Server'
manager: DonGill
ms.date: 09/06/2017
ms.topic: how-to
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: ad230f6c160b117444c7a82dff17b341c59f7a51
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97947140"
---
# <a name="updating-nano-server"></a>Обновление сервера Nano Server

> [!IMPORTANT]
> Начиная с Windows Server версии 1709, сервер Nano Server будет доступен только в качестве [базового образа ОС контейнера](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image). Ознакомьтесь с разделом [Изменения сервера Nano Server](nano-in-semi-annual-channel.md), чтобы узнать, что это означает.

Сервер Nano Server предоставляет несколько способов поддержания системы в актуальном состоянии. По сравнению с другими вариантами установки Windows Server сервер Nano Server имеет более активную модель обслуживания, похожую на модель Windows 10. Такие периодические выпуски называют выпусками **Current Branch for Business (CBB)** . Этот подход обеспечивает поддержку клиентов, которые желают реализовывать инновации быстрее и следовать быстрым жизненным циклам разработки облачных технологий. Дополнительные сведения о CBB доступны в блоге [Windows Server](https://cloudblogs.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/).

**Между выпусками CBB** актуальное состояние сервера Nano Server поддерживается благодаря ряду *накопительных обновлений*. Например, первый накопительный пакет обновления для сервера Nano Server был выпущен 26 сентября 2016 г. (статья базы знаний [№ 4093120](https://support.microsoft.com/help/4093120/windows-10-update-kb4093120)). Доступность этого и последующих накопительных обновлений позволяет нам предоставлять вам различные варианты установки этих обновлений на сервере Nano Server. В этой статье мы будем использовать обновление KB3192366 в качестве примера, чтобы показать получение и применение накопительных обновлений для сервера Nano Server. Дополнительные сведения о модели накопительных обновлений см. в блоге [Центра обновления Майкрософт](/archive/blogs/mu/patching-with-windows-server-2016).

> [!NOTE]
> Если устанавливается необязательный пакет Nano Server с носителя или из интернет-репозитория, он не будет содержать последних исправлений безопасности. Чтобы избежать несоответствия версий дополнительных пакетов и базовой операционной системы, последний накопительный пакет обновления следует установить сразу после установки любых дополнительных пакетов и **перед** перезапуском сервера.

В случае с накопительным пакетом обновления для Windows Server 2016, 26 сентября 2016 г. ([статья базы знаний № 3192366](https://support.microsoft.com/kb/3192366)), сначала следует установить последнее обновление стека обслуживания для Windows 10 версии 1607 за 23 августа 2016 г. как необходимый компонент ([статья базы знаний № 3192366](https://support.microsoft.com/kb/3176936)). Для большинства следующих вариантов потребуются MSU-файлы, содержащие CAB-пакеты обновления. Посетите каталог Центра обновления Майкрософт, чтобы скачать каждый из этих пакетов обновления:
- [https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3192366](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3192366)
- [https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3176936](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB3176936)

После скачивания MSU-файлов из каталога Центра обновления Майкрософт сохраните их в общей сетевой папке или локальном каталоге, например C:\ServicingPackages. Вы можете переименовать MSU-файлы, используя их номер в базе знаний, как это сделано ниже, чтобы их было легче идентифицировать. Затем воспользуйтесь служебной программой EXPAND, чтобы извлечь CAB-файлы из MSU-файлов в отдельные каталоги и копировать первые в одну папку.

```code
    mkdir C:\ServicingPackages_expanded
    mkdir C:\ServicingPackages_expanded\KB3176936
    mkdir C:\ServicingPackages_expanded\KB3192366
    Expand C:\ServicingPackages\KB3176936.msu -F:* C:\ServicingPackages_expanded\KB3176936
    Expand C:\ServicingPackages\KB3192366.msu -F:* C:\ServicingPackages_expanded\KB3192366
    mkdir C:\ServicingPackages_cabs
    copy C:\ServicingPackages_expanded\KB3176936\Windows10.0-KB3176936-x64.cab C:\ServicingPackages_cabs
    copy C:\ServicingPackages_expanded\KB3192366\Windows10.0-KB3192366-x64.cab C:\ServicingPackages_cabs
```

Теперь извлеченные CAB-файлы можно использовать для применения обновлений к образу сервера Nano Server разными способами в зависимости от ваших потребностей. Варианты ниже представлены в произвольном порядке — используйте наиболее подходящий для вашей среды.

> [!NOTE]
> При использовании средств DISM для обслуживания сервера Nano Server необходимо использовать версию DISM не ниже версии обслуживаемого сервера Nano Server. Для этого нужно запустить DISM из соответствующей версии Windows, установить подходящую версию [Комплекта средств для развертывания и оценки (ADK)](https://developer.microsoft.comwindows/hardware/windows-assessment-deployment-kit) или запустить DISM на самом сервере Nano Server.

## <a name="option-1-integrate-a-cumulative-update-into-a-new-image"></a>Вариант 1. Интеграция накопительного пакета обновления с новым образом
Если вы создаете образ сервера Nano Server, можно интегрировать последнее накопительное обновление непосредственно в образ, чтобы установить все обновления при первой загрузке.

```powershell
New-NanoServerImage -ServicingPackagePath 'C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab', 'C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab' -<other parameters>
```

## <a name="option-2-integrate-a-cumulative-update-into-an-existing-image"></a>Вариант 2. Интеграция накопительного пакета обновления с существующим образом
При наличии существующего образа сервера Nano Server, который вы используете как основу для создания определенных экземпляров сервера Nano Server, можно интегрировать последнее накопительное обновление непосредственно в существующий базовый образ, чтобы все обновления устанавливались при первой загрузке машин, созданных с помощью этого образа.

```powershell
Edit-NanoServerImage -ServicingPackagePath 'C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab', 'C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab' -TargetPath .\NanoServer.wim
```

## <a name="option-3-apply-the-cumulative-update-to-an-existing-offline-vhd-or-vhdx"></a>Вариант 3. Применение накопительного пакета обновления к существующему автономному диску VHD или VHDX
Если у вас есть существующий виртуальный жесткий диск (VHD или VHDX), применить обновление к виртуальному жесткому диску можно с помощью средств DISM. Необходимо убедиться, что диск не используется, завершив работу всех виртуальных машин, использующих диск, или отключив файл виртуального жесткого диска.

- Использование PowerShell

   ```powershell
   Mount-WindowsImage -ImagePath .\NanoServer.vhdx -Path .\MountDir -Index 1
   Add-WindowsPackage -Path .\MountDir -PackagePath  C:\ServicingPackages_cabs
   Dismount-WindowsImage -Path .\MountDir -Save
   ```

- Использование dism.exe

   ```code
   dism.exe /Mount-Image /ImageFile:C:\NanoServer.vhdx /Index:1 /MountDir:C:\MountDir
   dism.exe /Image:C:\MountDir /Add-Package /PackagePath:C:\ServicingPackages_cabs
   dism.exe /Unmount-Image /MountDir:C:\MountDir /Commit
   ```

## <a name="option-4-apply-the-cumulative-update-to-a-running-nano-server"></a>Вариант 4. Применение накопительного пакета обновления к работающему серверу Nano Server
Если у вас есть работающая виртуальная машина или физический узел Nano Server и вы скачали CAB-файл для обновления, применить обновление к подключенной к сети системе можно с помощью средств DISM. Потребуется копировать CAB-файл локально на сервер Nano Server или в доступное сетевое расположение. Если вы применяете обновление для служебного стека, не забудьте перезапустить сервер после применения обновления для служебного стека и до применения дополнительных обновлений.

> [!NOTE]
> Если образ диска VHD или VHDX сервера Nano Server создан с использованием командлета New-NanoServerImage и вы не указали параметр MaxSize для файла виртуального жесткого диска, размер по умолчанию (4 ГБ) слишком мал, чтобы применить накопительное обновление. Перед установкой обновления используйте диспетчер Hyper-V, средство управления дисками, PowerShell или другое средство для увеличения размера виртуального жесткого диска и системного тома по меньшей мере до 10 ГБ или воспользуйтесь параметром ScratchDir в составе средств DISM, чтобы задать для каталога временных файлов том с объемом свободного пространства не менее 10 ГБ.

```powershell
$s = New-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
Copy-Item -ToSession $s -Path C:\ServicingPackages_cabs -Destination C:\ServicingPackages_cabs -Recurse
Enter-PSSession $s
```

- Использование PowerShell

   ```powershell
   # Apply the servicing stack update first and then restart
   Add-WindowsPackage -Online -PackagePath C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab
   Restart-Computer; exit

   # After restarting, apply the cumulative update and then restart
   Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
   Add-WindowsPackage -Online -PackagePath C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab
   Restart-Computer; exit
   ```

- Использование dism.exe
   ```powershell
   # Apply the servicing stack update first and then restart
   dism.exe /Online /Add-Package /PackagePath:C:\ServicingPackages_cabs\Windows10.0-KB3176936-x64.cab

   # After the operation completes successfully and you are prompted to restart, it's safe to
   # press Ctrl+C to cancel the pipeline and return to the prompt
   Restart-Computer; exit

   # After restarting, apply the cumulative update and then restart
   Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
   dism.exe /Online /Add-Package /PackagePath:C:\ServicingPackages_cabs\Windows10.0-KB3192366-x64.cab
   Restart-Computer; exit
   ```

## <a name="option-5-download-and-install-the-cumulative-update-to-a-running-nano-server"></a>Вариант 5. Загрузка и установка накопительного пакета обновления на работающем сервере Nano Server

Если имеется работающая виртуальная машина или физический узел сервера Nano Server, можно использовать поставщик WMI Центра обновления Windows для загрузки и установки обновления в подключенной к сети операционной системе. При использовании этого метода скачивать MSU-файл отдельно от каталога Центра обновления Майкрософт не требуется. Поставщик WMI обнаружит, скачает и установит все доступные обновления одновременно.

```powershell
Enter-PSSession -ComputerName (Read-Host "Enter Nano Server IP address") -Credential (Get-Credential)
```

- Сканирование на наличие доступных обновлений
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession
   $result = $ci | Invoke-CimMethod -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=0";OnlineScan=$true}
   $result.Updates
   ```

- Установка всех доступных обновлений
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession
   Invoke-CimMethod -InputObject $ci -MethodName ApplyApplicableUpdates
   Restart-Computer; exit
   ```

- Получение списка установленных обновлений
   ```powershell
   $ci = New-CimInstance -Namespace root/Microsoft/Windows/WindowsUpdate -ClassName MSFT_WUOperationsSession
   $result = $ci | Invoke-CimMethod -MethodName ScanForUpdates -Arguments @{SearchCriteria="IsInstalled=1";OnlineScan=$true}
   $result.Updates
   ```

## <a name="additional-options"></a>Дополнительные параметры
Другие методы обновления сервера Nano Server могут частично совпадать с вышеперечисленными или дополнять их. Эти варианты включают использование служб Windows Server Update Services (WSUS), диспетчера System Center Virtual Machine Manager (VMM), планировщика задач или стороннее решение.
- [Настройка Центра обновления Windows для WSUS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd939844(v=ws.10)) путем установки следующих разделов реестра:
  - WUServer;
  - WUStatusServer (как правило, значение совпадает со значением WUServer);
  - UseWUServer;
  - AUOptions.
- [Управление обновлениями структуры в VMM](/previous-versions/system-center/system-center-2012-R2/gg675084(v=sc.12)).
- [Регистрация запланированной задачи](/previous-versions/system-center/system-center-2012-R2/gg675084(v=sc.12)).
