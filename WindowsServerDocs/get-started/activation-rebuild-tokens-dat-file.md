---
title: Перестроение файла Tokens.dat
description: Как перестроить файл Tokens.dat при устранении неполадок, связанных с активацией Windows.
ms.topic: troubleshooting
ms.date: 09/18/2019
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: bc44dae97422e4d9d9e55b32004f806bbb7860f7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941786"
---
# <a name="rebuild-the-tokensdat-file"></a>Перестроение файла Tokens.dat

При устранении неполадок, связанных с активацией Windows, может потребоваться перестроить файл Tokens.dat. В данной статье подробно описано, как это сделать.

## <a name="resolution"></a>Разрешение

Чтобы перестроить файл Tokens.dat, выполните следующие действия.

1. Откройте окно командной строки с повышенными привилегиями. **Для Windows 10**

   1. Откройте меню **Пуск** и введите **cmd**.
   1. В списке результатов щелкните правой кнопкой мыши **Командная строка**, а затем выберите **Запуск от имени администратора**.

   **Для Windows 8.1**
   1. Проведите пальцем от правого края экрана, а затем коснитесь **Найти**. Если вы используете мышь, наведите указатель мыши на правый нижний угол экрана, а затем выберите **Найти**.
   1. В поле поиска введите **cmd**.
   1. Проведите пальцем по отображенному значку **Командная строка** или щелкните его правой кнопкой мыши.
   1. Коснитесь или щелкните **Запуск от имени администратора**.

   **Для Windows 7**
   1. Откройте меню **Пуск** и введите **cmd**.
   1. В результатах поиска щелкните правой кнопкой мыши файл **cmd.exe** и выберите **Запуск от имени администратора**.

1. Введите набор команд, подходящих для вашей операционной системы.

   Для Windows 10, Windows Server 2016 и более поздних версий Windows последовательно введите следующие команды.
   ```cmd
   net stop sppsvc
   cd %windir%\system32\spp\store\2.0
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
   Для Windows 8.1, Windows Server 2012 и Windows Server 2012 R2 последовательно введите следующие команды.
   ```cmd
   net stop sppsvc
   cd %windir%\ServiceProfiles\LocalService\AppData\Local\Microsoft\WSLicense
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
   Для Windows 7, Windows Server 2008 и Windows Server 2008 R2 последовательно введите следующие команды.
   ```cmd
   net stop sppsvc
   cd %windir%\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft\SoftwareProtectionPlatform
   ren tokens.dat tokens.bar
   net start sppsvc
   cscript.exe %windir%\system32\slmgr.vbs /rilc
   ```
1. Перезагрузите компьютер.

## <a name="more-information"></a>Дополнительные сведения

После перестроения файла Tokens.dat необходимо переустановить ключ продукта с помощью одного из следующих методов.

- В той же командной строке с повышенными привилегиями введите приведенную ниже команду и нажмите клавишу ВВОД.

   ```cmd
   cscript.exe %windir%\system32\slmgr.vbs /ipk <Product key>
   ```

  > [!IMPORTANT]
  > Не используйте параметр **/upk** для удаления ключа продукта. Чтобы установить ключ продукта вместо имеющегося ключа продукта, используйте параметр **/ipk**.
- Щелкните правой кнопкой мыши **Мой компьютер**, выберите **Свойства**, а затем выберите **Изменить ключ продукта**.

Дополнительные сведения о ключах установки клиента KMS см. в разделе [Ключи установки клиента KMS](kmsclientkeys.md).
