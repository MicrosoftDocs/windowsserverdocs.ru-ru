---
title: Настройка системы архивации данных сервера
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 19b2559c-6090-45af-9a08-2eefc28473c8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a0992ed2858adbe713a25ec73f35c4b74a54ccd5
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181330"
---
# <a name="customize-server-backup"></a>Настройка системы архивации данных сервера

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

## <a name="turn-off-server-backup-by-default"></a>Выключение архивации сервера по умолчанию
 Архивацию сервера можно выключать по умолчанию. Чтобы включить эту опцию, необходимо установить для раздела **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Server\ServerBackup\ProviderDisabled** значение 1.

 После установки значения данного раздела пользовательский интерфейс архивации сервера не будет отображаться на панели мониторинга и в панели запуска. Это позволяет использовать для архивации сервера приложения сторонних разработчиков.

#### <a name="to-add-serverbackupproviderdisabled-registry-key-and-set-the-value-to-1"></a>Добавить Сервербаккуп\провидердисаблед? раздел реестра и установите значение 1

1.  На сервере нажмите кнопку **Пуск**, щелкните **Выполнить**, в поле **Открыть** введите **regedit**, а затем нажмите кнопку **OK**.

2.  В области навигации разверните разделы **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server** и **ServerBackup**.

3.  Щелкните правой кнопкой мыши **ServerBackup**, щелкните **Создать**, затем щелкните **Значение DWARD**.

4.  Для изменения имени введите **ProviderDisabled**.

5.  Щелкните правой кнопки мыши **Изменить**, введите **1** для значения переменной, а затем щелкните **OK**.

## <a name="turn-on-server-backup"></a>Включение архивации сервера
 Если архивация сервера была отключена, ее можно включить, создав раздел реестра **ProviderDisabled** (как описано выше).

 Необходимо удалить раздел **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Server\ServerBackup\ProviderDisabled**, чтобы включить архивацию сервера по умолчанию, изменить тип запуска службы архивации данных сервера Windows Server и перезапустить сервер.

#### <a name="to-delete-serverbackupproviderdisabled-registry-key"></a>Удалить Сервербаккуп\провидердисаблед? раздел реестра

1.  На сервере переместите указатель мыши в правый верхний угол экрана и нажмите кнопку **Поиск**.

2.  В поле поиска введите **regedit**, затем щелкните приложение **Regedit**.

3.  В области навигации разверните разделы **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server** и **ServerBackup**.

4.  Нажмите правой кнопкой мыши файл **ProviderDisabled**, а затем щелкните **Удалить**.

#### <a name="change-the-start-type-of-windows-server-server-backup-service"></a>Изменение типа запуска службы архивации данных сервера Windows Server

1.  На сервере переместите указатель мыши в правый верхний угол экрана и нажмите кнопку **Поиск**.

2.  В поле поиска введите **services.msc**, затем щелкните приложение **Службы**.

3.  В области служб щелкните правой кнопкой мыши опцию **Служба архивации данных сервера Windows Server**, и щелкните **Свойства**.

4.  На вкладке **Общие** выберите для параметра **Тип запуска** значение **Автоматический**.

5.  Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно.

#### <a name="restart-the-server"></a>Перезагрузите сервер.

1.  На сервере переместите указатель мыши в правый верхний угол экрана, нажмите кнопку **Параметры**, нажмите **Питание** и затем нажмите кнопку "Перезапустить".