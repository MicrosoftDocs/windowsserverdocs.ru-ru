---
title: Создание пакетов данных сервера содержимого для содержимого веб-сайтов и файлов (необязательно)
description: Узнайте, как выполнить предварительное хэширование содержимого на веб-и файловых серверах, а затем создать пакеты данных для импорта на сервере размещенного кэша.
manager: brianlic
ms.topic: article
ms.assetid: 31e8428f-a482-4734-be1b-213912e34825
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 07252687031b0c89e315a087e21e5724bb70c806
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101832231"
---
# <a name="create-content-server-data-packages-for-web-and-file-content-optional"></a>Создание пакетов данных сервера содержимого для содержимого веб-сайтов и файлов (необязательно)

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Эту процедуру можно использовать для предварительного хэширования содержимого на веб-и файловых серверах, а затем создавать пакеты данных для импорта на сервере размещенного кэша.

Эта процедура является необязательной, так как вам не требуется предварительно хэшировать и загружать содержимое на серверы размещенного кэша. Если содержимое не будет загружено, данные добавляются в размещенный кэш автоматически, так как клиенты загружают его через подключение к глобальной сети.

Эта процедура содержит инструкции по созданию данных о том, как на файловых серверах, так и на веб-серверах. Если у вас нет такого типа серверов содержимого, вам не нужно выполнять инструкции для этого типа сервера содержимого.

>[!IMPORTANT]
>Перед выполнением этой процедуры необходимо установить и настроить BranchCache на серверах содержимого. Кроме того, если вы планируете изменить секрет сервера на сервере содержимого, сделайте это перед предварительным \- хэшированием содержимого — изменение секрета сервера делает недействительными ранее \- созданные хэши.

Для выполнения этой процедуры необходимо быть членом группы "Администраторы".

## <a name="to-create-content-server-data-packages"></a>Создание пакетов данных сервера содержимого

1. На каждом сервере содержимого выберите папки и файлы, которые необходимо добавить в пакет данных. Найдите или создайте папку, в которой вы хотите сохранить пакет данных позже в этой процедуре.

2. На компьютере сервера откройте Windows PowerShell с правами администратора.

3. Выполните одно или оба следующих действия в зависимости от типов серверов содержимого:

    > [!NOTE]
    > Значением параметра – path является папка, в которой находится содержимое. Необходимо заменить примеры значений в приведенных ниже командах на допустимое расположение папки на сервере содержимого, содержащем данные, которые необходимо добавить в пакет.

    - Если содержимое, которое требуется создать, находится на файловом сервере, введите следующую команду и нажмите клавишу ВВОД.

        ```
        Publish-BCFileContent -Path D:\share -StageData
        ```

    -   Если содержимое, которое требуется создать, находится на веб-сервере, введите следующую команду и нажмите клавишу ВВОД.

        ```
        Publish-BCWebContent –Path D:\inetpub\wwwroot -StageData
        ```

4. Создайте пакет данных, выполнив следующую команду на каждом сервере содержимого. Замените пример значения \( D: \\ TEMP значением \) параметра – destination на расположение, которое вы определили или создали в начале этой процедуры.

    ```
    Export-BCDataPackage –Destination D:\temp
    ```

5. На сервере содержимого получите доступ к общей папке на серверах размещенного кэша, где нужно загрузить содержимое, и скопируйте пакеты данных в общие папки на серверах размещенного кэша.

Чтобы продолжить работу с этим руководством, см. раздел [Импорт пакетов данных на сервере размещенного кэша &#40;Необязательные&#41;](9-Bc-Import-Data.md).

