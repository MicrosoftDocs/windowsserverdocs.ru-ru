---
title: Общие сведения о кворуме кластеров и пулов
description: Общие сведения о кластере и кворуме пула с конкретными примерами для перебора сложных.
ms.author: adagashe
manager: eldenc
ms.topic: article
author: adagashe
ms.date: 01/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: ffd1afdc76ddefbf53ff8f78d15666f343654022
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970141"
---
# <a name="understanding-cluster-and-pool-quorum"></a>Общие сведения о кворуме кластеров и пулов

>Применяется к: Windows Server 2019, Windows Server 2016

[Отказоустойчивая кластеризация Windows Server](../../failover-clustering/failover-clustering-overview.md) обеспечивает высокий уровень доступности для рабочих нагрузок. Эти ресурсы считаются высокодоступными, если узлы, на которых размещены ресурсы, работают; Однако кластер обычно требует более половины выполняемых узлов, что называется наличием *кворума*.

Кворум предназначен для предотвращения сценариев с *разделением* , которые могут возникнуть, если в сети есть секция и подмножества узлов не могут взаимодействовать друг с другом. Это может привести к тому, что оба подмножества узлов пытаются владеть рабочей нагрузкой и запись на тот же диск, что может привести к многочисленным проблемам. Однако это предотвращается концепцией кворума отказоустойчивой кластеризации, которая приводит к тому, что только одна из этих групп узлов продолжает работать, поэтому только одна из этих групп останется в сети.

Кворум определяет количество сбоев, в течение которых кластер может оставаться в сети. Кворум предназначен для решения проблемы связи между подмножествами узлов кластера, так что несколько серверов не пытаются одновременно разместить группу ресурсов и записывать их на один и тот же диск. Используя эту концепцию кворума, кластер принудительно останавливает службу кластеров в одном из подмножеств узлов, чтобы убедиться, что существует только один истинный владелец определенной группы ресурсов. После того как остановленные узлы снова взаимодействуют с основной группой узлов, они автоматически повторно присоединяются к кластеру и запускают службу кластеров.

В Windows Server 2019 и Windows Server 2016 есть два компонента системы с собственными механизмами кворума:

- **Кворум кластера**. это работает на уровне кластера (т. е. Вы можете потерять узлы и оставить кластер неизменным).
- **Кворум пула**. это происходит на уровне пула, если включен Локальные дисковые пространства (т. е. можно потерять узлы и диски, чтобы они оставались в пуле). Пулы носителей были разработаны для использования как в кластеризованных, так и в некластеризованных сценариях, поэтому у них есть другой механизм кворума.

## <a name="cluster-quorum-overview"></a>Общие сведения о кворуме кластера

В таблице ниже приводятся общие сведения о результатах кворума кластера для каждого сценария.

| Узлы сервера | Может содерживаться сбоя одного узла сервера | Может сосуществовать один сбой узла сервера, а затем другой | Может содерживаться двух сбоев одновременного узла сервера |
|--------------|-------------------------------------|---------------------------------------------------|----------------------------------------------------|
| 2            | 50/50                               | Нет                                                | Нет                                                 |
| 2 + следящий сервер  | да                                 | Нет                                                | Нет                                                 |
| 3            | Да                                 | 50/50                                             | Нет                                                 |
| 3 + следящий сервер  | да                                 | да                                               | Нет                                                 |
| 4            | Да                                 | да                                               | 50/50                                              |
| 4 + следящий сервер  | да                                 | да                                               | да                                                |
| 5 и выше  | да                                 | да                                               | да                                                |

### <a name="cluster-quorum-recommendations"></a>Рекомендации по кворуму кластера

- При наличии двух узлов **требуется**следящий сервер.
- При наличии трех или четырех узлов **настоятельно рекомендуется использовать**следящий сервер.
- Если у вас есть доступ к Интернету, используйте ** [следящий сервер облака](../../failover-clustering/deploy-cloud-witness.md) .**
- Если вы находитесь в среде ИТ с другими компьютерами и общими папками, используйте файловый ресурс-свидетель

## <a name="how-cluster-quorum-works"></a>Как работает кворум кластера

Если происходит сбой узлов или если какое-либо подмножество узлов теряет связь с другим подмножеством, остальные узлы должны убедиться, что они составляют *большую* часть кластера, чтобы остаться в сети. Если они не могут проверить, они будут переведены в автономный режим.

Но концепция *большинства* работает только в том случае, если общее число узлов в кластере нечетное (например, три узла в кластере из пяти узлов). Итак, как насчет кластеров с четным числом узлов (скажем, кластером из четырех узлов)?

Существует два способа, с помощью которых кластер может сделать *Общее число* нечетных голосов:

1. Во-первых, его *up* можно добавить, добавив *следящий сервер* с дополнительным проголосуем. Для этого требуется настройка пользователя.
2.    Кроме того, он может *Перейти на* другой узел, отменив один несчастливый голос узла (происходит автоматически по мере необходимости).

Когда работоспособные узлы успешно проверяют, что они являются *большинством*, определение *большинства* обновляется так, чтобы быть в выжившие объекты поколений. Это позволяет кластеру потерять один узел, затем другой, другой и т. д. Эта концепция *общего числа голосов* , адаптированных после последовательных сбоев, называется ***динамическим кворумом***.

### <a name="dynamic-witness"></a>Динамический следящий сервер

Динамический следящий сервер переключает голос следящего сервера, чтобы убедиться, что *Общее число голосов* нечетное. Если число голосов нечетное, следящий сервер не имеет голоса. Если имеется четное число голосов, следящий сервер имеет голосование. Динамический следящий сервер значительно снижает риск отказа кластера из-за сбоя следящего сервера. Кластер принимает решение, следует ли использовать голосование следящего сервера в зависимости от числа узлов голосования, доступных в кластере.

Динамический кворум работает с динамическим следящим сервером, как описано ниже.

### <a name="dynamic-quorum-behavior"></a>Динамическое поведение кворума

- Если у вас **четное** число узлов и следящий сервер, *один узел получает свой голос, равный нулю*. Например, только три из четырех узлов получают голоса, поэтому *Общее число голосов* равно трем, а два выжившие объекты поколений с голосовыми данными считаются большинством.
- При наличии **нечетного** числа узлов и отсутствия следящего сервера *все они получают голоса*.
- Если у вас **четное** число узлов плюс следящий сервер, *то в нем*будет нечетные голос.
- При наличии **нечетного** числа узлов и следящего сервера *следящий сервер не проголосует*.

Динамический кворум позволяет назначать голосование на узел динамически, чтобы избежать потери большинства голосов и разрешать кластеру работать с одним узлом (который называется Last-Man). Возьмем в качестве примера кластер из четырех узлов. Предположим, что для кворума требуется 3 голоса.

В этом случае кластер был бы отключен, если вы потеряли два узла.

![Схема, на которой показаны четыре узла кластера, каждый из которых получает голосование](media/understand-quorum/dynamic-quorum-base.png)

Однако динамический кворум предотвращает возникновение этого события. *Общее число голосов* , необходимых для кворума, теперь определяется на основе числа доступных узлов. Таким образом, при использовании динамического кворума кластер будет оставаться даже в случае утери трех узлов.

![Диаграмма, на которой показаны четыре узла кластера с узлами, на которые произошел сбой по одному, и количество требуемых голосов после каждого сбоя.](media/understand-quorum/dynamic-quorum-step-through.png)

Приведенный выше сценарий применяется к общему кластеру, в котором не включена Локальные дисковые пространства. Однако при включении Локальные дисковые пространства кластер может поддерживать только два сбоя узла. Это объясняется в [разделе кворум пула](#pool-quorum-overview).

### <a name="examples"></a>Примеры

#### <a name="two-nodes-without-a-witness"></a>Два узла без следящего сервера.
Голосование в одном узле обнуляется, поэтому голосом *большинства* выдается всего один **голос**. Если узел, не использующий голосование, неожиданно выходит из строя, выжившую» имеет 1/1, а кластер остается неработоспособным. Если узел голосования неожиданно выходит из строя, выжившую» имеет 0/1, а кластер выходит из строя. Если узел голосования правильно включен, голосование передается на другой узел, и кластер остается неустойчивым. ***Именно поэтому важно настроить следящий сервер.***

![Описание кворума в случае с двумя узлами без следящего сервера](media/understand-quorum/2-node-no-witness.png)

- Может содерживаться одного сбоя сервера: **50% шансов**.
- Может выдерживать один сбой сервера, а второй — **нет**.
- Может выдерживать две ошибки сервера одновременно: **нет**.

#### <a name="two-nodes-with-a-witness"></a>Два узла с следящим сервером.
Оба узла проголосуют и голоса следящего сервера, поэтому *большинство* из них выдается из **3 голосов**. Если один из узлов выходит из строя, выжившую» имеет 2/3, а кластер остается неработоспособным.

![Описание кворума в случае с двумя узлами с следящим сервером](media/understand-quorum/2-node-witness.png)

- Может содерживаться одного сбоя сервера: **Да**.
- Может выдерживать один сбой сервера, а второй — **нет**.
- Может выдерживать две ошибки сервера одновременно: **нет**.

#### <a name="three-nodes-without-a-witness"></a>Три узла без следящего сервера.
Все узлы проголосуют, поэтому *большая* часть состоит из **трех голосов**. Если какой либо узел выходит из строя, выжившие объекты поколений составляет 2/3, а кластер остается неработоспособным. Кластер преобразуется в два узла без следящего сервера — в этом случае вы находитесь в сценарии 1.

![Описание кворума в случае с тремя узлами без следящего сервера](media/understand-quorum/3-node-no-witness.png)

- Может содерживаться одного сбоя сервера: **Да**.
- Может выдерживать один сбой сервера, а второй — **50% шансов**.
- Может выдерживать две ошибки сервера одновременно: **нет**.

#### <a name="three-nodes-with-a-witness"></a>Три узла с следящим сервером.
Все узлы проголосуют, поэтому следящий сервер изначально не проголосу. *Большая* часть состоит из всего **3 голосов**. После одного сбоя кластер содержит два узла с следящим сервером, который возвращается к сценарию 2. Итак, теперь два узла и голосование за следящего сервера.

![Описание кворума в случае с тремя узлами с следящим сервером](media/understand-quorum/3-node-witness.png)

- Может содерживаться одного сбоя сервера: **Да**.
- Может выдерживать один сбой сервера, а затем другой: **Да**.
- Может выдерживать две ошибки сервера одновременно: **нет**.

#### <a name="four-nodes-without-a-witness"></a>Четыре узла без следящего сервера
Голосование одного узла обнуляется, поэтому *большинство* из них выдается всего за **3 голоса**. После одного сбоя кластер превратится в три узла, и в сценарии 3.

![Описание кворума в случае с четырьмя узлами без следящего сервера](media/understand-quorum/4-node-no-witness.png)

- Может содерживаться одного сбоя сервера: **Да**.
- Может выдерживать один сбой сервера, а затем другой: **Да**.
- Может выдерживать две ошибки сервера одновременно: **50% шансов**.

#### <a name="four-nodes-with-a-witness"></a>Четыре узла с следящим сервером.
Все узлы являются голосовыми и голосовыми, поэтому *большинство* из них выдается всего **5 голосов**. После одного сбоя вы находитесь в сценарии 4. После двух одновременных сбоев вы переходите к сценарию 2.

![Описание кворума в случае с четырьмя узлами с следящим сервером](media/understand-quorum/4-node-witness.png)

- Может содерживаться одного сбоя сервера: **Да**.
- Может выдерживать один сбой сервера, а затем другой: **Да**.
- Может выдерживать две ошибки сервера одновременно: **Да**.

#### <a name="five-nodes-and-beyond"></a>Пять узлов и больше.
Все узлы проголосуют или все, кроме одного голоса, независимо от того, что это делает. Локальные дисковые пространства не может одновременно справиться с более чем двумя узлами, поэтому на этом этапе следящий сервер не нужен и не полезен.

![Описание кворума в случае с пятью узлами и за пределами](media/understand-quorum/5-nodes.png)

- Может содерживаться одного сбоя сервера: **Да**.
- Может выдерживать один сбой сервера, а затем другой: **Да**.
- Может выдерживать две ошибки сервера одновременно: **Да**.

Теперь, когда мы понимаем, как работает кворум, давайте взглянем на типы следящих серверов кворума.

### <a name="quorum-witness-types"></a>Типы следящего сервера кворума

Отказоустойчивая кластеризация поддерживает три типа следящих серверов кворума:

- **[Облако-свидетель](../../failover-clustering/deploy-cloud-witness.md)** — хранилище больших двоичных объектов в Azure доступно для всех узлов кластера. Он хранит сведения о кластеризации в файле следящего сервера. log, но не сохраняет копию базы данных кластера.
- **Файловый ресурс-свидетель** — общая папка SMB, настроенная на файловом сервере под управлением Windows Server. Он хранит сведения о кластеризации в файле следящего сервера. log, но не сохраняет копию базы данных кластера.
- **Диск-свидетель** — небольшой кластерный диск, который находится в группе доступных кластеров хранения. Этот диск обладает высокой доступностью и может отработки отказа между узлами. Он содержит копию базы данных кластера.  ***С Локальные дисковые пространства не поддерживается диск-свидетель***.

## <a name="pool-quorum-overview"></a>Общие сведения о кворуме пула

Мы только что говорили о кворуме кластера, который работает на уровне кластера. Теперь давайте подробно рассмотрим кворум пула, который работает на уровне пула (т. е. Вы можете потерять узлы и диски и оставить пул в состоянии). Пулы носителей были разработаны для использования как в кластеризованных, так и в некластеризованных сценариях, поэтому у них есть другой механизм кворума.

В таблице ниже приводятся общие сведения о результатах кворума пула для каждого сценария.

| Узлы сервера | Может содерживаться сбоя одного узла сервера | Может сосуществовать один сбой узла сервера, а затем другой | Может содерживаться двух сбоев одновременного узла сервера |
|--------------|-------------------------------------|---------------------------------------------------|----------------------------------------------------|
| 2            | Нет                                  | Нет                                                | Нет                                                 |
| 2 + следящий сервер  | да                                 | Нет                                                | Нет                                                 |
| 3            | Да                                 | Нет                                                | Нет                                                 |
| 3 + следящий сервер  | да                                 | Нет                                                | Нет                                                 |
| 4            | Да                                 | Нет                                                | Нет                                                 |
| 4 + следящий сервер  | да                                 | да                                               | да                                                |
| 5 и выше  | да                                 | да                                               | да                                                |

## <a name="how-pool-quorum-works"></a>Как работает кворум пула

При сбое дисков или невозможности подмножества дисков связаться с другим подмножеством, остальные диски должны убедиться, что они составляют *большую* часть пула, чтобы остаться в сети. Если они не могут проверить, они будут переведены в автономный режим. Пул — это сущность, которая переходит в автономный режим или остается в сети в зависимости от наличия достаточного количества дисков для кворума (50% + 1). Владелец ресурса пула (активный узел кластера) может быть + 1.

Но кворум пула работает иначе из кворума кластера следующими способами.

- пул использует один узел в кластере как следящий, чтобы выдерживать половину дисков (этот узел является владельцем ресурса пула).
- в пуле отсутствует динамический кворум
- в пуле не реализована собственная версия удаления голоса

### <a name="examples"></a>Примеры

#### <a name="four-nodes-with-a-symmetrical-layout"></a>Четыре узла с симметричным макетом.
Каждый из 16 дисков имеет один голос, а два узла также имеют один голос (так как он является владельцем ресурса пула). *Большая* часть состоит из всего **16 голосов**. Если узлы три и четыре пути вниз, то в работающем подмножестве будет 8 дисков, а владелец ресурса пула — 9/16 голосов. Таким образом, пул остается неработоспособным.

![Кворум пула 1](media/understand-quorum/pool-1.png)

- Может содерживаться одного сбоя сервера: **Да**.
- Может выдерживать один сбой сервера, а затем другой: **Да**.
- Может выдерживать две ошибки сервера одновременно: **Да**.

#### <a name="four-nodes-with-a-symmetrical-layout-and-drive-failure"></a>Четыре узла с симметричным разметкой и сбоем диска.
Каждый из 16 дисков имеет один голос, а узел 2 также имеет один голос (так как он является владельцем ресурса пула). *Большая* часть состоит из всего **16 голосов**. Сначала диск 7 выйдет из строя. Если узлы три и четыре пути вниз, то в работающем подмножестве будет 7 дисков, а владелец ресурса пула — 8/16 голосов. Таким образом, пул не имеет большинства и не выходит из строя.

![Кворум пула 2](media/understand-quorum/pool-2.png)

- Может содерживаться одного сбоя сервера: **Да**.
- Может выдерживать один сбой сервера, а второй — **нет**.
- Может выдерживать две ошибки сервера одновременно: **нет**.

#### <a name="four-nodes-with-a-non-symmetrical-layout"></a>Четыре узла с несимметричным макетом.
Каждый из 24 дисков имеет один голос, а два узла также имеют один голос (так как он является владельцем ресурса пула). *Большая* часть состоит из всего **24 голосов**. Если узлы три и четыре пути вниз, то в работающем подмножестве будет 8 дисков, а владелец ресурса пула — 9/24 голосов. Таким образом, пул не имеет большинства и не выходит из строя.

![Кворум пула 3](media/understand-quorum/pool-3.png)

- Может содерживаться одного сбоя сервера: **Да**.
- Может содерживаться одного сбоя сервера, а затем другой: * * зависит от * * (не может выдерживаться, если оба узла три и четыре выходят из строя, но могут содержаться в других сценариях.
- Может выдерживать две ошибки сервера одновременно: * * зависит от * * (не может выдерживаться, если оба узла три и четыре выходят из строя, но могут продолжать работать во всех других сценариях).

### <a name="pool-quorum-recommendations"></a>Рекомендации по кворуму пула

- Убедитесь, что каждый узел в кластере является симметричным (каждый узел имеет одинаковое количество дисков).
- Включите трехстороннее зеркальное отображение или двойной контроль четности, чтобы можно было допускать сбои узла и сохранять виртуальные диски в оперативном режиме. Дополнительные сведения см. на [странице руководств по томам](plan-volumes.md) .
- Если несколько узлов не работают или два узла и диск на другом узле отключены, тома могут не иметь доступа ко всем трем копиям своих данных, поэтому они будут переведены в автономный режим и будут недоступны. Рекомендуется быстро восстановить или заменить диски, чтобы обеспечить максимальную устойчивость для всех данных в томе.

## <a name="more-information"></a>Дополнительные сведения

- [Настройка кворума и управление им](../../failover-clustering/manage-cluster-quorum.md)
- [Развертывание облака-свидетеля](../../failover-clustering/deploy-cloud-witness.md)
