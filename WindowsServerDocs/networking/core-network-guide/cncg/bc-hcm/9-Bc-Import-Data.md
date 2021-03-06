---
title: Импорт пакетов данных на сервере размещенного кэша (необязательно)
description: Узнайте, как импортировать пакеты данных и загрузить содержимое на серверы размещенного кэша.
manager: brianlic
ms.topic: article
ms.assetid: d6159e91-f77c-42ec-9180-14bbb230ad17
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 08b47c2ec0fdd8e71ad6c415f4ec62ec2124a99b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101831215"
---
# <a name="import-data-packages-on-the-hosted-cache-server-optional"></a>Импорт пакетов данных на сервере размещенного кэша \( необязательно\)

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Эту процедуру можно использовать для импорта пакетов данных и загрузки содержимого на серверы размещенного кэша.

Эта процедура является необязательной, так как вам не требуется предварительно хэшировать и загружать содержимое на серверы размещенного кэша.

Если вы не \- загрузили содержимое, данные добавляются в размещенный кэш автоматически, так как клиенты загружают его через подключение к глобальной сети.

Для выполнения этой процедуры необходимо быть членом группы "Администраторы".

## <a name="to-import-data-packages-on-the-hosted-cache-server"></a>Импорт пакетов данных на сервере размещенного кэша

1. На компьютере сервера откройте Windows PowerShell с правами администратора.

2. Введите следующую команду, заменив значение параметра – Path на расположение папки, где хранятся пакеты данных, и нажмите клавишу ВВОД.

    ```
    Import-BCCachePackage –Path D:\temp\PeerDistPackage.zip
    ```

3. При наличии нескольких серверов размещенного кэша, для которых требуется предварительная загрузка содержимого, выполните эту процедуру на каждом сервере размещенного кэша.

Чтобы продолжить работу с этим руководством, см. статью [Настройка автоматического обнаружения размещенного кэша клиента с помощью точки подключения службы](10-Bc-Client-By-Scp.md).
