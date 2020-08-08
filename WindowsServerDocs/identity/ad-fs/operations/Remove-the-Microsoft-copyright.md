---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: Удаление авторского права Майкрософт
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: ec7d9cb02508fc046ce3e8f0378e63c82eecca8d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949778"
---
# <a name="remove-the-microsoft-copyright"></a>Удаление авторского права Майкрософт



По умолчанию страницы AD FS содержат авторские права Майкрософт. Для удаления этих сведений с настроенных страниц можно воспользоваться следующей процедурой.

![удалить авторские права](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)

## <a name="to-remove-the-microsoft-copyright"></a>Удаление сведений об авторских правах Майкрософт

1. Создайте пользовательскую тему на основе стандартной.

   ```powershell
   New-AdfsWebTheme –Name custom –SourceName default
   ```

2. Экспортируйте тему в указанную папку вывода.

   ```powershell
   Export-AdfsWebTheme -Name custom -DirectoryPath C:\CustomWebTheme
   ```

3. Найти `Style.css` файл, расположенный в папке выходных данных. Используя предыдущий пример, путь будет выглядеть так:`C:\CustomWebTheme\Css\Style.css.`

4. Откройте `Style.css` файл в редакторе, например в блокноте.

5. Найдите часть `#copyright` и измените ее следующим образом:

   ```css
   #copyright {color:#696969; display:none;}
   ```

6. Создайте пользовательскую тему, основанную на новом `Style.css` файле.

   ```powershell
   Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}
   ```

7. Активируйте новую тему.

   ```powershell
   Set-AdfsWebConfig -ActiveThemeName custom
   ```

Теперь вы больше не должны видеть авторские права в нижней части страницы входа.

![удалить авторские права](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png)

## <a name="additional-references"></a>Дополнительная справка
[AD FS настройки входа пользователя](AD-FS-user-sign-in-customization.md)
