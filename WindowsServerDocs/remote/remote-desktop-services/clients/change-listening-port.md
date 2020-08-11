---
title: Изменение порта прослушивания в удаленном рабочем столе
description: Узнайте, как изменить порт прослушивания для клиента удаленного рабочего стола.
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 07/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0add2c2d577c475044064394b7bd77e5eab5d802
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958112"
---
# <a name="change-the-listening-port-for-remote-desktop-on-your-computer"></a>Изменение порта прослушивания для удаленного рабочего стола на компьютере

>Применяется к: Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2008 R2

При подключении компьютера (клиентской версии Windows или Windows Server) с помощью клиента удаленного рабочего стола функции удаленного рабочего стола на компьютере "слышат" запрос на соединение через заданный порт прослушивания (по умолчанию — 3389). Этот порт прослушивания на компьютерах Windows можно изменить путем изменения реестра.

1. Откройте редактор реестра. (В поле поиска введите "regedit").
2. Перейдите к следующему разделу реестра: HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\PortNumber
3. Нажмите кнопку **Редактировать > Изменить**, а затем выберите пункт **Десятичное**.
4. Введите новый номер порта, а затем нажмите кнопку **ОК**.
5. Закройте редактор реестра и перезагрузите компьютер.

При очередном подключении компьютера к этому компьютеру с помощью удаленного рабочего стола необходимо будет ввести новый номер порта. Если вы используете брандмауэр, убедитесь, что в нем разрешены подключения к новому номеру порта.
