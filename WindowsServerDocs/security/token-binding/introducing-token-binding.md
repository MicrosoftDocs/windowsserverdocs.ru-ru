---
title: Введение в привязку токенов
ms.topic: article
ms.assetid: 4623a48c-cefd-4a27-9173-2af58ac212f2
author: justinha
ms.author: Justinha
ms.date: 11/09/2016
ms.openlocfilehash: 08042ef376587c1e3370c07bf6c77b07f7aedc1f
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078521"
---
# <a name="introducing-token-binding"></a>Введение в привязку токенов

>Область применения: Windows Server 2016 и Windows 10

Протокол привязки токенов позволяет приложениям и службам криптографически привязывать свои маркеры безопасности к уровню TLS для устранения атак с кражой и воспроизведением маркеров.
Долгосрочные, однозначно идентифицируемые привязки TLS [RFC5246] могут охватывать несколько сеансов TLS и соединений.

Поддержка версий:

- Windows 10, версия 1507 — отключено по умолчанию
    - Добавлен протокол привязки маркеров [[черновик-IETF-токбинд-Protocol-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - WinInet & HTTP.SYS поддержку привязки маркеров по протоколу HTTP [[черновик-IETF-токбинд-HTTPS-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/01/)
- Windows 10, версии 1511 и 1607 и Windows Server 2016 — включено по умолчанию
    - Протокол привязки токена обновлен [[черновик-IETF-токбинд-Protocol-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - Расширение TLS для согласования привязки токена Добавлено [[черновик-Попов-токбинд-переговоры-00]](https://tools.ietf.org/html/draft-popov-tokbind-negotiation-00)
    - WinInet & HTTP.SYS поддержка привязки маркера по протоколу HTTP updated [[черновик-IETF-токбинд-HTTPS-02]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/02/)
- Windows 10, версия 1507 с обслуживанием Update [KB4034668](https://support.microsoft.com/kb/KB4034668), Windows 10, версия 1511 с обслуживанием Update [KB4034660](https://support.microsoft.com/kb/KB4034660), windows 10, версия 1607 и Windows Server 2016 с обслуживанием Update [KB4034658](https://support.microsoft.com/kb/KB4034658) поддержка протокола привязки маркеров версия 0,10 — включено по умолчанию
    - Протокол привязки токена обновлен [[черновик — IETF-токбинд-Protocol-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - Добавлено расширение TLS для согласования привязки маркеров [[черновик-IETF-токбинд-переговоры-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet & HTTP.SYS поддержка привязки маркера по протоколу HTTP updated [[черновик-IETF-токбинд-HTTPS-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
- Windows 10, версия 1703 поддерживает протокол привязки маркеров версии 0,10 — по умолчанию
    - Протокол привязки токена обновлен [[черновик — IETF-токбинд-Protocol-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - Добавлено расширение TLS для согласования привязки маркеров [[черновик-IETF-токбинд-переговоры-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet & HTTP.SYS поддержка привязки маркера по протоколу HTTP updated [[черновик-IETF-токбинд-HTTPS-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
    - Устройства Windows с включенной безопасностью на основе виртуализации будут поддерживать ключи привязки маркеров в защищенной среде, изолированной от работающей операционной системы.

Сведения о поддержке ASP .NET можно найти в [источнике ссылки на .NET Framework](https://referencesource.microsoft.com/#System.Web/ITlsTokenBindingInfo.cs,4a5e5668f5c31170).

Дополнительные сведения о .NET Framework см. в следующих разделах:

- [Улучшения работы с сетью](https://blogs.msdn.microsoft.com/dotnet/2015/11/30/net-framework-4-6-1-is-now-available/#networking)

- [Класс .NET Токенбиндинг](/dotnet/api/system.security.authentication.extendedprotection.tokenbinding?view=netframework-4.8)