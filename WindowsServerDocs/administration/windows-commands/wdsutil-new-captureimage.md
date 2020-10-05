---
title: New-Каптуреимаже
description: Справочная статья по New-Каптуреимаже, которая создает новый образ записи из существующего образа загрузки.
ms.topic: reference
ms.assetid: 2dfd08f0-be59-4715-96e6-c498305873f4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ab582e65ad3f1c9920071260541fefd0125bf428
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91730759"
---
# <a name="new-captureimage"></a>New-Каптуреимаже

Создает новый образ записи из существующего образа загрузки. Образы записи — это загрузочные образы, которые запускают служебную программу записи служб развертывания Windows вместо запуска программы установки. При загрузке компьютера-образца (который был подготовлен с помощью Sysprep) в образ записи мастер создает образ установки эталонного компьютера и сохраняет его как файл образа Windows (WIM). Можно также добавить образ на носитель (например, компакт-диск, DVD-диск или USB-накопитель), а затем загрузить компьютер с этого носителя. После создания образа установки можно добавить образ на сервер для развертывания PXE-загрузки. Дополнительные сведения см. в разделе Создание образов ( [https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311) ).

## <a name="syntax"></a>Синтаксис

```
WDSUTIL [Options] /New-CaptureImage [/Server:<Server name>]
     /Image:<Image name>
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /DestinationImage
        /FilePath:<File path and name>
        [/Name:<Name>]
        [/Description:<Description>]
        [/Overwrite:{Yes | No | Append}]
        [/UnattendFilePath:<File path>]
```

### <a name="parameters"></a>Параметры

|        Параметр         |                                                                                                                                                                                                                         Описание                                                                                                                                                                                                                          |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server: \<Server name> ] |                                                                                                                                       Указывает имя сервера. Это может быть либо NetBIOS-имя, либо полное доменное имя (FQDN). Если имя сервера не указано, будет использоваться локальный сервер.                                                                                                                                        |
|   Эскиз\<Image name>   |                                                                                                                                                                                                         Указывает имя исходного загрузочного образа.                                                                                                                                                                                                         |
|   /Арчитектуре: {x86    |                                                                                                                                                                                                                             ia64                                                                                                                                                                                                                             |
| [/Филенаме: \<Filename> ] |                                                                                                                                                                            Если образ не может быть однозначно идентифицирован по имени, необходимо использовать этот параметр, чтобы указать имя файла.                                                                                                                                                                            |
|    /дестинатионимаже     | Задает параметры для конечного образа. Параметры задаются с помощью следующих параметров.</br>-/FilePath.: \<File path and name> задает полный путь к файлу для нового образа записи.</br>-[/Name: \<Name> ] — задает отображаемое имя образа. Если отображаемое имя не указано, будет использоваться отображаемое имя исходного изображения.</br>-[/Description: \<Description> ] — задает описание образа.</br>-[/Overwrite: {Да |

## <a name="examples"></a>Примеры

Чтобы создать образ записи и назовите его Винпекаптуре. wim, введите:
```
WDSUTIL /New-CaptureImage /Image:WinPE boot image /Architecture:x86 /DestinationImage /FilePath:C:\Temp\WinPECapture.wim
```
Чтобы создать образ записи и применить указанные параметры, введите:
```
WDSUTIL /Verbose /Progress /New-CaptureImage /Server:MyWDSServer /Image:WinPE boot image /Architecture:x64 /Filename:boot.wim
/DestinationImage /FilePath:\\Server\Share\WinPECapture.wim /Name:New WinPE image /Description:WinPE image with capture utility /Overwrite:No /UnattendFilePath:\\Server\Share\WDSCapture.inf
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)