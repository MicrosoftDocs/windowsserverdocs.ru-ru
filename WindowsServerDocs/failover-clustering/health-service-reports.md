---
title: Отчеты служба работоспособности
manager: eldenc
ms.author: cosdar
ms.topic: article
author: cosmosdarwin
ms.date: 10/05/2017
ms.openlocfilehash: 1e6b11bc73ef34e5247ca43140d3e2122e77ab61
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990784"
---
# <a name="health-service-reports"></a>Отчеты служба работоспособности

> Применяется к: Windows Server 2019, Windows Server 2016

## <a name="what-are-reports"></a>Что такое отчеты

Служба работоспособности сокращает объем работы, необходимый для получения сведений о производительности и емкости из кластера Локальные дисковые пространства. Один новый командлет предоставляет проверенный список необходимых метрик, которые эффективно собираются и объединяются динамически на узлах с помощью встроенной логики для обнаружения членства в кластере. Все значения предоставляются только в режиме реального времени по состоянию на конкретный момент.

## <a name="usage-in-powershell"></a>Использование в PowerShell

Используйте этот командлет для получения метрик для всего кластера Локальные дисковые пространства:

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport
```

Параметр необязательный **Счетчик** указывает количество возвращаемых наборов значений с интервалом в одну секунду.

```PowerShell
Get-StorageSubSystem Cluster* | Get-StorageHealthReport -Count <Count>
```

Вы также можете получить метрики для одного конкретного тома или сервера:

```PowerShell
Get-Volume -FileSystemLabel <Label> | Get-StorageHealthReport -Count <Count>

Get-StorageNode -Name <Name> | Get-StorageHealthReport -Count <Count>
```

## <a name="usage-in-net-and-c"></a>Использование в .NET и C #

### <a name="connect"></a>Подключить

Чтобы запросить служба работоспособности, необходимо будет установить **CimSession** с кластером. Для этого вам потребуются некоторые вещи, которые доступны только в полной среде .NET. Это означает, что вы не можете сделать это непосредственно из веб-приложения или с мобильных приложений. В этих примерах кода будет использоваться язык C \# , самый простой выбор для этого уровня доступа к данным.

```
using System.Security;
using Microsoft.Management.Infrastructure;

public CimSession Connect(string Domain = "...", string Computer = "...", string Username = "...", string Password = "...")
{
    SecureString PasswordSecureString = new SecureString();
    foreach (char c in Password)
    {
        PasswordSecureString.AppendChar(c);
    }

    CimCredential Credentials = new CimCredential(
        PasswordAuthenticationMechanism.Default, Domain, Username, PasswordSecureString);
    WSManSessionOptions SessionOptions = new WSManSessionOptions();
    SessionOptions.AddDestinationCredentials(Credentials);
    Session = CimSession.Create(Computer, SessionOptions);
    return Session;
}
```

Указанное имя пользователя должно быть локальным администратором конечного компьютера.

Рекомендуется создавать **SecureString** с паролем непосредственно из входных данных пользователя в режиме реального времени, поэтому пароль никогда не хранится в памяти в виде открытого текста. Это помогает устранить различные проблемы безопасности. Но на практике его создание, как и раньше, является общим для целей создания прототипов.

### <a name="discover-objects"></a>Обнаружение объектов

После установки **CimSession** можно запросить инструментарий управления Windows (WMI) (WMI) в кластере.

Прежде чем можно будет получить ошибки или метрики, необходимо получить экземпляры нескольких соответствующих объектов. Во первых, **MSFT \_ сторажесубсистем** , представляющий Локальные дисковые пространства в кластере. Используя это, вы можете получить все ** \_ стораженодеы MSFT** в кластере и каждый ** \_ том MSFT**, тома данных. Наконец, вам потребуется ** \_ сторажехеалс MSFT**, а также сам служба работоспособности.

```
CimInstance Cluster;
List<CimInstance> Nodes;
List<CimInstance> Volumes;
CimInstance HealthService;

public void DiscoverObjects(CimSession Session)
{
    // Get MSFT_StorageSubSystem for Storage Spaces Direct
    Cluster = Session.QueryInstances(@"root\microsoft\windows\storage", "WQL", "SELECT * FROM MSFT_StorageSubSystem")
        .First(Instance => (Instance.CimInstanceProperties["FriendlyName"].Value.ToString()).Contains("Cluster"));

    // Get MSFT_StorageNode for each cluster node
    Nodes = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToStorageNode", null, "StorageSubSystem", "StorageNode").ToList();

    // Get MSFT_Volumes for each data volume
    Volumes = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToVolume", null, "StorageSubSystem", "Volume").ToList();

    // Get MSFT_StorageHealth itself
    HealthService = Session.EnumerateAssociatedInstances(Cluster.CimSystemProperties.Namespace,
        Cluster, "MSFT_StorageSubSystemToStorageHealth", null, "StorageSubSystem", "StorageHealth").First();
}
```

Это те же объекты, которые вы получаете в PowerShell с помощью таких командлетов, как **Get-сторажесубсистем**, **Get-стораженоде**и **Get-Volume**.

Вы можете получить доступ ко всем тем же свойствам, описанным в статье [классы API управления хранением](/previous-versions/windows/desktop/stormgmt/storage-management-api-classes).

```
using System.Diagnostics;

foreach (CimInstance Node in Nodes)
{
    // For illustration, write each node's Name to the console. You could also write State (up/down), or anything else!
    Debug.WriteLine("Discovered Node " + Node.CimInstanceProperties["Name"].Value.ToString());
}
```

Вызовите метод- **Report** , чтобы начать потоковую передачу примеров проверенного экспертом списка ключевых метрик, которые эффективно собираются и объединяются динамически на узлах, со встроенной логикой для обнаружения членства в кластере. После этого все примеры будут поступать. Все значения предоставляются только в режиме реального времени по состоянию на конкретный момент.

Метрики можно передавать в поток для трех областей: кластер, любой узел или любой том.

Полный список метрик, доступных в каждой области в Windows Server 2016, приведен ниже.

### <a name="iobserveronnext"></a>IObserver. OnNext ()

В этом примере кода используется [шаблон разработки наблюдателя](/dotnet/standard/events/observer-design-pattern) для реализации наблюдателя, метод **OnNext ()** которого будет вызываться при поступлении каждого нового образца метрик. Его метод **Oncompleteed ()** будет вызываться, если потоковая передача завершается. Например, вы можете использовать его для повторного запуска потоковой передачи, чтобы он продолжал работать в течение неограниченного времени.

```
class MetricsObserver<T> : IObserver<T>
{
    public void OnNext(T Result)
    {
        // Cast
        CimMethodStreamedResult StreamedResult = Result as CimMethodStreamedResult;

        if (StreamedResult != null)
        {
            // For illustration, you could store the metrics in this dictionary
            Dictionary<string, string> Metrics = new Dictionary<string, string>();

            // Unpack
            CimInstance Report = (CimInstance)StreamedResult.ItemValue;
            IEnumerable<CimInstance> Records = (IEnumerable<CimInstance>)Report.CimInstanceProperties["Records"].Value;
            foreach (CimInstance Record in Records)
            {
                /// Each Record has "Name", "Value", and "Units"
                Metrics.Add(
                    Record.CimInstanceProperties["Name"].Value.ToString(),
                    Record.CimInstanceProperties["Value"].Value.ToString()
                    );
            }

            // TODO: Whatever you want!
        }
    }
    public void OnError(Exception e)
    {
        // Handle Exceptions
    }
    public void OnCompleted()
    {
        // Reinvoke BeginStreamingMetrics(), defined in the next section
    }
}
```

### <a name="begin-streaming"></a>Начать потоковую передачу

Определив наблюдатель, можно начать потоковую передачу.

Укажите целевой объект **CimInstance** , для которого необходимо задать метрики. Это может быть кластер, любой узел или любой том.

Параметр Count — это число выборок до завершения потоковой передачи.

```
CimInstance Target = Cluster; // From among the objects discovered in DiscoverObjects()

public void BeginStreamingMetrics(CimSession Session, CimInstance HealthService, CimInstance Target)
{
    // Set Parameters
    CimMethodParametersCollection MetricsParams = new CimMethodParametersCollection();
    MetricsParams.Add(CimMethodParameter.Create("TargetObject", Target, CimType.Instance, CimFlags.In));
    MetricsParams.Add(CimMethodParameter.Create("Count", 999, CimType.UInt32, CimFlags.In));
    // Enable WMI Streaming
    CimOperationOptions Options = new CimOperationOptions();
    Options.EnableMethodResultStreaming = true;
    // Invoke API
    CimAsyncMultipleResults<CimMethodResultBase> InvokeHandler;
    InvokeHandler = Session.InvokeMethodAsync(
        HealthService.CimSystemProperties.Namespace, HealthService, "GetReport", MetricsParams, Options
        );
    // Subscribe the Observer
    MetricsObserver<CimMethodResultBase> Observer = new MetricsObserver<CimMethodResultBase>(this);
    IDisposable Disposeable = InvokeHandler.Subscribe(Observer);
}
```

Нет необходимости говорить, что эти метрики можно визуально отобразить, сохранить в базе данных или использовать по своему усмотрению.

### <a name="properties-of-reports"></a>Свойства отчетов

Каждый пример метрик — один «отчет», который содержит много записей, соответствующих отдельным метрикам.

Для полной схемы изучите классы **MSFT \_ Сторажехеалсрепорт** и **MSFT \_ хеалсрекорд** в *сторажевми. mof*.

Каждая метрика имеет только три свойства в каждой таблице.

| **Property** | **Пример**       |
| -------------|-------------------|
| name         | иолатенциавераже  |
| Значение        | 0,00021           |
| единиц(ы)        | 3                 |

Единицы измерения = {0, 1, 2, 3, 4}, где 0 = "bytes", 1 = "BytesPerSecond", 2 = "CountPerSecond", 3 = "секунды" или 4 = "процент".

## <a name="coverage"></a>Охват

Ниже приведены метрики, доступные для каждой области в Windows Server 2016.

### <a name="msft_storagesubsystem"></a>MSFT_StorageSubSystem

| **Имя**                        | **единиц(ы)** |
|---------------------------------|-----------|
| CPUUsage                        | 4         |
| капаЦитифисикалпуледаваилабле | 0         |
| капаЦитифисикалпуледтотал     | 0         |
| капаЦитифисикалтотал           | 0         |
| капаЦитифисикалунпулед        | 0         |
| капаЦитиволумесаваилабле        | 0         |
| капаЦитиволуместотал            | 0         |
| иолатенциавераже                | 3         |
| иолатенциреад                   | 3         |
| иолатенциврите                  | 3         |
| иопсреад                        | 2         |
| иопстотал                       | 2         |
| иопсврите                       | 2         |
| иосраугхпутреад                | 1         |
| иосраугхпуттотал               | 1         |
| иосраугхпутврите               | 1         |
| меморяваилабле                 | 0         |
| MemoryTotal                     | 0         |


### <a name="msft_storagenode"></a>MSFT_StorageNode

| **Имя**            | **единиц(ы)** |
|---------------------|-----------|
| CPUUsage            | 4         |
| иолатенциавераже    | 3         |
| иолатенциреад       | 3         |
| иолатенциврите      | 3         |
| иопсреад            | 2         |
| иопстотал           | 2         |
| иопсврите           | 2         |
| иосраугхпутреад    | 1         |
| иосраугхпуттотал   | 1         |
| иосраугхпутврите   | 1         |
| меморяваилабле     | 0         |
| MemoryTotal         | 0         |

### <a name="msft_volume"></a>MSFT_Volume

| **Имя**            | **единиц(ы)** |
|---------------------|-----------|
| капаЦитяваилабле   | 0         |
| капаЦититотал       | 0         |
| иолатенциавераже    | 3         |
| иолатенциреад       | 3         |
| иолатенциврите      | 3         |
| иопсреад            | 2         |
| иопстотал           | 2         |
| иопсврите           | 2         |
| иосраугхпутреад    | 1         |
| иосраугхпуттотал   | 1         |
| иосраугхпутврите   | 1         |

## <a name="additional-references"></a>Дополнительные ссылки

- [Служба работоспособности в Windows Server 2016](health-service-overview.md)