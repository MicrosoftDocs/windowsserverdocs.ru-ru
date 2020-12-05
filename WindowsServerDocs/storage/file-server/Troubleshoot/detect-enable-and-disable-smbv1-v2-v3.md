---
title: Как обнаруживать, включать и отключать SMBv1, SMB и SMBv3 в Windows
description: Описание включения и отключения протокола SMB (SMBv1, SMB и SMBv3) в клиентских и серверных средах Windows.
author: Deland-Han
manager: dcscontentpm
ms.topic: how-to
ms.author: delhan
ms.date: 10/29/2020
ms.custom: contperfq2
ms.openlocfilehash: e38bbc5a80f80747ae3cb90c91123d91ed4e5e25
ms.sourcegitcommit: 28b5ab74cb0b40539ccc1a83998d6391e87fe51f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2020
ms.locfileid: "96614956"
---
# <a name="how-to-detect-enable-and-disable-smbv1-smbv2-and-smbv3-in-windows"></a>Как обнаруживать, включать и отключать SMBv1, SMB и SMBv3 в Windows

>Область применения: Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этой статье описывается, как включить и отключить протокол SMB версии 1 (SMBv1), SMB версии 2 (SMB) и SMB версии 3 (SMBv3) на клиентских и серверных компонентах SMB.

Хотя отключение или удаление SMBv1 может вызвать некоторые проблемы совместимости со старыми компьютерами или программами, SMBv1 имеет существенные уязвимости, и [мы настоятельно рекомендуем не использовать ее](https://techcommunity.microsoft.com/t5/storage-at-microsoft/stop-using-smb1/ba-p/425858).

## <a name="disabling-smbv2-or-smbv3-for-troubleshooting"></a>Отключение SMB или SMBv3 для устранения неполадок

Хотя мы рекомендуем использовать протоколы SMB 2.0 и SMBv3, может оказаться полезным временно отключить их для устранения неполадок, как описано в статье [Обнаружение состояния, включение и отключение протокола SMB на сервере SMB](detect-enable-and-disable-smbv1-v2-v3.md#how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-server).

В Windows 10, Windows 8.1 и Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 и Windows Server 2012 отключение SMBv3 деактивирует следующие функции (а также функции 2.0, описанные в предыдущем списке):

- Прозрачная отработка отказа — клиенты повторно подключаются без прерывания узлов кластера во время обслуживания или отработки отказа
- Scale Out — одновременный доступ к общим данным на всех узлах кластеров файлов 
- Многоканальное агрегирование пропускной способности сети и отказоустойчивости при наличии нескольких путей между клиентом и сервером
- SMB Direct — добавляет поддержку сети RDMA для очень высокой производительности с низкой задержкой и низкой загрузкой ЦП.
- Шифрование — обеспечивает сквозное шифрование и защищает от перехвата в ненадежных сетях.
- Аренда каталога — улучшает время отклика приложений в филиалах за счет кэширования
- Оптимизация производительности — оптимизация для небольшого случайного чтения и записи ввода-вывода

В Windows 7 и Windows Server 2008 R2 отключение SMB отключает следующие функциональные возможности.

- Составной запрос — позволяет отправлять несколько запросов SMB 2 в виде одного сетевого запроса.
- Большие операции чтения и записи — лучшее использование более быстрых сетей.
- Кэширование свойств папок и файлов — клиенты сохраняют локальные копии папок и файлов
- Устойчивые дескрипторы. разрешение на прозрачное повторное подключение к серверу при наличии временного отключения
- Улучшенная подпись сообщения — HMAC SHA-256 заменяет MD5 как алгоритм хеширования
- Улучшенная масштабируемость общего доступа к файлам — число пользователей, общих папок и открытых файлов на сервере значительно увеличилось.
- Поддержка символьных ссылок
- Модель нежесткой аренды клиента — ограничивает данные, передаваемые между клиентом и сервером, повышая производительность в сетях с высокой задержкой и повышая масштабируемость сервера SMB.
- Поддержка большого MTU — для полного использования 10-гигабе (ГБ) Ethernet
- Повышение эффективности энергопотребления — клиенты, которые имеют открытые файлы на сервере, могут перейти в спящий режим

Протокол SMB был впервые появился в Windows Vista и Windows Server 2008, а протокол SMBv3 появился в Windows 8 и Windows Server 2012. Дополнительные сведения о возможностях протоколов SMB 2.0 и SMBv3 см. в следующих статьях:

[Общие сведения о протоколе SMB](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831795(v=ws.11))

[Новые возможности SMB](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff625695(v=ws.10))

## <a name="how-to-remove-smb-v1"></a>Удаление SMB v1

Вот как можно удалить SMBv1 в Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016 и Windows 2012 R2.

#### <a name="powershell-methods"></a>Методы PowerShell

##### <a name="smb-v1-client-and-server"></a>SMB v1 (клиент и сервер)

- Автоматическое

  ```PowerShell
  Get-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

- Включен

  ```PowerShell
  Disable-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

- Включите параметр

  ```PowerShell
  Enable-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

#### <a name="windows-server-2012-r2-windows-server-2016-windows-server-2019-server-manager-method-for-disabling-smb"></a>Windows Server 2012 R2, Windows Server 2016, Windows Server 2019: диспетчер сервера метод отключения SMB

##### <a name="smb-v1"></a>SMB v1

![Диспетчер сервера — метод панели мониторинга](media/detect-enable-and-disable-smbv1-v2-v3-1.png)

#### <a name="windows-81-and-windows-10-powershell-method"></a>Windows 8.1 и Windows 10: метод PowerShell

##### <a name="smb-v1-protocol"></a>Протокол SMB v1

- Автоматическое

  ```PowerShell
  Get-WindowsOptionalFeature –Online –FeatureName SMB1Protocol
  ```

- Включен

  ```PowerShell
  Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
  ```

- Включите параметр

  ```PowerShell
  Enable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
  ```

##### <a name="smb-v2v3-protocol-only-disables-smb-v2v3-server"></a>Протокол SMB V2/V3 (отключается только сервер SMB V2/V3)

- Автоматическое

  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- Включен

  ```PowerShell
  Set-SmbServerConfiguration –EnableSMB2Protocol $false
  ```

- Включите параметр

  ```PowerShell
  Set-SmbServerConfiguration –EnableSMB2Protocol $true
  ```

#### <a name="windows-81-and-windows-10-add-or-remove-programs-method"></a>Windows 8.1 и Windows 10: метод "Установка и удаление программ"

![Клиентский метод Add-Remove Programs](media/detect-enable-and-disable-smbv1-v2-v3-2.png)

## <a name="how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-server"></a>Как определить состояние, включить и отключить протоколы SMB на сервере SMB

### <a name="for-windows-8-and-windows-server-2012"></a>Для Windows 8 и Windows Server 2012

Windows 8 и Windows Server 2012 представляют новый командлет Windows PowerShell **Set-смбсерверконфигуратион** . Командлет позволяет включать или отключать протоколы SMBv1, SMB и SMBv3 на серверном компоненте. 

> [!NOTE]
> При включении или отключении протоколов SMB в Windows 8 или Windows Server 2012 также включается или отключается SMBv3. Это происходит из-за того, что эти протоколы используют один и тот же стек.

После запуска командлета **Set-смбсерверконфигуратион** перезагружать компьютер не требуется.

##### <a name="smb-v1-on-smb-server"></a>SMB v1 на SMB Server

- Автоматическое

  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB1Protocol
  ```

- Включен

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB1Protocol $false
  ```

- Включите параметр
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB1Protocol $true
  ```

Дополнительные сведения см. [в статье хранилище сервера в корпорации Майкрософт](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Stop-using-SMB1/ba-p/425858).
##### <a name="smb-v2v3-on-smb-server"></a>SMB V2/V3 на SMB-сервере

- Автоматическое

  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- Включен

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $false
  ```

- Включите параметр

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $true
  ```

### <a name="for-windows-7-windows-server-2008-r2-windows-vista-and-windows-server-2008"></a>Для Windows 7, Windows Server 2008 R2, Windows Vista и Windows Server 2008

Чтобы включить или отключить протоколы SMB на сервере SMB под управлением Windows 7, Windows Server 2008 R2, Windows Vista или Windows Server 2008, используйте Windows PowerShell или редактор реестра.

#### <a name="powershell-methods"></a>Методы PowerShell

> [!NOTE]
> Для этого метода требуется PowerShell 2,0 или более поздней версии PowerShell.

##### <a name="smb-v1-on-smb-server"></a>SMB v1 на SMB Server

Автоматическое

```PowerShell
Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath}
```

Конфигурация по умолчанию — включено (раздел реестра не создается), поэтому значение SMB1 не будет возвращено.

Включен

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 0 –Force
```

Включите параметр

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 1 –Force
```

**Примечание** . После внесения этих изменений необходимо перезагрузить компьютер.
Дополнительные сведения см. [в статье хранилище сервера в корпорации Майкрософт](https://techcommunity.microsoft.com/t5/storage-at-microsoft/stop-using-smb1/ba-p/425858).
##### <a name="smb-v2v3-on-smb-server"></a>SMB V2/V3 на SMB-сервере

Автоматическое

```PowerShell
Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath}
```

Включен

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 0 –Force
```

Включите параметр

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 1 –Force
```

> [!NOTE]
> После внесения этих изменений необходимо перезагрузить компьютер.

#### <a name="registry-editor"></a>Редактор реестра

> [!IMPORTANT]
> Внимательно выполните действия, описанные в этом разделе. Неправильное изменение реестра может привести к серьезным проблемам. Перед внесением изменений [создайте резервную копию реестра для его восстановления](https://support.microsoft.com/help/322756) в случае возникновения проблем.

Чтобы включить или отключить SMBv1 на сервере SMB, настройте следующий раздел реестра:

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters**

```
Registry entry: SMB1
REG_DWORD: 0 = Disabled
REG_DWORD: 1 = Enabled
Default: 1 = Enabled (No registry key is created)
```

Чтобы включить или отключить протокол SMB 2.0 на сервере SMB, настройте следующий раздел реестра:

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters**

```
Registry entry: SMB2
REG_DWORD: 0 = Disabled
REG_DWORD: 1 = Enabled
Default: 1 = Enabled (No registry key is created)
```

> [!NOTE]
> После внесения этих изменений необходимо перезагрузить компьютер.

## <a name="how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-client"></a>Как определить состояние, включить и отключить протоколы SMB на клиенте SMB

### <a name="for-windows-vista-windows-server-2008-windows-7-windows-server-2008-r2-windows-8-and-windows-server-2012"></a>Для Windows Vista, Windows Server 2008, Windows 7, Windows Server 2008 R2, Windows 8 и Windows Server 2012

> [!NOTE]
> При включении или отключении SMB 2.0 в Windows 8 или Windows Server 2012 также включается или отключается SMBv3. Это происходит из-за того, что эти протоколы используют один и тот же стек.

##### <a name="smb-v1-on-smb-client"></a>SMB v1 на клиенте SMB

- Определение

  ```cmd
  sc.exe qc lanmanworkstation
  ```

- Включен

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb20/nsi
  sc.exe config mrxsmb10 start= disabled
  ```

- Включите параметр

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
  sc.exe config mrxsmb10 start= auto
  ```

Дополнительные сведения см. [в статье хранилище сервера в корпорации Майкрософт](https://techcommunity.microsoft.com/t5/storage-at-microsoft/stop-using-smb1/ba-p/425858) .
##### <a name="smb-v2v3-on-smb-client"></a>SMB V2/V3 на клиенте SMB

- Автоматическое

  ```cmd
  sc.exe qc lanmanworkstation
  ```

- Включен

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/nsi
  sc.exe config mrxsmb20 start= disabled
  ```

- Включите параметр

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
  sc.exe config mrxsmb20 start= auto
  ```

> [!NOTE]
> - Эти команды необходимо выполнить в командной строке с повышенными привилегиями.
> - После внесения этих изменений необходимо перезагрузить компьютер.


## <a name="disable-smbv1-server-with-group-policy"></a>Отключение сервера SMBv1 с групповая политика

Эта процедура настраивает следующий новый элемент в реестре:

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters**

- Запись реестра: **SMB1**
- REG_DWORD: **0** = отключено

Чтобы настроить это с помощью групповая политика, выполните следующие действия.

1. Откройте **Консоль управления групповыми политиками**. Щелкните правой кнопкой мыши объект групповой политики (GPO), который должен содержать новый элемент настройки, а затем щелкните **Изменить**.

2. В дереве консоли в разделе **Конфигурация компьютера** **разверните папку настройки** , а затем разверните папку **Параметры Windows** .

3. Щелкните правой кнопкой мыши узел **реестра** , наведите указатель на пункт **создать** и выберите пункт **Реестр**.

   ![Реестр — новый элемент реестра](media/detect-enable-and-disable-smbv1-v2-v3-3.png)

В диалоговом окне « **Свойства нового реестра**» выберите следующие параметры.

- **Действие**: создать
- **Hive**: HKEY_LOCAL_MACHINE
- **Путь к ключу**: систем\куррентконтролсет\сервицес\ланмансервер\параметерс
- **Имя значения**: SMB1
- **Тип значения**: REG_DWORD
- **Данные значения**: 0

![Новые свойства реестра — общие сведения](media/detect-enable-and-disable-smbv1-v2-v3-4.png)

Это отключает серверные компоненты SMBv1. Этот групповая политика должен применяться ко всем необходимым рабочим станциям, серверам и контроллерам домена в домене.

> [!NOTE]
> [Фильтры WMI](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc947846(v=ws.10)) также можно настроить таким образом, чтобы исключить Неподдерживаемые операционные системы или выбранные исключения, например Windows XP.

> [!IMPORTANT]
> Будьте внимательны при внесении этих изменений на контроллерах домена, на которых устаревшие ОС Windows XP или Linux и сторонние системы (которые не поддерживают протоколы SMB или SMBv3) не нуждаются в доступе к SYSVOL или другим общим папкам, в которых отключен SMB v1.

## <a name="disable-smbv1-client-with-group-policy"></a>Отключение клиента SMBv1 с групповая политика

Чтобы отключить клиент SMBv1, необходимо обновить раздел реестра Services, чтобы отключить запуск **MRxSMB10** , а затем зависимость от **MRxSMB10** должна быть удалена из записи для **LanmanWorkstation** , чтобы ее можно было запустить нормально, не требуя запуска **MRxSMB10** .

При этом будут обновлены и заменены значения по умолчанию в следующих двух элементах реестра:

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\mrxsmb10**

Запись реестра: **Start** REG_DWORD: **4**= отключено

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation**

Запись реестра: **депендонсервице** REG_MULTI_SZ: **"Бовсер", "MRxSmb20", "NSI"**

> [!NOTE]
> Включенная по умолчанию MRxSMB10, которая теперь удалена как зависимость.

Чтобы настроить это с помощью групповая политика, выполните следующие действия.

1. Откройте **Консоль управления групповыми политиками**. Щелкните правой кнопкой мыши объект групповой политики (GPO), который должен содержать новый элемент настройки, а затем щелкните **Изменить**.

2. В дереве консоли в разделе **Конфигурация компьютера** **разверните папку настройки** , а затем разверните папку **Параметры Windows** .

3. Щелкните правой кнопкой мыши узел **реестра** , наведите указатель на пункт **создать** и выберите пункт **Реестр**.

4. В диалоговом окне « **Свойства нового реестра** » выберите следующие параметры.

   - **Действие**: обновление
   - **Hive**: HKEY_LOCAL_MACHINE
   - **Путь к ключу**: SYSTEM\CurrentControlSet\services\mrxsmb10
   - **Имя значения**: начало
   - **Тип значения**: REG_DWORD
   - **Данные значения**: 4

   ![Свойства запуска — общие сведения](media/detect-enable-and-disable-smbv1-v2-v3-5.png)

5. Затем удалите зависимость от **MRxSMB10** , который был только что отключен.

   В диалоговом окне « **Свойства нового реестра** » выберите следующие параметры.

   - **Действие**: Replace
   - **Hive**: HKEY_LOCAL_MACHINE
   - **Путь к ключу**: систем\куррентконтролсет\сервицес\ланманворкстатион
   - **Имя значения**: депендонсервице
   - **Тип значения**: REG_MULTI_SZ
   - **Данные значения**:
      - бовсер
      - MRxSmb20
      - NSI

   > [!NOTE]
   > Эти три строки не будут содержать маркеры (см. следующий снимок экрана).

   ![Свойства Депендонсервице](media/detect-enable-and-disable-smbv1-v2-v3-6.png)

   Значение по умолчанию включает в себя **MRxSMB10** во многих версиях Windows, поэтому, заменяя их строкой с несколькими значениями, она действует путем удаления **MRxSMB10** в качестве зависимости для **LanmanServer** и перехода от четырех значений по умолчанию к этим трем приведенным выше значениям.

   > [!NOTE]
   > При использовании консоль управления групповыми политиками не нужно использовать кавычки или запятые. Просто введите каждую запись в отдельные строки.

6. Перезапустите целевые системы, чтобы завершить отключение SMB v1.

### <a name="auditing-smbv1-usage"></a>Аудит использования SMBv1

Чтобы определить, какие клиенты пытаются подключиться к серверу SMB с помощью SMBv1, можно включить аудит в Windows Server 2016, Windows 10 и Windows Server 2019. Вы также можете проводить аудит в Windows 7 и Windows Server 2008 R2, если они установили обновление Май 2018 ежемесячно и в Windows 8, Windows 8.1, Windows Server 2012 и Windows Server 2012 R2, если они установили ежемесячное обновление за Июль 2017.

- Включите параметр

  ```PowerShell
  Set-SmbServerConfiguration –AuditSmb1Access $true
  ```

- Включен

  ```PowerShell
  Set-SmbServerConfiguration –AuditSmb1Access $false
  ```

- Автоматическое

  ```PowerShell
  Get-SmbServerConfiguration | Select AuditSmb1Access
  ```

Если включен аудит SMBv1, в журнале событий Микрософт-Виндовс-смбсервер\аудит появляется событие 3000, определяющее каждого клиента, который пытается подключиться с помощью SMBv1.

### <a name="summary"></a>Сводка

Если все параметры находятся в одном объекте групповая политика (GPO), групповая политика управления отображает следующие параметры.

![Редактор "Управление групповыми политиками"-Registry](media/detect-enable-and-disable-smbv1-v2-v3-7.png)

### <a name="testing-and-validation"></a>Тестирование и проверка

После настройки разрешите репликацию и обновление политики. При необходимости выполните команду **gpupdate/Force** из командной строки, а затем просмотрите целевые компьютеры, чтобы убедиться, что параметры реестра применены правильно. Убедитесь, что SMB V2 и SMB v3 работают для всех остальных систем в среде.

> [!NOTE]
> Не забудьте перезапустить целевые системы.
