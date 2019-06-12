---
title: Настройка Kerberos для IP-адреса
description: Поддержка аутентификации Kerberos для имен участников-служб на основе IP-адресов
ms.openlocfilehash: 30741f7a0f1978fcaa6ac83c98a54c07e1ef25c5
ms.sourcegitcommit: c6acac3622e5d34714ca5c569805931681f98779
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/30/2019
ms.locfileid: "66391525"
---
# <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Клиенты Kerberos разрешить hostnames адреса IPv4 и IPv6 в имена участника-службы (SPN)

>Область применения. Windows Server (полугодовой канал), Windows Server 2016

Начиная с Windows 10 версии 1507 и Windows Server 2016, клиенты Kerberos можно настроить для поддержки IPv4 и IPv6 имена узлов в имена участников-служб.

По умолчанию Windows не будет пытаться проверки подлинности Kerberos для узла, если имя узла является IP-адресом. Он вернется на другие протоколы аутентификации, например NTLM. Тем не менее иногда приложения являются явно задано использование IP-адреса, который означает, что приложение будет вернуться к NTLM и не использовать Kerberos. Это может вызвать проблемы совместимости, поскольку перемещение сред для отключения NTLM.

Чтобы снизить влияние отключения NTLM новая возможность появилась, позволяющая администраторам использовать IP-адреса в качестве имен узлов в имена участников-служб. Эта возможность поддерживается на клиентском компьютере через значение раздела реестра.

```cmd
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters" /v TryIPSPN /t REG_DWORD /d 1 /f
```

Чтобы настроить поддержку для имен узлов IP адрес в имена участников-служб, создайте запись TryIPSPN. Эта запись не существует в реестре по умолчанию. После создания этой записи измените значение DWORD на 1. Это значение реестра необходимо установить на каждый клиентский компьютер, которому требуется доступ к ресурсам, защищенного протоколом Kerberos по IP-адресу.

## <a name="configuring-a-service-principal-name-as-ip-address"></a>Настройка имени участника-службы в качестве IP-адрес

Имя участника-службы — это уникальный идентификатор, используемый при проверке подлинности Kerberos для идентификации службы в сети. Имя SPN состоит из службы, имя узла и при необходимости порт в форме `service/hostname[:port]` например `host/fs.contoso.com`. Windows будут регистрироваться несколько имен участников-служб с объектом компьютера, если компьютер присоединен к Active Directory.

IP-адресов не используются обычно вместо имен узлов, так как IP-адреса часто являются временными. Это может привести к конфликты и ошибки проверки подлинности, как Арендованные адреса истекает и обновления. Поэтому регистрация имени участника службы на основе адреса IP-адрес создается вручную и должен использоваться только когда невозможно переключиться на основе DNS имя узла.

Рекомендуется использовать [Setspn.exe](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)) средство. Обратите внимание на то, что имя SPN можно зарегистрировать только для одной учетной записи в Active Directory одновременно, рекомендуется наличие аренды статического IP-адресов при использовании DHCP.

```
Setspn -s <service>/ip.address> <domain-user-account>  
```

Пример.

```
Setspn -s host/192.168.1.1 server01
```