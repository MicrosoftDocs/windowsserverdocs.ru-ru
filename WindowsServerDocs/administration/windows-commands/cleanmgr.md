---
title: cleanmgr
description: Настройте средство очистки диска (Cleanmgr.exe) для автоматической очистки определенных файлов.
ms.reviewer: cosmosdarwin
author: JasonGerend
ms.author: jgerend
manager: daveba
ms.date: 06/20/2019
ms.topic: reference
ms.openlocfilehash: ab98e0dd28ccc3529aa6ad8416c14d0960d56125
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946360"
---
# <a name="cleanmgr"></a>cleanmgr

> Область применения: Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2008 R2, Windows Server (половина ежегодного канала)

Удаляет ненужные файлы с жесткого диска компьютера. С помощью параметров командной строки можно указать, что **cleanmgr** очищает временные файлы, файлы Интернета, скачанные и перезапускают файлы bin. Затем можно запланировать выполнение задачи в определенное время с помощью средства **запланированные задания** .

## <a name="syntax"></a>Синтаксис

```
cleanmgr [/d <driveletter>] [/sageset:n]  [/sagerun:n] [/TUNEUP:n] [/LOWDISK] [/VERYLOWDISK]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- | ----------- |
| /d `<driveletter>` | Указывает диск, на котором должна быть очищена Очистка диска.<p>**Примечание.** Параметр **/d** не используется с `/sagerun:n` . |
| /sageset: n | Отображает диалоговое окно **Параметры очистки диска** , а также создает раздел реестра для хранения выбранных вами параметров. `n`Значение, которое хранится в реестре, позволяет указать задачи для выполнения очистки диска. `n`Значением может быть любое целочисленное значение от 0 до 9999. |
| /сажерун: n | Выполняет указанные задачи, назначенные значению n при использовании параметра **/sageset** . Все диски на компьютере перечисляются, и выбранный профиль выполняется для каждого диска. |
| /тунеуп: n | Для этого выполните команду **/sageset** и **/сажерун** `n` . |
| /ловдиск | Запустите с параметрами по умолчанию. |
| /вериловдиск | Запустите с параметрами по умолчанию без запросов пользователя. |
| /? | Отображение справки в командной строке. |

#### <a name="options"></a>Варианты

Параметры для файлов, которые можно указать для очистки диска с помощью команды **/sageset** и **/сажерун** , включают:

- **Временные файлы установки** — это файлы, созданные программой установки, которая больше не выполняется.

- **Загруженные файлы программы** — Скачанные программные файлы — это элементы ActiveX и Java-программы, загружаемые автоматически из Интернета при просмотре определенных страниц. Эти файлы временно хранятся в папке downloaded Program Files на жестком диске. Этот параметр включает кнопку "просмотреть файлы", чтобы просмотреть файлы до их удаления. При нажатии кнопки открывается папка Program Files К:\виннт\довнлоадед.

- **Временные файлы Интернета** . папка временных файлов Интернета содержит веб-страницы, которые хранятся на жестком диске для быстрого просмотра. Программа очистки диска удаляет эти страницы, но оставляет личные настройки веб-страниц без изменений. Этот параметр также включает кнопку «Просмотреть файлы», которая открывает папку «C:\Documents and Сеттингс\усернаме\локал Сеттингс\темпорари Internet Files\Content.IE5».

- **Старые файлы chkdsk** . когда chkdsk проверяет диск на наличие ошибок, CHKDSK может сохранять потерянные фрагменты файлов в виде файлов в корневой папке на диске. Эти файлы не нужны.

- **Корзина — в** корзине содержатся файлы, удаленные с компьютера. Эти файлы не удаляются окончательно, пока корзина не будет очищена. Этот параметр включает кнопку «Просмотреть файлы», которая открывает корзину.<p>**Примечание.** Корзина может отображаться на нескольких дисках, например, не только в% SystemRoot%.

- **Временные файлы** — программы иногда хранят временные данные во временной папке. Перед завершением работы программы эта информация обычно удаляется. Вы можете безопасно удалить временные файлы, которые не были изменены в течение прошлой недели.

- **Временные автономные файлы** — временные автономные файлы — это локальные копии недавно использованных сетевых файлов. Эти файлы кэшируются автоматически, поэтому их можно использовать после отключения от сети. Кнопка **Просмотреть файлы** открывает папку автономные файлы.

- **Автономные файлы** — автономные файлы — это локальные копии сетевых файлов, которые должны быть доступны в автономном режиме, чтобы их можно было использовать после отключения от сети. Кнопка **Просмотреть файлы** открывает папку автономные файлы.

- **Сжатие старых файлов** — Windows может сжимать файлы, которые не использовались недавно. Сжатие файлов экономит место на диске, но вы по-прежнему можете использовать эти файлы. Файлы не удаляются. Поскольку файлы сжимаются по разным тарифам, отображаемый объем дискового пространства будет приблизительным. Кнопка Параметры позволяет указать число дней ожидания перед тем, как программа очистки диска будет сжимать неиспользуемый файл.

- **Файлы каталога для индексатора содержимого** . Служба индексирования ускоряет и улучшает поиск файлов, сохраняя индекс файлов на диске. Эти файлы каталога остаются из предыдущей операции индексирования и могут быть удалены безопасно.<p>**Примечание.** Файл каталога может отображаться на нескольких дисках, например, не только в `%SystemRoot%` .

>[!NOTE]
> При указании очистки диска, содержащего установку Windows, все эти параметры доступны на вкладке **Очистка диска** . Если указать любой другой диск, на вкладке **Очистка диска** будут доступны только Корзина и файлы каталога для параметров индекса содержимого.

## <a name="examples"></a>Примеры

Чтобы запустить приложение "Очистка диска", чтобы можно было использовать его диалоговое окно для указания параметров для дальнейшего использования, сохраните параметры в набор **1**, введите следующую команду:

```
cleanmgr /sageset:1
```

Чтобы запустить очистку диска и включить параметры, указанные с помощью команды cleanmgr/sageset: 1, введите:

```
cleanmgr /sagerun:1
```

Для запуска `cleanmgr /sageset:1` и `cleanmgr /sagerun:1` совместного выполнения введите:

```
cleanmgr /tuneup:1
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Освобождение места на диске в Windows 10](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space)

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)
