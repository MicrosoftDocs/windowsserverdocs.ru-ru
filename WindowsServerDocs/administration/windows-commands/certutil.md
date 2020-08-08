---
title: certutil
description: Справочная статья по команде certutil, которая является программой командной строки, которая выводит дампы и отображает сведения о конфигурации центра сертификации (ЦС), настраивает службы сертификации, компоненты ЦС для резервного копирования и восстановления, а также проверяет сертификаты, пары ключей и цепочки сертификатов.
ms.topic: article
ms.assetid: c264ccf0-ba1e-412b-9dd3-d77dd9345ad9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: afaf0c75350cfb4121d0ebc664469f4494afe8c7
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992952"
---
# <a name="certutil"></a>certutil

Certutil.exe — это программа командной строки, которая устанавливается как часть служб сертификации. certutil.exe можно использовать для дампа и просмотра сведений о конфигурации центра сертификации (ЦС), настройки служб сертификатов, резервного копирования и восстановления компонентов ЦС, а также для проверки сертификатов, пар ключей и цепочек сертификатов.

Если программа certutil запущена в центре сертификации без дополнительных параметров, отобразится текущая конфигурация центра сертификации. Если программа certutil запущена в некотором центре сертификации, команда по умолчанию выполняет `certutil [-dump]` команду.

> [!IMPORTANT]
> Более ранние версии программы Certutil не могут предоставить все параметры, описанные в этом документе. Вы можете просмотреть все параметры, предоставляемые конкретной версией программы Certutil, выполнив `certutil -?` или `certutil <parameter> -?` .

## <a name="parameters"></a>Параметры

### <a name="-dump"></a>— дамп

Дамп сведений о конфигурации или файлов.

```
certutil [options] [-dump]
certutil [options] [-dump] file
```

```
[-f] [-silent] [-split] [-p password] [-t timeout]
```

### <a name="-asn"></a>— ASN

Проанализируйте файл ASN. 1.

```
certutil [options] -asn file [type]
```

`[type]`: numeric CRYPT_STRING_ * тип декодирования

### <a name="-decodehex"></a>-декодехекс

Декодирование файла в шестнадцатеричном формате.

```
certutil [options] -decodehex infile outfile [type]
```

`[type]`: numeric CRYPT_STRING_ * тип кодировки

```
[-f]
```

### <a name="-decode"></a>-декодирование

Декодирование файла в кодировке Base64.

```
certutil [options] -decode infile outfile
```

```
[-f]
```

### <a name="-encode"></a>-Encoded

Кодирование файла в Base64.

```
certutil [options] -encode infile outfile
```

```
[-f] [-unicodetext]
```

### <a name="-deny"></a>— Deny

Отклонить ожидающий запрос.

```
certutil [options] -deny requestID
```

```
[-config Machine\CAName]
```

### <a name="-resubmit"></a>— Повторная отправка

Повторная отправка ожидающего запроса.

```
certutil [options] -resubmit requestId
```

```
[-config Machine\CAName]
```

### <a name="-setattributes"></a>-сетаттрибутес

Задание атрибутов для запроса ожидающего сертификата.

```
certutil [options] -setattributes RequestID attributestring
```

Где:

- **requestID** — это числовой идентификатор запроса для ожидающего запроса.

- **аттрибутестринг** — это пары имен и значений атрибутов запросов.

```
[-config Machine\CAName]
```

#### <a name="remarks"></a>Remarks

- Имена и значения должны быть разделены двоеточием, в то время как несколько пар "имя — значение" должны быть разделены символами новой строки. Например: `CertificateTemplate:User\nEMail:User@Domain.com` где `\n` последовательность преобразуется в разделитель новой строки.

### <a name="-setextension"></a>-сетекстенсион

Задайте расширение для ожидающего запроса сертификата.

```
certutil [options] -setextension requestID extensionname flags {long | date | string | \@infile}
```

Где:

- **requestID** — это числовой идентификатор запроса для ожидающего запроса.

- **ExtensionName** — строка ObjectID для расширения.

- **Флаги** задает приоритет расширения. `0`При задании `1` расширения как критическое, `2` Отключение расширения и и то, и `3` другое.

```
[-config Machine\CAName]
```

#### <a name="remarks"></a>Remarks

- Если последний параметр является числовым, он принимается как **длинное целое**.

- Если последний параметр может быть проанализирован как дата, он принимается как **Дата**.

- Если последний параметр начинается с `\@` , остальная часть маркера принимается как имя файла с двоичными данными или с шестнадцатеричным дампом текста ASCII.

- Если последний параметр является любым другим, он принимается в виде строки.

### <a name="-revoke"></a>-REVOKE

Отозвать сертификат.

```
certutil [options] -revoke serialnumber [reason]
```

Где:

- **SerialNumber** — это разделенный запятыми список серийных номеров сертификатов для отзыва.

- **Причина** — это числовое или символьное представление причины отзыва, в том числе:

  - **0. CRL_REASON_UNSPECIFIED** — не указано (по умолчанию)

  - **1. CRL_REASON_KEY_COMPROMISE** Компрометация ключа

  - **2. CRL_REASON_CA_COMPROMISE** — компрометация центра сертификации

  - **3. CRL_REASON_AFFILIATION_CHANGED** изменение принадлежности

  - **4. CRL_REASON_SUPERSEDED** заменено

  - **5. CRL_REASON_CESSATION_OF_OPERATION** — прекращение работы

  - **6. CRL_REASON_CERTIFICATE_HOLD** — хранение сертификата

  - **8. CRL_REASON_REMOVE_FROM_CRL** — удалить из списка отзыва сертификатов

  - **1. Отмена отзыва** — Отмена отзыва

```
[-config Machine\CAName]
```

### <a name="-isvalid"></a>-IsValid

Отобразить расположение текущего сертификата.

```
certutil [options] -isvalid serialnumber | certhash
```

```
[-config Machine\CAName]
```

### <a name="-getconfig"></a>-файл конфигурации

Возвращает строку конфигурации по умолчанию.

```
certutil [options] -getconfig
```

```
[-config Machine\CAName]
```

### <a name="-ping"></a>— Проверка связи

Попытка обращения к интерфейсу запроса служб сертификатов Active Directory.

```
certutil [options] -ping [maxsecondstowait | camachinelist]
```

Где:

- **камачинелист** — это разделенный запятыми список имен компьютеров ЦС. Для одного компьютера используйте завершающую запятую. Этот параметр также отображает стоимость сайта для каждого компьютера ЦС.

```
[-config Machine\CAName]
```

### <a name="-cainfo"></a>-каинфо

Отображение сведений о центре сертификации.

```
certutil [options] -cainfo [infoname [index | errorcode]]
```

Где:

- **инфонаме** указывает отображаемое свойство CA на основе следующего синтаксиса аргумента инфонаме:

  - **file** версия файла

  - **продукт** — версия продукта

  - **екситкаунт** — число модулей выхода

  - **выход `[index]` из программы** -Exit модуль описание

  - **Политика** — описание модуля политики

  - **имя** — имя ЦС

  - **санитизеднаме** — имя ИСКЛЮЧЕНного ЦС

  - **dsname** -исключенное краткое имя ЦС (имя DS)

  - **шаредфолдер** — общая папка

  - **Error1 ErrorCode** — текст сообщения об ошибке

  - **Error2 ErrorCode** — текст сообщения об ошибке и код ошибки

  - **тип** — тип CA

  - **сведения** — сведения о ЦС

  - **родительский** РОДИТЕЛЬСКИй ЦС

  - **церткаунт** — число сертификатов ЦС

  - **ксчгкаунт** — число сертификатов Exchange для ЦС

  - **кракаунт** — число сертификатов KRA

  - **краусед** — число использованных сертификатов KRA

  - **пропидмакс** — максимальный PropId CA

  - **цертстате `[index]` ** — Сертификат CA

  - **цертверсион `[index]` ** — Версия сертификата CA

  - **цертстатускоде `[index]` ** — Состояние проверки сертификата ЦС

  - **крлстате `[index]` ** — Список отзыва сертификатов

  - **крастате `[index]` ** — Сертификат KRA

  - **кроссстате + `[index]` ** -Прямой перекрестный сертификат

  - **кроссстате — `[index]` ** — Обратный перекрестный сертификат

  - **сертификат `[index]` ** — Сертификат CA

  - **цертчаин `[index]` ** — Цепочка сертификатов ЦС

  - **церткрлчаин `[index]` ** — Цепочка сертификатов CA с CRL

  - **ксчг `[index]` ** — Сертификат Exchange CA

  - **ксчгчаин `[index]` ** — Цепочка сертификатов ЦС Exchange

  - **ксчгкрлчаин `[index]` ** — Цепочка сертификатов ЦС Exchange с CRL

  - **KRA `[index]` ** — Сертификат KRA

  - **перекрестное + `[index]` ** -Прямой перекрестный сертификат

  - **Перекрестная `[index]` ** — Обратный перекрестный сертификат

  - **Список `[index]` отзыва сертификатов** — Базовый CRL

  - **делтакрл `[index]` ** — Разностный CRL

  - **крлстатус `[index]` ** — Состояние публикации CRL

  - **делтакрлстатус `[index]` ** — Состояние публикации разностного CRL

  - **DNS** -имя DNS

  - **роль** — разделение ролей

  - **ADS** — Advanced Server

  - **шаблоны** — шаблоны

  - **CSP `[index]` ** — URL-адреса OCSP

  - **AIA `[index]` ** — URL-адреса AIA

  - **CDP `[index]` ** — URL-адреса CDP

  - **localename** — имя локали ЦС

  - Идентификаторы OID шаблона субъекта **субжекттемплатеоидс**

  - **&#42;** — отображает все свойства

- **index** — это необязательный индекс свойства, начинающийся с нуля.

- **ErrorCode** — это числовой код ошибки.

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-cacert"></a>-CA. CERT

Получите сертификат для центра сертификации.

```
certutil [options] -ca.cert outcacertfile [index]
```

Где:

- **ауткацертфиле** — выходной файл.

- **index** — это индекс продления сертификата ЦС (по умолчанию — самый последний).

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-cachain"></a>-CA. Chain

Получите цепочку сертификатов для центра сертификации.

```
certutil [options] -ca.chain outcacertchainfile [index]
```

Где:

- **ауткацертчаинфиле** — выходной файл.

- **index** — это индекс продления сертификата ЦС (по умолчанию — самый последний).

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-getcrl"></a>-жеткрл

Возвращает список отзыва сертификатов (CRL).

Certutil [параметры] — жеткрл-файл [Индекс] [Дельта]

Где:

- **index** — это индекс списка отзыва сертификатов или индекс ключа (по умолчанию используется список CRL для самого последнего ключа).

- **Дельта** — это разностный CRL (по умолчанию — базовый CRL).

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-crl"></a>— список отзыва сертификатов

Опубликуйте новые списки отзыва сертификатов (CRL) или разностные CRL.

```
certutil [options] -crl [dd:hh | republish] [delta]
```

Где:

- **ДД: чч** — новый срок действия CRL в днях и часах.

- **Повторная** публикация повторно публикует последние списки отзыва сертификатов.

- **Дельта** публикует только разностные CRL (по умолчанию — базовый и разностный CRL).

```
[-split] [-config Machine\CAName]
```

### <a name="-shutdown"></a>— Завершение работы

Завершает работу служб Active Directory сертификатов.

```
certutil [options] -shutdown
```

```
[-config Machine\CAName]
```

### <a name="-installcert"></a>-инсталлцерт

Устанавливает сертификат центра сертификации.

```
certutil [options] -installcert [cacertfile]
```

```
[-f] [-silent] [-config Machine\CAName]
```

### <a name="-renewcert"></a>-реневцерт

Обновляет сертификат центра сертификации.

```
certutil [options] -renewcert [reusekeys] [Machine\ParentCAName]
```

- Используется `-f` для игнорирования ожидающего запроса на продление и создания нового запроса.

```
[-f] [-silent] [-config Machine\CAName]
```

### <a name="-schema"></a>-Schema

Выводит схему для сертификата.

```
certutil [options] -schema [ext | attrib | cRL]
```
Где:

- По умолчанию команда принимает значение таблицы Request и Certificate.

- **ext** — это таблица расширений.

- **атрибут** является таблицей атрибутов.

- **CRL** — это таблица списка отзыва сертификатов.

```
[-split] [-config Machine\CAName]
```

### <a name="-view"></a>-представление

Выводит дамп представления сертификатов.

```
certutil [options] -view [queue | log | logfail | revoked | ext | attrib | crl] [csv]
```

Где:

- **очередь** создает заданную очередь запросов.

- в **журнале** выдаются дампы выданных или отозванных сертификатов, а также все неудачные запросы.

- **логфаил** выводит на дамп невыполненные запросы.

- **отменяет** дамп отозванных сертификатов.

- **ext** создает дамп таблицы расширения.

- **атрибут** создает дамп таблицы атрибутов.

- **CRL** выводит таблицу CRL.

- **CSV** предоставляет выходные данные с помощью значений, разделенных запятыми.

```
[-silent] [-split] [-config Machine\CAName] [-restrict RestrictionList] [-out ColumnList]
```

#### <a name="remarks"></a>Remarks

- Чтобы отобразить столбец **StatusCode** для всех записей, введите`-out StatusCode`

- Чтобы отобразить все столбцы последней записи, введите:`-restrict RequestId==$`

- Чтобы отобразить идентификатор **запроса** и **расстановку** для трех запросов, введите:`-restrict requestID>37,requestID<40 -out requestID,disposition`

- Чтобы отобразить идентификаторы**строк** и **номера CRL** для всех базовых списков отзыва сертификатов, введите:`-restrict crlminbase=0 -out crlrowID,crlnumber crl`

- Чтобы отобразить, введите:`-v -restrict crlminbase=0,crlnumber=3 -out crlrawcrl crl`

- Чтобы отобразить всю таблицу CRL, введите:`CRL`

- Используется `Date[+|-dd:hh]` для ограничения дат.

- Используется `now+dd:hh` для даты относительно текущего времени.

### <a name="-db"></a>-DB

Выводит дамп необработанной базы данных.

```
certutil [options] -db
```

```
[-config Machine\CAName] [-restrict RestrictionList] [-out ColumnList]
```

### <a name="-deleterow"></a>-DeleteRow

Удаляет строку из базы данных сервера.

```
certutil [options] -deleterow rowID | date [request | cert | ext | attrib | crl]
```

Где:

- **запрос** удаляет невыполненные и ожидающие запросы, исходя из даты отправки.

- **сертификат** удаляет просроченные и отозванные сертификаты, исходя из даты истечения срока действия.

- **ext** удаляет таблицу расширений.

- **атрибут** удаляет таблицу атрибутов.

- **CRL** УДАЛЯЕТ таблицу CRL.

```
[-f] [-config Machine\CAName]
```

#### <a name="examples"></a>Примеры

- Для удаления невыполненных и ожидающих запросов, отправленных 22 января 2001, введите:`1/22/2001 request`

- Чтобы удалить все сертификаты, срок действия которых истек 22 января 2001, введите:`1/22/2001 cert`

- Чтобы удалить строку сертификата, атрибуты и расширения для RequestID 37, введите:`37`

- Чтобы удалить списки отзыва сертификатов, срок действия которых истек 22 января 2001, введите:`1/22/2001 crl`

### <a name="-backup"></a>-backup

Создает резервную копию служб сертификатов Active Directory.

```
certutil [options] -backup backupdirectory [incremental] [keeplog]
```

Где:

- **BackupDirectory** — это каталог для хранения резервных копий данных.

- **добавочное** выполнение только добавочного резервного копирования (по умолчанию — полная резервная копия).

- **киплог** сохраняет файлы журнала базы данных (по умолчанию файлы журнала усекаются).

```
[-f] [-config Machine\CAName] [-p Password]
```

### <a name="-backupdb"></a>-баккупдб

Создает резервную копию базы данных служб сертификации Active Directory.

```
certutil [options] -backupdb backupdirectory [incremental] [keeplog]
```

Где:

- **BackupDirectory** — это каталог для хранения резервных копий файлов базы данных.

- **добавочное** выполнение только добавочного резервного копирования (по умолчанию — полная резервная копия).

- **киплог** сохраняет файлы журнала базы данных (по умолчанию файлы журнала усекаются).

```
[-f] [-config Machine\CAName]
```

### <a name="-backupkey"></a>-баккупкэй

Создает резервную копию сертификата служб сертификатов Active Directory и закрытого ключа.

```
certutil [options] -backupkey backupdirectory
```

Где:

- **BackupDirectory** — это каталог для хранения резервной копии PFX-файла.

```
[-f] [-config Machine\CAName] [-p password] [-t timeout]
```

### <a name="-restore"></a>-restore

Восстанавливает Active Directory службы сертификатов.

```
certutil [options] -restore backupdirectory
```

Где:

- **BackupDirectory** — это каталог, содержащий восстанавливаемые данные.

```
[-f] [-config Machine\CAName] [-p password]
```

### <a name="-restoredb"></a>-RestoreDB

Восстанавливает базу данных служб сертификации Active Directory.

```
certutil [options] -restoredb backupdirectory
```

Где:

- **BackupDirectory** — это каталог, содержащий восстанавливаемые файлы базы данных.

```
[-f] [-config Machine\CAName]
```

### <a name="-restorekey"></a>-ресторекэй

Восстанавливает сертификат служб сертификации Active Directory и закрытый ключ.

```
certutil [options] -restorekey backupdirectory | pfxfile
```

Где:

- **BackupDirectory** — это каталог, содержащий восстанавливаемый PFX-файл.

```
[-f] [-config Machine\CAName] [-p password]
```

### <a name="-importpfx"></a>-importpfx

Импортируйте сертификат и закрытый ключ. Дополнительные сведения см. в описании `-store` параметра в этой статье.

```
certutil [options] -importpfx [certificatestorename] pfxfile [modifiers]
```

Где:

- **цертификатесторенаме** — имя хранилища сертификатов.

- **модификаторы** — это список с разделителями-запятыми, который может включать один или несколько из следующих элементов:

  1. **AT_SIGNATURE** — изменяет keySpec на сигнатуру.

  2. **AT_KEYEXCHANGE** — изменяет keySpec на обмен ключами.

  3. **Export** — делает закрытый ключ неэкспортируемым

  4. Параметр "No- **CERT** " не импортирует сертификат

  5. **Chain — не** импортирует цепочку сертификатов

  6. **Root — не** импортирует корневой сертификат

  7. **Защита** — защищает ключи с помощью пароля

  8. Без **защиты** — пароль не защищает ключи с помощью пароля

```
[-f] [-user] [-p password] [-csp provider]
```

#### <a name="remarks"></a>Remarks

- По умолчанию используется личное хранилище компьютера.

### <a name="-dynamicfilelist"></a>-динамикфилелист

Отображает динамический список файлов.

```
certutil [options] -dynamicfilelist
```

```
[-config Machine\CAName]
```

### <a name="-databaselocations"></a>-датабаселокатионс

Отображает расположения базы данных.

```
certutil [options] -databaselocations
```

```
[-config Machine\CAName]
```

### <a name="-hashfile"></a>-хашфиле

Создает и отображает криптографический хэш-код для файла.

```
certutil [options] -hashfile infile [hashalgorithm]
```

### <a name="-store"></a>-Store

Выводит дамп хранилища сертификатов.

```
certutil [options] -store [certificatestorename [certID [outputfile]]]
```

Где:

- **цертификатесторенаме** — это имя хранилища сертификатов. Например:

  - `My, CA (default), Root,`

  - `ldap:///CN=Certification Authorities,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?one?objectClass=certificationAuthority (View Root Certificates)`

  - `ldap:///CN=CAName,CN=Certification Authorities,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority (Modify Root Certificates)`

  - `ldap:///CN=CAName,CN=MachineName,CN=CDP,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?certificateRevocationList?base?objectClass=cRLDistributionPoint (View CRLs)`

  - `ldap:///CN=NTAuthCertificates,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority (Enterprise CA Certificates)`

  - `ldap: (AD computer object certificates)`

  - `-user ldap: (AD user object certificates)`

- **certID** — маркер совпадения сертификата или CRL. Это может быть серийный номер, сертификат SHA-1, CRL, CTL или хэш открытого ключа, индекс числового сертификата (0, 1 и т. д.), числовой индекс списка отзыва сертификатов (. 0, десятый и т. д.), числовой индекс CTL (.. 0,.. 1 и т. д.), общедоступный ключ, сигнатура или расширение ObjectId, общее имя субъекта сертификата, адрес электронной почты, имя участника-пользователя или DNS, имя контейнера ключей или имя CSP, имя шаблона или ObjectId, идентификатор субъекта политики приложения или общее имя поставщика CRL. Многие из них могут привести к нескольким совпадениям.

- **выходной_файл** — файл, используемый для сохранения соответствующих сертификатов.

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-silent] [-split] [-dc DCName]
```

#### <a name="options"></a>Параметры

- `-user`Параметр обращается к хранилищу пользователей вместо хранилища компьютера.

- Этот `-enterprise` параметр позволяет получить доступ к хранилищу машинного предприятия.

- `-service`Параметр обращается к хранилищу служб компьютера.

- `-grouppolicy`Параметр позволяет получить доступ к хранилищу групповой политики компьютера.

Например:

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-addstore"></a>-addstore

Добавляет сертификат в хранилище. Дополнительные сведения см. в описании `-store` параметра в этой статье.

```
certutil [options] -addstore certificatestorename infile
```

Где:

- **цертификатесторенаме** — это имя хранилища сертификатов.

- " **файл** " — это сертификат или файл списка отзыва сертификатов, который необходимо добавить в магазин.

```
[-f] [-user] [-enterprise] [-grouppolicy] [-dc DCName]
```

### <a name="-delstore"></a>-delstore

Удаляет сертификат из хранилища. Дополнительные сведения см. в описании `-store` параметра в этой статье.

```
certutil [options] -delstore certificatestorename certID
```

Где:

- **цертификатесторенаме** — это имя хранилища сертификатов.

- **certID** — маркер совпадения сертификата или CRL.

```
[-enterprise] [-user] [-grouppolicy] [-dc DCName]
```

### <a name="-verifystore"></a>-верифисторе

Проверяет сертификат в хранилище. Дополнительные сведения см. в описании `-store` параметра в этой статье.

```
certutil [options] -verifystore certificatestorename [certID]
```

Где:

- **цертификатесторенаме** — это имя хранилища сертификатов.

- **certID** — маркер совпадения сертификата или CRL.

```
[-enterprise] [-user] [-grouppolicy] [-silent] [-split] [-dc DCName] [-t timeout]
```

### <a name="-repairstore"></a>-репаирсторе

Восстанавливает сопоставление ключа или обновляет свойства сертификата или ключевой дескриптор безопасности. Дополнительные сведения см. в описании `-store` параметра в этой статье.

```
certutil [options] -repairstore certificatestorename certIDlist [propertyinffile | SDDLsecuritydescriptor]
```

Где:

- **цертификатесторенаме** — это имя хранилища сертификатов.

- **цертидлист** — это разделенный запятыми список маркеров сертификата или списка отзыва сертификатов. Дополнительные сведения см `-store certID` . в описании в этой статье.

- **пропертинффиле** — это INF-файл, содержащий внешние свойства, включая:

  ```
  [Properties]
      19 = Empty ; Add archived property, OR:
      19 =       ; Remove archived property

      11 = {text}Friendly Name ; Add friendly name property

      127 = {hex} ; Add custom hexadecimal property
          _continue_ = 00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f
          _continue_ = 10 11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f

      2 = {text} ; Add Key Provider Information property
        _continue_ = Container=Container Name&
        _continue_ = Provider=Microsoft Strong Cryptographic Provider&
        _continue_ = ProviderType=1&
        _continue_ = Flags=0&
        _continue_ = KeySpec=2

      9 = {text} ; Add Enhanced Key Usage property
        _continue_ = 1.3.6.1.5.5.7.3.2,
        _continue_ = 1.3.6.1.5.5.7.3.1,
  ```

```
[-f] [-enterprise] [-user] [-grouppolicy] [-silent] [-split] [-csp provider]
```

### <a name="-viewstore"></a>-виевсторе

Выводит дамп хранилища сертификатов. Дополнительные сведения см. в описании `-store` параметра в этой статье.

```
certutil [options] -viewstore [certificatestorename [certID [outputfile]]]
```

Где:

- **цертификатесторенаме** — это имя хранилища сертификатов.

- **certID** — маркер совпадения сертификата или CRL.

- **выходной_файл** — файл, используемый для сохранения соответствующих сертификатов.

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-dc DCName]
```

#### <a name="options"></a>Параметры

- `-user`Параметр обращается к хранилищу пользователей вместо хранилища компьютера.

- Этот `-enterprise` параметр позволяет получить доступ к хранилищу машинного предприятия.

- `-service`Параметр обращается к хранилищу служб компьютера.

- `-grouppolicy`Параметр позволяет получить доступ к хранилищу групповой политики компьютера.

Например:

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-viewdelstore"></a>-виевделсторе

Удаляет сертификат из хранилища.

```
certutil [options] -viewdelstore [certificatestorename [certID [outputfile]]]
```

Где:

- **цертификатесторенаме** — это имя хранилища сертификатов.

- **certID** — маркер совпадения сертификата или CRL.

- **выходной_файл** — файл, используемый для сохранения соответствующих сертификатов.

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-dc DCName]
```

#### <a name="options"></a>Параметры

- `-user`Параметр обращается к хранилищу пользователей вместо хранилища компьютера.

- Этот `-enterprise` параметр позволяет получить доступ к хранилищу машинного предприятия.

- `-service`Параметр обращается к хранилищу служб компьютера.

- `-grouppolicy`Параметр позволяет получить доступ к хранилищу групповой политики компьютера.

Например:

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-dspublish"></a>-дспублиш

Публикует сертификат или список отзыва сертификатов (CRL) для Active Directory.

```
certutil [options] -dspublish certfile [NTAuthCA | RootCA | SubCA | CrossCA | KRA | User | Machine]
```

```
certutil [options] -dspublish CRLfile [DSCDPContainer [DSCDPCN]]
```

Где:

- **CertFile** — это имя файла сертификата для публикации.

- **Нтауска** публикует сертификат в хранилище DS Enterprise.

- **RootCA** публикует сертификат в доверенном корневом хранилище DS.

- **Субка** ПУБЛИКУЕТ сертификат ЦС в объекте ЦС службы каталогов.

- **Кросска** публикует перекрестный сертификат для объекта ЦС DS.

- **KRA** публикует сертификат для объекта агента восстановления ключей DS.

- **Пользователь** публикует сертификат в ОБЪЕКТЕ пользовательской службы.

- **Компьютер** публикует сертификат для объекта Machine DS.

- **Крлфиле** — имя публикуемого файла списка отзыва сертификатов.

- **Дскдпконтаинер** — это контейнер CDP DS, обычно имя компьютера ЦС.

- **Дскдпкн** — это общее имя объекта CDP DS, обычно основанное на исключенном коротком имени ЦС и индексе ключа.

- Используйте `-f` для создания нового объекта DS.

```
[-f] [-user] [-dc DCName]
```

### <a name="-adtemplate"></a>-адтемплате

Отображает Active Directory шаблоны.

```
certutil [options] -adtemplate [template]
```

```
[-f] [-user] [-ut] [-mt] [-dc DCName]
```

### <a name="-template"></a>-Template

Отображает шаблоны сертификатов.

```
certutil [options] -template [template]
```

```
[-f] [-user] [-silent] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-templatecas"></a>-темплатекас

Отображает центры сертификации (ЦС) для шаблона сертификата.

```
certutil [options] -templatecas template
```

```
[-f] [-user] [-dc DCName]
```

### <a name="-catemplates"></a>-катемплатес

Отображает шаблоны для центра сертификации.

```
certutil [options] -catemplates [template]
```

```
[-f] [-user] [-ut] [-mt] [-config Machine\CAName] [-dc DCName]
```

### <a name="-setcasites"></a>-сеткаситес

Управляет именами сайтов, включая настройку, проверку и удаление имен сайтов центра сертификации.

```
certutil [options] -setcasites [set] [sitename]
certutil [options] -setcasites verify [sitename]
certutil [options] -setcasites delete
```

Где:

- **имя сайта** допускается только при использовании одного центра сертификации.

```
[-f] [-config Machine\CAName] [-dc DCName]
```

#### <a name="remarks"></a>Remarks

- `-config`Параметр предназначен для одного центра сертификации (по умолчанию все ЦС).

- Этот `-f` параметр можно использовать для переопределения ошибок проверки для указанного **SiteName** или для удаления всех ЦС sitename.

> [!NOTE]
> Дополнительные сведения о настройке центров сертификации для поддержки сайта служб домен Active Directory Services (AD DS) см. в разделе [сведения о поддержке сайта AD DS для клиентов AD CS и PKI](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740(v=ws.11)).

### <a name="-enrollmentserverurl"></a>-Енроллментсерверурл

Отображает, добавляет или удаляет URL-адреса серверов регистрации, связанные с центром сертификации.

```
certutil [options] -enrollmentServerURL [URL authenticationtype [priority] [modifiers]]
certutil [options] -enrollmentserverURL URL delete
```

Где:

- **AuthenticationType** указывает один из следующих методов проверки подлинности клиента при добавлении URL-адреса:

  1. **Kerberos** — используйте учетные данные Kerberos SSL.

  2. **username** — использовать именованную учетную запись для SSL-учетных данных.

  3. **clientcertificate**— используйте учетные данные SSL сертификата X. 509.

  4. **анонимное** использование анонимных учетных данных SSL.

- **Delete** удаляет указанный URL-адрес, связанный с центром сертификации.

- значение **Priority** по умолчанию равно, `1` Если при добавлении URL-адреса не указано.

- **модификаторы** — это список с разделителями-запятыми, который включает один или несколько следующих элементов:

1. запросы на продление только для **алловреневалсонли** могут отправляться в этот центр сертификации через этот URL-адрес.

2. **алловкэйбаседреневал** — разрешает использование сертификата, не имеющего связанной учетной записи в Active Directory. Это относится только к режимам clientcertificate и алловреневалсонли

```
[-config Machine\CAName] [-dc DCName]
```

### <a name="-adca"></a>-адка

Отображает Active Directory центров сертификации.

```
certutil [options] -adca [CAName]
```

```
[-f] [-split] [-dc DCName]
```

### <a name="-ca"></a>-CA

Отображает центры сертификации политики регистрации.

```
certutil [options] -CA [CAName | templatename]
```

```
[-f] [-user] [-silent] [-split] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-policy"></a>политика

Отображает политику регистрации.

```
[-f] [-user] [-silent] [-split] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-policycache"></a>-полицикаче

Отображает или удаляет записи кэша политики регистрации.

```
certutil [options] -policycache [delete]
```

Где:

- **Delete** удаляет записи кэша сервера политики.

- **-f** удаляет все записи кэша

```
[-f] [-user] [-policyserver URLorID]
```

### <a name="-credstore"></a>-кредсторе

Отображает, добавляет или удаляет записи хранилища учетных данных.

```
certutil [options] -credstore [URL]
certutil [options] -credstore URL add
certutil [options] -credstore URL delete
```

Где:

- **URL** -адрес — это целевой URL-адрес. Также можно использовать `*` для сопоставления всех записей или `https://machine*` для сопоставления с префиксом URL-адреса.

- **Добавить** добавляет запись хранилища учетных данных. При использовании этого параметра также требуется использовать учетные данные SSL.

- **Удалить** удаляет записи хранилища учетных данных.

- **-f** перезаписывает одну запись или удаляет несколько записей.

```
[-f] [-user] [-silent] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-installdefaulttemplates"></a>-инсталлдефаулттемплатес

Устанавливает шаблоны сертификатов по умолчанию.

```
certutil [options] -installdefaulttemplates
```

```
[-dc DCName]
```

### <a name="-urlcache"></a>-Урлкаче

Отображает или удаляет записи кэша URL-адресов.

```
certutil [options] -URLcache [URL | CRL | * [delete]]
```

Где:

- **URL** -адрес — это кэшированный URL-адрес.

- **CRL** выполняется только для всех кэшированных URL-адресов CRL.

- **&#42;** работает со всеми кэшированными URL-адресами.

- **Delete** удаляет соответствующие URL-адреса из локального кэша текущего пользователя.

- **-f** принудительно выбирает конкретный URL-адрес и обновляет кэш.

```
[-f] [-split]
```

### <a name="-pulse"></a>импульс

События автоматической регистрации пульса.

```
certutil [options] -pulse
```

```
[-user]
```

### <a name="-machineinfo"></a>-мачинеинфо

Отображает сведения об объекте Active Directory компьютере.

```
certutil [options] -machineinfo domainname\machinename$
```

### <a name="-dcinfo"></a>-ДЦинфо

Отображает сведения об контроллере домена. По умолчанию сертификаты контроллера домена отображаются без проверки.

```
certutil [options] -DCInfo [domain] [verify | deletebad | deleteall]
```

```
[-f] [-user] [-urlfetch] [-dc DCName] [-t timeout]
```

> [!TIP]
> В Windows Server 2012 можно AD DS домен Active Directory указать домен **[домен]** и указать контроллер домена (**-DC**). Для успешного выполнения команды необходимо использовать учетную запись, которая является членом группы **"Администраторы домена"** или **"Администраторы предприятия"**. Ниже приведены изменения в поведении этой команды.<ol><li>1. Если домен не указан и не указан определенный контроллер домена, этот параметр возвращает список контроллеров домена для обработки с контроллера домена по умолчанию.</li><li>2. Если домен не указан, но указан контроллер домена, создается отчет о сертификатах на указанном контроллере домена.</li><li>3. Если указан домен, но не указан контроллер домена, то создается список контроллеров домена вместе с отчетами по сертификатам для каждого контроллера домена в списке.</li><li>4. Если указан домен и контроллер домена, то из целевого контроллера домена создается список контроллеров домена. Также создается отчет о сертификатах для каждого контроллера домена в списке.</li></ol>
>
>Например, предположим, что существует домен с именем КПАНДЛ и контроллером домена с именем КПАНДЛ-DC1. Можно выполнить следующую команду, чтобы получить список контроллеров домена и их сертификаты из КПАНДЛ-DC1:`certutil -dc cpandl-dc1 -DCInfo cpandl`

### <a name="-entinfo"></a>-ентинфо

Отображает сведения о центре сертификации предприятия.

```
certutil [options] -entinfo domainname\machinename$
```

```
[-f] [-user]
```

### <a name="-tcainfo"></a>-ткаинфо

Отображает сведения о центре сертификации.

```
certutil [options] -tcainfo [domainDN | -]
```

```
[-f] [-enterprise] [-user] [-urlfetch] [-dc DCName] [-t timeout]
```

### <a name="-scinfo"></a>-сЦинфо

Отображает сведения о смарт-карте.

```
certutil [options] -scinfo [readername [CRYPT_DELETEKEYSET]]
```

Где:

- **CRYPT_DELETEKEYSET** удаляет все ключи на смарт-карте.

```
[-silent] [-split] [-urlfetch] [-t timeout]
```

### <a name="-scroots"></a>-скрутс

Управляет корневыми сертификатами смарт-карт.

```
certutil [options] -scroots update [+][inputrootfile] [readername]
certutil [options] -scroots save \@in\\outputrootfile [readername]
certutil [options] -scroots view [inputrootfile | readername]
certutil [options] -scroots delete [readername]
```

```
[-f] [-split] [-p Password]
```

### <a name="-verifykeys"></a>-верификэйс

Проверяет набор открытых или закрытых ключей.

```
certutil [options] -verifykeys [keycontainername cacertfile]
```

Где:

- **KeyContainerName** — это имя контейнера ключей для проверяемого ключа. По умолчанию этот параметр имеет значение ключи компьютера. Чтобы переключиться на пользовательские ключи, используйте `-user` .

- **кацертфиле** подписывает или шифрует файлы сертификатов.

```
[-f] [-user] [-silent] [-config Machine\CAName]
```

#### <a name="remarks"></a>Remarks

- Если аргументы не указаны, то каждый сертификат ЦС для подписи проверяется на соответствие закрытому ключу.

- Эта операция может выполняться только с локальным ЦС или локальными ключами.

### <a name="-verify"></a>— Проверка

Проверяет сертификат, список отзыва сертификатов (CRL) или цепочку сертификатов.

```
certutil [options] -verify certfile [applicationpolicylist | - [issuancepolicylist]]
certutil [options] -verify certfile [cacertfile [crossedcacertfile]]
certutil [options] -verify CRLfile cacertfile [issuedcertfile]
certutil [options] -verify CRLfile cacertfile [deltaCRLfile]
```

Где:

- **CertFile** — имя сертификата для проверки.

- **аппликатионполицилист** — это необязательный список обязательных идентификаторов политик приложений, разделенных запятыми.

- **иссуанцеполицилист** — это необязательный список обязательных идентификаторов ObjectID политики выдачи, разделенных запятыми.

- **кацертфиле** — это необязательный сертификат выдающего ЦС для проверки.

- **кросседкацертфиле** — это необязательный сертификат, перекрестно сертифицированный **CertFile**.

- **Крлфиле** — это файл списка отзыва сертификатов, используемый для проверки **кацертфиле**.

- **иссуедцертфиле** — это необязательный выданный сертификат, охваченный крлфиле.

- **делтакрлфиле** — это необязательный разностный файл CRL.

```
[-f] [-enterprise] [-user] [-silent] [-split] [-urlfetch] [-t timeout]
```

#### <a name="remarks"></a>Remarks

- Использование **аппликатионполицилист** ограничивают построение цепочки только последовательностями, допустимыми для указанных политик приложений.

- Использование **иссуанцеполицилист** ограничивают построение цепочки только последовательностями, допустимыми для указанных политик выдачи.

- С помощью **кацертфиле** проверяет поля в файле на наличие **CertFile** или **крлфиле**.

- С помощью **иссуедцертфиле** проверяет поля в файле на соответствие **крлфиле**.

- С помощью Делтакрлфиле проверяет поля в файле на наличие **CertFile**.

- Если **кацертфиле** не указан, создается полная цепочка и проверяется на наличие **CertFile**.

- Если указаны значения **кацертфиле** и **кросседкацертфиле** , то поля в обоих файлах проверяются по протоколу **CertFile**.

### <a name="-verifyctl"></a>-Верификтл

Проверяет CTL Аусрут или неразрешенных сертификатов.

```
certutil [options] -verifyCTL CTLobject [certdir] [certfile]
```

Где:

- **Ктлобжект** определяет список проверяемых сертификатов (CTL), включая:

  - **Аусрутву** — считывает CAB-файл аусрут и соответствующие сертификаты из кэша URL. `-f`Вместо этого используйте для скачивания из центр обновления Windows.

  - **Дисалловедву** — чтение CAB-файла запрещенных сертификатов и неразрешенный файл хранилища сертификатов из кэша URL. `-f`Вместо этого используйте для скачивания из центр обновления Windows.

  - **Аусрут** — считывает кэш-список аусрут, кэшированный в реестре. Используйте с `-f` и недоверенным **CertFile** для принудительного обновления кэша реестра аусрут и недопустимых списков CTL сертификатов.

  - **Запрещено** — считывает список доверенных сертификатов, кэшированных в реестре. Используйте с `-f` и недоверенным **CertFile** для принудительного обновления кэша реестра аусрут и недопустимых списков CTL сертификатов.

- **Ктлфиленаме** указывает файл или путь HTTP к файлу CTL или CAB.

- **цертдир** указывает папку, содержащую сертификаты, соответствующие записям CTL. По умолчанию используется та же папка или веб-сайт, что и **ктлобжект**. Для использования пути к папке HTTP в конце необходимо указать разделитель пути. Если не указать **аусрут** или не **разрешено**, будет выполнен поиск соответствующих сертификатов в нескольких расположениях, включая локальные хранилища сертификатов, crypt32.dll ресурсы и локальный кэш URL-адресов. `-f`При необходимости используйте для скачивания из центр обновления Windows.

- **CertFile** указывает сертификаты для проверки. Сертификаты сопоставляются с записями CTL, отображая результаты. Этот параметр подавляет большую часть выходных данных по умолчанию.

```
[-f] [-user] [-split]
```

### <a name="-sign"></a>-Sign

Повторно подписывает список отзыва сертификатов (CRL) или сертификат.

```
certutil [options] -sign infilelist | serialnumber | CRL outfilelist [startdate+dd:hh] [+serialnumberlist | -serialnumberlist | -objectIDlist | \@extensionfile]
certutil [options] -sign infilelist | serialnumber | CRL outfilelist [#hashalgorithm] [+alternatesignaturealgorithm | -alternatesignaturealgorithm]
```

Где:

- **инфилелист** — это разделенный запятыми список файлов сертификатов или CRL для изменения и повторного подписания.

- **SerialNumber** — это серийный номер создаваемого сертификата. Срок действия и другие параметры не могут присутствовать.

- **CRL** создает пустой список отзыва сертификатов. Срок действия и другие параметры не могут присутствовать.

- **аутфилелист** — это разделенный запятыми список измененных выходных файлов сертификата или CRL. Число файлов должно совпадать с инфилелист.

- **StartDate + ДД: чч** — это новый срок действия для сертификатов или файлов CRL, включая следующие:

  - Дополнительная Дата и время

  - необязательные дни и часы периода действия

  Если указаны оба значения, необходимо использовать разделитель плюс (+). Используйте `now[+dd:hh]` для запуска в текущее время. Используйте `never` , чтобы не использовать дату истечения срока действия (только для списков отзыва сертификатов).

- **сериалнумберлист** — это список серийных номеров с разделителями-запятыми для добавления или удаления файлов.

- **обжектидлист** — список имен ObjectID с разделителями-запятыми удаляемых файлов.

- ** \@ екстенсионфиле** — это INF-файл, содержащий расширения для обновления или удаления. Например:

  ```
  [Extensions]
      2.5.29.31 = ; Remove CRL Distribution Points extension
      2.5.29.15 = {hex} ; Update Key Usage extension
      _continue_=03 02 01 86
  ```

- **HashAlgorithm** — имя хэш-алгоритма. Это должен быть только текст, предшествующий `#` знаку.

- **алтернатесигнатуреалгорисм** — это альтернативный описатель алгоритма подписи.

```
[-nullsign] [-f] [-silent] [-cert certID]
```

#### <a name="remarks"></a>Remarks

- Использование знака "минус" (-) удаляет серийные номера и расширения.

- Использование знака плюс (+) добавляет серийные номера в список отзыва сертификатов.

- Список можно использовать для одновременного удаления серийных номеров и идентификаторов ObjectID из списка отзыва сертификатов.

- Использование знака «минус» перед **алтернатесигнатуреалгорисм** позволяет использовать устаревший формат подписи. Использование знака «плюс» позволяет использовать альтернативный формат подписи. Если не указать **алтернатесигнатуреалгорисм**, будет использоваться формат подписи сертификата или списка отзыва сертификатов.

### <a name="-vroot"></a>— vroot

Создает или удаляет виртуальные корневые каталоги и общие файловые ресурсы.

```
certutil [options] -vroot [delete]
```

### <a name="-vocsproot"></a>-вокспрут

Создает или удаляет виртуальные корневые каталоги для веб-прокси OCSP.

```
certutil [options] -vocsproot [delete]
```

### <a name="-addenrollmentserver"></a>-адденроллментсервер

При необходимости добавьте приложение сервера регистрации и пул приложений для указанного центра сертификации. Эта команда не устанавливает двоичные файлы и пакеты.

```
certutil [options] -addenrollmentserver kerberos | username | clientcertificate [allowrenewalsonly] [allowkeybasedrenewal]
```

Где:

- **адденроллментсервер** требует использовать метод проверки подлинности для клиентского подключения к серверу регистрации сертификатов, включая:

  - **Kerberos** использует учетные данные Kerberos SSL.

  - **имя пользователя** использует именованную учетную запись для SSL-учетных данных.

  - **clientcertificate** использует учетные данные SSL сертификата X. 509.

- **алловреневалсонли** позволяет только отправку запросов на продление в центр сертификации через URL-адрес.

- **алловкэйбаседреневал** позволяет использовать сертификат без связанной учетной записи в Active Directory. Это применимо при использовании с режимом **clientcertificate** и **алловреневалсонли** .

```
[-config Machine\CAName]
```

### <a name="-deleteenrollmentserver"></a>-делетинроллментсервер

При необходимости удаляет приложение сервера регистрации и пул приложений для указанного центра сертификации. Эта команда не устанавливает двоичные файлы и пакеты.

```
certutil [options] -deleteenrollmentserver kerberos | username | clientcertificate
```

Где:

- **делетинроллментсервер** требует использовать метод проверки подлинности для клиентского подключения к серверу регистрации сертификатов, включая:

  - **Kerberos** использует учетные данные Kerberos SSL.

  - **имя пользователя** использует именованную учетную запись для SSL-учетных данных.

  - **clientcertificate** использует учетные данные SSL сертификата X. 509.

```
[-config Machine\CAName]
```

### <a name="-addpolicyserver"></a>-аддполицисервер

При необходимости добавьте приложение сервера политики и пул приложений. Эта команда не устанавливает двоичные файлы и пакеты.

```
certutil [options] -addpolicyserver kerberos | username | clientcertificate [keybasedrenewal]
```

Где:

- **аддполицисервер** требует использовать метод проверки подлинности для клиентского подключения к серверу политики сертификатов, в том числе:

  - **Kerberos** использует учетные данные Kerberos SSL.

  - **имя пользователя** использует именованную учетную запись для SSL-учетных данных.

  - **clientcertificate** использует учетные данные SSL сертификата X. 509.

- **кэйбаседреневал** позволяет использовать политики, возвращаемые клиенту, содержащему шаблоны кэйбаседреневал. Этот параметр применяется только для проверки подлинности **username** и **clientcertificate** .

### <a name="-deletepolicyserver"></a>-делетеполицисервер

При необходимости удаляет приложение сервера политики и пул приложений. Эта команда не удаляет двоичные файлы или пакеты.

Certutil [параметры]-Делетеполицисервер Kerberos | имя пользователя | clientcertificate [кэйбаседреневал]

Где:

- **делетеполицисервер** требует использовать метод проверки подлинности для клиентского подключения к серверу политики сертификатов, в том числе:

  - **Kerberos** использует учетные данные Kerberos SSL.

  - **имя пользователя** использует именованную учетную запись для SSL-учетных данных.

  - **clientcertificate** использует учетные данные SSL сертификата X. 509.

- **кэйбаседреневал** позволяет использовать сервер политики кэйбаседреневал.

### <a name="-oid"></a>-OID

Отображает идентификатор объекта или задает отображаемое имя.

```
certutil [options] -oid objectID [displayname | delete [languageID [type]]]
certutil [options] -oid groupID
certutil [options] -oid agID | algorithmname [groupID]
```

Где:

- **ObjectID** отображает или добавляет отображаемое имя.

- **groupId** — это число (в десятичной системе), которое перечисляет ObjectIds.

- **алгид** — это шестнадцатеричный идентификатор, который ищет ObjectID.

- **algorithmName** — это имя алгоритма, который ищет ObjectID.

- **DisplayName** отображает имя для хранения в DS.

- **Delete** удаляет отображаемое имя.

- **LanguageId** — это значение идентификатора языка (по умолчанию: 1033).

- **Тип** — это тип создаваемого объекта DS, включая следующие:

  - `1`-Template (по умолчанию)

  - `2`— Политика выдачи

  - `3`— Политика приложения

- `-f`Создает объект DS.

### <a name="-error"></a>-Ошибка

Отображает текст сообщения, связанного с кодом ошибки.

```
certutil [options] -error errorcode
```

### <a name="-getreg"></a>-жетрег

Отображает значение реестра.

```
certutil [options] -getreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]][registryvaluename]
```

Где:

- **ЦС** использует раздел реестра центра сертификации.

- **RESTORE** использует раздел реестра Restore центра сертификации.

- **Политика** использует раздел реестра модуля политики.

- **Exit** использует раздел реестра первого модуля выхода.

- **шаблон** использует раздел реестра Template (используется `-user` для пользовательских шаблонов).

- **Регистрация** использует раздел реестра регистрации (используется `-user` для контекста пользователя).

- **цепочка** использует раздел реестра конфигурации цепочки.

- **полицисерверс** использует раздел реестра "серверы политики".

- **ProgID** использует идентификатор ProgID модуля политики или выхода (имя подраздела реестра).

- **регистривалуенаме** использует имя значения реестра (используйте `Name*` в качестве префикса).

- **значение** использует новое числовое значение, строку или дату или имя файла реестра. Если числовое значение начинается с `+` или `-` , биты, указанные в новом значении, задаются или очищаются в существующем значении реестра.

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>Remarks

- Если строковое значение начинается с `+` или `-` , а существующее значение является `REG_MULTI_SZ` значением, строка добавляется в существующий параметр реестра или удаляется из него. Чтобы принудительно создать `REG_MULTI_SZ` значение, добавьте `\n` в конец строкового значения.

- Если значение начинается с `\@` , оставшаяся часть значения представляет собой имя файла, содержащего шестнадцатеричное текстовое представление двоичного значения. Если он не ссылается на допустимый файл, он будет проанализирован как `[Date][+|-][dd:hh]` необязательная дата плюс или минус необязательные дни и часы. Если указаны оба значения, используйте знак плюса (+) или знак минуса (-). Используется `now+dd:hh` для даты относительно текущего времени.

- Используйте `chain\chaincacheresyncfiletime \@now` для эффективного сброса кэшированных списков отзыва сертификатов.

### <a name="-setreg"></a>-Setreg

Задает значение реестра.

```
certutil [options] -setreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]]registryvaluename value
```

Где:

- **ЦС** использует раздел реестра центра сертификации.

- **RESTORE** использует раздел реестра Restore центра сертификации.

- **Политика** использует раздел реестра модуля политики.

- **Exit** использует раздел реестра первого модуля выхода.

- **шаблон** использует раздел реестра Template (используется `-user` для пользовательских шаблонов).

- **Регистрация** использует раздел реестра регистрации (используется `-user` для контекста пользователя).

- **цепочка** использует раздел реестра конфигурации цепочки.

- **полицисерверс** использует раздел реестра "серверы политики".

- **ProgID** использует идентификатор ProgID модуля политики или выхода (имя подраздела реестра).

- **регистривалуенаме** использует имя значения реестра (используйте `Name*` в качестве префикса).

- **значение** использует новое числовое значение, строку или дату или имя файла реестра. Если числовое значение начинается с `+` или `-` , биты, указанные в новом значении, задаются или очищаются в существующем значении реестра.

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>Remarks

- Если строковое значение начинается с `+` или `-` , а существующее значение является `REG_MULTI_SZ` значением, строка добавляется в существующий параметр реестра или удаляется из него. Чтобы принудительно создать `REG_MULTI_SZ` значение, добавьте `\n` в конец строкового значения.

- Если значение начинается с `\@` , оставшаяся часть значения представляет собой имя файла, содержащего шестнадцатеричное текстовое представление двоичного значения. Если он не ссылается на допустимый файл, он будет проанализирован как `[Date][+|-][dd:hh]` необязательная дата плюс или минус необязательные дни и часы. Если указаны оба значения, используйте знак плюса (+) или знак минуса (-). Используется `now+dd:hh` для даты относительно текущего времени.

- Используйте `chain\chaincacheresyncfiletime \@now` для эффективного сброса кэшированных списков отзыва сертификатов.

### <a name="-delreg"></a>-делрег

Удаляет значение реестра.

```
certutil [options] -delreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]][registryvaluename]
```

Где:

- **ЦС** использует раздел реестра центра сертификации.

- **RESTORE** использует раздел реестра Restore центра сертификации.

- **Политика** использует раздел реестра модуля политики.

- **Exit** использует раздел реестра первого модуля выхода.

- **шаблон** использует раздел реестра Template (используется `-user` для пользовательских шаблонов).

- **Регистрация** использует раздел реестра регистрации (используется `-user` для контекста пользователя).

- **цепочка** использует раздел реестра конфигурации цепочки.

- **полицисерверс** использует раздел реестра "серверы политики".

- **ProgID** использует идентификатор ProgID модуля политики или выхода (имя подраздела реестра).

- **регистривалуенаме** использует имя значения реестра (используйте `Name*` в качестве префикса).

- **значение** использует новое числовое значение, строку или дату или имя файла реестра. Если числовое значение начинается с `+` или `-` , биты, указанные в новом значении, задаются или очищаются в существующем значении реестра.

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>Remarks

- Если строковое значение начинается с `+` или `-` , а существующее значение является `REG_MULTI_SZ` значением, строка добавляется в существующий параметр реестра или удаляется из него. Чтобы принудительно создать `REG_MULTI_SZ` значение, добавьте `\n` в конец строкового значения.

- Если значение начинается с `\@` , оставшаяся часть значения представляет собой имя файла, содержащего шестнадцатеричное текстовое представление двоичного значения. Если он не ссылается на допустимый файл, он будет проанализирован как `[Date][+|-][dd:hh]` необязательная дата плюс или минус необязательные дни и часы. Если указаны оба значения, используйте знак плюса (+) или знак минуса (-). Используется `now+dd:hh` для даты относительно текущего времени.

- Используйте `chain\chaincacheresyncfiletime \@now` для эффективного сброса кэшированных списков отзыва сертификатов.

### <a name="-importkms"></a>-Импорткмс

Импортирует ключи и сертификаты пользователей в базу данных сервера для архивирования ключей.

```
certutil [options] -importKMS userkeyandcertfile [certID]
```

Где:

- **усеркэйандцертфиле** — это файл данных с закрытыми ключами пользователей и сертификатами, которые должны быть архивированы. Этот файл может быть следующим:

  - Файл экспорта Exchange Key Management Server (KMS).

  - PFX-файл.

- certID — маркер соответствия сертификата расшифровки файла экспорта службы KMS. Дополнительные сведения см. в описании `-store` параметра в этой статье.

- `-f`импортирует сертификаты, не выданные центром сертификации.

```
[-f] [-silent] [-split] [-config Machine\CAName] [-p password] [-symkeyalg symmetrickeyalgorithm[,keylength]]
```

### <a name="-importcert"></a>-импортцерт

Импортирует файл сертификата в базу данных.

```
certutil [options] -importcert certfile [existingrow]
```

Где:

- **ексистингров** импортирует сертификат вместо ожидающего запроса для того же ключа.

- `-f`импортирует сертификаты, не выданные центром сертификации.

```
[-f] [-config Machine\CAName]
```

#### <a name="remarks"></a>Remarks

Также может потребоваться настроить центр сертификации для поддержки внешних сертификатов. Для этого введите `import - certutil -setreg ca\KRAFlags +KRAF_ENABLEFOREIGN` .

### <a name="-getkey"></a>-GetKey

Извлекает заархивированный большой двоичный объект восстановления закрытого ключа, создает скрипт восстановления или восстанавливает архивированные ключи.

```
certutil [options] -getkey searchtoken [recoverybloboutfile]
certutil [options] -getkey searchtoken script outputscriptfile
certutil [options] -getkey searchtoken retrieve | recover outputfilebasename
```

Где:

- **Скрипт** создает скрипт для получения и восстановления ключей (поведение по умолчанию при обнаружении нескольких соответствующих кандидатов восстановления или если выходной файл не указан).

- **Извлечение** получает один или несколько больших двоичных объектов восстановления (поведение по умолчанию, если найден только один подходящий кандидат для восстановления и если указан выходной файл). При использовании этого параметра происходит усечение любого расширения и добавляется строка, относящаяся к сертификату, и расширение REC для каждого большого двоичного объекта восстановления ключей.  Каждый файл содержит цепочку сертификатов и связанный закрытый ключ, которые по-прежнему шифруются для одного или нескольких сертификатов агента восстановления ключей.

- **Восстановление** извлекает и восстанавливает закрытые ключи за один шаг (требуются сертификаты агента восстановления ключей и закрытые ключи). При использовании этого параметра все расширения усекаются и добавляется расширение P12.  Каждый файл содержит восстановленные цепочки сертификатов и связанные закрытые ключи, сохраненные в виде PFX-файла.

- **сеарчтокен** выбирает ключи и сертификаты для восстановления, в том числе:

  - 1. Общее имя сертификата

  - 2. Серийный номер сертификата

  - 3. Хэш SHA-1 сертификата (отпечаток)

  - 4. Хэш SHA-1 сертификата KeyId (идентификатор ключа субъекта)

  - 5. Имя запросившего (домен \ пользователь)

  - 6. UPN ( \@ домен пользователя)

- **рековериблобаутфиле** выводит файл с цепочкой сертификатов и связанным закрытым ключом, который по-прежнему шифруется одним или несколькими сертификатами агента восстановления ключей.

- **outputscriptfile** выводит файл с пакетным скриптом для извлечения и восстановления закрытых ключей.

- **аутпутфилебасенаме** выводит базовое имя файла.

```
[-f] [-unicodetext] [-silent] [-config Machine\CAName] [-p password] [-protectto SAMnameandSIDlist] [-csp provider]
```

### <a name="-recoverkey"></a>-рековеркэй

Восстановление архивированного закрытого ключа.

```
certutil [options] -recoverkey recoveryblobinfile [PFXoutfile [recipientindex]]
```

```
[-f] [-user] [-silent] [-split] [-p password] [-protectto SAMnameandSIDlist] [-csp provider] [-t timeout]
```

### <a name="-mergepfx"></a>-Мержепфкс

Объединяет PFX-файлы.

```
certutil [options] -mergePFX PFXinfilelist PFXoutfile [extendedproperties]
```

Где:

- **Пфксинфилелист** — это список входных файлов PFX с разделителями-запятыми.

- **Пфксаутфиле** — имя выходного файла PFX.

- **расширенных свойств** включает любые расширенные свойства.

```
[-f] [-user] [-split] [-p password] [-protectto SAMnameAndSIDlist] [-csp provider]
```

#### <a name="remarks"></a>Remarks

- Пароль, указанный в командной строке, должен быть списком паролей с разделителями-запятыми.

- Если указано более одного пароля, для выходного файла используется последний пароль. Если указан только один пароль или последний пароль `*` , пользователю будет предложено ввести пароль для выходного файла.

### <a name="-convertepf"></a>-Конвертепф

Преобразует PFX-файл в файл EPF.

```
certutil [options] -convertEPF PFXinfilelist PFXoutfile [cast | cast-] [V3CAcertID][,salt]
```

Где:


- **Пфксинфилелист** — это список входных файлов PFX с разделителями-запятыми.

- **Пфксаутфиле** — имя выходного файла PFX.

- **EPF** — это имя выходного файла EPF.

- **приведение** использует шифрование с приведением 64.

- **приведение —** использует приведение шифрования 64 (Export)

- **V3CAcertID** — маркер соответствия сертификата ЦС v3. Дополнительные сведения см. в описании `-store` параметра в этой статье.

- **Salt** — это строка соли выходного файла EPF.

```
[-f] [-silent] [-split] [-dc DCName] [-p password] [-csp provider]
```

#### <a name="remarks"></a>Remarks

- Пароль, указанный в командной строке, должен быть списком паролей с разделителями-запятыми.

- Если указано более одного пароля, для выходного файла используется последний пароль. Если указан только один пароль или последний пароль `*` , пользователю будет предложено ввести пароль для выходного файла.

### <a name="-"></a>-?

Отображает список параметров.

```
certutil -?
certutil <name_of_parameter> -?
certutil -? -v
```

Где:

- **-?** Отображает полный список параметров

- **-`<name_of_parameter>` -?** Отображает содержимое справки для указанного параметра.

- **-?-v** отображает полный список параметров и параметров.

## <a name="options"></a>Параметры

В этом разделе определяются все параметры, которые вы можете указать, в зависимости от команды. Каждый параметр содержит сведения о том, какие параметры являются допустимыми для использования.

| Параметры | Описание |
| ------- | ----------- |
| -нуллсигн | Используйте хэш данных в качестве подписи. |
| -f | Принудительная перезапись. |
| -enterprise | Используйте хранилище сертификатов реестра для локального компьютера. |
| пользователь | Используйте ключи HKEY_CURRENT_USER или хранилище сертификатов. |
| -GroupPolicy | Используйте хранилище сертификатов групповой политики. |
| -UT | Отображение пользовательских шаблонов. |
| -MT | Отображение шаблонов компьютеров. |
| — Юникод | Запись перенаправленных выходных данных в Юникоде. |
| -Уникодетекст | Запись выходного файла в Юникоде. |
| -GMT | Отображение времени по ГРИНВИЧу. |
| -секунд | Отображение времени с использованием секунд и миллисекунд. |
| — без уведомления | Используйте `silent` флаг, чтобы получить контекст шифрования. |
| -Split | Разделите внедренные элементы ASN. 1 и сохраните их в файлах. |
| -v | Предоставление более подробных (подробных) сведений. |
| -privateKey | Отображение данных пароля и закрытого ключа. |
| -закрепить ПИН-код | Закрепление смарт-карты. |
| -урлфетч | Извлечение и проверка сертификатов AIA и CDP. |
| -config Мачине\канаме | Центр сертификации и строка имени компьютера. |
| -полицисервер Урлорид | URL-адрес или идентификатор сервера политики. Для выбора U/I используйте `-policyserver` . Для всех серверов политики используйте`-policyserver *`|
| — Анонимный | Используйте анонимные учетные данные SSL. |
| — Kerberos | Используйте учетные данные Kerberos SSL. |
| -clientcertificate Клиентцертид | Используйте учетные данные SSL сертификата X. 509. Для выбора U/I используйте `-clientcertificate` . |
| -username имя_пользователя | Использовать именованную учетную запись для SSL-учетных данных. Для выбора U/I используйте `-username` . |
| -CERT certID | Сертификат подписи. |
| -DC DCName | Нацеливание на конкретный контроллер домена. |
| — ограничить RestrictionList | Список ограничений с разделителями-запятыми. Каждое ограничение состоит из имени столбца, реляционного оператора и постоянного целого числа, строки или даты. Одному имени столбца может предшествовать знак плюс или минус, чтобы указать порядок сортировки. Например, `requestID = 47`, `+requestername >= a, requestername` или `-requestername > DOMAIN, Disposition = 21`. |
| -out колумнлист | Список столбцов с разделителями-запятыми. |
| -p пароль | Пароль |
| -протектто Самнамеандсидлист | Список имен SAM, разделенных запятыми/SID. |
| — Поставщик CSP | Поставщик |
| -t время ожидания | Время ожидания выборки URL-адреса в миллисекундах. |
| -симкэйалг симметриккэйалгорисм [, keylength] | Имя алгоритма симметричного ключа с необязательной длиной ключа. Например: `AES,128` или `3DES`. |

### <a name="additional-references"></a>Дополнительные ссылки

Дополнительные примеры использования этой команды см. в разделе.

- [Службы сертификатов Active Directory (AD CS)](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740(v=ws.11))

- [Задачи Certutil для управления сертификатами](/previous-versions/orphan-topics/ws.10/cc772898(v=ws.10))

- [Команда certutil](certutil.md)