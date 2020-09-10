---
title: Настройка общих папок
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 47bc4986-14eb-4a29-9930-83a25704a3a0
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: c1a6276199964ac7fd2eb3953cb3fac828063dfc
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623678"
---
# <a name="customize-shared-folders"></a>Настройка общих папок

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

По умолчанию папки сервера создаются в самом крупном разделе диска 0. Партнеры могут изменить их местоположение и указать дополнительные папки сервера, выполнив следующие действия:

1. Используя настраиваемую конфигурацию раздела, создайте заводской образ, затем создайте новый раздел реестра Storage, прежде чем использовать средство Sysprep. В ходе начальной настройки задача начальной настройки хранилища проверяет этот раздел реестра. Если он существует, серверные папки по умолчанию создаются в каталоге C:\ServerFolders.

   #### <a name="to-create-a-new-storage-registry-key"></a>Создание нового раздела реестра Storage

   1.  На сервере переместите указатель мыши в правый верхний угол экрана и нажмите кнопку **Поиск**.

   2.  В поле поиска введите **regedit**, затем щелкните приложение **Regedit**.

   3.  В области навигации последовательно разверните **HKEY_LOCAL_MACHINE**, **SOFTWARE** и **Microsoft**.

   4.  Щелкните правой кнопкой мыши **Windows Server**, выберите **Создать**, затем щелкните **Раздел**.

   5.  Присвойте разделу имя **Storage**.

   6.  В области навигации щелкните правой кнопкой мыши новый раздел реестра Storage, выберите **Создать**, затем щелкните **Параметр DWORD (32 бита)**.

   7.  Введите имя строки **CreateFoldersOnSystem**.

   8.  Нажмите правой кнопкой мыши запись **CreateFoldersOnSystem**, а затем выберите команду **Изменить**. Откроется диалоговое окно **Изменение строкового параметра**.

   9. Установите для нового раздела значение **1** и нажмите кнопку **ОК**.

2. С помощью скрипта PostIC.cmd переместите папки в другое расположение или создайте дополнительные папки. См. следующий пример: [Пример 1. Создание настраиваемой папки и перемещение папок по умолчанию в новое расположение из PostIC.cmd с помощью Windows PowerShell](Customize-Shared-Folders.md#BKMK_Example1).

3. С помощью пакета SDK для решений Windows Server переместите папки в другое расположение или создайте дополнительные папки. См. следующий пример: [Пример 2. Создание настраиваемой папки и перемещение папок по умолчанию с помощью пакета SDK для решений Windows Server](Customize-Shared-Folders.md#BKMK_Example2).

   Партнеры могут также оставлять папки данных на диске C. В таком случае конечный пользователь или продавец может определить структуру папок данных на дисках с данными.

###  <a name="example-1-create-a-custom-folder-and-move-the-default-folders-to-a-new-location-from-posticcmd-by-using-windows-powershell"></a><a name="BKMK_Example1"></a> Пример 1. Создание настраиваемой папки и перемещение папок по умолчанию в новое расположение из папки POST. cmd с помощью Windows PowerShell

1.  Создайте файл PostIC.cmd для выполнения задач после завершения начальной настройки, как описано в разделе [Создание файла PostIC.cmd для выполнения задач после завершения начальной настройки](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md).

2.  С помощью блокнота создайте файл с именем **customizefolders.ps1** в папке к:\виндовс\сетуп\скриптс, а затем вставьте следующие команды Windows PowerShell &reg; в файл (снимите отметку соответствующих строк в зависимости от требуемого поведения).

    ```
    # Move the Documents folder to D:\ServerFolders
    #Get-WssFolder -name Documents| Move-WssFolder - NewDrive D:\ -Force

    # Check for last error. If last error is not null, exit with return code 1
    #If ($error[0] -ne $null) { exit 1}

    # Move all folders to D:\ServerFolders
    #foreach( $folder in Get-WssFolder )
    #{
    #    Move-WssFolder $folder -NewDrive D:\ -Force
    #}

    # Check for last error. If last error is not null, exit with return code 1
    #If ($error[0] -ne $null) { exit 1}

    # Create a custom folder named Custom Folder
    #Add-WssFolder -Name CustomFolder -Path D:\ServerFolders\CustomFolder -Description "Custom Folder"

    # Check for last error. If last error is not null, exit with return code 1
    #If ($error[0] -ne $null) { exit 1}

    exit 0
    ```

3.  Чтобы запустить этот сценарий, добавьте следующую строку в файл PostIC.cmd.

    ```
    REM Lower the execution policy
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy RemoteSigned"

    REM Execute the folder customization script
    "%programfiles%\Windows Server\bin\WssPowershell.exe" -NoProfile -Noninteractive -command ". %windir%\setup\scripts\customizefolders.ps1;exit $LASTEXITCODE"
    Set error_level=%ERRORLEVEL%

    REM Restore the execution policy to default
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy Restricted"
    Set ERRORLEVEL=%error_level%
    ```

###  <a name="example-2-create-a-custom-folder-and-move-an-existing-folder-by-using-the-windows-server-solutions-sdk"></a><a name="BKMK_Example2"></a> Пример 2. Создание настраиваемой папки и перемещение существующей папки с помощью пакета SDK для Windows Server Solutions
 Созданный код может быть скомпилирован в исполняемый файл и впоследствии вызван из файла PostIC.cmd или напрямую вызван из установленной надстройки.

```
static void Main(string[] args)
{
 StorageManager storageManager = new StorageManager();
 //Connect to the StorageManager
 storageManager.Connect();

 //Move the Documents folder to D:\ServerFolders
 Folder targetFolder = storageManager.Folders.First(folder => folder.Name == "Documents");

 MoveFolderRequest moveRequest = targetFolder.GetMoveRequest(@"D:\");
 moveRequest.MoveFolder();

 //Verify operation was successful, if so print result
 if (moveRequest.Status == OperationStatus.Succeeded)
 {
  Console.WriteLine("Folder {0} now located at {1}", targetFolder.Name, targetFolder.Path);
 }

 string newFolderName = "New Custom Folder";
 string newFolderLocation = @"C:\ServerFolders\New Custom Folder";

 //Create add request based with specific name and location
 CreateFolderRequest request = storageManager.GetCreateFolderRequest(newFolderName, newFolderLocation);

 //Give Guest user read only permission to folder
 request.PermissionsByName.Add(new NamePermission("Guest", Permission.ReadOnly));

 //Create the new folders
 request.CreateFolder();

 //Verify operation was successful, if so print result
 if( request.Status == OperationStatus.Succeeded)
 {
  Folder newFolder = storageManager.Folders.First(folder => folder.Path == newFolderLocation);

  Console.WriteLine("Folder {0} created at {1}", newFolder.Name, newFolder.Path);
 }
}
```

## <a name="see-also"></a>См. также:
 [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)
