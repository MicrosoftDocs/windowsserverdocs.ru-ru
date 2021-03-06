---
title: Шаг 2. Настройка WSUS
description: Статья о службе обновления Windows Server (WSUS) с описанием настройки WSUS, второго из четырех шагов процесса развертывания WSUS
ms.topic: article
ms.assetid: d4adc568-1f23-49f3-9a54-12a7bec5f27c
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 9/18/2020
ms.openlocfilehash: 46f36fe87e4197ab9618cfa914be2b05f1fffea0
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101827429"
---
# <a name="step-2-configure-wsus"></a>Шаг 2. Настройка WSUS

> Область применения. Windows Server 2019, Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

После установки на ваш сервер роли сервера служб WSUS необходимо должным образом произвести его настройку. В следующем контрольном списке перечислены шаги для начальной настройки сервера служб WSUS.

|Задача|Описание|
|----|--------|
|[2.1 Настройка сетевых подключений](#21-configure-network-connections)|Настройка кластерной сети при помощи мастера настройки сети.|
|[2.2 Настройка служб WSUS с помощью мастера настройки WSUS](#22-configure-wsus-by-using-the-wsus-configuration-wizard)|Мастер настройки WSUS служит для выполнения базовой настройки служб WSUS.|
|[2.3. Настройка групп компьютеров WSUS](#23-configure-wsus-computer-groups)|Создайте группы компьютеров в консоли администрирования WSUS для управления обновлениями в организации.|
|[2.4 Настройка клиентских обновлений](#24-configure-client-updates)|Укажите, как и когда автоматические обновления будут применяться к клиентским компьютерам.|
|[2.5. Защита WSUS с помощью протокола SSL](#25-secure-wsus-with-the-secure-sockets-layer-protocol)|Настройте протокол SSL для защиты служб Windows Server Update Services (WSUS).|

## <a name="21-configure-network-connections"></a>2.1. Настройка сетевых подключений

До начала процесса настройки убедитесь в том, что вы знаете ответы на следующие вопросы.

1. Разрешают ли настройки брандмауэра на сервере доступ клиентов к серверу?

2. Может ли данный компьютер подключаться к вышестоящему серверу (например, серверу, предназначенному для загрузки обновлений из Центра обновления Майкрософт)?

3. Располагаете ли вы именем и адресом прокси-сервера, а также учетными данными пользователя для данного прокси-сервера, если они вам требуются?

Службы WSUS по умолчанию настроены на использование Центра обновления Майкрософт в качестве источника обновлений. Если в состав вашей сети входит прокси-сервер, вы можете настроить службы WSUS на использование данного прокси-сервера. Если между службами WSUS и сетью Интернет располагается корпоративный брандмауэр, возможно, потребуется настроить данный брандмауэр, чтобы обеспечить возможность получения обновлений службами WSUS.

> [!TIP]
> Несмотря на то, что загрузка обновлений из Центра обновления Майкрософт требует подключения к сети Интернет, службы WSUS предоставляют вам возможность импортировать обновления в сети, не подключенные к Интернету.

После ознакомления с ответами на данные вопросы вы можете приступать к настройке следующих сетевых параметров служб WSUS.

- **Обновления** Укажите способ получения обновлений данным сервером (из Центра обновления Майкрософт или с другого сервера WSUS).

- **Прокси** При выявлении необходимости использования службами WSUS прокси-сервера для получения доступа к Интернету требуется произвести настройку параметров прокси-сервера в службах WSUS.

- **Брандмауэр** При выявлении факта защищенности служб WSUS корпоративным брандмауэром требуется произвести с краевым устройством дополнительные действия, обеспечивающие необходимое разрешение на трафик для WSUS.

### <a name="211-connection-from-the-wsus-server-to-the-internet"></a>2.1.1 Подключение к Интернету с сервера WSUS

Если между службами WSUS и сетью Интернет располагается корпоративный брандмауэр, возможно, потребуется настроить данный брандмауэр для обеспечения возможности получения обновлений службами WSUS. Для получения обновлений из Центра обновления Майкрософт сервер WSUS использует порт 443 для протокола HTTPS. Несмотря на то, что большинство корпоративных брандмауэров разрешают этот тип трафика, в некоторых организациях доступ к Интернету с таких серверов ограничен в соответствии с политиками безопасности. Если в вашей организации существует ограничение доступа, вам требуется авторизация, разрешающая доступ служб WSUS к Интернету для перечисленных ниже URL-адресов:

- http\://windowsupdate.microsoft.com

- http\://\*.windowsupdate.microsoft.com

- https\://\*.windowsupdate.microsoft.com

- http\://\*.update.microsoft.com

- https\://\*.update.microsoft.com

- http\://\*.windowsupdate.com

- http\://download.windowsupdate.com

- https\://download.microsoft.com

- http\://\*.download.windowsupdate.com

- http\://wustat.windows.com

- http\://ntservicepack.microsoft.com

- http\://go.microsoft.com

- http\://dl.delivery.mp.microsoft.com

- https\://dl.delivery.mp.microsoft.com

> [!IMPORTANT]
> Если при получении обновлений в службах WSUS возникают сбои, вызванные настройками брандмауэра, см. [статью 885819](https://support.microsoft.com/kb/885819) в базе знаний Майкрософт.

Ниже приведена процедура настройки корпоративного брандмауэра, расположенного между службами WSUS и сетью Интернет. Так как службы WSUS инициируют весь сетевой трафик, настраивать брандмауэр Windows на сервере WSUS не требуется. Несмотря на то, что подключение служб WSUS к Центру обновления Майкрософт требует открытия портов 80 и 443, вы можете настроить несколько серверов WSUS для синхронизации с настраиваемыми портами.

### <a name="212-connection-between-wsus-servers"></a>2.1.2 Подключения между серверами WSUS

Вышестоящие и подчиненные серверы WSUS будет выполнять синхронизацию по порту, настроенному администратором служб WSUS. По умолчанию эти порты настроены следующим образом.

- В службах WSUS 3.2 и более ранних версий порт 80 для HTTP и порт 443 для HTTPS

- В службах WSUS 6.2 и более поздних версий (Windows Server 2012 или более поздняя версия) — порт 2012 для HTTP и порт 8530 для HTTPS

Чтобы разрешить входящий трафик по этим портам, необходимо настроить брандмауэр на сервере WSUS.

### <a name="213-connection-between-clients-windows-update-agent-and-wsus-servers"></a>2.1.3 Подключения между клиентами (агент обновления Windows) и серверами WSUS

Прослушивающие интерфейсы и порты настраиваются на сайте IIS для служб WSUS и в любых параметрах групповой политики, используемых для настройки клиентских компьютеров. Порты по умолчанию те же, что и в предыдущем разделе, **Подключения между серверами WSUS**. Брандмауэр на сервере WSUS также необходимо настроить, чтобы разрешить входящий трафик через эти порты.

## <a name="configure-the-proxy-server"></a>Настройка прокси-сервера

Если в корпоративной сети используются прокси-серверы, они должны поддерживать протоколы HTTP и SSL и использовать обычную проверку подлинности или проверку подлинности Windows. Эти требования могут быть выполнены с помощью одной из следующих конфигураций.

1. Один прокси-сервер, поддерживающий два канала протоколов. В этом случае настройте для одного канала использование протокола HTTP, а для другого канала использование протокола HTTPS.

    > [!NOTE]
    > Можно настроить один прокси-сервер, обрабатывающий оба протокола для служб WSUS, во время установки программного обеспечения сервера WSUS.

2. Два прокси-сервера, каждый из которых поддерживает один протокол. В этом случае один прокси-сервер настроен для использования протокола HTTP, а другой — для использования протокола HTTPS.

Чтобы настроить два прокси-сервера, каждый из которых будет обрабатывать один протокол для служб WSUS, используйте следующую процедуру.

#### <a name="to-set-up-wsus-to-use-two-proxy-servers"></a>Настройка служб WSUS для использования двух прокси-серверов

1. Войдите на компьютер, который будет использоваться в качестве сервера WSUS, используя учетную запись, которая является членом локальной группы "Администраторы".

2. Установите роль сервера WSUS. Не указывайте прокси-сервер в процессе работы с мастером настройки WSUS (как описано в следующем разделе).

3. Откройте командную строку (Cmd.exe) от имени администратора. Чтобы открыть командную строку от имени администратора, нажмите кнопку **Пуск**. В поле **Начать поиск** введите **Командная строка**. Вверху меню "Пуск" щелкните правой кнопкой мыши элемент **Командная строка** и выберите пункт **Запуск от имени администратора**. Если появится диалоговое окно **контроля учетных записей**, введите соответствующие учетные данные (при запросе), подтвердите, что отображаемое действие — именно то, которое требуется, и нажмите кнопку **Продолжить**.

4. В окне командной строки перейдите в папку C:\Program Files\Update Services\Tools. Введите следующую команду:

    **wsusutil ConfigureSSLproxy [< proxy_server proxy_port>] -enable**, где:

    1. proxy_server — имя прокси-сервера, который поддерживает протокол HTTPS;

    2. proxy_port — номер порта прокси-сервера.

5. Закройте окно командной строки.

Чтобы добавить прокси-сервер, использующий протокол HTTP, в конфигурацию WSUS, используйте следующую процедуру.

#### <a name="to-add-a-proxy-server-that-uses-the-http-protocol"></a>Добавление прокси-сервера, использующего протокол HTTP

1. Откройте консоль администрирования WSUS.

2. В левой панели разверните имя сервера и щелкните **Параметры**.

3. В области **Параметры** выберите **Источник обновления и прокси-сервер**, а затем перейдите на вкладку **Прокси-сервер** .

4. Чтобы изменить существующую конфигурацию прокси-сервера, используйте следующие параметры.

    ###### <a name="to-change-or-add-a-proxy-server-to-the-wsus-configuration"></a>Изменение или добавление прокси-сервера в конфигурацию WSUS

    1. Установите флажок **Использовать прокси-сервер при синхронизации**.

    2. В поле **Имя прокси-сервера** введите имя прокси-сервера.

    3. В поле **Номер порта прокси-сервера** введите номер порта прокси-сервера. Номер порта по умолчанию: 80.

    4. Если прокси-сервер требует использования определенной учетной записи пользователя, установите флажок **Использовать учетные данные пользователя для подключения к прокси-серверу**. Введите нужное имя пользователя, домен и пароль в соответствующие текстовые поля.

    5. Если прокси-сервер поддерживает обычную проверку подлинности, установите флажок **Разрешить обычную проверку подлинности (пароль передается открытым текстом)** .

    6. Нажмите кнопку **ОК**.

    ###### <a name="to-remove-a-proxy-server-from-the-wsus-configuration"></a>Удаление прокси-сервера из конфигурации WSUS

    1. Чтобы удалить прокси-сервер из конфигурации WSUS, снимите флажок **Использовать прокси-сервер при синхронизации**.

    2. Нажмите кнопку **ОК**.

## <a name="22-configure-wsus-by-using-the-wsus-configuration-wizard"></a>2.2. Настройка служб WSUS при помощи мастера настройки WSUS

Данная методика предполагает, что вы используете мастер настройки WSUS, появляющийся при первом запуске консоли управления WSUS. При дальнейшем изучении настоящего раздела вы научитесь производить данные настройки при помощи страницы **Параметры** :

#### <a name="to-configure-wsus"></a>Настройка служб WSUS

1. На Панели переходов диспетчера серверов выберите **Мониторинг**, затем **Служебные программы**, а затем нажмите **Службы обновления Windows Server**.

    > [!NOTE]
    > При появлении диалогового окна **Завершить установку WSUS** нажмите **Выполнить**. После успешного завершения установки в диалоговом окне **Завершить установку WSUS** нажмите кнопку **Закрыть**.

2. Откроется окно мастера служб Windows Server Update Services. Просмотрите сведения на странице **Перед началом работы** и нажмите кнопку **Далее**.

3. Ознакомьтесь с инструкциями на странице **Принять участие в программе улучшения качества Центра обновления Майкрософт** и примите решение о своем участии в данной программе. Если вы хотите принять участие в программе. Сохраните настройку по умолчанию или снимите флажок и нажмите кнопку **Далее**.

4. На странице **Выбор вышестоящего сервера** есть два варианта:

    1. Синхронизировать обновления с Центром обновления Майкрософт

    2. Синхронизировать с другим сервером Windows Server Update Services

        - Если выбрана синхронизация с другим сервером WSUS, укажите имя сервера и порт, через который этот сервер будет связываться с вышестоящим сервером.

        - Для использования SSL установите флажок **Использовать SSL при синхронизации данных об обновлениях** . Для синхронизации серверы будут использовать порт 443. (Убедитесь в том, что оба сервера поддерживают протокол SSL).

        - Если используется сервер-реплика, установите флажок **Это реплика вышестоящего сервера**.

5. По завершении выбора необходимых параметров развертывания нажмите **Далее** , чтобы продолжить.

6. На странице **Настройка прокси-сервера** установите флажок **Использовать прокси-сервер при синхронизации** , а затем введите в соответствующие поля имя прокси-сервера и номер порта (по умолчанию порт 80).

    > [!IMPORTANT]
    > Выполнение этого действия необходимо, если службам WSUS требуется прокси-сервер для доступа к Интернету.

7. Для подключения к прокси-серверу при помощи специальных учетных данных пользователя установите флажок **Использовать учетные данные пользователя для подключения к прокси-серверу**, а затем введите имя пользователя, домен и пароль пользователя в соответствующие поля. Чтобы задействовать обычную проверку подлинности для пользователя, подключающегося к прокси-серверу, установите флажок **Разрешить обычную проверку подлинности (пароль передается открытым текстом)**.

8. Нажмите кнопку **Далее**. На странице **Подключение к вышестоящему серверу** щелкните **Начать подключение**.

9. При состоявшемся подключении нажмите **Далее** , чтобы продолжить.

10. На странице **Выбор языков** можно выбрать языки для получения обновлений службами WSUS — все языки или некоторый набор языков. Выбор ограниченного набора языков позволяет сохранить пространство на диске, однако ВАЖНО выбрать все те языки, которые необходимы всем клиентам данного сервера WSUS. Для получения обновлений только для определенных языков выберите **Загружать обновления только для следующих языков:**, а затем выберите языки, для которых вы желаете получать обновления; в противном случае — оставьте выбор по умолчанию.

    > [!WARNING]
    > При выборе варианта **Загружать обновления только для следующих языков:** , а также при наличии подчиненного сервера WSUS, подключенного к данному серверу, подразумевается принудительное использование только выбранных языков также и подчиненным сервером.

11. По завершении выбора необходимых языковых параметров нажмите **Далее** , чтобы продолжить.

12. Страница **Выбор продуктов** позволяет вам указать, для каких продуктов нужно получать обновления. Выберите категории продуктов, например Windows, или определенные продукты, например Windows Server 2012. Выбор категории продукта подразумевает выбор всех продуктов в данной категории.

13. Выбрав нужные продукты для вашего развертывания, нажмите кнопку **Далее**.

14. На странице **Выбор классов** выберите классы обновлений, которые вы желаете получать. Выберите все классы либо их ограниченный набор, а затем нажмите кнопку **Далее**.

15. На странице **Настройка расписания синхронизации** можно выбрать выполнение синхронизации автоматически или вручную.

    - При выборе варианта **Синхронизация вручную** следует начинать процесс синхронизации с консоли администрирования служб WSUS.

    - Если выбран вариант **Автоматическая синхронизация**, сервер WSUS производит синхронизацию с установленными интервалами.

    Установите время **первой синхронизации** и укажите количество **синхронизаций в день** для выполнения данным сервером. Например, при указании четырех синхронизаций в день (начиная с 03:00) синхронизации будут выполняться в 03:00, 09:00, 15:00 и 21:00.

16. По завершении выбора необходимых параметров синхронизации нажмите **Далее** , чтобы продолжить.

17. На странице **Завершено** предусмотрена возможность немедленного начала синхронизации при выборе флажка **Запустить первоначальную синхронизацию** . Если вы не выбираете данный вариант, следует воспользоваться консолью управления служб WSUS для выполнения начальной синхронизации. Для получения информации о дополнительных параметрах нажмите **Далее** либо нажмите **Готово** для завершения работы мастера и окончания начальной установки служб WSUS.

18. После нажатия кнопки **Готово** появляется консоль управления служб WSUS.

Теперь, произведя базовую настройку служб WSUS, ознакомьтесь со следующими разделами, содержащими подробную информацию об изменении настроек при помощи консоли управления служб WSUS.

## <a name="23-configure-wsus-computer-groups"></a>2.3. Настройка групп компьютеров WSUS

Группы компьютеров являются ВАЖНОЙ составляющей развертывания служб обновления Windows Server (WSUS). Группы компьютеров позволяют проверять обновления и направлять их на конкретные компьютеры. По умолчанию создаются две группы компьютеров: "Все компьютеры" и "Неназначенные компьютеры". По умолчанию каждый клиентский компьютер прежде всего контактирует с сервером WSUS, а сервер добавляет клиентский компьютер в обе указанные группы.

Вы можете создать любое количество групп пользовательских компьютеров, необходимое для управления обновлениями в вашей организации. Наилучшей методикой является создание не менее одной группы компьютеров для проверки обновлений до их развертывания на других компьютерах вашей организации.

Для создания новой группы и назначения компьютера в данную группу воспользуйтесь следующей методикой:

#### <a name="to-create-a-computer-group"></a>Создание группы компьютеров

1. В консоли администрирования WSUS в разделе **Службы обновления** разверните узел сервера WSUS и узел **Компьютеры**, щелкните **Все компьютеры** правой кнопкой мыши, а затем выберите **Добавить группу компьютеров**.

2. В диалоговом окне **Добавить группу компьютеров** укажите **Имя** новой группы, а затем нажмите кнопку **Добавить**.

3. Щелкните **Компьютеры**, затем выберите компьютеры, которые нужно назначить в созданную группу.

4. Щелкните правой кнопкой мыши имена компьютеров, выбранных предыдущим действием, и нажмите **Изменить членство**.

5. В диалоговом окне **Настройка членства в группах компьютеров** выберите созданную вами тестовую группу и нажмите кнопку **ОК**.

## <a name="24-configure-client-updates"></a>2.4. Настройка клиентских обновлений

Программа установки WSUS автоматически настраивает IIS на распространение последней версии автоматического обновления на каждый клиентский компьютер, контактирующий с сервером WSUS. Наиболее оптимальный вариант настройки автоматического обновления зависит от сетевой среды.

- В среде, использующей службу каталогов Active Directory, вы можете воспользоваться существующим объектом групповой политики (GPO) на основе домена либо создать новый GPO.

- В среде, не использующей Active Directory, для настройки автоматического обновления воспользуйтесь редактором локальной групповой политики, а затем укажите серверу WSUS клиентские компьютеры.

> [!IMPORTANT]
> В приведенных ниже процедурах подразумевается, что в сети используется Active Directory. При этом также подразумевается ваше знакомство с групповой политикой и ее использованием для управления сетью.

Для настройки автоматического обновления клиентских компьютеров воспользуйтесь следующими методиками.

- [Шаг 4. Настройка параметров групповой политики для автоматического обновления](4-configure-group-policy-settings-for-automatic-updates.md)

- [2.3. Настройка групп компьютеров](#23-configure-wsus-computer-groups) (в этой статье)

### <a name="configure-automatic-updates-in-group-policy"></a>Настройка автоматического обновления в групповой политике

Если в вашей сети установлена служба Active Directory, можете настроить один или несколько компьютеров одновременно, включив их в объект групповой политики (GPO), а затем — настроив параметры WSUS для этого GPO. Рекомендуется создать новый объект групповой политики, содержащий исключительно параметры WSUS.

Свяжите этот объект групповой политики WSUS с контейнером Active Directory, который подходит для вашей среды. В простой среде вы можете привязать один объект групповой политики WSUS к домену. В более сложной среде вы можете привязать несколько объектов групповой политики WSUS к нескольким организационным подразделениям, что позволит вам применить разные установки политики WSUS к разным типам компьютеров.

##### <a name="to-enable-wsus-through-a-domain-gpo"></a>Задействование WSUS через доменный объект групповой политики

1. В консоли управления групповыми политиками (GPMC) найдите объект групповой политики, на котором нужно настроить WSUS, а затем щелкните **Изменить**.

2. В области консоли управления групповыми политиками последовательно разверните узлы **Конфигурация компьютера**, **Политики**, **Административные шаблоны**, **Компоненты Windows** и щелкните **Центр обновления Windows**.

3. В области сведений дважды щелкните элемент **Настройка автоматического обновления**. Откроется политика **Настройка автоматического обновления** .

4. Нажмите **Включить**, а затем выберите один из следующих вариантов в поле **Настройка автоматического обновления** .

    - **Уведомлять о загрузках и установках**. Данная настройка уведомляет вошедшего в систему пользователя с правами администратора перед загрузкой и установкой обновлений.

    - **Загружать автоматически и уведомлять об установках**. Данная настройка начинает загрузку обновлений автоматически, а затем уведомляет вошедшего в систему пользователя с правами администратора перед установкой обновлений. По умолчанию этот параметр выбран.

    - **Загружать автоматически и вносить установки в расписание**. Данная настройка начинает загрузку обновлений автоматически, а затем устанавливает их в указанные вами день и момент времени.

    - **Разрешить локальному администратору выбор параметров**. Данная настройка разрешает локальным администраторам для выбора параметров настройки использовать автоматическое обновление в панели управления. Например, администраторы могут выбирать время назначенной установки. При этом локальные администраторы не могут отключать автоматическое обновление.

5. Выберите **Разрешить клиенту присоединение к целевой группе**, выберите **Включено**, а затем введите имя группы компьютеров WSUS, в которую необходимо добавить этот компьютер, в поле **Имя целевой группы для данного компьютера** .

    > [!NOTE]
    > Политика **Разрешить клиенту присоединение к целевой группе** позволяет клиентским компьютерам добавлять себя в целевой группы компьютеров на сервере WSUS при перенаправлении автоматического обновления на сервер WSUS. Если эта политика включена, данный компьютер будет идентифицировать себя как члена определенной группы компьютеров при отправке информации на сервер WSUS, который будет использовать эти данные, чтобы определить, какие обновления будут развертываться на данном компьютере. Этот параметр указывает серверу WSUS, к какой группе принадлежит клиентский компьютер. Необходимо создать группу на сервере WSUS и добавить компьютеры-члены домена в эту группу.

6. Нажмите кнопку **ОК** , чтобы закрыть политику **Разрешить клиенту присоединение к целевой группе** и вернуться в область сведений Центра обновления Windows.

7. Нажмите кнопку **ОК** , чтобы закрыть политику **Настройка автоматического обновления** и вернуться в область сведений Центра обновления Windows.

8. В области сведений **Центр обновления Windows** дважды щелкните **Указать расположение внутрисетевой службы Центра обновления Майкрософт**.

9. Щелкните **Включено**, затем введите URL-адрес одного и того же сервера WSUS в поле **Укажите службу обновлений в интрасети для поиска обновлений** и в поле **Укажите сервер статистики в интрасети** . Например, введите *http://servername* в обоих полях (где *servername* — имя сервера WSUS).

    > [!WARNING]
    > При вводе внутрисетевого адреса своего сервера WSUS убедитесь, что вы указали используемый порт. По умолчанию службы WSUS используют порт 8530 для HTTP и порт 8531 для HTTPS. Например, при использовании HTTP следует ввести **http://servername:8530** .

10. Нажмите кнопку **ОК**.

После настройки клиентского компьютера пройдет несколько минут, прежде чем имя этого компьютера появится на странице **Компьютеры** консоли администрирования WSUS. У групповой политики может занять порядка 20 минут на применение параметров новой политики к клиентским компьютерам, настроенным с использованием объекта групповой политики на основе домена. По умолчанию групповая политика обновляется в фоновом режиме каждые 90 минут со случайным смещением от 0 до 30 минут. Для более частого обновления групповой политики вы можете открыть окно командной строки на клиентском компьютере и ввести команду gpupdate /force.

Для клиентских компьютеров, настраиваемых при помощи редактора локальной групповой политики, объект групповой политики применяется немедленно, а обновление занимает порядка 20 минут. Если вы начинаете обнаружение вручную, нет необходимости ждать установления связи клиентского компьютера со службами WSUS в течение 20 минут.

Поскольку ожидание начала обнаружения может занимать определенное время, для немедленной инициации обнаружения вы можете воспользоваться следующей методикой.

##### <a name="to-initiate-wsus-detection"></a>Инициация обнаружения служб WSUS

1. На клиентском компьютере откройте окно командной строки с повышенным правами.

2. Введите команду wuauclt.exe /detectnow, а затем нажмите клавишу ВВОД.

## <a name="25-secure-wsus-with-the-secure-sockets-layer-protocol"></a>2.5. Защита служб WSUS с помощью протокола SSL

Протокол SSL можно использовать для защиты развертывания WSUS. WSUS использует SSL для проверки подлинности клиентских компьютеров и подчиненных серверов WSUS на данном сервере WSUS. Службы WSUS также используют протокол SSL для шифрования метаданных обновлений.

> [!IMPORTANT]
> Клиенты и подчиненные серверы, которые настроены на использование протокола TLS или HTTPS, также должны быть настроены для использования полного доменного имени для вышестоящего сервера WSUS.

Службы WSUS используют шифрование SSL только для метаданных, а не для файлов обновлений. Центр обновления Майкрософт распространяет обновления аналогичным образом. Корпорация Майкрософт снижает риск передачи файлов обновлений по незашифрованному каналу, подписывая каждое обновление. Кроме того, вычисляется хэш, который отправляется с метаданными для каждого обновления. После загрузки обновления службы WSUS проверяют цифровую подпись и хэш. Если обновление было изменено, оно не устанавливается.

### <a name="limitations-of-wsus-ssl-deployments"></a>Ограничения развертывания WSUS с шифрованием SSL

При использовании протокола SSL для защиты развертывания WSUS необходимо учитывать следующие ограничения.

1. Использование протокола SSL увеличивает рабочую нагрузку сервера. Следует ожидать 10-процентное снижение производительности из-за затрат на шифрование всех метаданных, передаваемых по сети.

2. Если вы используете службы WSUS с удаленной базой данных SQL Server, подключение между сервером WSUS и сервером базы данных не защищается шифрованием SSL. Если требуется защитить подключение к базе данных, примите во внимание следующие рекомендации.

   - Переместите базу данных WSUS на сервер WSUS.

   - Переместите удаленный сервер базы данных и сервер WSUS в частную сеть.

   - Выполните развертывание протокола IPsec, чтобы обеспечить защиту сетевого трафика. Дополнительные сведения о протоколе IPsec см. в разделе [Создание и использование политик IPsec](https://go.microsoft.com/fwlink/?LinkID=203841).

### <a name="configure-ssl-on-the-wsus-server"></a>Настройка SSL на сервере WSUS

Службам WSUS требуется два порта для протокола SSL: один порт, который использует протокол HTTPS для отправки зашифрованных метаданных, и один порт, который использует протокол HTTP для отправки обновлений. При настройке служб WSUS для использования SSL необходимо учитывать следующее.

- Нельзя настроить требование использования протокола SSL для всего веб-сайта WSUS, поскольку при этом потребуется шифровать весь трафик на сайт WSUS. Службы WSUS шифруют только метаданные обновлений. Если компьютер попытается получить файлы обновлений по порту HTTPS, произойдет сбой передачи.

    Требовать шифрование SSL следует только для следующих виртуальных корневых папок:

    - **SimpleAuthWebService**

    - **DSSAuthWebService**

    - **ServerSyncWebService**

    - **APIremoting30**

    - **ClientWebService**

    Шифрование SSL не следует требовать для следующих виртуальных корневых папок:

    - **Содержимое**

    - **Inventory**

    - **ReportingWebService**

    - **SelfUpdate**

- Сертификат центра сертификации (ЦС) должен быть импортирован в хранилище доверенных корневых ЦС локального компьютера или в хранилище доверенных корневых ЦС служб Windows Server Update Services на подчиненных серверах WSUS. Если сертификат импортируется только в хранилище доверенных корневых ЦС локального пользователя, подчиненный сервер WSUS не сможет проходить проверку подлинности на вышестоящем сервере.

    Дополнительные сведения об использовании сертификатов SSL в службах IIS см. в разделе [Требование протокола SSL (IIS 7)](https://go.microsoft.com/fwlink/?LinkID=203846).

- Необходимо импортировать сертификат на все компьютеры, которые будут взаимодействовать с сервером WSUS. К ним относятся все клиентские компьютеры, подчиненные серверы и компьютеры, на которых выполняется консоль администрирования WSUS. Сертификат должен быть импортирован в хранилище доверенных корневых ЦС локального компьютера или в хранилище доверенных корневых ЦС служб Windows Server Update Services.

- Для SSL можно использовать любой порт. Однако порт, который настраивается для использования SSL, также определяет порт, используемый службами WSUS для отправки незащищенного HTTP-трафика. Рассмотрим следующие примеры.

    - При использовании стандартного отраслевого порта 443 для HTTPS-трафика службы WSUS используют стандартный отраслевой порт 80 для незащищенного HTTP-трафика.

    - При использовании для HTTPS-трафика любого порта вместо 443 службы WSUS будут отправлять незащищенный HTTP-трафик через порт, численно предшествующий номеру порта для протокола HTTPS. Например, если для HTTPS используется порт 8531, службы WSUS будут использовать порт 8530 для HTTP.

- При изменении имени сервера, конфигурации SSL или номера порта необходимо повторно инициализировать *ClientServicingProxy*.

##### <a name="to-configure-ssl-on-the-wsus-root-server"></a>Настройка SSL на корневом сервере WSUS

1. Войдите в систему сервера WSUS, используя учетную запись, которая является членом группы "Администраторы WSUS" или локальной группы "Администраторы".

2. В меню **Пуск** введите **CMD**, щелкните **Командная строка** правой кнопкой мыши, а затем выберите пункт **Запуск от имени администратора**.

3. Перейдите к папке _%ProgramFiles%_ **\\Update Services\\Tools\\** .

4. В окне командной строки введите следующую команду:

    **Wsusutil configuressl** _certificateName_

    Где:

    *certificateName* — DNS-имя сервера WSUS.

### <a name="configure-ssl-on-client-computers"></a>Настройка SSL на клиентских компьютерах

При настройке SSL на клиентских компьютерах необходимо учитывать следующие аспекты.

- Необходимо включить URL-адрес для безопасного порта на сервере WSUS. Поскольку нельзя настроить требование SSL на сервере, единственным способом гарантии того, что клиентские компьютеры могут использовать защищенный канал, будет использование URL-адреса HTTPS. При использовании для протокола SSL любого порта вместо 443 необходимо также включить этот порт в URL-адрес.

- Сертификат на клиентском компьютере должен быть импортирован в хранилище доверенных корневых ЦС локального компьютера или в хранилище доверенных корневых ЦС службы автоматического обновления. Если сертификат импортируется только в хранилище доверенных корневых ЦС локального пользователя, автоматическое обновление не сможет пройти проверку подлинности на сервере.

- Клиентские компьютеры должны доверять сертификату, привязанному к серверу WSUS. В зависимости от типа используемого сертификата необходимо настроить для службы включение для клиентских компьютеров доверия сертификату, привязанному к серверу WSUS.

### <a name="configure-ssl-for-downstream-wsus-servers"></a>Настройка SSL для подчиненных серверов WSUS

Ниже приведены инструкции по настройке подчиненного сервера для синхронизации с вышестоящим сервером, который использует протокол SSL.

##### <a name="to-synchronize-a-downstream-server-to-an-upstream-server-that-uses-ssl"></a>Синхронизация подчиненного сервера с вышестоящим сервером, использующим протокол SSL

1. Войдите в систему компьютера, используя учетную запись, которая является членом группы "Администраторы WSUS" или локальной группы "Администраторы".

2. В меню **Пуск** выберите пункт **Все программы**, щелкните **Администрирование**, а затем **Windows Server Update Services**.

3. В правой панели разверните имя сервера.

4. Щелкните **Параметры**, а затем **Источник обновления и прокси-сервер**.

5. На странице **Источник обновления** выберите вариант **Синхронизировать с другим сервером Windows Server Update Services**.

6. Введите имя вышестоящего сервера в поле **Имя сервера**. Введите номер порта, который используется сервером для SSL-подключений, в поле **Номер порта**.

7. Установите флажок **Использовать SSL при синхронизации данных об обновлениях**, а затем нажмите кнопку **ОК**.

### <a name="additional-ssl-resources"></a>Дополнительные ресурсы, посвященные SSL

Шаги, необходимые для настройки центра сертификации, привязки сертификата к веб-сайту WSUS и установки отношения доверия между клиентскими компьютерами и сертификатом, выходят за рамки данного руководства. Дополнительные сведения и инструкции по установке сертификатов и настройке этой среды см. в следующих статьях:

- [Пошаговое руководство по инфраструктуре PKI стандарта Suite B](https://go.microsoft.com/fwlink/?LinkID=203858)

- [Реализация и администрирование шаблонов сертификатов](https://go.microsoft.com/fwlink/?LinkID=203859)

- [Руководство по миграции и обновлению служб сертификатов Active Directory](https://go.microsoft.com/fwlink/?LinkID=203860)

- [Настройка автоматической регистрации сертификатов](https://go.microsoft.com/fwlink/?LinkID=203861)

### <a name="26-complete-iis-configuration"></a>2.6. Завершение настройки служб IIS

По умолчанию для всех новых веб-сайтов IIS и веб-сайтов IIS по умолчанию включен анонимный доступ для чтения. Некоторые приложения, в частности Windows SharePoint Services, могут блокировать анонимный доступ. Если это произошло, необходимо снова включить анонимный доступ для чтения, прежде чем можно будет успешно установить и использовать службы WSUS.

Чтобы включить анонимный доступ для чтения, выполните действия для соответствующей версии IIS.

1. [Включение анонимной проверки подлинности (IIS 7)](https://go.microsoft.com/fwlink/?LinkID=205316), как описано в руководстве пользователя служб IIS 7.

2. [Включение анонимной проверки подлинности (IIS 6.0)](https://go.microsoft.com/fwlink/?LinkId=211391), как описано в руководстве пользователя служб IIS 6.0.

### <a name="27-configure-a-signing-certificate"></a>2.7. Настройка сертификата для подписи

Службы WSUS позволяют публиковать пользовательские пакеты обновления для обновления продуктов Майкрософт и сторонних производителей. Службы WSUS могут автоматически подписывать такие пакеты обновления с помощью сертификата Authenticode. Чтобы включить подписывание пользовательских обновлений, необходимо установить сертификат для подписи пакетов на сервере WSUS. Существуют некоторые аспекты, связанные с подписыванием пользовательских обновлений.

1. **Распространения сертификатов**. Закрытый ключ должен быть установлен на сервере WSUS, а открытый ключ должен быть явно установлен в хранилище доверенных сертификатов на всех клиентских компьютерах и серверах, для которых предназначены подписанные пользовательские обновления.

2. **Окончание срока действия**. При истечении срока действия самозаверяющего сертификата (или его приближении) службы WSUS записывают события в журнал событий.

3. **Обновление и отзыв сертификатов**. Если требуется обновить или отозвать сертификат (например, после обнаружения того, что его срок действия истек), в службах WSUS не предусмотрены функции для решения этих задач. Эти задачи потребуется выполнить вручную, причем их успешность трудно гарантировать как в ручном, так и в автоматическом режиме.
