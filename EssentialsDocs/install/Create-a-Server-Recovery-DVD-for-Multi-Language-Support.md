---
title: Создание DVD-диска восстановления сервера с многоязычной поддержкой
description: Узнайте, как создать конфигурацию сервера и DVD-диск восстановления сервера для поддержки нескольких языков на локально администрируемых серверах.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: c7da0f6c-9732-4784-9c28-7dad72c4071d
author: daveba
ms.author: daveba
ms.openlocfilehash: d17a7103233b25553eb67a2c7d025d4647cbbbc5
ms.sourcegitcommit: d2224cf55c5d4a653c18908da4becf94fb01819e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/21/2020
ms.locfileid: "97711329"
---
# <a name="create-a-server-recovery-dvd-for-multi-language-support"></a>Создание DVD-диска восстановления сервера с многоязычной поддержкой

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="create-a-server-setup-and-server-recovery-dvd-for-multiple-language-support-on-locally-administered-servers"></a><a name="BKMK_MLHeadedRecovery"></a> Создание конфигурации сервера и DVD-диска восстановления сервера для поддержки нескольких языков на локально администрируемых серверах

> [!NOTE]
>  Сначала необходимо создать многоязыковой образ Windows, как описано в разделе [Пошаговое руководство. Создание многоязыкового образа Windows](/previous-versions/windows/it-pro/windows-8.1-and-8/jj126995(v=win.10)) перед добавлением пакета Лангауаже для Windows Server Essentials в install. wim.

 Существует два этапа установки: среда предустановки Windows (Windows PE) и начальная настройка. По умолчанию страница выбора языка при начальной настройке не отображается.

- В случае установки, удаленно администрируемой поставщиком вычислительной техники, или сценария предустановки у ПВТ необходимо добавить раздел реестра, используя следующую команду для отображения страницы выбора языка в ходе начальной настройки.

  ```
  %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f
  ```

  > [!IMPORTANT]
  >  При создании образа в лаборатории поставщики вычислительной техники должны выбирать **английский** язык на этапе установки среды предустановки Windows.

- В сценарии использования набора для торговых посредников Reseller Option Kit (ROK) пользователи получают DVD-диск, а иногда и некоторое оборудование. Пользователь должен иметь возможность выбрать язык при установке среды предустановки Windows, и страница выбора языка больше не отображается при начальной настройке.

  Можно выбрать вариант отправки одного двухслойного DVD-диска, содержащего пакеты на нескольких языках.

  В этом разделе приведено описание добавления языковой поддержки в программу установки Windows. Основное средство настройки среды предустановки Windows версии 3.0 - это программа командной строки "Система обслуживания образов развертывания и управления ими" (DISM). Данное решение обеспечивает выполнение следующих сценариев:

1.  создание многоязычных установок;

2.  создание распространяемых носителей.

### <a name="prerequisites"></a>Предварительные требования
 Чтобы добавить многоязычную поддержку в программу установки Windows, необходимо следующее:


-   Обслуживающий компьютер со всеми средствами и исходными файлами, необходимыми для создания настраиваемого образа среды предустановки Windows. Для получения дополнительной информации см. раздел [Подготовка обслуживающего компьютера](Prepare-the-Technician-Computer.md).

-   Обслуживающий компьютер со всеми средствами и исходными файлами, необходимыми для создания настраиваемого образа среды предустановки Windows. Для получения дополнительной информации см. раздел [Подготовка обслуживающего компьютера](../install/Prepare-the-Technician-Computer.md).


-   DVD-диск Windows Server Essentials.

-   DVD-диск языкового пакета Windows Server Essentials.

###  <a name="adding-multiple-language-support"></a><a name="BKMK_Steps"></a> Добавление поддержки нескольких языков
 Чтобы добавить поддержку нескольких языков в программа установки Windows вы обновите файл install. wim, добавив в него Windows Server 2012 и языковые пакеты Windows Server Essentials.

#### <a name="update-installwim"></a>Обновление файла install.wim
 На этом шаге вы добавите языковые пакеты Windows Server 2012 и Windows Server Essentials в install. wim.

> [!NOTE]
>  Убедитесь, что установлены языковые пакеты для Windows Server 2012. Это обеспечит использование надлежащей фирменной символики. Языковые пакеты многоязыкового пользовательского интерфейса для Windows Server 2012 доступны на [Microsoft.com](https://www.microsoft.com/OEM/en/installation/downloads/Pages/technical-downloads.aspx). Следуйте инструкциям, описанным в разделе [Пошаговое руководство. Создание многоязыкового образа Windows для](/previous-versions/windows/it-pro/windows-8.1-and-8/jj126995(v=win.10)) создания многоязычного образа Windows перед добавлением языкового пакета Windows Server Essentials в install. wim.
>
>  Языковые пакеты Windows Server Essentials доступны на носителе языкового пакета в \Лангуаже Packs \\<cultureName \> .

> [!NOTE]
>  Не все языковые пакеты могут быть недоступны до выпуска Windows Server 2012.

###### <a name="to-add-language-packs-to-installwim"></a>Добавление языковых пакетов в файл install.wim

1.  Добавьте языковые пакеты операционной системы и продукта в файл install.wim следующим образом (в данном примере используется французский язык):

    ```
    Dism /Mount-Wim /WimFile:C:\my_distribution\sources\install.wim /index:1 /MountDir:C:\InstallMount
    Mkdir c:\temp_Scratch
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<path_to_OS_language_packs>\fr-fr\lp.cab
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<OCD\Language Packs\FR-FR\lp.cab

    ```


2.  Добавьте файлы, зависящие от языка, для поддержки создания USB-устройства восстановления резервного копирования клиента с помощью процедуры, описанной в статье [Создание носителя для восстановления клиента на нескольких языках](Build-Multi-Language-Client-Restore-Media.md).

2.  Добавьте файлы, зависящие от языка, для поддержки создания USB-устройства восстановления резервного копирования клиента с помощью процедуры, описанной в статье [Создание носителя для восстановления клиента на нескольких языках](../install/Build-Multi-Language-Client-Restore-Media.md).


3.  Используя команду `DISM /Gen-LangINI` , заново создайте файл Lang.ini на съемном носителе для отражения поддержки дополнительных языков, например:

    ```
    Dism /image:C:\InstallMount /Gen-LangINI /distribution:C:\my_distribution

    ```

4.  Сохраните внесенные изменения в образе, используя команду `DISM /unmount /commit` , например:

    ```
    Dism /Unmount-Wim /MountDir:C:\InstallMount /Commit
    ```

## <a name="see-also"></a>См. также:

 [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)