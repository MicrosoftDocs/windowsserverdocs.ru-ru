---
title: Изменение параметров потоковой передачи мультимедиа
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: dec690d2-f80c-4b09-99d6-3bba41331972
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 041a7f53b02d9b6b6368bd2b2f4ac991a14a61fa
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623883"
---
# <a name="change-media-streaming-settings"></a>Изменение параметров потоковой передачи мультимедиа

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Для изменения параметров потоковой передачи мультимедиа предусмотрено несколько вариантов, Доступны следующие варианты:

-   [Скрытие надстройки удаленной потоковой передачи мультимедиа](Change-Media-Streaming-Settings.md#BKMK_DisableRemote)

-   [Задание имени библиотеки мультимедиа](Change-Media-Streaming-Settings.md#BKMK_LibraryName)

-   [Задание качества потоковой передачи видео](Change-Media-Streaming-Settings.md#BKMK_StreamingQuality)

-   [Включение или отключение потоковой передачи мультимедиа программными средствами](Change-Media-Streaming-Settings.md#BKMK_Program)

##  <a name="hide-remote-media-streaming-add-in"></a><a name="BKMK_DisableRemote"></a> Скрыть надстройку удаленной потоковой передачи мультимедиа
 Скрытие надстройки удаленной потоковой передачи мультимедиа можно выполнить путем добавления записи в реестр.

#### <a name="to-hide-the-remote-media-streaming-add-in"></a>Скрытие надстройки удаленной потоковой передачи мультимедиа

1.  На сервере переместите указатель мыши в правый верхний угол экрана и нажмите кнопку **Поиск**.

2.  В поле **Поиск** введите **regedit**, а затем щелкните приложение **Regedit**.

3.  В левой области разверните на следующую запись реестра:

     **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\RemoteAccess\DisabledAddIns**

4.  Щелкните правой кнопкой мыши раздел **DisabledAddIns**, выберите команду **Создать** и щелкните пункт **Параметр DWORD**.

5.  В поле нового значения введите идентификатор надстройки удаленной потоковой передачи медиаданных **497796c6-9cc7-43be-aa26-4e6b5695370d**, а затем нажмите клавишу **Enter**.

6.  Щелкните параметр правой кнопкой мыши и выберите команду **Изменить**.

7.  Введите **1** в поле значения и нажмите кнопку **ОК**.

##  <a name="set-the-media-library-name"></a><a name="BKMK_LibraryName"></a> Задание имени библиотеки мультимедиа
 Чтобы задать имя для библиотеки мультимедиа, можно использовать класс из пакета SDK для решений Windows Server. Для присвоения имени библиотеке мультимедиа используется метод **SetMediaLibraryName** класса **MediaStreamingManager** из пространства имен **Microsoft.WindowsServerSolutions.MediaStreaming**. Ниже показан пример задания имени для библиотеки мультимедиа:

```c#

MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();
string mediaLibraryName = Guid.NewGuid().ToString("B");
mediaStreamingManager.SetMediaLibraryName(mediaLibraryName);

```

 Дополнительные сведения см. в статье [Пакет SDK для решений Windows Server](https://go.microsoft.com/fwlink/?LinkID=248648).

##  <a name="set-video-streaming-quality"></a><a name="BKMK_StreamingQuality"></a> Настройка качества потоковой передачи видео
 Качество потоковой передачи видео задается путем получения оценки ЦП средства WinSAT и последующего создания и установки XML-файла, содержащего сведения об оценке WinSAT. Если XML-файл со сведениями об оценке WinSAT устанавливается раньше выполнения начальной настройки, пользовательский интерфейс для задания качества видео не отображается. Дополнительные сведения см. в разделе [Установка на сервере системы оценки WinSAT](Set-the-WinSAT-Score-on-the-Server.md).

##  <a name="programmatically-enable-or-disable-media-streaming"></a><a name="BKMK_Program"></a> Программное включение или отключение потоковой передачи мультимедиа
 Чтобы включить или отключить потоковую передачу мультимедиа, можно использовать класс из пакета SDK для решений Windows Server. Для включения или отключения потоковой передачи мультимедиа используется метод **SetMediaStreamingEnabled** класса **MediaStreamingManager** из пространства имен **Microsoft.WindowsServerSolutions.MediaStreaming**. Ниже показан пример кода для включения потоковой передачи мультимедиа:

```c#

MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();
mediaStreamingManager.SetMediaStreamingEnabled(true);

```

 Ниже показан пример кода для отключения потоковой передачи мультимедиа:

```c#

MediaStreamingManager mediaStreamingManager = new MediaStreamingManager();
mediaStreamingManager.SetMediaStreamingEnabled(false);
```

## <a name="see-also"></a>См. также:
 [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)