---
title: Always On удаленного доступа Обзор миграции VPN
description: Always On VPN устраняет предыдущие промежутки между VPN-подключениями Windows и DirectAccess, а также переход с DirectAccess на Always On VPN.
manager: dougkim
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: lizross
author: eross-msft
ms.date: 05/29/2018
ms.openlocfilehash: fcc04dcb9c76a2e25d768de18738078f425f2c76
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953750"
---
# <a name="overview-of-the-directaccess-to-always-on-vpn-migration"></a>Общие сведения о переносе DirectAccess в постоянно подключенный VPN-профиль

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10

&#187; [ **Далее:** планирование DirectAccess для Always on миграции VPN](da-always-on-migration-planning.md)

В предыдущих версиях архитектуры Windows VPN ограничения платформы затрудняют предоставление критически важных функций, необходимых для замены DirectAccess, например автоматических подключений, инициированных перед входом пользователей. В Always On VPN, однако, были устранены большинство этих ограничений или расширены функции VPN, помимо возможностей DirectAccess. Always On VPN устраняет предыдущие промежутки между VPN-подключениями Windows и DirectAccess.

Процесс миграции VPN "DirectAccess — Always On" состоит из четырех основных компонентов и процессов высокого уровня:


1.  **Спланируйте Always Onную миграцию VPN.** Планирование помогает указать целевые клиенты для разделения этапа пользователя, а также инфраструктуры и функциональности.

    1.  [!INCLUDE [build-migration-rings-shortdesc-include](../includes/build-migration-rings-shortdesc-include.md)]

    2.  [!INCLUDE [review-feature-mapping-shortdesc-include](../includes/review-feature-mapping-shortdesc-include.md)]

    3.  [!INCLUDE [review-the-enhancements-shortdesc-include](../includes/review-the-enhancements-shortdesc-include.md)]

    4.  [!INCLUDE [review-the-technology-overview-shortdesc-include](../includes/review-the-technology-overview-shortdesc-include.md)]

2.  **Развертывание параллельной инфраструктуры VPN.** Определив этапы миграции и компоненты, которые необходимо включить в развертывание, можно развернуть Always On инфраструктуру VPN параллельно с существующей инфраструктурой DirectAccess.

3.  **Развертывание сертификатов и конфигурации на клиентах.**  Когда инфраструктура VPN будет готова, вы создадите и опубликуете необходимые сертификаты для клиента. Когда клиенты получили сертификаты, вы развертываете скрипт настройки VPN_Profile.ps1. Кроме того, для настройки VPN-клиента можно использовать Intune. Чтобы отслеживать успешные развертывания конфигурации VPN, используйте Configuration Manager или Microsoft Intune конечной точки Майкрософт.

4.  **Удаление и списание.** После переноса всех участников из DirectAccess следует правильно списать среду.

    1.  [!INCLUDE [remove-da-from-client-shortdesc-include](../includes/remove-da-from-client-shortdesc-include.md)]

    2.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]


## <a name="directaccess-deployment-scenario"></a>Сценарий развертывания DirectAccess

В этом сценарии развертывания используется простой сценарий развертывания DirectAccess в качестве отправной точки для перехода, представленного этим руководством. Вам не нужно сопоставлять этот сценарий развертывания перед миграцией на Always On VPN, но во многих организациях эта простая настройка является точным представлением текущего развертывания DirectAccess. В таблице ниже приведен список основных функций для этой настройки.

Существует множество сценариев и вариантов развертывания DirectAccess, поэтому реализация, скорее всего, будет отличаться от описанной здесь. Если это так, обратитесь к статье [Сопоставление функций между DirectAccess и Always on VPN](../vpn/vpn-map-da.md) , чтобы определить Always on сопоставление набора функций VPN для текущих добавлений, а затем добавьте эти функции в конфигурацию. Кроме того, вы можете ознакомиться с [улучшенными Always on VPN](../vpn/always-on-vpn/always-on-vpn-enhancements.md) , чтобы добавить параметры в Always on развертывание VPN.

>[!NOTE]
>Для устройств, не присоединенных к домену, существуют дополнительные соображения, например регистрация сертификатов. Дополнительные сведения см. в разделе [Always on развертывание VPN для Windows Server и Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md).

### <a name="deployment-scenario-feature-list"></a>Список функций сценария развертывания

| Функция DirectAccess | Типичный сценарий |
|-----|----|
| Сценарий развертывания                   | Развертывание полного DirectAccess для клиентского доступа и удаленного управления                                               |
| Сетевые адаптеры                      | 2                                                                                                              |
| Аутентификация пользователей                   | Учетные данные Active Directory                                                                                   |
| Использование сертификатов компьютеров             | да                                                                                                            |
| Группы безопасности                       | да                                                                                                            |
| Один сервер DirectAccess            | да                                                                                                            |
| Топология сети                      | Преобразование сетевых адресов (NAT) за граничным брандмауэром с двумя сетевыми адаптерами                            |
| Режим доступа                           | От конца к краю                                                                                                    |
| Туннелирование                             | Разделить туннель                                                                                                   |
| Проверка подлинности                        | Стандартная аутентификация инфраструктуры открытых ключей (PKI) с сертификатом компьютера плюс Kerberos (не Кербпрокси) |
| Протоколы                             | IP через HTTPS (IP-HTTPS)                                                                                       |
| Сервер сетевых расположений (NLS) — "Выкл." | да                                                                                                            |

## <a name="always-on-vpn-deployment-scenario"></a>Сценарий развертывания Always On VPN

В этом сценарии развертывания вы Сосредоточьтесь на переносе простой среды DirectAccess в простую Always Onную среду VPN, которая является решением для замены DirectAccess. В следующей таблице приведены функции, используемые в этом простом решении. Более подробные сведения о дополнительных усовершенствованиях Always On VPN-клиента см. в статье [усовершенствования Always on VPN](../vpn/always-on-vpn/always-on-vpn-enhancements.md).

### <a name="always-on-vpn-features-used-in-the-simple-environment"></a>Always On функции VPN, используемые в простой среде

| Функция VPN | Конфигурация сценария развертывания |
|-----|-----|
| Тип подключения | Собственная протокол IKE версии 2 (IKEv2) |
| Сетевые адаптеры   | 2        |
| Аутентификация пользователей  | Учетные данные Active Directory            |
| Использование сертификатов компьютеров        | да                          |
| Маршрутизация | Раздельное туннелирование |
| Разрешение имен | Список сведений об имени домена и суффикс службы доменных имен (DNS) |
| Активации | Обнаружение Always on и доверенной сети |
| Проверка подлинности  | Защищенный протокол расширенной проверки подлинности — безопасность транспортного уровня (PEAP-TLS) с сертификатами пользователей, защищенными доверенный платформенный модуль (TPM) |

## <a name="next-step"></a>Следующий шаг

[Запланируйте DirectAccess для Always on миграции VPN](da-always-on-migration-planning.md). Основная цель миграции заключается в том, чтобы пользователи поддерживали удаленное подключение к офису в течение всего процесса.

---