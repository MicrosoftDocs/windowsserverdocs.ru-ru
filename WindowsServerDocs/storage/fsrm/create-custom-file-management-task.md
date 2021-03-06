---
title: Создание задачи управления пользовательскими файлами
description: В этой статье описывается процесс создания пользовательской задачи управления файлами и настраиваемых задач.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7fcfd9958787817a6945b220115c507f48924cbf
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954681"
---
# <a name="create-a-custom-file-management-task"></a>Создание задачи управления пользовательскими файлами

> Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Истечение срока действия не всегда является необходимым действие, которое требуется применить к файлам. Задачи управления файлами также позволяют выполнять пользовательские команды.

> [!Note]
> В описании этой процедуры предполагается, что вы уже знакомы с принципами работы задач управления файлами и поэтому в нем рассматривается только вкладка **Действие**, на которой выполняется настройка пользовательских параметров.

## <a name="to-create-a-custom-task"></a>Создание пользовательской задачи

1.  Щелкните узел **Задачи управления файлами**.

2.  Щелкните правой кнопкой мыши **Задачи управления файлами**, а затем нажмите кнопку **Создать задачу управления файлами** (или щелкните **Создать задачу управления файлами** на панели **Действия**). Откроется диалоговое окно **Создать задачу управления файлами**.

3.  На вкладке **Действие** введите следующие данные:

    -   **Type**. В раскрывающемся списке выберите **Пользовательская**.
    -   **Исполняемый файл**. Введите или выберите команду, которая будет выполняться при обработке файлов задачей управления файлами. Для этого исполняемого файла необходимо настроить права редактирования только для администраторов и системы. Если у других пользователей есть доступ к записи в исполняемом файле, оно будет работать правильно.
    -   **Параметры команд**. Чтобы настроить аргументы, передаваемые исполняемому файлу при обработке файлов задачей управления файлами, измените текстовое поле с меткой **Аргументы**. Чтобы добавить дополнительные переменные в текст, поместите курсор в место в текстовом поле, в котором необходимо вставить переменную, выберите переменную, которую необходимо вставить, и нажмите кнопку **Вставить переменную**. Текст в квадратных скобках вставляет сведения о переменных, получаемые исполняемым файлом. Например, \[ Переменная пути к исходному файлу \] вставляет имя файла, который должен быть обработан исполняемым файлом. При необходимости нажмите кнопку **Рабочий каталог**, чтобы указать расположение настраиваемого исполняемого файла.
    -   **Безопасность команд**. Настройте параметры безопасности для этого исполняемого файла. По умолчанию команда выполняется как локальная служба, которая представляет собой учетную запись с наиболее строгими ограничениями.

4.  Нажмите кнопку **ОК**.

## <a name="additional-references"></a>Дополнительные ссылки

-   [Управление классификациями](classification-management.md)
-   [Задачи управления файлами](file-management-tasks.md)