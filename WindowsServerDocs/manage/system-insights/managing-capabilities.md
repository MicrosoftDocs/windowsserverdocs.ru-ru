---
title: Управление возможностями
description: System Insights предоставляет разнообразные параметры, которые можно настроить для каждой возможности, и эти параметры могут быть настроены для удовлетворения конкретных потребностей развертывания. В этом разделе описывается, как управлять различными параметрами для каждой из возможностей с помощью центра администрирования Windows или PowerShell, предоставляя основные примеры PowerShell и снимки экрана центра администрирования Windows для демонстрации настройки этих параметров.
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 6/05/2018
ms.openlocfilehash: e82b27d2d746592b29b86a66ee34b21f8605a0d8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940165"
---
# <a name="managing-capabilities"></a>Управление возможностями

>Область применения: Windows Server 2019

В Windows Server 2019 System Insights предоставляет множество параметров, которые можно настроить для каждой возможности, и эти параметры можно настраивать для удовлетворения конкретных потребностей развертывания. В этом разделе описывается, как управлять различными параметрами для каждой из возможностей с помощью центра администрирования Windows или PowerShell, предоставляя основные примеры PowerShell и снимки экрана центра администрирования Windows для демонстрации настройки этих параметров.

>[!TIP]
>Эти короткие видеоматериалы также помогут вам приступить к работе и уверенно управлять System Insights: начало [работы с System Insights за 10 минут](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

Хотя в этом разделе приведены примеры PowerShell, вы можете использовать [документацию по PowerShell System Insights](https://aka.ms/systeminsightspowershell) для просмотра всех командлетов, параметров и наборов параметров в System Insights.

## <a name="viewing-capabilities"></a>Возможности просмотра

Чтобы приступить к работе, можно получить список всех доступных возможностей с помощью командлета **Get-инсигхтскапабилити** :

```PowerShell
Get-InsightsCapability
```
Эти возможности также видны в расширении System Insights:

![Страница обзора System Insights с перечнем доступных возможностей](media/overview-page-contoso.png)

## <a name="enabling-and-disabling-a-capability"></a>Включение и отключение возможности
Каждая возможность может быть включена или отключена. Отключение возможности предотвращает вызов этой возможности, а для возможностей, отличных от значений по умолчанию, отключение возможности останавливает сбор всех данных для этой возможности. По умолчанию все возможности включены, и можно проверить состояние возможности с помощью командлета **Get-инсигхтскапабилити** .

Чтобы включить или отключить возможность, используйте командлеты **Enable-инсигхтскапабилити** и **Disable-инсигхтскапабилити** :

```PowerShell
Enable-InsightsCapability -Name "CPU capacity forecasting"
Disable-InsightsCapability -Name "Networking capacity forecasting"
```
Эти параметры также можно переключить, выбрав возможность в центре администрирования Windows нажатием кнопок **включить** или **Отключить** .

### <a name="invoking-a-capability"></a>Вызов возможности
Вызов возможности немедленно запускает функцию для получения прогноза, а администраторы могут вызвать возможность в любое время, нажав кнопку **вызвать** в центре администрирования Windows или командлет **Invoke-инсигхтскапабилити** :

```PowerShell
Invoke-InsightsCapability -Name "CPU capacity forecasting"
```

>[!TIP]
>Чтобы обеспечить возможность вызова возможности не конфликтовать с критически важными операциями на компьютере, рассмотрите возможность планирования прогнозов в нерабочее время.

## <a name="retrieving-capability-results"></a>Получение результатов возможностей
После вызова возможности самые последние результаты отображаются с помощью командлета **Get-инсигхтскапабилити** или **Get-инсигхтскапабилитиресулт**. Эти командлеты выводят последние сведения **о состоянии** и **состоянии** каждой возможности, которые описывают результат каждого прогноза. Поля **состояние** и **Описание состояния** описаны далее в [документе Основные возможности](understanding-capabilities.md).

Кроме того, можно использовать командлет **Get-инсигхтскапабилитиресулт** , чтобы просмотреть последние 30 результатов прогноза и получить данные, связанные с прогнозом:

```PowerShell
# Specify the History parameter to see the last 30 prediction results.
Get-InsightsCapabilityResult -Name "CPU capacity forecasting" -History

# Use the Output field to locate and then show the results of "CPU capacity forecasting."
# Specify the encoding as UTF8, so that Get-Content correctly parses non-English characters.
$Output = Get-Content (Get-InsightsCapabilityResult -Name "CPU capacity forecasting").Output -Encoding UTF8 | ConvertFrom-Json
$Output.ForecastingResults
```
Расширение System Insights автоматически показывает журнал прогнозов и анализирует результаты JSON, предоставляя интуитивно понятный граф с высоким уровнем точности для каждого прогноза:

![Страница с одной возможностью, показывающая диаграмму прогнозирования и историю прогнозирования](media/cpu-forecast-2.png)

### <a name="using-the-event-log-to-retrieve-capability-results"></a>Использование журнала событий для получения результатов возможностей
System Insights регистрирует событие каждый раз, когда возможность завершает прогноз. Эти события отображаются в канале **Microsoft-Windows-System-Insights/администратора** , а System Insights ПУБЛИКУЕТ разные идентификаторы событий для каждого состояния:

| Состояние прогноза | Идентификатор события |
| --------------- | --------------- |
| ОК | 151 |
| Предупреждение | 148 |
| Критический | 150 |
| Ошибка | 149 |
| Нет | 132 |

>[!TIP]
>Используйте [Azure Monitor](https://azure.microsoft.com/services/monitor/) или [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) для агрегирования этих событий и просмотра результатов прогноза в группе компьютеров.


## <a name="setting-a-capability-schedule"></a>Настройка расписания возможностей
Помимо прогнозов по запросу, можно настроить периодические прогнозы для каждой возможности, чтобы указанная возможность автоматически вызывалась по предопределенному расписанию. Используйте командлет **Get-инсигхтскапабилитисчедуле** для просмотра расписаний возможностей:

>[!TIP]
>Используйте оператор конвейера в PowerShell, чтобы просмотреть сведения обо всех возможностях, возвращаемых командлетом **Get-инсигхтскапабилити** .

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilitySchedule
```

Периодические прогнозы включены по умолчанию, хотя их можно отключить в любое время с помощью командлетов **Enable-инсигхтскапабилитисчедуле** и **Disable-инсигхтскапабилитисчедуле** .

```PowerShell
Enable-InsightsCapabilitySchedule -Name "Total storage consumption forecasting"
Disable-InsightsCapabilitySchedule -Name "Volume consumption forecasting"
```

Каждая возможность по умолчанию запланирована на ежедневное выполнение в 03:00. Однако можно создавать пользовательские расписания для каждой возможности, а System Insights поддерживает различные типы расписания, которые можно настроить с помощью командлета **Set-инсигхтскапабилитисчедуле** :

```PowerShell
Set-InsightsCapabilitySchedule -Name "CPU capacity forecasting" -Daily -DaysInterval 2 -At 4:00PM
Set-InsightsCapabilitySchedule -Name "Networking capacity forecasting" -Daily -DaysOfWeek Saturday, Sunday -At 2:30AM
Set-InsightsCapabilitySchedule -Name "Total storage consumption forecasting" -Hourly -HoursInterval 2 -DaysOfWeek Monday, Wednesday, Friday
Set-InsightsCapabilitySchedule -Name "Volume consumption forecasting" -Minute -MinutesInterval 30
```
>[!NOTE]
>Поскольку возможности по умолчанию анализируют ежедневные данные, для этих возможностей рекомендуется использовать ежедневные расписания. Дополнительные сведения о возможностях по умолчанию см. [здесь](understanding-capabilities.md).

Вы также можете использовать центр администрирования Windows для просмотра и установки расписания для каждой возможности, нажав кнопку **Параметры**. Текущее расписание отображается на вкладке **Расписание** . для создания нового расписания можно использовать средства графического пользовательского интерфейса.

![Страница "Параметры", показывающая текущее расписание](media/schedule-page-contoso.png)

## <a name="creating-remediation-actions"></a>Создание действий по исправлению
System Insights позволяет запускать пользовательские сценарии исправления в зависимости от результата работы функции. Для каждой возможности можно настроить пользовательский скрипт PowerShell для каждого состояния прогноза, что позволит администраторам автоматически выполнять корректирующие действия, не требуя вмешательства вручную.

Примеры действий по исправлению: Запуск очистки диска, расширение тома, выполнение дедупликации, динамическая миграция виртуальных машин и настройка Синхронизация файлов Azure.

Действия для каждой возможности можно просмотреть с помощью командлета **Get-инсигхтскапабилитяктион** :

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilityAction
```

Вы можете создавать новые действия или удалять существующие действия с помощью командлетов **Set-инсигхтскапабилитяктион** и **Remove-инсигхтскапабилитяктион** . Каждое действие выполняется с использованием учетных данных, указанных в параметре **актионкредентиал** .

>[!NOTE]
>В первоначальном выпуске System Insights необходимо указать сценарии исправления за пределами пользовательских каталогов. Эта проблема будет устранена в будущем выпуске.

```PowerShell
$Cred = Get-Credential
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning -Action "C:\Users\Public\WarningScript.ps1" -ActionCredential $Cred
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Critical -Action "C:\Users\Public\CriticalScript.ps1" -ActionCredential $Cred

Remove-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning
```

Можно также использовать центр администрирования Windows для задания действий по исправлению с помощью вкладки **действия** на странице **Параметры** .

![Страница параметров, на которой пользователь может указать действия по исправлению](media/actions-page-contoso.png)


## <a name="additional-references"></a>Дополнительные ссылки
Дополнительные сведения о System Insights см. в следующих ресурсах:

- [Обзор системной аналитики](overview.md)
- [Общие сведения о возможностях](understanding-capabilities.md)
- [Добавление и разработка возможностей](adding-and-developing-capabilities.md)
- [Вопросы и ответы по System Insights](faq.md)