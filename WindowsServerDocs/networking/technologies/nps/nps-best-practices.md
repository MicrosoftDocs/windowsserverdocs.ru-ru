---
title: Передовые практики по работе с сервером политики сети
description: В этом разделе приводятся рекомендации по развертыванию и управлению сервером политики сети в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 90e544bd-e826-4093-8c3b-6a6fc2dfd1d6
ms.author: jgerend
author: JasonGerend
ms.date: 12/08/2020
ms.openlocfilehash: 6a9e5353dd553f8be4a32d116ad0ff3c5b2ecfeb
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101828203"
---
# <a name="network-policy-server-best-practices"></a>Передовые практики по работе с сервером политики сети

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

С помощью этого раздела вы узнаете о рекомендациях по развертыванию сервера политики сети и управлению им \( \) .

В следующих разделах приводятся рекомендации по различным аспектам развертывания NPS.

## <a name="accounting"></a>Учет

Ниже приведены рекомендации по ведению журнала NPS.

В NPS существует два типа учета, или ведение журнала:

- Ведение журнала событий для сервера политики сети. Ведение журнала событий можно использовать для записи событий NPS в системе и в журналах событий безопасности. Это используется в основном для аудита и устранения неполадок при попытках подключения.

- Ведение журнала запросов на проверку подлинности и учетных записей пользователей. Вы можете регистрировать запросы проверки подлинности и учета пользователей в файлах журнала в текстовом формате или в формате базы данных, а также записывать данные в хранимую процедуру в базе данных SQL Server 2000. Ведение журнала запросов используется в основном для анализа подключений и выставления счетов. оно также полезно в качестве средства для расследования безопасности, предоставляя метод отслеживания действий злоумышленника.

Чтобы наиболее эффективно использовать ведение журнала NPS, сделайте следующее:

- Сначала включите ведение \( журнала \) для записей проверки подлинности и учета. После определения того, что подходит для вашей среды, измените эти параметры.

- Убедитесь, что для ведения журнала событий настроена емкость, достаточная для обслуживания журналов.

- Регулярно создавайте резервные копии всех файлов журналов, так как они не могут быть созданы повторно при их повреждении или удалении.

- Используйте атрибут класса RADIUS, чтобы отследить использование и упростить идентификацию отдела или пользователя, за использование которого взимается плата. Хотя автоматически созданный атрибут класса уникален для каждого запроса, могут существовать повторяющиеся записи в случаях, когда ответ на сервер доступа теряется и запрос отсылается повторно. Чтобы точно контролировать использование, может потребоваться удалить дублирующиеся запросы из журналов.

- Если серверы доступа к сети и прокси-серверы RADIUS периодически отправляют вымышленные сообщения запросов на подключение в NPS для проверки того, что NPS находится в оперативном режиме, используйте параметр реестра **ping user-name** . Этот параметр настраивает NPS на автоматическую отклонять эти ложные запросы на подключение без их обработки. Кроме того, NPS не регистрирует транзакции, в которых используется вымышленное имя пользователя, в любом файле журнала, что упрощает интерпретацию журнала событий.

- Отключить перенаправление уведомлений NAS. Можно отключить перенаправление сообщений запуска и завершения с серверов доступа к сети (NAS) в группу удаленных серверов RADIUS, настроенную в NPS. Дополнительные сведения см. в разделе [Отключение пересылки уведомлений NAS](nps-disable-nas-notifications.md).

Дополнительные сведения см. в разделе [Настройка учета сервера политики сети](nps-accounting-configure.md).

- Чтобы обеспечить отработку отказа и избыточность с помощью ведения журнала SQL Server, поместите два компьютера, на которых выполняется SQL Server, в разные подсети. Используйте **Мастер создания публикаций** SQL Server, чтобы настроить репликацию базы данных между двумя серверами. Дополнительные сведения см. в разделе [SQL Server техническая документация](/sql/sql-server/) и [репликация SQL Server](/sql/relational-databases/replication/sql-server-replication).

## <a name="authentication"></a>Аутентификация

Ниже приведены рекомендации по проверке подлинности.

- Используйте методы проверки подлинности на основе сертификатов, такие как протокол \( PEAP \) и EAP протокол расширенной проверки подлинности \( \) для строгой проверки подлинности. Не используйте методы проверки подлинности только с помощью пароля, так как они уязвимы для различных атак и не являются безопасными. Для защищенной беспроводной сети рекомендуется использовать протокол PEAP \- MS \- CHAP v2, так как сервер политики сети подтверждает свою подлинность беспроводным клиентам, используя сертификат сервера, а пользователи подтверждают свою личность с помощью имени пользователя и пароля.  Дополнительные сведения об использовании NPS в развертывании беспроводных сетей см. в разделе [Deploy Password-Based 802.1 x аутентифицированный беспроводной доступ](../../core-network-guide/cncg/wireless/a-deploy-8021x-wireless-access.md).
- \( \) &reg; \( \) При использовании строгих методов проверки подлинности на основе сертификатов, таких как PEAP и EAP, необходимо развернуть собственный ЦС центра сертификации с помощью служб сертификатов Active Directory AD CS, для которого требуется использовать сертификат сервера в НПСС. Вы также можете использовать свой ЦС для регистрации сертификатов компьютеров и сертификатов пользователей. Дополнительные сведения о развертывании сертификатов сервера на серверах политики сети и сервере удаленного доступа см. в статье [Развертывание сертификатов сервера для беспроводных и беспроводных развертываний 802.1 x](../../core-network-guide/cncg/server-certs/deploy-server-certificates-for-802.1x-wired-and-wireless-deployments.md).

> [!IMPORTANT]
> Сервер политики сети (NPS) не поддерживает использование расширенных символов ASCII в паролях.

## <a name="client-computer-configuration"></a>Конфигурация клиентского компьютера

Ниже приведены рекомендации по настройке клиентского компьютера.

- Автоматически настройте все клиентские компьютеры 802.1 X в домене с помощью групповая политика. Дополнительные сведения см. в подразделе «Настройка политик беспроводной сети (IEEE 802,11)» раздела [развертывание беспроводного доступа](../../core-network-guide/cncg/wireless/e-wireless-access-deployment.md#bkmk_policies).

## <a name="installation-suggestions"></a>Варианты установки

Ниже приведены рекомендации по установке NPS.

- Перед установкой NPS установите и протестируйте все серверы доступа к сети с помощью локальных методов проверки подлинности, прежде чем настраивать их в качестве RADIUS-клиентов в NPS.

- После установки и настройки сервера политики сети сохраните конфигурацию с помощью команды Windows PowerShell [Export-нпсконфигуратион](/powershell/module/nps/export-npsconfiguration). Сохраните конфигурацию NPS с помощью этой команды при каждой перенастройке NPS.

>[!CAUTION]
>- Экспортированный файл конфигурации NPS содержит незашифрованные общие секреты для клиентов RADIUS и членов групп удаленных серверов RADIUS. Поэтому убедитесь, что файл сохранен в безопасном месте.
>- Процесс экспорта не включает параметры ведения журнала для Microsoft SQL Server в экспортированном файле. При импорте экспортированного файла на другой сервер политики сети необходимо вручную настроить SQL Server ведение журнала на новом сервере.

## <a name="performance-tuning-nps"></a>Настройка производительности NPS

Ниже приведены рекомендации по настройке производительности NPS.

- Чтобы оптимизировать время ожидания проверки подлинности и авторизации NPS и сократить сетевой трафик, установите NPS на контроллере домена.

- Если используются универсальные имена участников \( \) : UPN или windows Server 2008 и windows Server 2003, NPS использует глобальный каталог для проверки подлинности пользователей. Чтобы максимально сокращать время, необходимое для этого, установите NPS на сервере глобального каталога или на сервере, находящегося в той же подсети, что и сервер глобального каталога.

- Если вы настроили удаленные группы серверов RADIUS и, в политиках запросов на подключение NPS, снимите флажок **записывать данные учета на серверах в следующей удаленной группе RADIUS-серверов** . Эти группы все еще отправляются на сервер доступа к сети \( NAS \) Запуск и завершение уведомлений. Это создает ненужный сетевой трафик. Чтобы устранить этот трафик, отключите перенаправление уведомлений NAS для отдельных серверов в каждой группе удаленных серверов RADIUS, сняв флажок **Переслать сетевые запуск и остановка уведомлений на этот сервер** .

## <a name="using-nps-in-large-organizations"></a>Использование NPS в крупных организациях

Ниже приведены рекомендации по использованию NPS в крупных организациях.

- Если вы используете политики сети для ограничения доступа для всех групп, кроме определенных, создайте универсальную группу для всех пользователей, которым требуется разрешить доступ, а затем создайте политику сети, которая предоставит доступ для этой универсальной группы. Не помещайте всех пользователей непосредственно в универсальную группу, особенно если в сети имеется большое количество. Вместо этого создайте отдельные группы, являющиеся членами универсальной группы, и добавьте пользователей в эти группы.

- Используйте имя участника-пользователя, если это возможно. Пользователь может иметь то же имя участника-пользователя, независимо от членства в домене. Такой подход обеспечивает масштабируемость, которая может потребоваться в организациях с большим количеством доменов.

- Если сервер политики сети был установлен \( \) на компьютере, отличном от контроллера домена, и NPS получает большое количество запросов проверки подлинности в секунду, можно повысить производительность сервера политики сети, увеличив число одновременных проверок подлинности между сервером политики сети и контроллером домена. Дополнительные сведения см. в разделе [увеличение количества одновременных проверок подлинности, обрабатываемых NPS](./nps-concurrent-auth.md).

## <a name="security-issues"></a>Проблемы с безопасностью

Ниже приведены рекомендации по уменьшению проблем безопасности.

При удаленном администрировании сервера политики сети не следует отсылать конфиденциальные или конфиденциальные данные (например, общие секреты или пароли) по сети в виде открытого текста. Существует два рекомендуемых способа удаленного администрирования НПСС:

- Для доступа к NPS используйте службы удаленных рабочих столов. При использовании службы удаленных рабочих столов данные не передаются между клиентом и сервером. В клиент службы удаленных рабочих столов отправляется только пользовательский интерфейс сервера (например, образ консоли для операционной системы и консоль NPS), который называется подключение к удаленному рабочему столу в Windows &reg; 10. Клиент отправляет ввод с клавиатуры и мыши, который обрабатывается локально сервером, на котором включен службы удаленных рабочих столов. Когда службы удаленных рабочих столов пользователи входят в систему, они могут просматривать только свои индивидуальные сеансы клиентов, которые управляются сервером и не зависят друг от друга. Кроме того, подключение к удаленному рабочему столу обеспечивает 128-разрядное шифрование между клиентом и сервером.

- Используйте протокол IPsec для шифрования конфиденциальных данных. Протокол IPsec можно использовать для шифрования обмена данными между сервером политики сети и удаленным клиентским компьютером, который используется для администрирования сервера политики сети. Для удаленного администрирования сервера можно установить [средства удаленного администрирования сервера для Windows 10](https://www.microsoft.com/download/details.aspx?id=45520) на клиентском компьютере. После установки с помощью консоли управления (MMC) добавьте оснастку NPS в консоль.

>[!IMPORTANT]
>Средства удаленного администрирования сервера для Windows 10 можно установить только в полном выпуске Windows 10 профессиональная или Windows 10 Корпоративная.

Дополнительные сведения о NPS см. в разделе [сервер политики сети (NPS)](nps-top.md).
