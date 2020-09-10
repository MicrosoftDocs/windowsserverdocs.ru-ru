---
title: Автоматизация установки дополнительных компонентов во время установки
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 2e6ff6e4-8d68-4d49-9e38-8088bc8bf95e
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: ebfd0950c585e2383f736818789e8a2dce67ad4d
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623968"
---
# <a name="automate-installation-of-add-ins-during-setup"></a>Автоматизация установки дополнительных компонентов во время установки

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="automate-installing-add-ins-during-setup"></a><a name="BKMK_AddIns"></a> Автоматизация установки надстроек во время установки
 Для установки надстроек во время установки воспользуйтесь файлом PostIC.cmd, описанным в разделе [Создание файла PostIC.cmd для выполнения задач после завершения начальной настройки](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) настоящего документа.

 Добавьте следующую запись в файл PostIC.cmd:

```
C:\Program Files\Windows Server\bin\Installaddin.exe <full path to wssx file> -q
```

 Теперь надстройка поддерживает этапы предварительной установки и настраиваемого удаления.

 Шаг предварительной установки выполняется перед установкой всех файлов **.msi**, указанных в файле addin.xml. При выполнении в интерактивном режиме отображается диалоговое окно выполнения, однако индикатор выполнения не изменяется. На этапе предварительной установки кнопка отмены неактивна. Чтобы выполнить шаг предварительной установки, необходимо добавить следующее содержимое в файл addin.xml (непосредственно под Package):

> [!NOTE]
>  Схема XML должна в точности соответствовать указанной ниже:

```
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <Id>...</Id>
  <Version>...</Version>
  <Name>...</Name>
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>
  <ServerBinary>...</ServerBinary>
  <ClientBinary32>...</ClientBinary32>
  <ClientBinary64>...</ClientBinary64>
  <SupportedSkus>...</SupportUrl>
  <SupportUrl>...</SupportUrl>
  <Location>...</Location>
  <PrivacyStatement>...</PrivacyStatement>
  <OtherBinaries>...</OtherBinaries>
  <Preinstall>
<Executable>exefile</Executable>
<NormalArgs>args-for-interactive-mode</NormalArgs>
<SilentArgs>args-for-silent-mode</SilentArgs>
<IgnoreExitCode>true</IgnoreExitCode>
  </Preinstall>
  <UninstallConfirm>...</UninstallConfirm>
</Package>
<¦>
<¦>
```

 Где **exefile** – исполняемый файл в пакете надстройки для выполнения шага предварительной установки, его необходимо указать. **NormalArgs** указывает аргументы для передачи в exefile с помощью командной строки, если используется интерактивный режим. В этом режиме exefile может открывать некоторые всплывающие диалоговые окна, обеспечивая взаимодействие с пользователем. **SilentArgs** указывает аргументы для передачи в exefile с помощью командной строки, если используется автоматический режим (-q указывается в случае применения installaddin.exe). В данном режиме exefile не должен открывать всплывающих окон. Если тег **IgnoreExitCode** указан со значением "Истина", шаг предварительной установки всегда считается выполненным успешно, в противном случае код завершения 0 обозначает успешное завершение, 1 обозначает отмену, любые другие значения свидетельствуют о сбое. Теги **NormalArgs**, **SilentArgs** и **IgnoreExitCode** используются по желанию.

 Настраиваемый шаг удаления можно использовать в следующих случаях:

- Замена встроенного диалога подтверждения.

- Заполнение настраиваемых диалоговых окон перед удалением.

- Выполнение некоторых задач перед удалением.

  Чтобы выполнить шаг удаления, необходимо добавить следующее содержимое в файл addin.xml (непосредственно под Package):

```
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <Id>...</Id>
  <Version>...</Version>
  <Name>...</Name>
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>
  <ServerBinary>...</ServerBinary>
  <ClientBinary32>...</ClientBinary32>
  <ClientBinary64>...</ClientBinary64>
  <SupportedSkus>...</SupportUrl>
  <SupportUrl>...</SupportUrl>
  <Location>...</Location>
  <PrivacyStatement>...</PrivacyStatement>
  <OtherBinaries>...</OtherBinaries>
  <Preinstall>¦</Preinstall>
<UninstallConfirm>
<Executable>full-path-to-exefile</Executable>
<Arguments>command-line-arguments</Arguments>
</UninstallConfirm>
</Package>
```

 Где **full-path-to-exefile** указывает на exefile, уже установленный в системе. Пункт **Аргументы** является необязательным и указывает аргументы командной строки для exefile. Exefile вызывается, прежде чем появляется встроенный диалог подтверждения удаления.

 На этом этапе exefile может выполнять следующие задания:

- Открытие всплывающих диалоговых окон для обеспечения взаимодействия с пользователем.

- Выполнение некоторых фоновых задач.

  Код завершения данного EXE-файла определяет порядок дальнейшей работы процесса удаления:

- 0: процесс удаления продолжается без заполнения встроенного диалога подтверждения, как если бы пользователь ввел все необходимые подтверждения. (Этот подход можно использовать для замены встроенного диалога подтверждения);

- 1: процесс удаления отменен, и пользователь получает завершающее сообщение об отмене процедуры. Все остается без изменений;

- Другое: процесс удаления продолжается с использованием встроенного диалога подтверждения, как если бы шаг настраиваемого удаления отсутствовал.

  Любой сбой, активирующий exefile, вызовет такие же действия, как если бы exefile вернул код, отличный от 0 или 1.

## <a name="see-also"></a>См. также:
 [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)