---
title: Планирование сервера политики сети в качестве RADIUS-сервера
description: В этом разделе содержатся сведения о планировании развертывания сервера политики сети RADIUS в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 2900dd2c-0f70-4f8d-9650-ed83d51d509a
ms.author: jgerend
author: JasonGerend
ms.date: 08/07/2020
ms.openlocfilehash: 4e7253094bcffdf12aae9d3de6df737097d3bafb
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101832083"
---
# <a name="plan-nps-as-a-radius-server"></a>Планирование сервера политики сети в качестве RADIUS-сервера

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

При развертывании сервера политики сети \( в \) качестве сервера протокол RADIUS (RADIUS) NPS выполняет проверку подлинности, авторизацию и учет для запросов на подключение к локальному домену и доменам, которые доверяют локальному домену. Эти рекомендации по планированию можно использовать для упрощения развертывания RADIUS.

Эти рекомендации по планированию не включают обстоятельства, в которых требуется развернуть NPS в качестве прокси-сервера RADIUS. При развертывании сервера политики сети в качестве прокси-сервера RADIUS сервер политики сети перенаправляет запросы на подключение к серверу, на котором выполняются службы NPS или другие серверы RADIUS в удаленных доменах, недоверенных доменах или в обоих случаях.

Перед развертыванием NPS в качестве сервера RADIUS в сети используйте следующие рекомендации по планированию развертывания.

- Спланируйте конфигурацию NPS.

- Спланируйте клиенты RADIUS.

- Спланируйте использование методов проверки подлинности.

- Спланируйте политики сети.

- Планирование учета NPS.

## <a name="plan-nps-configuration"></a>Планирование конфигурации NPS

Необходимо выбрать домен, членом которого является NPS. Для сред с несколькими доменами сервер политики сети может проверять подлинность учетных данных для учетных записей пользователей в домене, членом которого он является, и для всех доменов, которые доверяют локальному домену NPS. Чтобы разрешить NPS считывать свойства входящих звонков учетных записей пользователей в процессе авторизации, необходимо добавить учетную запись компьютера NPS в группу RAS и НПСС для каждого домена.

Определив принадлежность к домену NPS, сервер должен быть настроен для взаимодействия с клиентами RADIUS, также называемыми серверами сетевого доступа, с использованием протокола RADIUS. Кроме того, можно настроить типы событий, которые будут записываться в журнал событий, а также ввести описание для сервера.

### <a name="key-steps"></a>Основные шаги

Во время планирования конфигурации NPS можно выполнить следующие действия.

- Определите порты RADIUS, используемые NPS для получения RADIUS-сообщений от клиентов RADIUS. Порты по умолчанию — UDP-порты 1812 и 1645 для сообщений проверки подлинности RADIUS и порты 1813 и 1646 для RADIUS-сообщений учета.

- Если сервер политики сети настроен с несколькими сетевыми адаптерами, определите адаптеры, по которым должен быть разрешен трафик RADIUS.

- Определите типы событий, которые должны записываться NPS в журнал событий. Можно регистрировать отклоненные запросы проверки подлинности, успешные запросы проверки подлинности или запросы обоих типов.

- Определите, развертывается ли более одного сервера политики сети. Чтобы обеспечить отказоустойчивость при проверке подлинности и учете на основе RADIUS, используйте по меньшей мере два НПСС. Один сервер политики сети используется в качестве основного сервера RADIUS, а другой используется в качестве резервной копии. Затем каждый клиент RADIUS настраивается как в НПСС. Если основной сервер политики сети становится недоступным, клиенты RADIUS отправляют Access-Request сообщения на альтернативный сервер политики сети.

- Спланируйте сценарий, используемый для копирования одной конфигурации NPS в другие НПСС, чтобы сэкономить на административных издержках и предотвратить неправильное заданными сервера. NPS предоставляет команды Netsh, позволяющие копировать конфигурацию NPS или ее часть для импорта на другой сервер политики сети. Команды можно выполнять вручную в командной строке Netsh. Однако если вы сохраните последовательность команд в качестве скрипта, вы можете запустить сценарий позже, если вы решите изменить конфигурацию сервера.

## <a name="plan-radius-clients"></a>Планирование клиентов RADIUS

RADIUS-клиенты — это серверы сетевого доступа, такие как точки беспроводного доступа, серверы виртуальной частной сети (VPN), коммутаторы с поддержкой 802.1 X и серверы удаленного доступа. Прокси-серверы RADIUS, которые перенаправляют сообщения запроса на подключение на серверы RADIUS, также являются RADIUS-клиентами. Сервер политики сети поддерживает все серверы доступа к сети и прокси-серверы RADIUS, соответствующие протоколу RADIUS, как описано в RFC 2865, "Служба удаленного доступа к аутентификации (RADIUS)" и RFC 2866, "учет RADIUS".

>[!IMPORTANT]
>Клиенты доступа, такие как клиентские компьютеры, не являются клиентами RADIUS. RADIUS-клиенты являются только серверами доступа к сети и прокси-серверами, поддерживающими протокол RADIUS.

Кроме того, точки беспроводного доступа и коммутаторы должны поддерживать проверку подлинности 802.1 X. Если требуется развернуть EAP протокол расширенной проверки подлинности \( \) или защищенный протокол \( PEAP \) , точки доступа и коммутаторы должны поддерживать использование EAP.

Чтобы проверить базовое взаимодействие подключений PPP для точек беспроводного доступа, настройте точку доступа и клиент доступа для использования протокола проверки пароля (PAP). Используйте дополнительные протоколы проверки подлинности на основе PPP, такие как PEAP, до тех пор, пока не протестировали те, которые планируется использовать для сетевого доступа.

### <a name="key-steps"></a>Основные шаги

При планировании клиентов RADIUS можно выполнить следующие действия.

- Задокументируйте зависящие от поставщика атрибуты (VSA), которые необходимо настроить в NPS. Если для серверов доступа к сети требуются VSA, заполните данные VSA для последующего использования при настройке политик сети в NPS.

- Задокументируйте IP-адреса клиентов RADIUS и NPS, чтобы упростить настройку всех устройств. При развертывании клиентов RADIUS необходимо настроить для них использование протокола RADIUS с IP-адресом NPS, введенным в качестве сервера проверки подлинности. При настройке NPS для взаимодействия с клиентами RADIUS необходимо ввести IP-адреса клиентов RADIUS в оснастку NPS.

- Создайте общие секреты для конфигурации на клиентах RADIUS и в оснастке NPS. Необходимо настроить RADIUS-клиенты с помощью общего секрета или пароля, которые также будут входить в оснастку NPS при настройке клиентов RADIUS в NPS.

## <a name="plan-the-use-of-authentication-methods"></a>Планирование использования методов проверки подлинности

NPS поддерживает методы проверки подлинности на основе пароля и на основе сертификатов. Однако не все серверы доступа к сети поддерживают одни и те же методы проверки подлинности. В некоторых случаях может потребоваться развернуть другой метод проверки подлинности в зависимости от типа доступа к сети.

Например, может потребоваться развернуть как беспроводной, так и VPN-доступ для вашей организации, но использовать другой метод проверки подлинности для каждого типа доступа: EAP-TLS для VPN-подключений из-за надежной безопасности, предоставляемой протоколом EAP с защитой транспортного уровня (EAP-TLS) и PEAP-MS-CHAP v2 для беспроводных подключений 802.1 X.

Протокол PEAP с проверкой подлинности Microsoft Challenge (PEAP-MS-CHAP v2) обеспечивает функцию быстрого повторного подключения, специально предназначенную для использования с портативными компьютерами и другими беспроводными устройствами. Быстрое повторное подключение позволяет беспроводным клиентам перемещаться между точками беспроводного доступа в одной сети без повторной проверки подлинности каждый раз, когда они связываются с новой точкой доступа. Это обеспечивает лучшую работу для беспроводных пользователей и позволяет им перемещаться между точками доступа без необходимости повторного ввода учетных данных.
Из-за быстрого повторного подключения и безопасности, предоставляемой PEAP-MS-CHAP v2, протокол PEAP-MS-CHAP v2 является логическим выбором в качестве метода проверки подлинности для беспроводных подключений.

Для подключений VPN EAP-TLS — это метод проверки подлинности на основе сертификатов, обеспечивающий надежную безопасность, которая защищает сетевой трафик, даже если он передается через Интернет с домашних или мобильных компьютеров на VPN-серверы Организации.

### <a name="certificate-based-authentication-methods"></a>Методы проверки подлинности на основе сертификатов

Методы проверки подлинности на основе сертификатов обладают преимуществом обеспечения надежной безопасности; и у них больше сложностей при развертывании, чем методы проверки подлинности на основе пароля.

PEAP-MS-CHAP v2 и EAP-TLS — это методы проверки подлинности на основе сертификатов, но между ними существует множество различий и способов их развертывания.

### <a name="eap-tls"></a>Протокол EAP-TLS

EAP-TLS использует сертификаты для проверки подлинности клиента и сервера и требует развертывания инфраструктуры открытых ключей (PKI) в Организации. Развертывание PKI может быть сложной задачей и требует этапа планирования, который не зависит от планирования использования NPS в качестве сервера RADIUS.

При использовании EAP-TLS NPS регистрирует сертификат сервера в ЦС центра сертификации \( \) , и сертификат сохраняется на локальном компьютере в хранилище сертификатов. В процессе аутентификации проверка подлинности сервера происходит, когда сервер политики сети отправляет сертификат сервера клиенту доступа для подтверждения его подлинности клиенту доступа. Клиент Access проверяет различные свойства сертификата, чтобы определить, является ли сертификат допустимым и подходящим для использования при проверке подлинности сервера. Если сертификат сервера соответствует минимальным требованиям к сертификату сервера и выдается центром сертификации, которому доверяет клиент Access, то сервер политики сети успешно проходит проверку подлинности клиента.

Аналогичным образом проверка подлинности клиента происходит во время проверки подлинности, когда клиент отправляет свой сертификат клиента на сервер политики сети, чтобы доказать свою личность серверу политики сети. NPS проверяет сертификат, и если сертификат клиента соответствует минимальным требованиям к сертификату клиента и выдается центром сертификации, которому доверяет сервер политики сети, клиент Access успешно прошел проверку подлинности в NPS.

Хотя сертификат сервера должен храниться в хранилище сертификатов на сервере политики сети, сертификат клиента или пользователя может храниться либо в хранилище сертификатов на клиенте, либо на смарт-карте.

Чтобы этот процесс проверки подлинности завершился успешно, необходимо, чтобы все компьютеры имели сертификат ЦС организации в хранилище сертификатов доверенных корневых центров сертификации для локального компьютера и текущего пользователя.

### <a name="peap-ms-chap-v2"></a>Протокол PEAP-MS-CHAP v2

Протокол PEAP-MS-CHAP v2 использует сертификат для проверки подлинности сервера и учетных данных на основе пароля для проверки подлинности пользователя. Поскольку сертификаты используются только для проверки подлинности сервера, развертывать PKI для использования протокола PEAP-MS-CHAP v2 не требуется. При развертывании протокола PEAP-MS-CHAP v2 можно получить сертификат сервера для сервера политики сети одним из следующих двух способов:

- Вы можете установить службы Active Directory Certificate Services (AD CS), а затем автоматически зарегистрировать сертификаты в НПСС. При использовании этого метода необходимо также зарегистрировать сертификат ЦС на клиентских компьютерах, подключающихся к сети, чтобы они доверяли сертификату, выданному NPS.

- Сертификат сервера можно приобрести в общедоступном центре сертификации, например VeriSign. При использовании этого метода убедитесь, что выбран центр сертификации, который уже является доверенным для клиентских компьютеров. Чтобы определить, доверяет ли клиентские компьютеры центру сертификации, откройте оснастку "сертификаты" консоли управления (MMC) на клиентском компьютере, а затем просмотрите хранилище доверенных корневых центров сертификации для локального компьютера и для текущего пользователя. Если в этих хранилищах сертификатов есть сертификат из центра сертификации, клиентский компьютер доверяет центру сертификации и, таким образом, доверяет любому сертификату, выданному центром сертификации.

Во время проверки подлинности с помощью протокола PEAP-MS-CHAP v2 проверка подлинности сервера происходит, когда сервер политики сети отправляет свой сертификат сервера клиентскому компьютеру. Клиент Access проверяет различные свойства сертификата, чтобы определить, является ли сертификат допустимым и подходящим для использования при проверке подлинности сервера. Если сертификат сервера соответствует минимальным требованиям к сертификату сервера и выдается центром сертификации, которому доверяет клиент Access, то сервер политики сети успешно проходит проверку подлинности клиента.

Проверка подлинности пользователя происходит, когда пользователь пытается подключиться к сети с учетными данными на основе пароля и пытается войти в систему. Сервер политики сети получает учетные данные и выполняет проверку подлинности и авторизацию. Если пользователь прошел проверку подлинности и авторизован, а клиентский компьютер успешно прошел проверку подлинности NPS, запрос на подключение предоставляется.

### <a name="key-steps"></a>Основные шаги

Во время планирования использования методов проверки подлинности можно выполнить следующие действия.

- Выберите типы доступа к сети, которые планируется предложить, например "беспроводная сеть", "VPN", коммутатор с поддержкой 802.1 X и удаленный доступ.

- Определите метод проверки подлинности или методы, которые необходимо использовать для каждого типа доступа. Рекомендуется использовать методы проверки подлинности на основе сертификатов, обеспечивающие надежную защиту. Однако развертывание PKI может оказаться нецелесообразным, так что другие методы проверки подлинности могут обеспечить более высокий баланс того, что нужно для вашей сети.

- Если вы развертываете EAP-TLS, Спланируйте развертывание PKI. Сюда входит планирование шаблонов сертификатов, которые вы будете использовать для сертификатов сервера и клиентских компьютеров. Он также включает определение способа регистрации сертификатов для компьютеров-членов домена и пользователей, не являющихся членами домена, и определение необходимости использования смарт-карт.

- Если вы развертываете PEAP-MS-CHAP v2, определите, хотите ли вы установить AD CS для выгрузки сертификатов сервера в НПСС или требуется ли покупать сертификаты сервера из общедоступного центра сертификации, например VeriSign.

### <a name="plan-network-policies"></a>Планирование политик сети

Политики сети используются NPS для определения того, являются ли запросы на подключение, получаемые от RADIUS-клиентов, разрешены. Сервер политики сети также использует свойства входящих звонков учетной записи пользователя, чтобы выполнить определение авторизации.

Так как политики сети обрабатываются в том порядке, в котором они отображаются в оснастке NPS, запланируйте размещение наиболее ограниченных политик первыми в списке политик. Для каждого запроса на подключение сервер политики сети пытается сопоставить условия политики с свойствами запроса на подключение. NPS проверяет каждую сетевую политику по порядку, пока не найдет совпадение. Если совпадение не найдено, запрос на подключение отклоняется.

### <a name="key-steps"></a>Основные шаги

Во время планирования сетевых политик можно выполнить следующие действия.

- Определите предпочтительный порядок обработки сетевых политик NPS, от наиболее ограниченного до наименее ограниченного.

- Определение состояния политики. Состояние политики может иметь значение включено или отключено. Если политика включена, NPS оценивает политику при выполнении авторизации. Если политика не включена, она не оценивается.

- Определите тип политики. Необходимо определить, предназначена ли политика для предоставления доступа, когда условия политики сопоставляются запросом соединения или если политика предназначена для запрета доступа в случае, если условия политики соответствуют запросу соединения. Например, если вы хотите явно запретить беспроводный доступ к членам группы Windows, можно создать сетевую политику, определяющую группу, метод беспроводного подключения и параметр типа политики запретить доступ.

- Определите, должен ли NPS игнорировать свойства входящих звонков учетных записей пользователей, являющихся членами группы, на которой основана политика. Если этот параметр не включен, свойства удаленного доступа учетных записей пользователей переопределяют параметры, настроенные в политиках сети. Например, если настроена сетевая политика, предоставляющая доступ пользователю, но свойства входящих звонков учетной записи пользователя для этого пользователя задаются как запрещающие доступ, пользователю будет отказано в доступе. Но если включить параметр типа политики игнорировать свойства удаленного доступа учетной записи пользователя, то этому пользователю будет предоставлен доступ к сети.

- Определите, использует ли политика параметр источник политики. Этот параметр позволяет легко указать источник для всех запросов на доступ. Возможными источниками являются шлюз служб терминалов, сервер удаленного доступа (VPN или удаленный доступ), DHCP-сервер, точка беспроводного доступа и сервер центра регистрации работоспособности. Кроме того, можно указать источник, зависящий от поставщика.

- Определите условия, которые должны быть сопоставлены, чтобы политика сети была применена.

- Определите параметры, применяемые при совпадении условий сетевой политики с помощью запроса на подключение.

- Определите, нужно ли использовать, изменить или удалить политики сети по умолчанию.

## <a name="plan-nps-accounting"></a>Планирование учета NPS

NPS предоставляет возможность регистрировать данные учета RADIUS, такие как запросы проверки подлинности и учета пользователей, в трех форматах: формат IAS, формат, совместимый с базой данных, а также ведение журнала Microsoft SQL Server.

Формат IAS и формат, совместимый с базой данных, создают файлы журналов на локальном сервере политики сети в формате текстового файла.

Ведение журнала SQL Server обеспечивает возможность входа в базу данных, совместимую с SQL Server 2000 или SQL Server 2005, расширение учета RADIUS для использования преимуществ ведения журнала в реляционной базе данных.

### <a name="key-steps"></a>Основные шаги

При планировании учета NPS можно выполнить следующие действия.

- Определите, нужно ли хранить данные учета NPS в файлах журналов или в базе данных SQL Server.

### <a name="nps-accounting-using-local-log-files"></a>Использование локального файла журнала для учета NPS

Запись запросов на проверку подлинности и учетных записей в файлах журнала используется главным образом для анализа подключения и выставления счетов, а также полезна в качестве средства для расследования в области безопасности, предоставляя способ отслеживания действий злоумышленника после атаки.

### <a name="key-steps"></a>Основные шаги

Во время планирования учета NPS с помощью локальных файлов журналов можно выполнить следующие действия.

- Определите формат текстового файла, который будет использоваться для файлов журналов NPS.

- Выберите тип сведений, которые необходимо заносить в журнал. Можно вести журнал запросов учета, запросов проверки подлинности и периодического состояния.

- Определите расположение жесткого диска, где будут храниться файлы журналов.

- Разработка решения для резервного копирования файлов журнала. Расположением на жестком диске, где хранятся файлы журналов, должно быть расположение, позволяющее легко создавать резервные копии данных. Кроме того, расположение жесткого диска должно быть защищено путем настройки списка управления доступом (ACL) для папки, в которой хранятся файлы журнала.

- Определите частоту создания новых файлов журналов. Если нужно, чтобы файлы журнала создавались на основе размера файла, Определите максимальный размер файла, разрешенный до создания нового файла журнала NPS.

- Определите, хотите ли вы, чтобы NPS удалил старые файлы журнала, если на жестком диске не хватает дискового пространства.

- Определите приложение или приложения, которые вы хотите использовать для просмотра данных учета и создания отчетов.

### <a name="nps-sql-server-logging"></a>Ведение журнала SQL Server NPS

Ведение журнала SQL Server NPS используется, когда требуется информация о состоянии сеанса, для создания отчетов и анализа данных, а также для централизации и упрощения управления данными учета.

NPS предоставляет возможность использовать SQL Server ведение журнала для записи запросов проверки подлинности пользователей и учетных записей, полученных от одного или нескольких серверов сетевого доступа к источнику данных на компьютере, на котором выполняется Microsoft SQL Server Desktop Engine \( MSDE 2000 \) или любая версия SQL Server более поздней, чем SQL Server 2000.

Данные учета передаются из NPS в формате XML в хранимую процедуру в базе данных, поддерживающую язык структурированных запросов \( SQL \) и XML \( SQLXML \) . Запись проверки подлинности и запросов учетных записей в базе данных, совместимой с XML SQL Server позволяет нескольким НПСС одному источнику данных.

### <a name="key-steps"></a>Основные шаги

При планировании учета NPS с помощью SQL Server ведения журнала NPS можно выполнить следующие действия.

- Определите, имеется ли у вас или другого члена вашей организации SQL Serverная Разработка реляционной базы данных 2000 или SQL Server 2005, и вы понимаете, как использовать эти продукты для создания, изменения, администрирования баз данных SQL Server и управления ими.

- Определите, установлена ли SQL Server на сервере политики сети или на удаленном компьютере.

- Создайте хранимую процедуру, которая будет использоваться в базе данных SQL Server, для обработки входящих XML-файлов, содержащих данные учета NPS.

- Создайте SQL Server структуру и последовательность репликации базы данных.

- Определите приложение или приложения, которые вы хотите использовать для просмотра данных учета и создания отчетов.

- Запланируйте использование серверов доступа к сети, которые передают атрибут класса во всех запросах учетных данных. Атрибут класса отправляется клиенту RADIUS в сообщении Access-Accept, и его можно использовать для корреляции Accounting-Requestных сообщений с сеансами проверки подлинности. Если атрибут класса отправляется сервером сетевого доступа в сообщениях запроса учета, его можно использовать для сопоставления записей учета и проверки подлинности. Сочетание атрибутов Unique-последовательный-номер, служба-перезагрузка-время и Server-Address должны быть уникальной идентификацией для каждой проверки подлинности, принимаемой сервером.

- Запланируйте использование серверов сетевого доступа, поддерживающих промежуточный учет.

- Запланируйте использование серверов доступа к сети, отправляющих сообщения о включении и отключении учетных записей.

- Запланируйте использование серверов доступа к сети, поддерживающих хранение и пересылку данных учета. Серверы доступа к сети, поддерживающие эту функцию, могут хранить данные учета, когда сервер сетевого доступа не может связаться с сервером политики сети. Когда NPS будет доступен, сервер доступа к сети перенаправляет сохраненные записи на сервер политики сети, обеспечивая повышенную надежность при учете на серверах доступа к сети, не предоставляющих эту функцию.

- Запланируйте всегда настраивать атрибут Acct-Interim-Interval в сетевых политиках. Атрибут Acct-Interim-Interval задает интервал (в секундах) между каждым промежуточным обновлением, которое отправляет сервер доступа к сети. В соответствии с RFC 2869 значение атрибута Acct-Interim-Interval не должно быть меньше 60 секунд или равно одной минуте и не должно быть меньше 600 секунд или 10 минут. Дополнительные сведения см. в RFC 2869, «расширения RADIUS».

- Убедитесь, что в НПСС включено ведение журнала периодического состояния.

