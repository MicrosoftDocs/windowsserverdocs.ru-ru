---
title: Каналы обслуживания Windows Server
description: 'Описание каналов обслуживания Windows Server 2019: LTSC (долгосрочное обслуживание) и SAC (полугодичное обслуживание)'
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: high
ms.date: 05/21/2019
ms.openlocfilehash: 49de69c5a21a9c16012d79609784ff89395358db
ms.sourcegitcommit: 893b9a24fd2efe30f5af909e3aa1f25907a17427
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "88681285"
---
# <a name="windows-server-servicing-channels-ltsc-and-sac"></a>Каналы обслуживания Windows Server: LTSC и SAC

> Применяется к: Windows Server 2019, Windows Server 2016, Windows Server (Semi-Annual Channel)

Пользователям Windows Server доступны два основных канала выпусков: Long-Term Servicing Channel и Semi-Annual Channel.

Вы можете хранить серверы в канале Long-Term Servicing Channel (LTSC), перенести их в канал Semi-Annual Channel либо поместить разные серверы в разные каналы, в зависимости от того, что вам лучше подходит.

## <a name="long-term-servicing-channel-ltsc"></a>Long-Term Servicing Channel (LTSC)

Это уже известная вам модель выпуска (ранее она носила название Long-Term Servicing *Branch*), в рамках которой выпуск новой версии Windows Server происходит каждые 2–3 года. Пользователи имеют право на 5 лет основной поддержки и 5 лет расширенной поддержки. Этот канал подходит для систем, которым требуются более продолжительный период обслуживания и стабильность работы. Новые выпуски Semi-Annual Channel никак не затронут уже развернутые среды Windows Server 2019 и более ранние версии Windows Server. Канал Long-Term Servicing Channel продолжит получать обновления системы безопасности и не связанные с безопасностью обновления, но не получит новые функции и возможности.

> [!NOTE]
> **Текущий продукт LTSC — Windows Server 2019**. Чтобы остаться в этом канале, необходимо установить (или продолжить использовать) ОС Windows Server 2019, которую можно установить в режиме основных серверных компонентов или в режиме сервера с возможностями рабочего стола.

## <a name="semi-annual-channel"></a>Полугодовой канал

Канал Semi-Annual Channel позволяет клиентам, быстро внедряющим инновации, скорее начать использовать возможности новой операционной системы с поддержкой контейнеров и микрослужб. В рамках канала Semi-Annual Channel для продуктов Windows Server будут доступны новые выпуски два раза в год — весной и осенью. Для каждого выпуска в этом канале будет предоставляться поддержка в течение 18 месяцев, начиная с даты начального выпуска.

Большая часть функций, реализованных в канале Semi-Annual Channel, будет содержаться в следующем выпуске канала Long-Term Servicing для Windows Server. Редакции, функции и вспомогательное содержимое, входящие в состав выпусков, будут зависеть от отзывов клиентов.

Канал Semi-Annual Channel доступен корпоративным клиентам, участвующим в программе [Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx), а также через Azure Marketplace или другого поставщика облачных услуг / услуг хостинга, а также в рамках программ лояльности, таких как подписки на Visual Studio.

> [!Note]
> **Текущий выпуск канала Semi-Annual Channel — Windows Server версии 2004.** Чтобы присоединиться к этому каналу, требуется ОС Windows Server версии 2004, которую можно установить в режиме основных серверных компонентов или в виде Nano Server с выполнением в контейнере. Обновления на месте выпуска Long-Term Servicing Channel не поддерживаются, так как они находятся в **разных каналах выпуска**. Выпуски канала Semi-Annual Channel не являются обновлениями — это следующий выпуск Windows Server на канале Semi-Annual Channel.

В этой модели выпуски Windows Server идентифицируются по году и месяцу выпуска, например выпуск от 9-го месяца (сентября) 2017 года будет обозначаться как **версия 1709**. Новые выпуски Windows Server в канале Semi-Annual Channel появляются два раза в год. Срок поддержки для каждого выпуска составляет 18 месяцев.

## <a name="should-you-keep-servers-on-the-ltsc-or-move-them-to-the-semi-annual-channel"></a>Следует ли оставить серверы в канале LTSC или переместить их в канал Semi-Annual Channel?

Ниже перечислены основные различия, которые следует принять во внимание.

- Вам необходимы быстрые инновации? Вам требуется ранний доступ к новейшим возможностям Windows Server? Вам необходимо поддерживать быстро меняющиеся гибридные приложения, интеграцию процессов эксплуатации и разработки, а также структуры Hyper-V? Если это так, **присоединитесь к каналу Semi-Annual Channel**, установив **Windows Server версии 2004**. Как описано в этом разделе, вы будете получать новые версии два раза в год с 18-месячной основной поддержкой в рабочей среде для каждого выпуска. Вы можете получать их по программе корпоративного лицензирования, в виде служб по подписке Azure и Visual Studio. В настоящее время для выпусков в канале Semi-Annual Channel требуются корпоративное лицензирование и программа Software Assurance, если вы планируете запускать продукт в рабочей среде.

- Вам требуются стабильность и предсказуемость? Вам требуется запускать виртуальные машины и традиционные рабочие нагрузки на физических серверах? Если это так, вам следует **сохранить эти серверы в канале Long-Term Servicing Channel**. Текущий выпуск LTSC — **Windows Server 2019**. Как описано в этом разделе, вы будете получать доступ к новым версиям каждые 2–3 года с 5-летней основной поддержкой и последующей 5-летней расширенной поддержкой для каждого выпуска. Выпуски LTSC доступны с помощью всех методов выпуска. Выпуски в канале LTSC доступны всем пользователям, независимо от применяемой модели лицензирования.

В следующей таблице приведены основные различия между каналами.

| Описание | Long-Term Servicing Channel (Windows Server 2019) | Semi-Annual Channel (Windows Server) |
| -----------------------|--|--|
| Рекомендуемые сценарии | Файловые серверы общего назначения, рабочие нагрузки Майкрософт и других производителей, традиционные приложения, инфраструктурные роли, программно-определяемые центры обработки данных и гиперконвергентная инфраструктура. | Контейнерные приложения, узлы контейнеров и сценарии с приложениями, где ускоренные инновации приносят пользу |
| Новые выпуски | Каждые 2–3 года | Каждые 6 месяцев |
| Поддержка | 5 лет основной поддержки, а также 5 лет расширенной поддержки | 18 месяцев |
| Выпуски | Все доступные выпуски Windows Server | Выпуски Standard и Datacenter |
| Кто может использовать | Все клиенты во всех каналах | Только клиенты облака и клиенты Software Assurance |
| Параметры установки | Основные серверные компоненты и сервер с возможностями рабочего стола | Основные серверные компоненты для узла контейнеров, образа контейнера и образа контейнера Nano Server |

## <a name="device-compatibility"></a>Совместимость устройств

Если не будет указано иное, минимальные требования к оборудованию для запуска выпусков Semi-Annual Channel будут аналогичны минимальным требованиям, предъявляемым к последнему выпуску Long-Term Servicing Channel для Windows Server. Например, **текущим выпуском канала Long-Term Servicing Channel является Windows Server 2019**. Большинство драйверов оборудования продолжат работать в этих выпусках.

## <a name="servicing"></a>Обслуживание

Для обоих выпусков — Long-Term Servicing Channel и Semi-Annual Channel — будут доступны обновления системы безопасности, а также не связанные с безопасностью обновления. Выпуски будут отличаться лишь длительностью предоставления поддержки, как описано выше.

### <a name="servicing-tools"></a>Средства обслуживания

Существует множество средств, с помощью которых ИТ-специалисты могут обслуживать Windows Server. Каждый вариант имеет свои преимущества и недостатки с точки зрения возможностей, контроля, простоты и низких административных требований. Ниже приведены примеры средств обслуживания для управления обслуживающими обновлениями.

- **Центр обновления Windows (автономный)** . Этот вариант доступен только для серверов, которые подключены к Интернету и для которых активирован Центр обновления Windows.
- **Windows Server Update Services (WSUS)** обеспечивают расширенный контроль над обновлениями Windows 10 и Windows Server и доступны в операционной системе Windows Server на уровне кода. Помимо возможности откладывать обновления организации могут также добавить уровень утверждения обновлений и развертывать их на конкретных компьютерах или в группах компьютеров по мере готовности.
- **Microsoft Endpoint Configuration Manager** обеспечивает максимальный контроль над обслуживанием. ИТ-специалисты могут откладывать обновления, утверждать их и использовать различные возможности для целевых развертываний и контроля над использованием пропускной способности и временем развертывания.

Скорее всего, вы уже используете хотя бы один из этих вариантов, выбрав его с учетом имеющихся ресурсов, персонала и знаний. Вы можете продолжать использовать тот же процесс для выпусков Semi-Annual Channel: например, если вы уже используете Configuration Manager для управления обновлениями, можно и дальше применять это решение. Аналогичным образом, если вы используете WSUS, можно продолжать это делать.

## <a name="where-to-obtain-semi-annual-channel-releases"></a>Где можно получить выпуски Semi-Annual Channel

Для выпусков Semi-Annual Channel следует применять чистую установку.

- Volume Licensing Service Center (VLSC). Корпоративным клиентам, участвующим в программе [Software Assurance](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx), для получения этого выпуска следует перейти на веб-сайт [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx) и нажать кнопку **Вход**. Затем необходимо щелкнуть **Загрузки и ключи** и найти этот выпуск.

- Выпуски каналов Semi-Annual Channel также доступны в [Microsoft Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WindowsServer?tab=Overview).

- Подписки Visual Studio. Подписчики Visual Studio могут получить выпуски Semi-Annual Channel, скачав их [на странице загрузки для подписчиков Visual Studio](https://my.visualstudio.com/downloads?pid=2347). Если вы еще не являетесь подписчиком, перейдите на страницу [Подписки на Visual Studio](https://www.visualstudio.com/subscriptions/), зарегистрируйтесь, а затем перейдите на [страницу скачивания для подписчиков Visual Studio](https://my.visualstudio.com/downloads?pid=2347), как указано выше. Выпуски, полученные с помощью подписок на Visual Studio, используются только для разработки и тестирования.

- Получение предварительных выпусков через Программу предварительной оценки Windows. Тестирование предварительных сборок Windows Server помогает корпорации Майкрософт и ее клиентам выявлять потенциальные проблемы до выпуска. Это также предоставляет клиентам уникальную возможность напрямую влиять на возможности продукта.
Процесс разработки сборок и внесение в них изменений зависят от отзывов пользователей, получаемых корпорацией Майкрософт. Раннее тестирование и отзывы являются важным аспектом быстрого выпуска сборок. Чтобы зарегистрироваться в Программе предварительной оценки Windows, ознакомьтесь с [документаций к Программе предварительной оценки Windows для Windows Server](/windows-insider/at-work/).

## <a name="activating-semi-annual-channel-releases"></a>Активация выпусков Semi-Annual Channel

- Если вы используете Microsoft Azure, выпуск должен активироваться автоматически.
- Если вы получили этот выпуск через центр Volume Licensing Service Center или подписки Visual Studio, для активации воспользуйтесь клиентским ключом корпоративного лицензирования Windows Server 2019 с помощью среды системы управления ключами (KMS). Дополнительные сведения см. в статье [KMS client setup keys](../get-started/kmsclientkeys.md) (Ключи установки клиента KMS).

Выпуски Semi-Annual Channel, выпущенные до Windows Server 2019, используют CSVLK для Windows Server 2016.

## <a name="why-do-semi-annual-channel-releases-offer-only-the-server-core-installation-option"></a>Почему выпуски Semi-Annual Channel предлагают только вариант установки основных компонентов?

Одним из важнейших наших шагов при планировании каждого выпуска Windows Server является учет отзывов клиентов о том, как они используют Windows Server. Какие новые возможности окажут наибольшее влияние на среды Windows Server и, следовательно, на текущую деятельность компании? Согласно вашим отзывам, приоритетной задачей является максимально быстрое и эффективное внедрение инноваций. В то же время клиенты, внедряющие инновации наиболее быстро, сообщили нам, что они в основном используют сценарии командной строки в PowerShell для управления центрами обработки данных. Поэтому при установке Windows Server с возможностями рабочего стола им едва ли потребуется графический пользовательский интерфейс рабочего стола, особенно теперь, когда для удаленного управления вашими серверами доступен [Windows Admin Center](../manage/windows-admin-center/overview.md).

Отдавая предпочтение варианту установки основных серверных компонентов, мы получаем возможность направить больше ресурсов на нововведения, сохраняя при этом присущие платформе Windows Server возможности и широкий спектр поддерживаемых приложений. Оставить отзыв, предложение или комментарий об этой или других проблемах, связанных с Windows Server или будущими выпусками, можно в [Центре отзывов](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app).

## <a name="what-about-nano-server"></a>Как насчет Nano Server?

Сервер Nano Server доступен в качестве операционной системы контейнера в канале Semi-Annual Channel. Подробные сведения см. в статье [Изменения сервера Nano Server в Semi-Annual Channel для Windows Server](../get-started/nano-in-semi-annual-channel.md).

## <a name="how-to-tell-whether-a-server-is-running-an-ltsc-or-sac-release"></a>Как определить, работает ли на сервере выпуск LTSC или SAC

В целом выпуски канала Long-Term Servicing Channel, такие как Windows Server 2019, выпускаются одновременно с новой версией канала Semi-Annual Channel, например Windows Server версии 1809. Из-за этого сложнее определить, работает ли на сервере выпуск канала Semi-Annual Channel. Вместо того, чтобы смотреть на номер сборки, следует посмотреть на название продукта. Выпуски канала Semi-Annual Channel используют имя продукта Windows Server Standard или Windows Server Datacenter без номера версии, в то время как выпуски канала Long-Term Servicing Channel содержат номер версии, например Windows Server 2019 Datacenter.

> [!Note]
> Приведенные ниже инструкции помогут идентифицировать LTSC и SAC и выявить различия между ними в целях управления жизненным циклом и общей инвентаризации.  Они не предназначены для определения совместимости приложений или представления поверхности определенного API.  Для обеспечения совместимости разработчикам приложений следует использовать другие инструкции, так как в течение срока эксплуатации системы могут добавляться компоненты, API и функции, либо они могут быть еще недоступны. [Версия операционной системы](/windows/desktop/sysinfo/operating-system-version) — оптимальная отправная точка для разработчиков приложений.

Откройте Powershell и используйте командлет Get-ItemProperty или командлет Get-ComputerInfo, чтобы проверить соответствующие свойства в реестре.  Вместе с номером сборки вы сможете найти информацию о наличии или отсутствии LTSC или SAC по году выпуска, например 2019.  Это свойственно LTSC и не свойственно SAC.  Вы также узнаете время выпуска по идентификатору ReleaseId или WindowsVersion, например 1809, а также тип установки: основные серверные компоненты или сервер с возможностями рабочего стола.

**Пример выпуска Windows Server 2019 Datacenter Edition (LTSC) с возможностями рабочего стола:**

````PowerShell
Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows NT\CurrentVersion" | Select ProductName, ReleaseId, InstallationType, CurrentMajorVersionNumber,CurrentMinorVersionNumber,CurrentBuild
````

````
ProductName               : Windows Server 2019 Datacenter
ReleaseId                 : 1809
InstallationType          : Server
CurrentMajorVersionNumber : 10
CurrentMinorVersionNumber : 0
CurrentBuild              : 17763
````

**Пример основных серверных компонентов Windows Server, версия 1809 (SAC), Standard Edition:**

````PowerShell
Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows NT\CurrentVersion" | Select ProductName, ReleaseId, InstallationType, CurrentMajorVersionNumber,CurrentMinorVersionNumber,CurrentBuild
````

````
ProductName               : Windows Server Standard
ReleaseId                 : 1809
InstallationType          : Server Core
CurrentMajorVersionNumber : 10
CurrentMinorVersionNumber : 0
CurrentBuild              : 17763
````

**Пример основных серверных компонентов Windows Server 2019 Standard Edition (LTSC):**


````PowerShell
Get-ComputerInfo | Select WindowsProductName, WindowsVersion, WindowsInstallationType, OsServerLevel, OsVersion, OsHardwareAbstractionLayer
````

````
WindowsProductName            : Windows Server 2019 Standard
WindowsVersion                : 1809
WindowsInstallationType       : Server Core
OsServerLevel                 : ServerCore
OsVersion                     : 10.0.17763
OsHardwareAbstractionLayer    : 10.0.17763.107
````

Чтобы уточнить наличие на сервере новой [функции совместимости приложений основных серверных компонентов по требованию](./install-fod-19.md), воспользуйтесь командлетом [Get-WindowsCapability](/powershell/module/dism/get-windowscapability?view=win10-ps) и найдите:
````
Name    :     ServerCore.AppCompatibility~~~~0.0.1.0
State   :     Installed
````

## <a name="additional-references"></a>Дополнительные ссылки

- [Изменения сервера Nano Server в Semi-Annual Channel для Windows Server](../get-started/nano-in-semi-annual-channel.md)

- [Политика жизненного цикла поддержки Майкрософт](https://support.microsoft.com/lifecycle)

- [Determining whether Server Core is running](https://msdn.microsoft.com/library/hh846315%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396) (Определение того, запущены ли основные серверные компоненты)

- [GetProductInfo function](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getproductinfo) (Функция GetProductInfo)

- [SoftwareInventoryLogging](https://docs.microsoft.com/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps) (Командлеты ведения журнала инвентаризации программного обеспечения)
