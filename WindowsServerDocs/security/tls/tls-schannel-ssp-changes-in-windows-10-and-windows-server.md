---
title: TLS (поставщик общих служб Schannel)
ms.topic: article
ms.assetid: ebd3c40c-b4c0-4f6d-a00c-f90eda4691df
manager: alanth
author: justinha
ms.date: 05/16/2018
ms.openlocfilehash: 92a61452d3c22c34bb3251ee2668679068f3a2ad
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989490"
---
# <a name="tls-schannel-ssp-changes-in-windows-10-and-windows-server-2016"></a>Изменения протокола TLS (Schannel SSP) в Windows 10 и Windows Server 2016

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016 и Windows 10

## <a name="cipher-suite-changes"></a>Изменения в наборе шифров

В Windows 10, версии 1511 и Windows Server 2016 добавлена поддержка настройки порядка комплектов шифров с помощью управления мобильными устройствами (MDM).

Изменения порядка приоритетов для набора шифров см. в разделе комплекты [шифров в SChannel](/windows/win32/secauthn/cipher-suites-in-schannel).

Добавлена поддержка следующих комплектов шифров:

- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (RFC 5289) в Windows 10, версия 1507 и Windows Server 2016
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (RFC 5289) в Windows 10, версия 1507 и Windows Server 2016

DisabledByDefault изменения для следующих комплектов шифров:

- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256 (RFC 5246) в Windows 10, версия 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256 (RFC 5246) в Windows 10, версия 1703
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA (RFC 5246) в Windows 10, версия 1703
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA (RFC 5246) в Windows 10, версия 1703
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA (RFC 5246) в Windows 10, версия 1703
- TLS_RSA_WITH_RC4_128_SHA в Windows 10, версия 1709
- TLS_RSA_WITH_RC4_128_MD5 в Windows 10, версия 1709

Начиная с Windows 10 версии 1507 и Windows Server 2016 сертификаты SHA 512 поддерживаются по умолчанию.

### <a name="rsa-key-changes"></a>Изменения ключей RSA

Windows 10, версии 1507 и Windows Server 2016 добавляют параметры конфигурации реестра для размеров ключей RSA клиента.

Дополнительные сведения см. в разделе [кэйексчанжеалгорисм-Client RSA Key sizes](tls-registry-settings.md#keyexchangealgorithm---client-rsa-key-sizes).

### <a name="diffie-hellman-key-changes"></a>Изменения ключей Диффи-Хелмана

Windows 10, версия 1507 и Windows Server 2016 добавляют параметры конфигурации реестра для размеров ключей Диффи-Хелмана.

Дополнительные сведения см. в разделе [кэйексчанжеалгорисм-diff Диффи-Хелмана Key sizes](tls-registry-settings.md#keyexchangealgorithm---diffie-hellman-key-sizes).

### <a name="sch_use_strong_crypto-option-changes"></a>Изменения параметров SCH_USE_STRONG_CRYPTO

В Windows 10 версии 1507 и Windows Server 2016 [SCH_USE_STRONG_CRYPTO](/windows/win32/api/schannel/ns-schannel-schannel_cred) параметр теперь отключает неопределенные шифры null, MD5, DES и Export.

## <a name="elliptical-curve-changes"></a>Изменения эллиптической кривой

Windows 10, версия 1507 и Windows Server 2016 добавьте групповая политика конфигурацию для эллиптических кривых в разделе Конфигурация компьютера > административные шаблоны > Network > параметры конфигурации SSL.
Список порядка кривых ECC определяет порядок, в котором эллиптические кривые являются предпочтительными, а также поддерживает поддерживаемые кривые, которые не включены.

Добавлена поддержка следующих эллиптических кривых:

- BrainpoolP256r1 (RFC 7027) в Windows 10, версия 1507 и Windows Server 2016
- BrainpoolP384r1 (RFC 7027) в Windows 10, версия 1507 и Windows Server 2016
- BrainpoolP512r1 (RFC 7027) в Windows 10, версия 1507 и Windows Server 2016
- Curve25519 (RFC черновик-IETF-TLS-Curve25519) в Windows 10, версия 1607 и Windows Server 2016

## <a name="dispatch-level-support-for-sealmessage--unsealmessage"></a>Поддержка уровня диспетчеризации для Сеалмессаже & Унсеалмессаже

Windows 10, версия 1507 и Windows Server 2016 добавляют поддержку Сеалмессаже/Унсеалмессаже на уровне диспетчеризации.

## <a name="dtls-12"></a>DTLS 1,2

Windows 10, версия 1607 и Windows Server 2016 добавлена поддержка DTLS 1,2 (RFC 6347).

## <a name="httpsys-thread-pool"></a>Пул потоков HTTP.SYS

Windows 10, версия 1607 и Windows Server 2016 добавляют конфигурацию реестра для размера пула потоков, используемого для обработки подтверждений TLS для HTTP.SYS.

Путь реестра:

хклм\систем\куррентконтролсет\контрол\лса

Чтобы указать максимальный размер пула потоков на ядро ЦП, создайте запись **максасинкворкерсреадсперкпу** .
Эта запись не существует в реестре по умолчанию.
После создания записи измените значение DWORD на нужный размер.
Если этот параметр не настроен, максимальное число потоков на ядро ЦП составляет 2.

## <a name="next-protocol-negotiation-npn-support"></a>Поддержка согласования следующего протокола (НПН)

Начиная с Windows 10 версии 1703, следующее согласование протокола (НПН) было удалено и больше не поддерживается.

## <a name="pre-shared-key-psk"></a>Предварительный общий ключ (PSK)

В Windows 10, версии 1607 и Windows Server 2016 добавлена поддержка алгоритма обмена ключами PSK (RFC 4279).

Добавлена поддержка следующих наборов шифров PSK:

- TLS_PSK_WITH_AES_128_CBC_SHA256 (RFC 5487) в Windows 10, версия 1607 и Windows Server 2016
- TLS_PSK_WITH_AES_256_CBC_SHA384 (RFC 5487) в Windows 10, версия 1607 и Windows Server 2016
- TLS_PSK_WITH_NULL_SHA256 (RFC 5487) в Windows 10, версия 1607 и Windows Server 2016
- TLS_PSK_WITH_NULL_SHA384 (RFC 5487) в Windows 10, версия 1607 и Windows Server 2016
- TLS_PSK_WITH_AES_128_GCM_SHA256 (RFC 5487) в Windows 10, версия 1607 и Windows Server 2016
- TLS_PSK_WITH_AES_256_GCM_SHA384 (RFC 5487) в Windows 10, версия 1607 и Windows Server 2016

## <a name="session-resumption-without-server-side-state-server-side-performance-improvements"></a>Возобновление сеанса без серверного состояния повышение производительности на стороне сервера

Windows 10 версии 1507 и Windows Server 2016 обеспечивают 30% дополнительных возобновлениях сеансов в секунду с билетами сеанса по сравнению с Windows Server 2012.

## <a name="session-hash-and-extended-master-secret-extension"></a>Хэш сеанса и расширенное главное расширение секрета

Windows 10, версия 1507 и Windows Server 2016 добавить поддержку RFC 7627: хэш сеанса протокола TLS и расширенное основное расширение секрета.

Из-за этого изменения в Windows 10 и Windows Server 2016 требуются сторонние обновления [поставщика SSL](/windows/win32/seccng/cng-ssl-provider-functions) для поддержки NCRYPT_SSL_INTERFACE_VERSION_3 и описание этого нового интерфейса.


## <a name="ssl-support"></a>Поддержка SSL

Начиная с Windows 10, версии 1607 и Windows Server 2016, клиент TLS и SSL-сервер 3,0 по умолчанию отключены.
Это означает, что если приложение или служба не запрашивают SSL 3,0 через SSPI, клиент никогда не будет предлагать или принимать SSL 3,0, а сервер никогда не будет выбирать SSL 3,0.

Начиная с Windows 10 версии 1607 и Windows Server 2016, протокол SSL 2,0 был удален и больше не поддерживается.

## <a name="changes-to-windows-tls-adherence-to-tls-12-requirements-for-connections-with-non-compliant-tls-clients"></a>Изменения, предъявляемые Windows TLS к требованиям TLS 1,2 для подключений с несовместимыми клиентами TLS

В TLS 1,2 клиент использует [расширение "signature_algorithms"](https://tools.ietf.org/html/rfc5246#section-7.4.1.4.1) , чтобы указать серверу, какие пары сигнатур и хэш-алгоритма могут использоваться в цифровых подписях (например, сертификаты сервера и обмен ключами сервера).
В стандарте TLS 1,2 RFC также требуется, чтобы сообщение сертификата сервера учитывало расширение "signature_algorithms":

"Если клиент предоставил расширение" signature_algorithms ", все сертификаты, предоставленные сервером, должны быть подписаны парой алгоритмов хэширования и подписи, которая отображается в этом расширении."

На практике некоторые сторонние клиенты TLS не соответствуют стандарту RFC 1,2 и не включают все пары сигнатур и хэш-алгоритма, которые они хотят принять в расширении "signature_algorithms", или вообще не указывайте расширение (Последнее указывает серверу, что клиент поддерживает только SHA1 с RSA, DSA или ECDSA).

Сервер TLS часто имеет только один сертификат, настроенный на конечную точку. Это означает, что сервер не всегда может предоставить сертификат, соответствующий требованиям клиента.

До Windows 10 и Windows Server 2016 стек Windows TLS строго придерживается требований спецификации TLS 1,2, что приводит к сбоям соединения с несовместимыми клиентами TLS и проблемам взаимодействия.
В Windows 10 и Windows Server 2016 ограничения неограниченны, и сервер может отправить сертификат, который не соответствует стандарту TLS 1,2, если это параметр сервера.
После этого клиент может продолжить работу или завершить подтверждение.

При проверке сертификатов сервера и клиента стек Windows TLS строго соответствует спецификации протокола TLS 1,2 и разрешает только согласованные алгоритмы подписи и хэширования в сертификатах сервера и клиента.