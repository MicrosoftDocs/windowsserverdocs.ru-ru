---
title: Использование сборщика журналов Windows Server Essentials
description: Узнайте, как использовать сборщик журналов Windows Server Essentials для сбора журналов с серверов, компьютеров в сети или и того, и другого.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: c6985518-b42d-4cfb-9761-eaa75306b6d7
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 4a540c52ee4cb84455f125c0d9f5c2f4ad0f3bf1
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810131"
---
# <a name="use-the-windows-server-essentials-log-collector"></a>Использование сборщика журналов Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

При устранении неполадок, связанных с компьютером, у представителя службы поддержки пользователей Майкрософт могут попросить вас собрать журналы с серверов, компьютеров в сети или с помощью сборщика журналов Windows Server Essentials.

 Сборщик журналов копирует журналы программ, событий и прочую информацию среды в единый ZIP-файл по указанному адресу. Сборщик журналов можно запускать непосредственно c сервера или любого компьютер сети, а также через удаленное подключение к компьютерам.

> [!NOTE]
>Сборщик журналов не проводит анализ сетевых проблем и не вносит изменения в настройки серверов или компьютеров сети. Дополнительную информацию об устранении сетевых неполадок см. в справочной документации по вашему серверу.
>В этом разделе Компьютеры в сети, отличные от сервера, называются сетевыми компьютерами.
>
>[Скачайте пакет установки сборщика журнала Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=34821).

 Чтобы установить и запустить сборщик журналов, выполните шаги, описанные в следующих разделах.

1. [Установка сборщика журналов](../support/Install-the-Windows-Server-Essentials-Log-Collector.md)

2. [Запуск сборщика журналов](../support/Run-the-Windows-Server-Essentials-Log-Collector.md)


## <a name="environment-information-collected"></a>Сбор сведений о среде
 Для каждого компьютера сети или сервера, указанного вами, сборщик журналов собирает следующие сведения о среде и помещает их в файл журнала коллекции:

-   Версия операционной системы

-   Изготовитель и описание ЦП

-   Объем памяти и ее выделение

-   Сетевые адаптеры, связанные с TCP/IP

-   Языковой стандарт

-   Процессы

-   Конфигурация хранилища

-   Сведения о файле узла

-   Журналы событий, включая события приложений, системные события, события Windows Server и Media Center

-   Сообщения диспетчера управления службами

-   События перезагрузки и Центра обновления Windows

-   Системные ошибки и ошибки приложений

## <a name="services-information-collected"></a>Собираемые сведения о службах

### <a name="server-services"></a>Службы сервера

-   Служба резервного копирования Windows Server клиентского компьютера

-   Поставщик службы резервного копирования Windows Server клиентского компьютера

-   Поставщик устройств Windows Server

-   Управление доменными именами Windows Server

-   Реестр поставщика службы Windows Server

-   Поставщик параметров Windows Server

-   Служба UPnP-устройств Windows Server

-   Поставщик средств удаленного администрирования Windows Server

-   Служба работоспособности Windows Server

-   Служба хранения данных Windows Server

-   Служба SQM Windows Server

### <a name="network-computer-services"></a>Службы сетевых компьютеров

-   Поставщик службы резервного копирования Windows Server клиентского компьютера

-   Служба работоспособности Windows Server

-   Реестр поставщика службы Windows Server

-   Служба SQM Windows Server

## <a name="logs-and-registry-information-collected"></a>Сбор сведений из журналов и реестров
 Для каждого указанного компьютера сети или сервера сборщик журналов собирает следующие сведения из журналов и реестра от сервера и компьютеров сети:

### <a name="server-logs-and-registry-information"></a>Сведения из журналов и реестра сервера

-   Журналы серверных продуктов, с <папка ProgramData \> \Микрософт\виндовс сервер\логс

-   Запланированные задачи

-   Журналы API установки

-   Журналы центра обновления Windows

-   Файл оповещений о работоспособности

-   Файл сведений об устройствах

-   Файл журнала архивации сервера

-   Файл журнала Panther

-   Службы

-   Разделы реестра из

    -   \\\ HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\

    -   \\\ HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DevicesProviderSvc

    -   \\\ HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DomainManagerProviderSvc

### <a name="network-computer-logs-and-registry-information"></a>Сведения из журналов и реестра компьютеров сети

-   Журналы продуктов для сетевого компьютера в <папка ProgramData \> \Микрософт\виндовс сервер\логс

-   Файл оповещений о работоспособности в <папка ProgramData \> \Микрософт\виндовс сервер\дата

-   Журналы центра обновления Windows

-   Журналы API установки

-   Сведения о запланированных задачах

-   Разделы реестра от \\ \ HKEY_LOCAL_MACHINE \Софтваре\микрософт\виндовс Server \

## <a name="logs-for-computers-that-do-not-run-a-version-of-the-windows-operating-system"></a>Журналы компьютеров, которые работают не под управлением ОС Windows
 Сборщик журналов не собирает файлы журналов с компьютеров, которые работают не под управлением ОС Windows. При использовании компьютеров, работающих под управлением ОС, отличной от Windows, вручную скопируйте следующие файлы журналов в ту же папку, где хранятся файлы сборщика журналов:

-   System.log

-   Library/Logs/Windows Server.log

-   Библиотека/журналы/Крашрепортер/панель запуска — <nnn \> (копирование всех файлов панели запуска-<nnn \> . Crash)

-   Библиотека/журналы/Диагностикрепортс/панель запуска — <nnn \> (копирование всех файлов панели запуска-<nnn \> . Crash)

## <a name="see-also"></a>См. также раздел

-   [Устранение неполадок сборщика журналов](../support/Troubleshoot-Windows-Server-Essentials-Log-Collector-Errors.md)

