---
title: Шаг 7. Задачи, выполняемые после миграции Windows Server Essentials
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: d382e3fd-d393-4bd0-883f-db50104a969f
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 5186cc808b46aa334dc994186e3d7d8d898f9d96
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625361"
---
# <a name="step-7-perform-post-migration-tasks-for-the-windows-server-essentials-migration"></a>Шаг 7. Задачи, выполняемые после миграции Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials

Следующие задачи помогут вам завершить настройку конечного сервера с теми же параметрами, которые были на исходном сервере. Возможно, вы отключили некоторые из этих параметров на исходном сервере во время процесса миграции, поэтому они не были перенесены на конечный сервер.

1.  [Удаление записей DNS для исходного сервера](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_DeleteDNSEntries)

2.  [Общий доступ к папкам с данными бизнес-приложений и прочих приложений](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md#BKMK_ShareLineOfBusinessAndOtherApplications)

##  <a name="delete-dns-entries-for-the-source-server"></a><a name="BKMK_DeleteDNSEntries"></a> Удаление записей DNS для исходного сервера
 После списания исходного сервера, сервера сервер службы доменных имен (DNS) может все еще содержать элементы, указывающие на этот исходный сервер. Удалите эти записи DNS.

#### <a name="to-delete-dns-entries-that-point-to-the-source-server"></a>Чтобы удалить DNS-записи, которые ссылаются на исходный сервер

1.  Откройте **Диспетчер DNS** на конечном сервере .

2.  В диспетчере DNS щелкните правой кнопкой мыши имя сервера, щелкните **Свойства**, а затем перейдите на вкладку **Серверы пересылки**.

3.  Определите, имеется ли в списке пересылок запись, указывающая на исходный сервер. Если такая запись есть, нажмите кнопку **Изменить** и удалите эту запись в окне **Редактировать серверы пересылки**.

4.  В окне **Диспетчер DNS** разверните имя сервера и затем разверните пункт **Зоны прямого просмотра**.

5.  Для каждой зоны прямого просмотра щелкните правой кнопкой мыши зону, выберите пункт **Свойства**, а затем откройте вкладку **Серверы имен**.

6.  Выберите запись в текстовом поле **Серверы имен**, которая указывает на исходный сервер, нажмите **Удалить**, а затем нажмите **ОК**.

7.  Повторите шаги 5 и 6, пока не будут удалены все указатели на исходный сервер.

8.  Нажмите кнопку **ОК**, чтобы закрыть окно **Свойства**.

9. В окне **Диспетчер DNS** разверните пункт **Зоны обратного просмотра**.

10. Повторите шаги 6–9, чтобы удалить все зоны обратного просмотра, которые указывают на исходный сервер.

##  <a name="share-line-of-business-and-other-application-data-folders"></a><a name="BKMK_ShareLineOfBusinessAndOtherApplications"></a> Совместное использование бизнес-и других папок данных приложений
 Для скопированных на конечный сервер папок с данными бизнес-приложений и прочих приложений необходимо задать разрешения для общей папки и разрешения NTFS. После настройки разрешений общие папки отображаются на панели мониторинга на вкладке **Хранилище**.

 Если для сопоставления дисков с общими папками вы используете сценарий входа, для сопоставления с дисками на конечном сервере сценарий необходимо обновить.

## <a name="next-steps"></a>Дальнейшие действия
 Вы выполнили задачи, выполняемые после миграции для Windows Server Essentials. Теперь перейдите к [шагу 8--запустите анализатор соответствия рекомендациям Windows Server Essentials](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).


Для просмотра всех шагов см. статью [Переход на Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

