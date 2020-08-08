---
title: Новые возможности защиты учетных данных
description: Безопасность Windows Server
ms.topic: article
ms.assetid: 1b0b5180-f65a-43ac-8ef3-66014116f297
author: gitmichiko
ms.author: michikos
manager: dongill
ms.date: 03/06/2017
ms.openlocfilehash: 9522988946fbf5aa060ff81ab7a54077f5ca28f4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948717"
---
# <a name="whats-new-in-credential-protection"></a>Новые возможности защиты учетных данных

## <a name="credential-guard-for-signed-in-user"></a>Credential Guard для пользователя, выполнившего вход

Начиная с Windows 10 версии 1507, Kerberos и NTLM используют безопасность на основе виртуализации для защиты секретов Kerberos & NTLM для сеанса входа пользователя, выполнившего вход.

Начиная с Windows 10 версии 1511, диспетчер учетных данных использует безопасность на основе виртуализации для защиты сохраненных учетных данных типа учетных данных домена. Учетные данные для входа и сохраненные учетные данные домена не будут переданы удаленному узлу с помощью удаленного рабочего стола. Credential Guard можно включить без блокировки UEFI.

Начиная с Windows 10, версия 1607 в режиме изолированного пользователя входит в состав Hyper-V, поэтому она больше не устанавливается отдельно для развертывания Credential Guard.

Дополнительные [сведения об Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard).


## <a name="remote-credential-guard-for-signed-in-user"></a>Удаленный Credential Guard для пользователя, выполнившего вход

Начиная с Windows 10, версия 1607 Remote Credential Guard защищает учетные данные пользователя, выполнившего вход, при использовании удаленный рабочий стол путем защиты секретов Kerberos и NTLM на клиентском устройстве. Чтобы удаленный узел оценил сетевые ресурсы в качестве пользователя, для запросов проверки подлинности требуется, чтобы клиентское устройство использовало секреты.

Начиная с Windows 10, версия 1703 Remote Credential Guard защищает предоставленные учетные данные пользователя при использовании удаленный рабочий стол.

Дополнительные [сведения об удаленном Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard).

## <a name="domain-protections"></a>Защита домена

Для защиты домена требуется домен Active Directory.

### <a name="domain-joined-device-support-for-authentication-using-public-key"></a>Поддержка устройства, присоединенного к домену, для проверки подлинности с помощью открытого ключа

Начиная с Windows 10 версии 1507 и Windows Server 2016, если устройство, присоединенное к домену, может зарегистрировать связанный открытый ключ с контроллером домена Windows Server 2016, устройство может пройти проверку подлинности с помощью открытого ключа, используя проверку подлинности Kerberos PKINIT на КОНТРОЛЛЕРе домена Windows Server 2016.

Начиная с Windows Server 2016, Кдкс поддерживает проверку подлинности с использованием доверия Kerberos Key.

Дополнительные [сведения о поддержке открытых ключей для устройств, присоединенных к домену, & доверительных отношений ключей Kerberos](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication).

### <a name="pkinit-freshness-extension-support"></a>Поддержка расширения PKINIT

Начиная с Windows 10, версии 1507 и Windows Server 2016, клиенты Kerberos будут пытаться получить свежее расширение PKInit для входа на основе открытых ключей.

Начиная с Windows Server 2016, Кдкс может поддерживать свежее расширение PKInit.  По умолчанию Кдкс не будет предоставлять свежее расширение PKInit.

Дополнительные [сведения о поддержке расширения PKINIT](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication).

### <a name="rolling-public-key-only-users-ntlm-secrets"></a>Пошаговые секреты NTLM пользователя только открытого ключа

Начиная с Windows Server 2016 режим работы домена (ДФЛ), контроллеры домена могут поддерживать откат секретов NTLM пользователя только открытого ключа. Эта функция недоступен в более низких Дфлс.

> [!WARNING]
> Добавление контроллера домена в домен с развернутыми секретами NTLM перед обновлением контроллера домена по крайней мере до 8 ноября обслуживание 2016 выполняет риск сбоя контроллера домена.

Конфигурация. для новых доменов эта функция включена по умолчанию. Для существующих доменов его необходимо настроить в центре администрирования Active Directory:

1. В центре администрирования Active Directory щелкните правой кнопкой мыши домен на левой панели и выберите пункт **Свойства**.

    ![Свойства домена](../media/Credentials-Protection-And-Management/domain-properties.png)

2. Установите флажок **включить истечение срока действия секретов NTLM при входе для пользователей, которым необходимо использовать Microsoft Passport или смарт-карту для интерактивного входа**в систему.

    ![Секреты NTLM срок действия автонакат](../media/Credentials-Protection-And-Management/autoroll-ntlm.png)

3. Нажмите кнопку **ОК**.

### <a name="allowing-network-ntlm-when-user-is-restricted-to-specific-domain-joined-devices"></a>Разрешение сетевой NTLM, если пользователь ограничен конкретными устройствами, присоединенными к домену

Начиная с Windows Server 2016 режим работы домена (ДФЛ), контроллеры домена могут поддерживать сетевую NTLM, если пользователь ограничен конкретными устройствами, присоединенными к домену. Эта функция недоступна в более низких Дфлс.

Конфигурация: в политике проверки подлинности щелкните **Разрешить проверку подлинности сети NTLM, если пользователь ограничен выбранными устройствами**.

Дополнительные [сведения о политиках проверки подлинности](https://technet.microsoft.com/windows-server-docs/security/credentials-protection-and-management/authentication-policies-and-authentication-policy-silos).
