---
title: Мастер очистки сервера
description: Раздел о службе Windows Server Update Service (WSUS). Использование мастера очистки сервера для управления дисковым пространством
ms.topic: article
ms.assetid: 7c351797-2716-4442-a668-60d5b4e77751
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 85ae240204bc030cf74069dca08cef43dc656e3f
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101827269"
---
# <a name="the-server-cleanup-wizard"></a>Мастер очистки сервера

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Мастер очистки сервера интегрирован в пользовательский интерфейс и может использоваться для управления дисковым пространством. Этот мастер может выполнять следующие операции:

- Удалить неиспользуемые обновления и редакции обновления удалить все старые обновления и обновления, которые не были утверждены.

- Удаление компьютеров, не имеющих связи с сервером удалите все клиентские компьютеры, которые не связывались с сервером в течение тридцати дней или более.

- Удаление ненужных файлов обновления Удаление всех файлов обновлений, которые не требуются для обновлений или подчиненных серверов.

- Отклонить просроченные обновления отклонять все обновления, срок действия которых истек корпорацией Майкрософт.

- Отклонить замененные обновления отклонять все обновления, соответствующие следующим критериям:

  -   Заменяемое обновление не является обязательным

  -   Заменяемое обновление было на сервере в течение тридцати дней или более

  -   Заменяемое обновление в настоящее время не сообщается ни одному из клиентов

  -   Заменяющее обновление не было явно развернуто в группе компьютеров в течение 90 дней и более.

  -   Заменяющее обновление должно быть утверждено для установки в группе компьютеров

  > [!WARNING]
  >  В иерархии WSUS настоятельно рекомендуется сначала запустить процесс очистки на нижнем, нисходящем и реплике WSUS-сервере, а затем переместить иерархию. Неправильное выполнение очистки на любом вышестоящем сервере до выполнения очистки на каждом подчиненном сервере может привести к несоответствию данных, имеющихся в вышестоящей базе данных и подчиненных базах данных. Несоответствие данных может привести к сбоям синхронизации между вышестоящим и подчиненным серверами.
  >
  > [!IMPORTANT]
  >  При удалении ненужного содержимого с помощью мастера очистки сервера все файлы закрытых обновлений, скачанные с сайта Центр обновления Майкрософт каталога, также будут удалены. После запуска мастера очистки сервера необходимо повторно импортировать эти файлы.

Если обновления утверждены с помощью правила автоматического утверждения, они могут по-прежнему находиться в утвержденном состоянии и не будут удалены мастером очистки сервера. Чтобы удалить автоматически утвержденные обновления, находящиеся в утвержденном состоянии, администратор WSUS должен вручную задать для параметра Состояние утверждения замененные обновления значение не утверждено, чтобы они были доступны для отклонения мастером очистки сервера. Мастер очистки сервера обеспечит утверждение более нового обновления, и клиентская система по-прежнему сообщает о необходимости обновления, прежде чем пометить обновление как отклоненное.




