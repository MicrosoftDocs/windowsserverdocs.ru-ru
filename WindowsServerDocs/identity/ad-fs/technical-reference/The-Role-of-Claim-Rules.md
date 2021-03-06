---
description: 'Дополнительные сведения: роль правил утверждений'
ms.assetid: 65e474b5-3076-4ba3-809d-a09160f7c2bd
title: Роль правил утверждений
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 738d15fa7303610ddbb8c3297bc056f9db61ca2d
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97045332"
---
# <a name="the-role-of-claim-rules"></a>Роль правил утверждений
Общей функцией служба федерации в службы федерации Active Directory (AD FS) \( AD FS \) является выдача маркера, содержащего набор утверждений. Решение о том, какие утверждения AD FS принимают, а затем проблемы определяются правилами утверждений.

## <a name="what-are-claim-rules"></a>Что такое правила утверждений
Правило утверждения представляет экземпляр бизнес-логики, который принимает одно или несколько входящих утверждений, применяет к ним условия, \( если x then y \) и создает одно или несколько исходящих утверждений на основе параметров условия. Дополнительные сведения о входящих и исходящих утверждениях см. [в разделе роль утверждений](The-Role-of-Claims.md).

Правила утверждений используются, когда необходимо реализовать бизнес-логику, контролирующую поток утверждений через конвейер утверждений. Хотя конвейер утверждений является более логичным понятием сквозного \- \- процесса для передаваемых утверждений, правила утверждений — это фактический административный элемент, который можно использовать для настройки потока заявок с помощью процесса выдачи утверждений.

Дополнительные сведения о конвейере утверждений см. [в разделе роль подсистемы утверждений](The-Role-of-the-Claims-Engine.md).

Правила утверждений обеспечивают следующие преимущества:

-   Предоставление администраторам механизма применения \- бизнес-логики среды выполнения для доверия утверждений от поставщиков утверждений

-   предоставляют администраторам механизм определения утверждений, которые должны предоставляться проверяющим сторонам;

-   Предоставьте \- администраторам, которым требуется разрешить или запретить доступ определенным пользователям, широкие и подробные возможности авторизации на основе утверждений.

### <a name="how-claim-rules-are-processed"></a>Порядок обработки правил утверждений
Правила утверждений обрабатываются посредством конвейера утверждений с помощью *модуля утверждений*. Модуль утверждений — это логический компонент службы федерации, который проверяет набор входящих утверждений, представленный пользователем, и в соответствии с логикой каждого правила создает выходной набор утверждений.

Подсистема правил утверждений и набор правил утверждений, связанных с данным федеративным доверием, определяют, должны ли входящие утверждения передаваться по мере их поступления, фильтроваться в соответствии с критериями определенного условия или преобразовываться в совершенно новый набор утверждений, прежде чем они выдаются в качестве исходящих утверждений служба федерации.

Дополнительные сведения об этом процессе см. [в разделе роль подсистемы утверждений](The-Role-of-the-Claims-Engine.md).

## <a name="what-are-claim-rule-templates"></a>Что такое шаблоны правил утверждений
AD FS включает предопределенный набор шаблонов правил утверждений, предназначенных для упрощения выбора и создания наиболее подходящих правил утверждений в соответствии с нуждами конкретного бизнеса. Шаблоны правил утверждений используются только в процессе создания правил утверждений.

В оснастке управления AD FS \- в можно создавать правила только с помощью шаблонов правил утверждений. После использования оснастки \- для выбора шаблона правила утверждения введите необходимые данные для логики правила и сохраните их в базе данных конфигурации. в этом случае \( \) в пользовательском интерфейсе в качестве правила утверждения будет отображаться ссылка на этот момент.

### <a name="how-claim-rule-templates-work"></a>Как работают шаблоны правил утверждений
На первый взгляд шаблоны правил заявок являются просто формами ввода, предоставляемыми оснасткой, \- для получения данных и обработки конкретной логики входящих утверждений. Однако если взглянуть глубже, окажется, что в шаблонах правил утверждений хранятся языковые структуры правил утверждений, которые образуют базовую логику, необходимую для быстрого создания правила без близкого знакомства с языком.

Каждый шаблон, предоставляемый в пользовательском интерфейсе \( пользовательского интерфейса \) , представляет предварительно заполненный синтаксис языка правил для утверждений на основе наиболее часто необходимых административных задач. Однако один шаблон правил представляет исключение. Он называется настраиваемым шаблонов правил. В этом шаблоне синтаксис не заполнен. Вместо этого вам надо самостоятельно составить синтаксическую структуру языка правил утверждений в теле формы шаблона.

Дополнительные сведения об использовании синтаксиса языка правил для утверждений см. в разделе [роль языка правил утверждений](The-Role-of-the-Claim-Rule-Language.md) руководства по развертыванию AD FS.

> [!TIP]
> В любой момент можно просмотреть язык правила утверждения, связанный с правилом, нажав кнопку **Просмотреть язык правила** в свойствах правила утверждения.

### <a name="how-to-create-a-claim-rule"></a>Создание правила утверждения
Правила утверждений создаются отдельно для каждого федеративного отношения доверия в службе федерации и не используются совместно несколькими отношениями. Вы можете создать правило на основе шаблона правил утверждений, создать правило с нуля с помощью языка правил утверждений или настроить правило с помощью Windows PowerShell.

Все эти варианты доступны одновременно, что обеспечивает гибкость при выборе подходящего способа для конкретного сценария. Дополнительные сведения о создании правила утверждений см. в разделе [Настройка правил утверждений](../deployment/configuring-claim-rules.md) в справочнике по AD фсдеплоймент.

#### <a name="using-claim-rule-templates"></a>Использование шаблонов правил утверждений
Шаблоны правил утверждений используются только в процессе создания правил утверждений. Для создания правила утверждения можно использовать любой из следующих шаблонов:

-   Пропуск или фильтрация входящего утверждения

-   Преобразование входящего утверждения

-   Отправка атрибутов LDAP как утверждений

-   Отправка членства в группах в качестве утверждения

-   Отправка утверждений с помощью настраиваемого правила

-   Разрешать или запрещать пользователям на основании входящего утверждения

-   Разрешить всем пользователям

Дополнительные сведения о каждом из этих шаблонов правил заявок см. [в разделе Определение типа используемого шаблона правила для утверждений](Determine-the-Type-of-Claim-Rule-Template-to-Use.md).

#### <a name="using-the-claim-rule-language"></a>С помощью языка правил утверждений
Для бизнес-правил, не охватываемых стандартными шаблонами правил утверждений, можно использовать настраиваемый шаблон правила для выражения сложных условий логики с помощью языка правил утверждений. Дополнительные сведения об использовании настраиваемого правила см. в разделе [когда следует использовать настраиваемое правило утверждения](When-to-Use-a-Custom-Claim-Rule.md).

#### <a name="using-windows-powershell"></a>Использование Windows PowerShell
Можно также использовать объект командлета Адфсклаимрулесет с Windows PowerShell для создания или администрирования правил в AD FS. Подробнее об использовании этого командлета в Windows PowerShell см. в разделе [Администрирование служб федерации Active Directory с помощью Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=179634).

## <a name="what-is-a-claim-rule-set"></a>Что такое набор правил утверждений
Как показано на рисунке ниже, набор правил утверждений — это группа из одного или нескольких правил для определенного федеративного отношения доверия, которая определяет способ обработки утверждений модулем утверждений. Когда служба федерации получает входящее утверждение, модуль утверждений применяет логику, заданную в соответствующем наборе правил утверждений. То, как будут выпущены утверждения для всего отношения доверия, определяется общим результатом применения логики из каждого правила в наборе.

![Роли AD FS](media/adfs2_claimruleset.gif)

Правила утверждений обрабатываются модулем утверждений в хронологическом порядке в пределах заданного набора правил. Этот порядок важен, так как выходные данные одного правила могут служить входными данными для следующего правила в наборе.

## <a name="what-are-claim-rule-set-types"></a>Типы наборов правил утверждений
Тип набора правил утверждений — это логическая часть федеративного отношения доверия, которая категорически определяет, будет ли набор правил утверждений, связанный с отношением доверия, использоваться для выдачи, авторизации или принятия утверждений. С каждым федеративным отношением доверия может быть связан один или несколько типов наборов правил утверждений в зависимости от типа этого отношения.

В таблице ниже описываются различные типы наборов правил утверждений и объясняется их связь с отношением доверия с поставщиком утверждений или с отношением доверия с проверяющей стороной.

|Тип набора правил утверждений|Описание|Область применения|
|-----------------------|---------------|-----------|
|Набор правил преобразования принятия|Набор правил утверждений, применяющийся к определенному отношению доверия с поставщиком утверждений для указания входящих утверждений, которые будут приняты от организации поставщика утверждений, и исходящих утверждений, которые будут отправлены в отношение доверия с проверяющей стороной.<p>Входящие утверждения, служащие источником для этого набора правил, будут выходными утверждениями набора правил преобразования выдачи, определенного в организации поставщика утверждений.<p>По умолчанию узел отношений доверия с поставщиком утверждений содержит отношение с именем **Active Directory**, которое представляет исходное хранилище атрибутов для набора правил преобразования принятия. Этот объект отношения доверия представляет связь службы федерации с базой данных Active Directory в вашей сети. Именно это отношение доверия по умолчанию обрабатывает утверждения для пользователей, прошедших аутентификацию в Active Directory, и его нельзя удалить.|Отношения доверия с поставщиком утверждений|
|Набор правил преобразования выдачи|Набор правил утверждений, который применяется к отношению доверия с проверяющей стороной для указания утверждений, которые будут выданы проверяющей стороне.<p>Входящие утверждения, служащие источником для этого набора правил, изначально будут выходными утверждениями правил преобразования принятия.|Отношения доверия с проверяющей стороной|
|Набор правил авторизации выдачи|Набор правил утверждений, который применяется к отношению доверия с проверяющей стороной для указания пользователей, которым будет разрешено получить токен для проверяющей стороны.<p>Эти правила определяют, может ли пользователь получать утверждения для проверяющей стороны и, таким образом, получать доступ к ней.<p>Если правило авторизации выдачи не задано, по умолчанию доступ запрещен для всех пользователей.|Отношения доверия с проверяющей стороной|
|Набор правил авторизации делегирования|Набор правил утверждений, который применяется к отношению доверия с проверяющей стороной для указания пользователей, которым будет разрешено выступать в роли делегатов других пользователей для проверяющей стороны.<p>Эти правила определяют, разрешено ли инициатору запроса выступать от лица пользователя. При этом инициатор запроса указывается в токене, отправляемом проверяющей стороне.<p>Если не указано правило авторизации делегирования, пользователи по умолчанию не могут действовать как делегаты.|Отношения доверия с проверяющей стороной|
|Набор правил авторизации олицетворения|Набор правил утверждений, который настраивается с помощью Windows PowerShell для определения того, может ли пользователь полностью олицетворять другого пользователя для проверяющей стороны.<p>Эти правила определяют, разрешено ли инициатору запроса олицетворять пользователя без указания инициатора в токене, отправляемом проверяющей стороне.<p>Такое олицетворение пользователя — это очень эффективная возможность, так как проверяющей стороне будет неизвестно, что пользователь олицетворяется.|Отношения доверия с проверяющей стороной|

Дополнительные сведения о выборе соответствующих правил утверждений для использования в организации см. в разделе [Определение типа используемого шаблона правила для утверждений](Determine-the-Type-of-Claim-Rule-Template-to-Use.md).
