---
title: Работа с правилами политик ограниченного использования программ
description: Сведения о процедурах, которые работают с сертификатами, путями, зонами Интернета и хэш-правилами с помощью политик ограниченного использования программ.
ms.topic: article
ms.assetid: 4a8047d5-9bb9-4bed-bc8f-583a237731e2
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: cbc6bb676ea699cbfaa3ed3f83c6bbf664c60528
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101830815"
---
# <a name="work-with-software-restriction-policies-rules"></a>Работа с правилами политик ограниченного использования программ

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этом разделе описываются процедуры, работающие с сертификатами, путями, зонами Интернета и правилами хеширования с помощью политик ограниченного использования программ.

## <a name="introduction"></a>Введение
С помощью политик ограниченного использования программ можно защитить вычислительную среду от ненадежного программного обеспечения, определив и указав, какое программное обеспечение разрешено для выполнения. Можно определить уровень безопасности по умолчанию **неограниченный** или **запрещенный** для объекта Групповая политика (GPO), чтобы программное обеспечение было разрешено или запрещено по умолчанию. Исключения можно сделать на уровне безопасности по умолчанию, создав правила политик ограниченного использования программ для конкретного программного обеспечения. Например, если уровень безопасности по умолчанию имеет значение **Запрещено**, можно создавать правила, которые разрешают выполнение отдельных программ. Существуют следующие типы правил.

-   **Правила для сертификатов**

    Процедуры см. в разделе о [работе с правилами для сертификатов](#BKMK_Cert_Rules).

-   **Правила хэширования**

    Процедуры см. в разделе о [работе с правилами хэширования](#BKMK_Hash_Rules).

-   **Правила для зон Интернета**

    Процедуры см. [в разделе Работа с правилами зоны Интернета](#BKMK_Internet_Zone_Rules).

-   **Правила для путей**

    Процедуры см. в разделе о [работе с правилами для путей](#BKMK_Path_Rules).

Сведения о других задачах для управления политиками ограниченного использования программ см. в разделе [Администрирование политик ограниченного использования программ](administer-software-restriction-policies.md).

## <a name="working-with-certificate-rules"></a><a name="BKMK_Cert_Rules"></a>Работа с правилами для сертификатов
Политики ограниченного использования программ могут также обнаруживать программное обеспечение по его сертификату подписи. Можно создать правило для сертификата, которое определяет программу, а потом разрешает или запрещает ее запуск в зависимости от уровня безопасности. Например, с помощью правил для сертификатов можно автоматически считать доверенным программное обеспечение из доверенного источника в домене, не запрашивая пользователя. С помощью правил для сертификатов также можно запускать файлы в запрещенных областях операционной системы. По умолчанию правила для сертификатов не включены.

При создании правил для домена с помощью групповая политика необходимо иметь разрешения на создание или изменение объекта групповая политика. При создании правил для локального компьютера необходимы административные учетные данные на этом компьютере.

#### <a name="to-create-a-certificate-rule"></a>Создание правила для сертификатов

1.  Откройте окно "Политики ограниченного использования программ".

2.  В дереве консоли или области сведений щелкните правой кнопкой мыши **Дополнительные правила**, а затем выберите команду **создать правило сертификата**.

3.  Нажмите кнопку **Обзор** и выберите сертификат или подписанный файл.

4.  В списке **уровень безопасности** выберите значение **запрещено** или не **ограничено**.

5.  В поле **Описание** введите описание данного правила и нажмите кнопку **ОК**.

> [!NOTE]
> -   Может понадобиться создать новый параметр политики ограниченного использования программ для объекта групповой политики, если это еще не сделано.
> -   По умолчанию правила для сертификатов не включены.
> -   Правила для сертификатов действуют только на те типы файлов, которые включены в список **Назначенные типы файлов** в области сведений для политик ограниченного использования программ. Все правила используют общий список назначенных типов файлов.
> -   Чтобы политики ограниченного использования программ вступили в силу, пользователи должны обновить параметры политики, выполнив выход из системы и войдя в систему на своих компьютерах.
> -   Если к параметрам политики применяется более одного правила политики ограниченного использования программ, для обработки конфликтов существует приоритет правил.

### <a name="enabling-certificate-rules"></a>Включение правил для сертификатов
Правила для сертификатов включаются различными процедурами в зависимости от среды.

-   [Для локального компьютера](#BKMK_1)

-   [Для объекта групповая политика и находится на сервере, присоединенном к домену.](#BKMK_2)

-   [Для групповая политика объекта, на контроллере домена или на рабочей станции с установленным средства удаленного администрирования сервера](#BKMK_3)

-   [Только для контроллеров домена, на контроллере домена или на рабочей станции с установленным пакетом средства удаленного администрирования сервера](#BKMK_4)

#### <a name="to-enable-certificate-rules-for-your-local-computer"></a><a name="BKMK_1"></a>Включение правил сертификатов для локального компьютера

1.  Откройте окно "Локальные параметры безопасности".

2.  В дереве консоли щелкните **Параметры безопасности** , расположенные в разделе Параметры безопасности/Локальные политики.

3.  В области сведений дважды щелкните элемент **Параметры системы: использовать правила сертификатов для исполняемых файлов Windows для политик ограниченного использования программ**.

4.  Выполните одно из следующих действий, а затем нажмите кнопку **ОК**.

    -   Чтобы включить правила для сертификатов, выберите вариант **Включено**.

    -   Чтобы отключить правила для сертификатов, выберите вариант **Отключено**.

#### <a name="to-enable-certificate-rules-for-a-group-policy-object-and-you-are-on-a-server-that-is-joined-to-a-domain"></a><a name="BKMK_2"></a>Включение правил сертификатов для объекта групповая политика и на сервере, присоединенном к домену

1.  Откройте консоль управления (MMC).

2.  В меню **Файл** выберите команду **Добавить или удалить оснастку** и нажмите кнопку **Добавить**.

3.  Щелкните элемент **Редактор объектов групповой политики** и нажмите кнопку **Добавить**.

4.  В окне **Выбор объекта групповой политики** нажмите кнопку **Обзор**.

5.  В окне **поиск групповая политика объекта** выберите объект Групповая политика (GPO) в соответствующем домене, сайте или подразделении или создайте новый, а затем нажмите кнопку **Готово**.

6.  Щелкните **Закрыть**, а затем нажмите кнопку **ОК**.

7.  В дереве консоли щелкните **Параметры безопасности** , расположенные в разделе *граупполициобжект* [*имя_компьютера*] Политика/Конфигурация компьютера/параметры Windows/параметры безопасности/Локальные политики/.

8.  В области сведений дважды щелкните элемент **Параметры системы: использовать правила сертификатов для исполняемых файлов Windows для политик ограниченного использования программ**.

9. Если этот параметр политики еще не определен, установите флажок **Определить параметры политики**.

10. Выполните одно из следующих действий, а затем нажмите кнопку **ОК**.

    -   Чтобы включить правила для сертификатов, выберите вариант **Включено**.

    -   Чтобы отключить правила для сертификатов, выберите вариант **Отключено**.

#### <a name="to-enable-certificate-rules-for-a-group-policy-object-and-you-are-on-a-domain-controller-or-on-a-workstation-that-has-the-remote-server-administration-tools-installed"></a><a name="BKMK_3"></a>Включение правил сертификатов для объекта групповая политика, на контроллере домена или на рабочей станции с установленным средства удаленного администрирования сервера

1.  Откройте оснастку "Пользователи и компьютеры Active Directory".

2.  В дереве консоли щелкните правой кнопкой мыши объект групповой политики, для которого следует включить правила для сертификатов.

3.  Выберите пункт **Свойства** и перейдите на вкладку **Групповая политика**.

4.  Нажмите кнопку **Изменить**, чтобы открыть объект групповой политики для правки. Также можно нажать кнопку **Создать**, чтобы создать новый объект групповой политики, а затем нажать кнопку **Изменить**.

5.  В дереве консоли щелкните **Параметры безопасности** , расположенные в разделе *граупполициобжект*[*имя_компьютера*] Политика/Конфигурация компьютера/параметры Windows/параметры безопасности/Локальные политики.

6.  В области сведений дважды щелкните элемент **Параметры системы: использовать правила сертификатов для исполняемых файлов Windows для политик ограниченного использования программ**.

7.  Если этот параметр политики еще не определен, установите флажок **Определить параметры политики**.

8.  Выполните одно из следующих действий, а затем нажмите кнопку **ОК**.

    -   Чтобы включить правила для сертификатов, выберите вариант **Включено**.

    -   Чтобы отключить правила для сертификатов, выберите вариант **Отключено**.

#### <a name="to-enable-certificate-rules-for-only-domain-controllers-and-you-are-on-a-domain-controller-or-on-a-workstation-that-has-the-remote-server-administration-tools-installed"></a><a name="BKMK_4"></a>Включение правил сертификатов только для контроллеров домена, на контроллере домена или на рабочей станции с установленным средства удаленного администрирования сервера

1.  Откройте консоль параметров безопасности контроллера домена.

2.  В дереве консоли щелкните элемент **Параметры безопасности**, расположенный в узле "Политика *объект_групповой_политики**[имя_компьютера]*/Конфигурация компьютера/Конфигурация Windows/Параметры безопасности/Локальные политики".

3.  В области сведений дважды щелкните элемент **Параметры системы: использовать правила сертификатов для исполняемых файлов Windows для политик ограниченного использования программ**.

4.  Если этот параметр политики еще не определен, установите флажок **Определить параметры политики**.

5.  Выполните одно из следующих действий, а затем нажмите кнопку **ОК**.

    -   Чтобы включить правила для сертификатов, выберите вариант **Включено**.

    -   Чтобы отключить правила для сертификатов, выберите вариант **Отключено**.

> [!NOTE]
> Эту процедуру необходимо выполнить, чтобы правила для сертификатов вступили в силу.

### <a name="set-trusted-publisher-options"></a>Настройка параметров доверенного издателя
Все большее число издателей программного обеспечения и разработчиков приложений используют подписи для программного обеспечения, чтобы подтвердить, что их приложения поступают из надежного источника. Однако многие пользователи не понимают назначение сертификатов подписей, связанных с устанавливаемыми приложениями, или уделяют им мало внимания.

Параметры политики на вкладке **Доверенные издатели** в окне политики проверки пути сертификации позволяют администраторам контролировать, какие сертификаты могут приниматься как поступающие от доверенного издателя.

##### <a name="to-configure-the-trusted-publishers-policy-settings-for-a-local-computer"></a>Настройка параметров политики доверенных издателей для локального компьютера

1.  На **начальном** экране введите **gpedit. msc** и нажмите клавишу ВВОД.

2.  В дереве консоли в разделе **Политика "Локальный компьютер"\Конфигурация компьютера\Конфигурация Windows\Параметры безопасности** щелкните пункт **Политики открытого ключа**.

3.  Дважды щелкните элемент **Параметры подтверждения пути сертификата**, а затем перейдите на вкладку **Доверенные издатели**.

4.  Установите флажок **Определить следующие параметры политики**, выберите параметры политики, которые нужно применить, затем нажмите кнопку **ОК**, чтобы применить новые параметры.

##### <a name="to-configure-the-trusted-publishers-policy-settings-for-a-domain"></a>Настройка параметров политики доверенных издателей для домена

1.  Откройте раздел **Управление групповой политикой**.

2.  В дереве консоли дважды щелкните **Групповая политика объекты** в лесу и домене, содержащие объект **политики домена по умолчанию** групповая политика объекта (GPO), который требуется изменить.

3.  Щелкните объект **Политика домена по умолчанию** правой кнопкой мыши и выберите команду **Изменить**.

4.  В дереве консоли в разделе **Конфигурация компьютера\Параметры Windows\Параметры безопасности** щелкните пункт **Политики открытого ключа**.

5.  Дважды щелкните элемент **Параметры подтверждения пути сертификата**, а затем перейдите на вкладку **Доверенные издатели**.

6.  Установите флажок **Определить следующие параметры политики**, выберите параметры политики, которые нужно применить, затем нажмите кнопку **ОК**, чтобы применить новые параметры.

##### <a name="to-allow-only-administrators-to-manage-certificates-used-for-code-signing-for-a-local-computer"></a>Чтобы разрешить только администраторам управление сертификатами, используемыми для подписи кода на локальном компьютере, выполните следующие действия.

1.  На **начальном** экране введите команду **gpedit. msc** в поле **поиска программы и файлы** или в Windows 8 на рабочем столе и нажмите клавишу ВВОД.

2.  В дереве консоли в разделе **Политика домена по умолчанию** или **Политика локального компьютера** дважды щелкните **Конфигурация компьютера**, **Параметры Windows** и **Параметры безопасности**, а затем щелкните **политики открытого ключа**.

3.  Дважды щелкните элемент **Параметры подтверждения пути сертификата**, а затем перейдите на вкладку **Доверенные издатели**.

4.  Установите флажок **Определить параметры политики**.

5.  В группе **Управление доверенными издателями** щелкните **Разрешать всем администраторам управлять доверенными издателями**, а затем нажмите кнопку **ОК**, чтобы применить новые параметры.

##### <a name="to-allow-only-administrators-to-manage-certificates-used-for-code-signing-for-a-domain"></a>Чтобы разрешить только администраторам управление сертификатами, используемыми для подписи кода в домене, выполните следующие действия.

1.  Откройте раздел **Управление групповой политикой**.

2.  В дереве консоли дважды щелкните **Групповая политика объектов** в лесу и домене, содержащем объект групповой **политики домена по умолчанию** , который необходимо изменить.

3.  Щелкните объект **Политика домена по умолчанию** правой кнопкой мыши и выберите команду **Изменить**.

4.  В дереве консоли в разделе **Конфигурация компьютера\Параметры Windows\Параметры безопасности** щелкните пункт **Политики открытого ключа**.

5.  Дважды щелкните элемент **Параметры подтверждения пути сертификата**, а затем перейдите на вкладку **Доверенные издатели**.

6.  Установите флажок **Определить следующие параметры политики**, внесите нужные изменения, а затем нажмите кнопку **ОК**, чтобы применить новые параметры.

## <a name="working-with-hash-rules"></a><a name="BKMK_Hash_Rules"></a>Работа с правилами хэширования
Хэш — это последовательность байтов фиксированной длины, уникальным образом определяющая программу или файл. Хэш вычисляется по хэш-алгоритму. Когда для программы создается правило хэширования, политики ограниченного использования программ вычисляют хэш программы. Когда пользователь пытается открыть программу, ее хэш сравнивается с существующими правилами хэширования для политик ограниченного использования программ. Хэш программы остается неизменным независимо от ее расположения на компьютере. Однако если программа каким-либо образом меняется, то ее хэш также меняется и перестает совпадать с хэшем в правиле хэширования для политик ограниченного использования программ.

Например, можно создать правило хэширования и задать уровень безопасности **Запрещено**, чтобы запретить пользователям запускать определенный файл. Этот файл можно переименовать или переместить в другую папку, однако он будет иметь тот же хэш. Однако при изменении содержимого файла его хэш-значение также изменится, и файл сможет обойти ограничения.

#### <a name="to-create-a-hash-rule"></a>Создание правила хэширования

1.  Откройте окно "Политики ограниченного использования программ".

2.  В дереве консоли или области сведений щелкните правой кнопкой мыши **Дополнительные правила**, а затем выберите **создать правило хэширования**.

3.  Нажмите кнопку **Обзор** , чтобы найти файл.

    > [!NOTE]
    > В Windows XP можно вставить предварительно вычисленный хэш в **хэш файла**. В Windows Server 2008 R2, Windows 7 и более поздних версиях этот параметр недоступен.

4.  В списке **уровень безопасности** выберите значение **запрещено** или не **ограничено**.

5.  В поле **Описание** введите описание данного правила и нажмите кнопку **ОК**.

> [!NOTE]
> -   Может понадобиться создать новый параметр политики ограниченного использования программ для объекта групповой политики, если это еще не сделано.
> -   Правило хэширования можно создать для вируса или вредоносной программы типа "троянский конь", чтобы предотвратить их запуск.
> -   Если вы хотите, чтобы другие пользователи использовали правило хэширования, чтобы вирус не смог запуститься, вычислите хэш вируса с помощью политик ограниченного использования программ, а затем отдавайте по электронной почте значение хэша другим людям. Никогда не отменяйте электронную почту самого вируса.
> -   Если вирус был отправлен по электронной почте, можно также создать правило для пути, чтобы предотвратить выполнение вложений электронной почты.
> -   После переименования или перемещения в другую папку файл будет иметь тот же хэш. Любые изменения в самом файле приводят к другому хэшу.
> -   Правила хэширования действуют только на те типы файлов, которые включены в список **Назначенные типы файлов** в области сведений для политик ограниченного использования программ. Все правила используют общий список назначенных типов файлов.
> -   Чтобы политики ограниченного использования программ вступили в силу, пользователи должны обновить параметры политики, выполнив выход из системы и войдя в систему на своих компьютерах.
> -   Если к параметрам политики применяется более одного правила политики ограниченного использования программ, для обработки конфликтов существует приоритет правил.

## <a name="working-with-internet-zone-rules"></a><a name="BKMK_Internet_Zone_Rules"></a>Работа с правилами зоны Интернета
Правила для зон Интернета применяются только к пакетам установщика Windows. Правило для зоны может определять программу из зоны, заданной в Internet Explorer. Это зоны "Интернет", "Локальная интрасеть", "Опасные сайты", "Надежные сайты" и "Мой компьютер". Правило зоны Интернета предназначено для предотвращения загрузки и установки программного обеспечения пользователями.

#### <a name="to-create-an-internet-zone-rule"></a>Создание правила для зоны Интернета

1.  Откройте окно "Политики ограниченного использования программ".

2.  В дереве консоли или области сведений щелкните правой кнопкой мыши **Дополнительные правила**, а затем выберите **создать правило зоны Интернета**.

3.  В поле **Зона Интернета** выберите зону Интернета.

4.  На панели **уровень безопасности** выберите **запрещенные** или **неограниченные**, а затем нажмите кнопку **ОК**.

> [!NOTE]
> -   Может понадобиться создать новый параметр политики ограниченного использования программ для объекта групповой политики, если это еще не сделано.
> -   Правила для зон применяются только к файлам типа MSI, то есть к пакетам установщика Windows.
> -   Чтобы политики ограниченного использования программ вступили в силу, пользователи должны обновить параметры политики, выполнив выход из системы и войдя в систему на своих компьютерах.
> -   Если к параметрам политики применяется более одного правила политики ограниченного использования программ, для обработки конфликтов существует приоритет правил.

## <a name="working-with-path-rules"></a><a name="BKMK_Path_Rules"></a>Работа с правилами для путей
Правило для пути определяет программу по пути к ее файлу. Например, даже если для компьютера задан уровень безопасности по умолчанию **Запрещено**, можно предоставить каждому пользователю неограниченный доступ к определенной папке. Можно создать правило для пути с помощью пути к файлу и задать в правиле для пути уровень безопасности **Не ограничено**. Для этого типа правила часто используются пути %userprofile%, %windir%, %appdata%, %programfiles% и %temp%. Также можно создавать правила для пути в реестре, где путем служит раздел реестра для программы.

Поскольку такие правила задаются для пути, при перемещении программы правило для пути перестает действовать.

#### <a name="to-create-a-path-rule"></a>Создание правила для пути

1.  Откройте окно "Политики ограниченного использования программ".

2.  В дереве консоли или области сведений щелкните правой кнопкой мыши **Дополнительные правила**, а затем выберите команду **создать правило для пути**.

3.  В поле **Путь** введите путь или нажмите кнопку **Обзор**, чтобы найти файл или папку.

4.  В списке **уровень безопасности** выберите значение **запрещено** или не **ограничено**.

5.  В поле **Описание** введите описание данного правила и нажмите кнопку **ОК**.

> [!CAUTION]
> -   В некоторых папках, например в папке Windows, установка уровня безопасности « **запрещено** » может негативно сказаться на работе операционной системы. Убедитесь, что не запрещается доступ к важному компоненту операционной системы или какой-либо из ее зависимых программ.

> [!NOTE]
> -   Может понадобиться создать новые политики ограниченного использования программ для объекта групповой политики, если это еще не сделано.
> -   Если создать правило для пути для программы с уровнем безопасности **Запрещено**, пользователи смогут запустить эту программу, скопировав ее в другое место.
> -   В правиле для пути поддерживаются подстановочные знаки звездочки (*) и вопроса (?).
> -   В правиле для пути можно использовать переменные среды, например %programfiles% и %systemroot%.
> -   Если нужно создать правило для программы, когда неизвестно ее расположение на компьютере, но имеется ее раздел реестра, то можно создать правило для пути в реестре.
> -   Чтобы запретить пользователям выполнять вложения электронной почты, можно создать правило для пути к каталогу вложений программы электронной почты, которое запрещает пользователям запускать вложения электронной почты.
> -   Правила для путей действуют только на те типы файлов, которые включены в список **Назначенные типы файлов** в области сведений для политик ограниченного использования программ. Все правила используют общий список назначенных типов файлов.
> -   Чтобы политики ограниченного использования программ вступили в силу, пользователи должны обновить параметры политики, выполнив выход из системы и войдя в систему на своих компьютерах.
> -   Если к параметрам политики применяется более одного правила политики ограниченного использования программ, для обработки конфликтов существует приоритет правил.

#### <a name="to-create-a-registry-path-rule"></a>Создание правила для пути в реестре

1.  На **начальном** экране введите regedit.

2.  В дереве консоли щелкните правой кнопкой мыши раздел реестра, для которого нужно создать правило, и выберите команду **Копировать имя раздела**. Найдите параметр в области сведений.

3.  Откройте окно "Политики ограниченного использования программ".

4.  В дереве консоли или области сведений щелкните правой кнопкой мыши **Дополнительные правила**, а затем выберите команду **создать правило для пути**.

5.  В поле **путь** вставьте имя раздела реестра, за которым следует имя значения.

6.  Заключите путь реестра в знаки процента (%), например% HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PlatformSDK\Directories\InstallDir%.

7.  В списке **уровень безопасности** выберите значение **запрещено** или не **ограничено**.

8.  В поле **Описание** введите описание данного правила и нажмите кнопку **ОК**.


