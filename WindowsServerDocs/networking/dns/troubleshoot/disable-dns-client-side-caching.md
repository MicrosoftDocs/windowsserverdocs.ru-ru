---
title: Отключение кэширования на стороне клиента DNS на DNS-клиентах
description: В этой статье рассказывается, как отключить кэширование на стороне клиента DNS для DNS-клиентов.
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: 107527f621dd82f9ca78df2f036600b7ecb7bccd
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947194"
---
# <a name="disable-dns-client-side-caching-on-dns-clients"></a>Отключение кэширования на стороне клиента DNS на DNS-клиентах

Windows содержит кэш DNS на стороне клиента. Функция кэширования DNS на стороне клиента может создать ложное впечатление, что балансировка нагрузки DNS с циклическим перебором не происходит с DNS-сервера на клиентский компьютер Windows. При использовании команды ping для поиска того же имени домена A-записи клиент может использовать тот же IP-адрес.

## <a name="how-to-disable-client-side-caching"></a>Как отключить кэширование на стороне клиента

Чтобы отключить кэширование DNS, выполните одну из следующих команд:

```cmd
net stop dnscache
```

```cmd
sc servername stop dnscache
```


Для безвозвратного отключения кэша DNS в Windows используйте средство контроллера служб или средство "службы", чтобы задать для параметра "тип запуска службы DNS-клиента значение" **отключено**". Обратите внимание, что имя службы DNS-клиента Windows также может отображаться как "Днскаче".

> [!NOTE]
> Если кэш сопоставителя DNS деактивируется, Общая производительность клиентского компьютера снижается, а сетевой трафик для запросов DNS увеличивается.

Служба DNS-клиента оптимизирует производительность разрешения имен DNS за счет хранения ранее разрешенных имен в памяти. Если служба DNS-клиента отключена, компьютер может по-прежнему разрешать DNS-имена с помощью DNS-серверов сети.

Когда сопоставитель Windows получает в запрос положительный или отрицательный ответ, он добавляет этот ответ в свой кэш и тем самым создает запись ресурса DNS. Сопоставитель всегда проверяет кэш перед запросом DNS-сервера. Если запись ресурса DNS находится в кэше, сопоставитель использует запись из кэша вместо запроса к серверу. Такое поведение ускоряет запросы и уменьшает сетевой трафик для запросов DNS.

Для просмотра и очистки кэша сопоставителя DNS можно использовать средство ipconfig. Чтобы просмотреть кэш сопоставителя DNS, выполните в командной строке следующую команду:

```cmd
ipconfig /displaydns
```

Эта команда отображает содержимое кэша сопоставителя DNS, включая записи ресурсов DNS, предварительно загруженные из файла Hosts, и все недавно запрошенные имена, разрешенные системой. Через некоторое время сопоставитель отклоняет запись из кэша. Период времени указывается значением срока жизни **(TTL)** , связанным с записью ресурса DNS. Кэш также можно очистить вручную. После очистки кэша компьютер должен снова запрашивать DNS-серверы для любых записей ресурсов DNS, которые ранее были разрешены компьютером. Чтобы удалить записи в кэше сопоставителя DNS, выполните `ipconfig /flushdns` команду из командной строки.

## <a name="using-the-registry-to-control-the-caching-time"></a>Использование реестра для управления временем кэширования

> [!IMPORTANT]
> Внимательно выполните действия, описанные в этом разделе. Неправильное изменение реестра может привести к серьезным проблемам. Перед внесением изменений [создайте резервную копию реестра для его восстановления](https://support.microsoft.com/help/322756) в случае возникновения проблем.

Промежуток времени, в течение которого кэшируется положительный или отрицательный ответ, зависит от значений записей в следующем разделе реестра:

**HKEY_LOCAL_MACHINE \Систем\куррентконтролсет\сервицес\днскаче\параметерс**

TTL для положительных ответов — это меньшее из следующих значений:

- Число секунд, указанное в ответе на запрос, полученным распознавателем

- Значение параметра реестра **макскачеттл** .

>[!Note]
>- По умолчанию TTL для положительных ответов составляет 86 400 секунд (1 день).
>- TTL для отрицательных ответов — это количество секунд, указанное в параметре реестра Макснегативекачеттл.
>- По умолчанию TTL для отрицательных ответов составляет 5 секунд; до Windows 10 версия 1703 по умолчанию составила 900 секунд (15 минут).
Если вы не хотите кэшировать отрицательные ответы, присвойте параметру реестра Макснегативекачеттл значение 0.

Чтобы задать время кэширования на клиентском компьютере, выполните следующие действия.

1. Запустите редактор реестра (Regedit.exe).

2. Найдите и выберите в реестре следующий раздел:

   **HKEY_LOCAL_MACHINE \Систем\куррентконтролсет\сервицес\днскаче\параметерс**

3. В меню Правка наведите указатель мыши на пункт Создать, выберите пункт значение DWORD, а затем добавьте следующие значения реестра:

   - Имя значения: Макскачеттл

     Тип данных: REG_DWORD

     Данные значения: значение по умолчанию 86400 секунд.

     Если вы уменьшите максимальное значение TTL в кэше DNS клиента на 1 секунду, это даст внешнее представление о том, что кэш DNS на стороне клиента отключен.

   - Имя значения: Макснегативекачеттл

     Тип данных: REG_DWORD

     Значение данные: значение по умолчанию 5 секунд.

     Установите значение 0, если не нужно кэшировать отрицательные ответы.

4. Введите значение, которое необходимо использовать, и нажмите кнопку ОК.

5. Закройте редактор реестра.
