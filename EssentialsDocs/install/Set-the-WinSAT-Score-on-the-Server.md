---
title: Установка на сервере системы оценки WinSAT
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 911dc494-0f8f-4723-93d6-2106f914b906
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 56769966cbfb6778c06abc4ba07d21f258e900a4
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89623342"
---
# <a name="set-the-winsat-score-on-the-server"></a>Установка на сервере системы оценки WinSAT

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Для оптимизации разрешения потоковой передачи видео необходимо задать оценку производительности WinSAT для сервера, работающего под управлением операционной системы Windows Server Essentials. Для этого необходимо создать и установить XML-файл, содержащий сведения об оценках WinSAT.

## <a name="obtain-the-winsat-cpu-score"></a>Получение оценки ЦП средства WinSAT
 В состав предустановочного набора OPK входит программа WinServerSAT.exe, которая обнаруживает оценку ЦП средства WinSAT и помещает эти сведения в файл WinServerSAT.xml, считываемый операционной системой.

#### <a name="to-obtain-the-winsat-cpu-score"></a>Получение оценки ЦП средства WinSAT

1. Скопируйте Ресаурцес\винсерверсат \\ * на носитель ADK на эталонный компьютер.

2. На компьютере-образце откройте окно командной строки с повышенными привилегиями.

3. Если папка %ProgramFiles%\Windows Server\Bin\OEM не существует, введите следующую команду и нажмите ВВОД

    **mkdir "%ProgramFiles%\Windows Server\Bin\OEM"**

4. Введите следующую команду и нажмите ВВОД.

    **WinServerSAT.exe "%ProgramFiles%\Windows Server\Bin\OEM\WinServerSAT.xml"**

   В примере показано содержимое XML созданного файла WinServerSAT.xml.

```

<?xml version="1.0" encoding="UTF-16"?>
<WinSAT>
   <CpuScore description="WinSAT CPU score">WinSAT_Score</CpuScore>
</WinSAT>
```

 где *оценка_WinSAT* заменяется значением, обнаруживаемым сервером.

> [!IMPORTANT]
>  Перед началом записи образа необходимо удалить файлы WinServerSAT.exe, winsat.prx, winsat.wmv и WinSATEncode.wmv с компьютера-образца.
