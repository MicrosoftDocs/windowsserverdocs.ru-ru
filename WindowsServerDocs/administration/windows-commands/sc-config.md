---
title: Конфигурация sc.exe
description: Справочная статья по команде sc.exe config, которая изменяет конфигурации службы, изменяя значения записей службы в реестре и в базе данных диспетчера управления службами.
ms.topic: reference
ms.assetid: ad4d68a6-efe5-452b-8501-7f1f1c552a4a
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 06/05/2018
ms.openlocfilehash: 4bd66fb86cd8f7f0b8772853e5b933e054a0398b
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101806596"
---
# <a name="scexe-config"></a>Конфигурация sc.exe

Изменяет значение записей службы в реестре и в базе данных диспетчера управления службами.

## <a name="syntax"></a>Синтаксис

```
sc.exe [<servername>] config [<servicename>] [type= {own | share | kernel | filesys | rec | adapt | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled | delayed-auto}] [error= {normal | severe | critical | ignore}] [binpath= <binarypathname>] [group= <loadordergroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<accountname> | <objectname>}] [displayname= <displayname>] [password= <password>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| `<servername>` | Указывает имя удаленного сервера, на котором расположена служба. Имя должно использовать формат UNC (например, \\ MyServer). Чтобы запустить SC.exe локально, не используйте этот параметр. |
| `<servicename>` | Указывает имя службы, возвращенное операцией **жеткэйнаме** . |
| `type= {own | share | kernel | filesys | rec | adapt | interact type= {own | share}}` | Указывает тип службы. Эти способы могут быть следующими:<ul><li>**собственный** — указывает службу, которая выполняется в собственном процессе. Он не предоставляет доступ к исполняемому файлу другим службам. Это значение по умолчанию.</li><li>**Share** — указывает службу, которая выполняется как общий процесс. Он использует исполняемый файл совместно с другими службами.</li><li>**kernel** — указывает драйвер.</li><li>**филесис** — указывает драйвер файловой системы.</li><li>**REC** — указывает драйвер, распознаваемый файловой системой, который определяет файловые системы, используемые на компьютере.</li><li>**адаптация** — указывает драйвер адаптера, который определяет устройства, такие как клавиатуры, мыши и диски.</li><li>**взаимодействие** — указывает службу, которая может взаимодействовать с рабочим столом и получать входные данные от пользователей. Интерактивные службы должны запускаться под учетной записью LocalSystem. Этот тип должен использоваться в сочетании с **Type = владеть** или **Type = Shared** (например, **Type = взаимодействие** **Type = владеет**). При использовании **типа = взаимодействие** само по себе вызывает ошибку.</li></ul> |
| `start= {boot | system | auto | demand | disabled | delayed-auto}` | Указывает тип запуска для службы. Эти способы могут быть следующими:<ul><li>**Загрузка** — указывает драйвер устройства, который загружается загрузчиком.</li><li>**система** — указывает драйвер устройства, который запускается во время инициализации ядра.</li><li>**автоматически** указывает службу, которая автоматически запускается при каждом перезапуске компьютера и выполняется, даже если никто из них не входит в систему.</li><li>**Demand** — указывает службу, которая должна быть запущена вручную. Это значение по умолчанию, если **Start =** не задано.</li><li>**Disabled (отключено** ) — указывает службу, которая не может быть запущена. Чтобы запустить отключенную службу, измените тип запуска на другое значение.</li><li>**отложенный — автоматически** указывает службу, которая запускается автоматически через некоторое время после запуска других автоматических служб.</li></ul> |
| `error= {normal | severe | critical | ignore}` | Указывает серьезность ошибки, если служба не запускается при запуске компьютера. Эти способы могут быть следующими:<ul><li>**Обычная** — указывает, что ошибка записывается в журнал и отображается окно сообщения, информирующее пользователя о том, что не удалось запустить службу. Запуск будет продолжен. Это параметр по умолчанию.</li><li>**серьезная** — указывает, что ошибка регистрируется (по возможности). Компьютер пытается перезапуститься с последней удачной конфигурацией. Это может привести к тому, что компьютер сможет перезапуститься, но служба по-прежнему может не запуститься.</li><li>**критическая** — указывает, что ошибка записывается в журнал (если возможно). Компьютер пытается перезапуститься с последней удачной конфигурацией. Если последняя удачная конфигурация завершается сбоем, запуск также завершается сбоем, а процесс загрузки останавливается с ошибкой остановки.</li><li>**Ignore** — указывает, что ошибка записывается в журнал, и запуск продолжится. Пользователю не выдается уведомление, кроме записи ошибки в журнал событий.</li></ul> |
| `binpath= <binarypathname>` | Указывает путь к двоичному файлу службы. Значение по умолчанию для **BinPath =**, и эта строка должна быть указана. |
| `group= <loadordergroup>` | Указывает имя группы, членом которой является эта служба. Список групп хранится в реестре в подразделе **хклм\систем\куррентконтролсет\контрол\сервицеграупордер** . По умолчанию используется значение NULL. |
| `tag= {yes | no}` | Указывает, следует ли получить TagID из вызова CreateService. Теги используются только для драйверов загрузки и запуска системы. |
| `depend= <dependencies>` | Указывает имена служб или групп, которые должны быть запущены перед этой службой. Имена разделяются косой чертой (/). |
| `obj= {<accountname> | <objectname>}` | Указывает имя учетной записи, в которой будет выполняться служба, или задает имя объекта драйвера Windows, в котором будет выполняться драйвер. Значение по умолчанию — **LocalSystem**. |
| `displayname= <displayname>` | Указывает описательное имя для идентификации службы в программах пользовательского интерфейса. Например, имя подраздела одной конкретной службы — **wuauserv**, которое имеет более понятное отображаемое имя автоматическое обновление. |
| `password= <password>` | Указывает пароль. Это необходимо, если используется учетная запись, отличная от учетной записи LocalSystem. |
| /? | Отображение справки в командной строке. |

#### <a name="remarks"></a>Комментарии

- Каждый параметр командной строки (параметр) должен включать знак равенства как часть имени параметра.

- Между параметром и его значением требуется пробел (например, **Type =** an). Если пространство не указано, операция завершается ошибкой.

## <a name="examples"></a>Примеры

Чтобы указать путь к двоичному файлу для службы *невсервице* , введите:

```
sc.exe config NewService binpath= ntsd -d c:\windows\system32\NewServ.exe
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
