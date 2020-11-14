---
title: Синтаксис и форматирование команд пктмон
description: Эта страница используется для понимания синтаксиса, команд, форматирования и выходных данных пктмон для сборок вибраниум Windows.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: 3e4c73af3b00f42301b34e59493f25b6d2ccb95c
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632660"
---
# <a name="pktmon-command-syntax-and-formatting"></a>Синтаксис и форматирование команд пктмон

>Область применения: Windows Server (половина ежегодного канала), Windows Server 2019, Windows 10, Azure Stack ХЦИ, центр Azure Stack, Azure

Монитор пакетов (Пктмон) — это встроенное средство диагностики сети для Windows. Он может использоваться для записи пакетов, обнаружения пакетов, фильтрации пакетов и подсчета. Этот инструмент особенно полезен в сценариях виртуализации, например в сетях контейнеров и SDN, так как он обеспечивает видимость сетевого стека. Монитор пакетов доступен в окне с помощью команды pktmon.exe в вибраниум OS (сборка 19041). С помощью этого раздела вы узнаете, как понять синтаксис пктмон, форматирование команд и выходные данные.

## <a name="quick-start"></a>Быстрый запуск

Чтобы приступить к работе в универсальных сценариях, выполните следующие действия.

1. Укажите тип пакетов, необходимых для записи, т. е. определенные IP-адреса, порты или протоколы, связанные с пакетом. Затем проверьте синтаксис для применения фильтров захвата и примените фильтры для пакетов, определенных на предыдущем шаге.

   ```PowerShell
   C:\Test> pktmon filter add help
   C:\Test> pktmon filter add <filters>
   ```

2. Запустите запись и включите ведение журнала пакетов.

   ```PowerShell
   C:\Test> pktmon start --etw
   ```

3. Воспроизведите проблему, которую следует диагностировать. Счетчики запросов для подтверждения наличия ожидаемого трафика и получения обобщенного представления о том, как трафик проходит на компьютере.

   ```PowerShell
   C:\Test> pktmon counters
   ```

4. Останавливает запись и получает журналы в формате txt для анализа.

   ```PowerShell
   C:\Test> pktmon stop
   C:\Test> pktmon format <etl file>
   ```

Инструкции по анализу выходных данных txt см. в разделе [анализ выходных данных монитора пакетов](#analyze-packet-monitor-output) .

## <a name="capture-filters"></a>Фильтры записи

Настоятельно рекомендуется применять фильтры перед запуском записи пакетов, так как устранение неполадок с подключением к определенному назначению упрощается при фокусе на одном потоке пакетов. Захват *всего* сетевого трафика может сделать вывод слишком бесшумным для анализа. Чтобы сообщить о пакете, он должен соответствовать всем условиям, указанным по крайней мере в одном фильтре. Одновременно поддерживается до 32 фильтров.

Например, следующий набор фильтров захватывает трафик ICMP с IP-адреса 10.0.0.10, а также любой трафик через порт 53.

```PowerShell
C:\Test> pktmon filter add -i 10.0.0.10 -t icmp
C:\Test> pktmon filter add -p 53
```

### <a name="filtering-capability"></a>Возможность фильтрации

- Монитор пакетов поддерживает фильтрацию по MAC-адресам, IP-адресам, портам, Есертипе, транспортному протоколу и идентификатору виртуальной ЛС. 

- Монитор пакетов не различает источник или назначение, когда дело доходит до MAC-адреса, IP-адреса или фильтров портов. 

- Для дальнейшей фильтрации пакетов TCP можно указать дополнительный список флагов TCP для сопоставления. Поддерживаемые флаги: FIN, SYN, RST, КОМАНДНОМ PSH, ACK, УРГ, ECE и КВР.

  - Например, следующий фильтр будет фиксировать все пакеты SYN, отправленные или полученные IP-адресом 10.0.0.10:

```PowerShell
C:\Test> pktmon filter add -i 10.0.0.10 -t tcp syn
```

- Монитор пакетов может применить фильтр к инкапсулированным внутренним пакетам в дополнение к внешнему пакету, если флаг [-e] был добавлен к любому фильтру. Поддерживаемые методы инкапсуляции: ВКСЛАН, GRE, NVGRE и IP-in-IP. Пользовательский порт ВКСЛАН является необязательным и по умолчанию равен 4789.

### <a name="pktmon-filters-syntax"></a>Синтаксис фильтров пктмон

```PowerShell
C:\Test> pktmon filter help
pktmon filter { list | add | remove } [OPTIONS | help]

Commands
    list      Display active packet filters.
    add       Add a filter to control which packets are reported.
    remove    Removes all filters.

help
    Show help text for a command.

C:\Test> pktmon filter add help
pktmon filter add <name> [-m mac [mac2]] [-v vlan] [-d { IPv4 | IPv6 | number }]
                         [-t { TCP [flags...] | UDP | ICMP | ICMPv6 | number }]
                         [-i ip [ip2]] [-p port [port2]] [-e [port]]
    Add a filter to control which packets are reported. For a packet to be
    reported, it must match all conditions specified in at least one filter.
    Up to 8 filters can be active at once.

    NOTE1: When two MACs (-m), IPs (-i), or ports (-p) are specified, the filter
           matches packets that contain both. It will not distinguish between source
           or destination for this purpose.

name
    Optional name or description of the filter.

Ethernet frame
    -m, --mac[-address]
        Match source or destination MAC address. See NOTE1 above.

    -v, --vlan
        Match by VLAN Id (VID) in the 802.1Q header.

    -d, --data-link[-protocol], --ethertype
        Match by data link (layer 2) protocol. Can be IPv4, IPv6, ARP, or
        a protocol number.

IP header
    -t, --transport[-protocol], --ip-protocol
        Match by transport (layer 4) protocol. Can be TCP, UDP, ICMP, ICMPv6, or
        a protocol number.
        To further filter TCP packets, an optional list of TCP flags to match can
        be provided. Supported flags are FIN, SYN, RST, PSH, ACK, URG, ECE, and CWR.

    -i, --ip[-address]
        Match source or destination IP address. See NOTE1 above.
        To match by subnet, use CIDR notation with the prefix length.

TCP/UDP header
    -p, --port
        Match source or destination port number. See NOTE1 above.

Encapsulation
    -e, --encap
        This filter also applies to encapsulated inner packets, in addition to the outer
        packet. Supported encapsulation methods are VXLAN, GRE, NVGRE, and IP-in-IP.
        Custom VXLAN port is optional, and defaults to 4789.

Example 1: Ping filter
        pktmon filter add MyPing -i 10.10.10.10 -t ICMP

Example 2: TCP SYN filter for SMB traffic
    pktmon filter add MySmbSyn -i 10.10.10.10 -t TCP SYN -p 445

Example 3: Subnet filter
    pktmon filter add MySubnet -i 10.10.10.0/24
```

## <a name="packet-capture-and-logging"></a>Запись пакетов и ведение журнала

Монитор пакетов может записывать сетевой трафик с ведением журнала пакетов или без него. Дополнительные сведения о захвате трафика без ведения журнала пакетов см. в разделе счетчики пакетов ниже. Чтобы записывать и записывать в журнал пакеты, добавьте параметр **[--ETW]** в команду Start.

Выберите компоненты для отслеживания с помощью параметра **[-c]** . Это могут быть все компоненты, только сетевые карты или список идентификаторов компонентов. Значение по умолчанию — записывать трафик для всех компонентов. Отслеживать пропущенные пакеты только с помощью параметра [-d]. Значение по умолчанию — захват передаваемых и пропущенных пакетов.

Например, следующая команда будет записывать счетчики пакетов для всех сетевых адаптеров, не записывая в журнал пакеты:

```PowerShell
C:\Test> pktmon start -c nics
```

Однако следующая команда захватывает только удаленные пакеты, которые проходят через компоненты 4 и 5, и записывает их в журнал:

```PowerShell
C:\Test> pktmon start --etw -c 4,5 -d
```

### <a name="packet-logging-capability"></a>Возможность ведения журнала пакетов

- Монитор пакетов поддерживает несколько режимов ведения журнала:

  - Циклический: новые пакеты перезапишут самые старые при достижении максимального размера файла. Это режим ведения журнала по умолчанию.
  - Несколько файлов: при достижении максимального размера файла создается новый файл журнала. Файлы журнала нумеруются последовательно: PktMon1. ETL, PktMon2. ETL и т. д. Примените этот режим ведения журнала, чтобы сохранить весь журнал, но будьте осторожны при использовании хранилища. Примечание. Используйте метку времени создания файла для каждого файла журнала в качестве указания на заданный промежуток времени в записи.
  - Реальное время: пакеты отображаются на экране в режиме реального времени. Файл журнала не создается. Нажмите клавиши CTRL + C, чтобы прерывать наблюдение.
  - Память: события записываются в буфер кольцевой памяти. Размер буфера задается с помощью параметра **[-s]** . Содержимое буфера записывается в файл журнала после остановки записи. Используйте этот режим ведения журнала для очень шумных сценариев, чтобы захватывать огромный объем трафика за очень короткий промежуток времени в буфере памяти. При использовании любого другого режима ведения журнала может потеряться часть трафика.

- Укажите объем пакета для записи в параметр **[-p]** . Заносить в журнал весь пакет каждого пакета независимо от его размера, присвоив этому параметру значение 0. Значение по умолчанию — 128 байт, которое должно включать заголовки большинства пакетов.

- Укажите размер файла журнала с помощью параметра **[-s]** . Это будет максимальный размер файла в циклической записи, прежде чем монитор пакетов начнет перезаписывать старые пакеты с новыми. Это также будет максимальный размер каждого файла в многофайлового режима ведения журнала перед тем, как монитор пакетов создаст новый файл для записи следующих пакетов. С помощью этого параметра можно также задать размер буфера для режима ведения журнала в памяти.

### <a name="pktmon-start-syntax"></a>Синтаксис пктмон Start

```PowerShell
C:\Test> pktmon start help
pktmon start [-c { all | nics | [ids...] }] [-d] [--etw [-p size] [-k keywords]]
             [-f] [-s] [--log-mode {circular | multi-file | real-time | memory}]
    Start packet monitoring.

-c, --components
    Select components to monitor. Can be all components, NICs only, or a
    list of component ids. Defaults to all.

-d, --drop-only
    Only report dropped packets. By default, successful packet propagation
    is reported as well.

ETW Logging
    --etw
        Start a logging session for packet capture.

    -p, --packet-size
        Number of bytes to log from each packet. To always log the entire
        packet, set this to 0. Default is 128 bytes.

    -k, --keywords
        Hexadecimal bitmask (i.e. sum of the below flags) that controls
        which events are logged. Default is 0x012.

        Flags:
        0x001 - Internal Packet Monitor errors.
        0x002 - Information about components, counters and filters.
                This information is added to the end of the log file.
        0x004 - Source and destination information for the first
                packet in NET_BUFFER_LIST group.
        0x008 - Select packet metadata from NDIS_NET_BUFFER_LIST_INFO
                enumeration.
        0x010 - Raw packet, truncated to the size specified in
                [--packet-size] parameter.

    -f, --file-name
        .etl log file. Default is PktMon.etl.

    -s, --file-size
        Maximum log file size in megabytes. Default is 512 MB.

    -l, --log-mode
        Select logging mode. Default is circular.

        circular
            New events overwrite the oldest ones when
            when the maximum file size is reached.

        multi-file
            A new log file is created when the maximum file size is reached.
            Log files are sequentially numbered. PktMon1.etl, PktMon2.etl, etc.

        real-time
            Display events and packets on screen at real time. No log file is created.
            Press Ctrl+C to stop monitoring.

        memory
            Events are written to a circular memory buffer.
            Buffer size is specified in [--file-size] parameter.
            Buffer contents is written to a log file during stop operation.

Example: pktmon start --etw -l real-time
```

## <a name="packet-analysis-and-formatting"></a>Анализ пакетов и форматирование

Монитор пакетов создает файлы журнала в формате ETL. Существует несколько способов форматирования ETL-файла для анализа.

- Преобразуйте журнал в текстовый формат (параметр по умолчанию) и проанализируйте его с помощью текстового редактора, например TextAnalysisTool.NET. Данные пакетов будут отображаться в формате TCPDump. Следуйте указаниям ниже, чтобы узнать, как анализировать выходные данные в текстовом файле.
- Преобразование журнала в формат пкапнг для анализа с помощью [Wireshark](pktmon-pcapng-support.md)*
- Откройте ETL-файл с [сетевой монитор](pktmon-netmon-support.md)*

>[!NOTE]
>* Используйте гиперссылки выше, чтобы узнать, как анализировать и анализировать журналы монитора пакетов в **Wireshark** и **сетевой монитор**.

### <a name="pktmon-format-syntax"></a>Синтаксис формата пктмон

```PowerShell
C:\Test> pktmon format help
pktmon format log.etl [-o log.txt] [-b] [-v [level]] [-x] [-e] [-l [port]
    Convert log file to text format.

-o, --out
    Name of the formatted text file.

-s, --stats-only
    Display log file statistical information.

Network packet formatting options

    -b, --brief
        Abbreviated packet format.

    -v, --verbose
        Verbosity level [1..3].

    -x, --hex
        Hexadecimal format.

    -e, --no-ethernet
        Don't print ethernet header.

    -l, --vxlan
        Custom VXLAN port.


Example: pktmon format C:\tmp\PktMon.etl

C:\Test> pktmon pcapng help
pktmon pcapng log.etl [-o log.pcapng]
    Convert log file to pcapng format.
    Dropped packets are not included by default.

-o, --out
    Name of the formatted pcapng file.

-d, --drop-only
    Convert dropped packets only.

-c, --component-id
    Filter packets by a specific component ID.

Example: pktmon pcapng C:\tmp\PktMon.etl -d -c nics
```

### <a name="analyze-packet-monitor-output"></a>Анализ выходных данных монитора пакетов

Монитор пакетов фиксирует моментальный снимок пакета каждым компонентом сетевого стека. Соответственно, будет существовать несколько моментальных снимков каждого пакета (представленного на изображении ниже синим полем).
Каждый из этих моментальных снимков пакетов представлен рядом строк (красного и зеленого прямоугольников). Существует по крайней мере одна строка, содержащая некоторые данные о экземпляре пакета, начиная с метки времени. Сразу после этого по крайней мере одна строка (Полужирная на рисунке ниже) показывает проанализированный необработанный пакет в текстовом формате (без метки времени); Это может быть несколько строк, если пакет инкапсулирован, как и пакет в зеленом поле.

<center>

:::image type="content" source="media/pktmon-log-example.png" alt-text="Пример выходных данных журнала пакета мониторинга пакетов" border="false":::

</center>

Для сопоставления всех моментальных снимков одних и тех же пакетов отслеживайте значения Пктграупид и Пктнумбер (выделены желтым цветом). все моментальные снимки одного пакета должны иметь два общих значения. Значение внешнего вида (выделенное синим цветом) выступает в качестве счетчика для каждого последующего моментального снимка того же пакета. Например, первый моментальный снимок пакета (где пакет впервые появился в сетевом стеке) имеет значение 1 для внешнего вида, следующий моментальный снимок имеет значение 2 и т. д.

Каждый снимок пакета имеет идентификатор компонента (подчеркнутый на изображении выше), обозначающий компонент, связанный с моментальным снимком. Чтобы разрешить имя компонента и параметры, найдите этот идентификатор компонента в списке компонентов в нижней части файла журнала. Часть таблицы Components показана на рисунке ниже, в котором выделяется «компонент 1» в желтом цвете (это компонент, в котором был захвачен последний снимок выше).
Компоненты с 2 краями будут сообщать 2 моментальных снимка на каждом крае (например, моментальные снимки с внешним видом 3 и внешним видом 4).

В нижней части каждого файла журнала представлен список фильтров, как показано на рисунке ниже (выделяется синим цветом). Каждый фильтр отображает указанные параметры (протокол ICMP в примере ниже) и нули для остальных параметров.

<center>

:::image type="content" source="media/pktmon-log-example-components.png" alt-text="Пример выходных компонентов журнала пакета мониторинга пакетов":::

</center>

Для пропущенных пакетов слово «Drop» появляется перед любой из строк, представляющих моментальный снимок, в котором был удален пакет. Каждый отброшенный пакет также предоставляет значение Дропреасон. Этот параметр Дропреасон предоставляет краткое описание причины удаления пакета; Например, несоответствие MTU, отфильтрованная виртуальная ЛС и т. д.

<center>

:::image type="content" source="media/dropped-packet-log-example.png" alt-text="Пример журнала отброшенных пакетов":::

</center>

## <a name="packet-counters"></a>Счетчики пакетов

Счетчики монитора пакетов обеспечивают общее представление сетевого трафика по всему сетевому стеку без необходимости анализировать журнал, что может быть дорогостоящим процессом. Изучите шаблоны трафика, запросив счетчики пакетов с помощью **счетчиков пктмон** после запуска записи монитора пакетов. Сбросьте счетчики в ноль с помощью **пктмон Reset** или отключите мониторинг совместно с помощью **пктмон**.

- Счетчики упорядочиваются с помощью привязок с сетевыми адаптерами в верхней части и с помощью протоколов внизу.
- TX/RX: счетчики разделяются на два столбца для направлений отправки (TX) и приема (RX).  
- Края: компоненты сообщают о распространении пакетов, когда пакет пересекает границу компонента (EDGE). Каждый компонент может иметь один или несколько краев. Драйверы минипорта обычно имеют один верхний край, протоколы имеют один нижний край, а драйверы фильтров имеют верхние и нижние края.  
- Падения: счетчики сброса пакетов включаются в одну и ту же таблицу.

В следующем примере был запущен новый захват, а затем команда **пктмон Counters** использовалась для запроса счетчиков до остановки записи. Счетчики показывают один пакет, который делает его выходом из сетевого стека, начиная от уровня протокола до физического сетевого адаптера, и его ответ возвращается в другом направлении. Если проверка связи или ответ отсутствовали, это легко определить с помощью счетчиков.

<center>

:::image type="content" source="media/pktmon-counters-with-perfect-flow.png" alt-text="Пример счетчика пакетов с точным потоком" border="false":::

</center>

В следующем примере в столбце "Counter" отображаются сведения о падении. Получение последней причины сброса для каждого компонента путем запроса данных счетчиков в формате JSON с помощью **счетчиков пктмон--JSON** или анализа выходного журнала для получения более подробных сведений.

<center>

:::image type="content" source="media/pktmon-counters-drop-example.png" alt-text="Пример счетчика пакетов с удаленным пакетом" border="false":::

</center>

Как показано в этих примерах, счетчики могут предоставить большой объем информации через диаграмму, которая может быть проанализирована простым поиском.

### <a name="pktmon-counters-syntax"></a>Синтаксис счетчиков пктмон

```PowerShell
C:\Test> pktmon counters help
pktmon [comp] counters [-t { all | drop | flow }] [-z] [--json]
    Display current per-component counters.

-t, --counter-type
    Select which types of counters to show.
    Supported values are all counters (default), drops only, or flows only.

-z, --show-zeros
    Show counters that are zero in both directions.

-i, --show-hidden
    Show components that are hidden by default.

--json
    Output the counters in JSON format.
```

## <a name="networking-stack-layout"></a>Макет сетевого стека

Изучите структуру сетевого стека с помощью команды **пктмон List**.

:::image type="content" source="media/pktmon-networking-stack-example.png" alt-text="Пример макета сетевого стека" border="false":::

Команда отображает сетевые компоненты (драйверы), упорядоченные по привязкам адаптеров.

Типичная привязка состоит из следующих компонентов:

- Один сетевой адаптер (NIC);
- Несколько (возможно, нуль) драйверов фильтров
- Один или несколько драйверов протоколов (TCP/IP или другие)

Каждый компонент однозначно идентифицируется ИДЕНТИФИКАТОРом компонента монитора пакетов, который используется для наблюдения за отдельными компонентами.

>[!NOTE]
>Идентификаторы не являются постоянными и могут изменяться при перезагрузках, а также при перезапуске драйвера для монитора пакетов.

### <a name="pktmon-list-syntax"></a>Синтаксис списка пктмон

```powershell
C:\Test> pktmon list help
pktmon [comp] list
    List all active components.

-i, --show-hidden
    Show components that are hidden by default.

--json
    Output the list in JSON format.
```