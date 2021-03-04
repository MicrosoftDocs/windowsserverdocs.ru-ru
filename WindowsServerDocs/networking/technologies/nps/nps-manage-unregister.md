---
title: Отмена регистрации сервера политики сети в домене Active Directory
description: Узнайте, как отменить регистрацию NPS в домен Active Directory, чтобы можно было переместить сервер политики сети в другой домен, заменить NPS или снять с учета NPS.
manager: brianlic
ms.topic: article
ms.assetid: 68a94616-3c29-45bd-bd33-e4c578f119e1
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: cf26e85fe042d4a6d7c031e6c1f5512ffef392bd
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101833271"
---
# <a name="unregister-an-nps-from-an-active-directory-domain"></a>Отмена регистрации сервера политики сети в домене Active Directory

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

В процессе управления развертыванием NPS может оказаться полезным переместить сервер политики сети в другой домен, заменить NPS или снять с учета NPS.

При перемещении или списании NPS можно отменить регистрацию сервера политики сети в доменах Active Directory, в которых NPS имеет разрешение на чтение свойств учетных записей пользователей в Active Directory.

Выполнить эти операции может только член группы **Администраторы** или пользователь с аналогичными правами.

## <a name="to-unregister-an-nps"></a>Отмена регистрации сервера политики сети

1. На контроллере домена в диспетчер сервера выберите **средства**, а затем **Active Directory пользователи и компьютеры**. Откроется консоль Active Directory пользователи и компьютеры.

2. Щелкните **Пользователи**, а затем дважды щелкните **Серверы RAS и IAS**.

3. Перейдите на вкладку **члены** , а затем выберите NPS, для которого требуется отменить регистрацию.

4. Нажмите кнопку **Удалить**, выберите **Да**, а затем нажмите кнопку **ОК**.

