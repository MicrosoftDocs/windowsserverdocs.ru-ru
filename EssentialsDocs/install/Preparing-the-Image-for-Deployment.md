---
title: Подготовка образа для развертывания
description: Узнайте, как использовать файл sysprep.exe для подготовки образа к развертыванию.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 681c6cad-7fde-494f-86a5-f4c7c15d23f9
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: abe50e40cf8de99b94c6ba956745c8df43f02ed7
ms.sourcegitcommit: e00e789dff216dbade861e61365f078b758a5720
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/23/2020
ms.locfileid: "97755390"
---
# <a name="preparing-the-image-for-deployment"></a>Подготовка образа для развертывания

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Обычное средство для подготовки образа – это sysprep.exe. Запуск этого средства позволяет подготовить к использованию образ и выключить сервер, чтобы выполнить начальную настройку после перезапуска сервера с образом. Перед запуском sysprep.exe все изменения образа должны быть завершены.

> [!NOTE]
>  С помощью sysprep.exe активацию Windows можно сбросить не более трех раз.

#### <a name="to-prepare-the-image"></a>Подготовка образа

1.  Удалите добавленный файл SkipIC.txt.

2.  Откройте окно командной строки с повышенными привилегиями. Нажмите кнопку **Пуск**, щелкните правой кнопкой мыши пункт **Командная строка** и выберите команду **Запуск от имени администратора**.

3.  Выполните следующую команду и сбросьте раздел реестра, чтобы в распоряжении пользователя был полный льготный период, прежде чем сервер станет несоответствующим.

    ```
    %systemroot%\system32\reg.exe add HKLM\Software\Microsoft\ServerInfrastructureLicensing /v Rearm /t REG_DWORD /d 1 /f
    ```

4.  Выполните следующую команду, чтобы добавить раздел реестра для отображения ключа, страницы языка, страницы языкового стандарта и страницы лицензионного соглашения. По умолчанию эти страницы во время начальной настройки не отображаются. Поэтому в случае выпуска предустановленного пакета необходимо добавить данный раздел реестра. Впрочем, если вы выпускаете DVD-диск, не стоит добавлять этот раздел, так как эти страницы будут отображены в ходе WinPE и начальной настройки.

    ```
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f
    ```

5.  Если пакет содержит предварительно созданные разделы, отключите страницу раздела начальной настройки. Страница раздела будет отображаться только в том случае, если выполняются следующие условия: ShowPreinstallPages = true и KeyPreInstalled != true.

    ```
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v KeyPreInstalled /t REG_SZ /d true /f
    ```

6.  Выполните следующую команду, чтобы добавить раздел реестра, если необходимо отключить проверки требований к оборудованию. Это относится только к предустановленному пакету, который не отвечает требованиям к оборудованию. Если создается диск DVD или пакет отвечает требованиям к оборудованию, рекомендуется не добавлять этот реестр.

    ```
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f
    ```

7.  (Необязательно) Удалите журналы из папки **%programdata%\Microsoft\Windows Server\Logs**.

8.  Приготовьте xml-файл автоматической установки для sysprep, как показано в шаблоне.

    ```
    <unattend xmlns="urn:schemas-microsoft-com:unattend" xmlns:ms="urn:schemas-microsoft-com:asm.v3">

      <settings pass="oobeSystem">
        <component name="Microsoft-Windows-Shell-Setup" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" xmlns:wcm="https://schemas.microsoft.com/WMIConfig/2002/State" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

          <!-- Must have -->
          <OOBE>
             <HideEULAPage>true</HideEULAPage>
          </OOBE>
          <!-- Must have -->
          <AutoLogon>
            <Enabled>true</Enabled>
            <Username>Administrator</Username>
            <Domain>.</Domain>
            <Password>
              <!--You can set any password you like, but keep it consistent with password settings -->
              <Value>Admin@123</Value>
              <PlainText>true</PlainText>
            </Password>
          </AutoLogon>
          <UserAccounts>
           <AdministratorPassword>
             <!--You can set any password you like, but keep it consistent with auto logon settings -->
             <Value>Admin@123</Value>
             <PlainText>true</PlainText>
           </AdministratorPassword>
          </UserAccounts>

          <!-- Optional -->
          <OEMInformation>
             <HelpCustomized>true</HelpCustomized>
             <Manufacturer>OEM name</Manufacturer>
             <Model>model name</Model>
             <SupportHours>hours</SupportHours>
             <SupportPhone>123-456-7890</SupportPhone>
             <SupportURL>http://www.contoso.com</SupportURL>
          </OEMInformation>

        </component>

      </settings>

      <settings pass="specialize">
        <component name="Microsoft-Windows-Shell-Setup" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" processorArchitecture="amd64">
          <!-- Must have -->
          <ComputerName>Server</ComputerName>
          <!-- Optional -->
          <ProductKey>XXXXX-XXXXX-XXXXX-XXXXX-XXXXX</ProductKey>
        </component>
      </settings>
    </unattend>
    ```

9. Выполните следующую команду для sysprep.

    ```
    %systemroot%\system32\sysprep\sysprep.exe /generalize /OOBE /unattend:xxx.xml /Quit
    ```

    > [!IMPORTANT]
    >  Кроме того, в качестве параметра sysprep можно добавить файл unattend.xml на %systemdrive%. Если файл находится в папке c:\ Он будет охватывать параметры пользователя, но если он используется в качестве параметра Sysprep, он не будет охватывать параметры пользователя. Файл unattend.xml на %systemdrive% будет удаляться при каждом перезапуске сервера. Поэтому после создания файла unattend.xml в %systemdrive% следите, чтобы сервер не перезапускался.

10. Выполните следующую команду, чтобы добавить раздел реестра и пропустить страницу ключа Windows OOBE.

    ```
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedProductKey /t REG_DWORD /d 1 /f
    ```

11. Выполните следующую команду, чтообы добавить раздел регистра и пропустить страницу выбора языка Windows.

    ```
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedLanguageSelection /t REG_DWORD /d 1 /f
    ```

    > [!IMPORTANT]
    >  Необходимо выполнить последние 2 шага, в противном случае отобразится страница запуска Windows при первом включении компьютера, связанная со страницей начальной настройки, и нарушит сценарий для удаленно администрируемого сервера.

12. Выключите сервер после выполнения Sysprep; можно записать образ или перезапустить сервер, чтобы продолжить начальную настройку с клиентского компьютера.

> [!IMPORTANT]
>  Партнерам, планирующим создать носитель для восстановления сервера, необходимо записать образ и создать носитель для восстановления перед переходом к следующему этапу.