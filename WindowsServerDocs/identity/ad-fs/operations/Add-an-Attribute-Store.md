---
description: 'Дополнительные сведения: Добавление хранилища атрибутов'
ms.assetid: c60227a8-7b44-40f8-b807-a6532851a4a6
title: Добавление хранилища атрибутов
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: d35d56bf2a30e023fccd9ea6e5f47e5c4c949f10
ms.sourcegitcommit: 528bdff90a7c797cdfc6839e5586f2cd5f0506b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/07/2021
ms.locfileid: "97977409"
---
# <a name="add-an-attribute-store"></a>Добавление хранилища атрибутов


Учетные записи пользователей и компьютеров, которым требуется доступ к ресурсу, защищенному службы федерации Active Directory (AD FS) \( AD FS, \) хранятся в хранилище атрибутов, например домен Active Directory Services \( AD DS \) . Подсистема выдачи утверждений использует хранилища атрибутов для сбора данных, необходимых для выдачи утверждений. Данные из хранилищ атрибутов затем проецируются в виде утверждений.

Для добавления хранилища атрибутов в служба федерации можно использовать следующую процедуру.

Для выполнения этой процедуры требуется членство в группе **Администраторы** или в эквивалентной группе на локальном компьютере.  Просмотрите сведения об использовании соответствующих учетных записей и членстве в группах в [локальной среде и группах домена по умолчанию](https://go.microsoft.com/fwlink/?LinkId=83477).

#### <a name="to-add-an-attribute-store"></a>Добавление хранилища атрибутов

1.  Откройте **управление AD FS**.

2.  В разделе **действия** щелкните **Добавить хранилище атрибутов**.

![Снимок экрана, который выделяет действие "добавить хранилище атрибутов".](media/Add-an-Attribute-Store/addstore1.PNG)

3. В диалоговом окне **Добавление хранилища атрибутов** настройте следующие свойства для хранилища атрибутов, которое требуется добавить.

   -   В поле **Отображаемое имя** введите имя, которое будет использоваться для распознавания хранилища атрибутов.

   -   В списке **тип хранилища атрибутов** выберите поддерживаемый тип хранилища атрибутов: **Active Directory**, **LDAP** или **SQL**.

   -   Если в поле **строка подключения** выбрано хранилище LDAP для протокола Lightweight Directory \( \) или \( хранилище SQL язык SQL \) , введите строку, которая использовалась для подключения к хранилищу атрибутов. Для Active Directory хранилищ атрибутов строка подключения не требуется. Поэтому это поле отключено.

       > [!NOTE]
       > AD FS автоматически создает хранилище атрибутов Active Directory по умолчанию.

![Добавить хранилище атрибутов](media/Add-an-Attribute-Store/addstore2.PNG)

4. Нажмите кнопку **OK**.

## <a name="additional-references"></a>Дополнительная справка

[Операции AD FS](../ad-fs-operations.md)

[Роль хранилищ атрибутов](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md)
