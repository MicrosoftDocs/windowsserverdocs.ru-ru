---
title: Настройка параметров производительности файловых серверов
description: Настройка параметров производительности для файловых серверов под управлением Windows Server
ms.topic: article
author: phstee
ms.author: nedpyle; danlo; dkruse; v-tea
ms.date: 12/12/2019
manager: dcscontentpm
audience: Admin
ms.openlocfilehash: ecbd1bc751f133b80cf1d9cb264cf70a4ac4f47c
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992193"
---
# <a name="performance-tuning-for-file-servers"></a>Настройка параметров производительности файловых серверов

Следует правильно выбирать оборудование в соответствии с ожидаемой нагрузкой на файловый сервер и с учетом таких параметров, как средняя и пиковая нагрузка, емкость, планы развития и время отклика. Аппаратные ограничения снижают эффективность программной настройки.

## <a name="general-tuning-parameters-for-clients"></a>Общие параметры для настройки клиентов

Следующие параметры реестра REG\_DWORD могут влиять на производительность клиентских компьютеров, которые взаимодействуют с файловыми серверами SMB:

-   **ConnectionCountPerNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerNetworkInterface
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 и Windows Server 2012

    По умолчанию имеет значение 1, которое мы настоятельно рекомендуем использовать. Допускаются значения от 1 до 16. Максимальное число подключений к серверу по одному интерфейсу, отличающемуся от интерфейсов RSS.


-   **ConnectionCountPerRssNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerRssNetworkInterface
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 и Windows Server 2012

    По умолчанию имеет значение 4, которое мы настоятельно рекомендуем использовать. Допускаются значения от 1 до 16. Максимальное число подключений к серверу по одному интерфейсу RSS.

-   **ConnectionCountPerRdmaNetworkInterface**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\ConnectionCountPerRdmaNetworkInterface
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 и Windows Server 2012

    По умолчанию имеет значение 2, которое мы настоятельно рекомендуем использовать. Допускаются значения от 1 до 16. Максимальное число подключений к серверу по одному интерфейсу RDMA.

-   **MaximumConnectionCountPerServer**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\MaximumConnectionCountPerServer
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 и Windows Server 2012

    По умолчанию имеет значение 32. Допускаются значения от 1 до 64. Максимальное число подключений к серверу под управлением Windows Server 2012 по всем интерфейсам.

-   **DormantDirectoryTimeout**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantDirectoryTimeout
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 и Windows Server 2012

    По умолчанию имеет значение 600 секунд. Максимальное время, в течение которого сервер сохраняет открытыми дескрипторы каталогов с арендой каталогов.

-   **FileInfoCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheLifetime
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    Значение по умолчанию — 10 секунд. Срок хранения в кэше сведений о файлах.

-   **DirectoryCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheLifetime
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    Значение по умолчанию — 10 секунд. Обозначает срок хранения кэша каталогов.

    > [!NOTE]
    > Этот параметр управляет кэшированием метаданных каталогов при отсутствии аренды каталогов.

     > [!NOTE]
     > Известная проблема в Windows 10 версии 1803 влияет на возможность системы кэшировать большие каталоги. Обновив ОС компьютера до Windows 10 версии 1803, вы получите доступ к сетевой папке, содержащей тысячи файлов и папок. Вам потребуется открывать документ, расположенный в этой сетевой папке. Обе эти операции сопровождаются значительными задержками.
     >
     > Чтобы устранить эту проблему, установите Windows 10 версии 1809 или более поздней версии.
     >
     > Чтобы обойти эту проблему, задайте для параметра **DirectoryCacheLifetime** значение **0**.
     >
     > Эта проблема затрагивает следующие выпуски Windows 10:
     > - Windows 10 Enterprise версии 1803;
     > - Windows 10 Pro для рабочих станций версии 1803;
     > - Windows 10 Pro для образовательных учреждений версии 1803;
     > - Windows 10 Профессиональная версии 1803;
     > - Windows 10 для образовательных учреждений версии 1803;
     > - Windows 10 Домашняя версии 1803.

-   **DirectoryCacheEntrySizeMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntrySizeMax
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    По умолчанию имеет значение 64 КБ. Обозначает максимальный размер записей в кэше каталога.

-   **FileNotFoundCacheLifetime**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheLifetime
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    Значение по умолчанию — 5 секунд. Обозначает срок хранения в кэше данных об отсутствии файла.

-   **CacheFileTimeout**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\CacheFileTimeout
    ```

    Область применения: Windows 8.1, Windows 8, Windows Server 2012, Windows Server 2012 R2 и Windows 7

    Значение по умолчанию — 10 секунд. Этот параметр определяет время (в секундах), в течение которого перенаправитель сохраняет кэшированные данные о файле после закрытия в приложении последнего дескриптора для этого файла.

-   **DisableBandwidthThrottling**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableBandwidthThrottling
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    Значение по умолчанию — 0. По умолчанию перенаправитель SMB регулирует пропускную способность для сетевых подключений с высокой задержкой, что позволяет в некоторых случаях избежать превышения времени ожидания, связанного с сетью. Значение 1 для этого параметра реестра отключает такое регулирование, ускоряя передачу файлов через сетевые соединения с высокой задержкой.

-   **DisableLargeMtu**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DisableLargeMtu
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    По умолчанию имеет значение 0 только для Windows 8. В Windows 8 перенаправитель SMB передает полезные данные размером до 1 МБ на один запрос, ускоряя передачу файлов. Значение 1 для этого параметра ограничивает запросы размером 64 КБ. Следует тщательно оценить влияние этого параметра, прежде чем применять его.

-   **RequireSecuritySignature**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\RequireSecuritySignature
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    По умолчанию имеет значение 0 и отключает подписывание SMB. Значение 1 этого параметра включает подписывание SMB для всех взаимодействий по протоколу SMB, блокируя обмен данными по протоколу SMB с компьютерами, на которых отключено подписывание SMB. Подписывание SMB может повысить нагрузку на ЦП и замедлить круговые пути, но оно также блокирует атаки "злоумышленник в середине". Если подписывание SMB не требуется, этот параметр реестра должен иметь значение 0 на всех клиентах и серверах.

    См. подробнее о [подписывании SMB](/archive/blogs/josebda/the-basics-of-smb-signing-covering-both-smb1-and-smb2).

-   **FileInfoCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileInfoCacheEntriesMax
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    По умолчанию имеет значение 64. Допускаются значения от 1 до 65536. Это значение используется для определения объема метаданных файла, которые могут кэшироваться клиентом. Увеличение значения позволяет сократить сетевой трафик и повысить производительность, если осуществляется доступ к большому числу файлов.

-   **DirectoryCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DirectoryCacheEntriesMax
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    По умолчанию имеет значение 16. Допускаются значения от 1 до 4096. Это значение используется для определения объема сведений о каталогах, которые могут кэшироваться клиентом. Увеличение значения позволяет сократить сетевой трафик и повысить производительность, если осуществляется доступ к большому числу каталогов.

-   **FileNotFoundCacheEntriesMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\FileNotFoundCacheEntriesMax
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    По умолчанию имеет значение 128. Допускаются значения от 1 до 65536. Это значение используется для определения объема сведений об именах файлов, которые могут кэшироваться клиентом. Увеличение значения позволяет сократить сетевой трафик и повысить производительность, если осуществляется доступ к большому числу имен файлов.

-   **MaxCmds**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\MaxCmds
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    Значение по умолчанию — 15. Этот параметр ограничивает число ожидающих запросов в одном сеансе. Увеличение этого значения приводит к повышению использования памяти, но может повысить производительность благодаря использованию более глубокого конвейера запросов. Увеличение значения в сочетании с MaxMpxCt также позволяет устранить ошибки, возникающие из-за большого числа долгосрочных ожиданий по запросам файлов, таких как вызовы FindFirstChangeNotification. Этот параметр не влияет на подключение к серверам SMB 2.0.

-   **DormantFileLimit**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanWorkstation\Parameters\DormantFileLimit
    ```

    Область применения: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 и Windows Server 2008

    Значение по умолчанию — 1023. Этот параметр определяет максимальное число файлов, которые нужно оставить открытыми в общем ресурсе после того, как приложение закроет файл.

### <a name="client-tuning-example"></a>Пример настройки клиента

Общие параметры настройки для клиентских компьютеров позволяют оптимизировать доступ к удаленным файловым ресурсам, особенно в некоторых сетях с высокой задержкой (например, при подключениях между офисами филиалов, центрами обработки данных и домашними офисами, а также мобильных широкополосных подключениях). Предложенные значения не являются оптимальными и применимыми на всех компьютерах. Следует тщательно оценить влияние каждого параметра, прежде чем применять его.

| Параметр                   | Значение | Значение по умолчанию |
|-----------------------------|-------|---------|
| DisableBandwidthThrottling  | 1     | 0       |
| FileInfoCacheEntriesMax     | 32768 | 64      |
| DirectoryCacheEntriesMax    | 4096  | 16      |
| FileNotFoundCacheEntriesMax | 32768 | 128     |
| MaxCmds                     | 32768 | 15      |



Начиная с Windows 8, вы можете настроить многие из этих параметров SMB с помощью командлетов Windows PowerShell **Set-SmbClientConfiguration** и **Set-SmbServerConfiguration**. Кроме того, Windows PowerShell позволяет настраивать параметры, доступные только в реестре.

```
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecuritySignature -Value 0 -Force
```