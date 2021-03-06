---
title: Group Managed Service Accounts Overview
description: Сведения о групповой управляемой учетной записи службы. в частности, это практические приложения, изменения в реализации корпорации Майкрософт, требования к оборудованию и программному обеспечению.
ms.topic: article
ms.assetid: cef0693c-f861-48a7-a1c0-8d1bc06143ce
ms.author: jgerend
author: JasonGerend
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: 70ba26e94dbd3e9ad111dfb5cac94530fa4a2a6d
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101827767"
---
# <a name="group-managed-service-accounts-overview"></a>Group Managed Service Accounts Overview

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

В этом разделе для ИТ Professional представлена групповая управляемая учетная запись службы с описанием практических приложений, изменений в реализации Майкрософт и требований к оборудованию и программному обеспечению.


## <a name="feature-description"></a><a name="BKMK_OVER"></a>Описание функции
Автономная управляемая учетная запись службы (sMSA) — это управляемая Доменная учетная запись, которая обеспечивает автоматическое управление паролями, упрощенное управление именами участников-служб и возможность делегирования управления другим администраторам. Такой тип управляемой учетной записи службы реализован в ОС Windows Server 2008 R2 и Windows 7.

Групповая управляемая учетная запись службы (gMSA) предоставляет те же функции в домене, но также расширяет эту функциональность на нескольких серверах. При подключении к службе, размещенной в ферме серверов, такой как решение с балансировкой сетевой нагрузки, протоколы проверки подлинности, поддерживающие взаимную проверку подлинности, должны использовать один и тот же субъект для всех экземпляров служб. Если в качестве субъектов-служб используется gMSA, операционная система Windows управляет паролем для учетной записи, а не полагается на администратора для управления паролем.

Служба распространения ключей (Майкрософт) \(kdssvc.dll\) предоставляет механизм для безопасного получения последнего ключа или определенного ключа с идентификатором ключа для учетной записи Active Directory. Служба распространения ключей использует общий секрет для создания ключей учетной записи. Эти ключи периодически изменяются. Для gMSA контроллер домена определяет пароль для ключа, предоставляемого службами распространения ключей, в дополнение к другим атрибутам gMSA.  Узлы-члены могут получить текущие и предшествующие значения пароля, обратившись к контроллеру домена.

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Практическое применение
Gmsa предоставляют единое решение идентификации для служб, работающих на ферме серверов, или для систем, использующих сетевые Load Balancer. Предоставляя решение gMSA, можно настроить службы для нового субъекта gMSA, а управление паролями будет обрабатываться Windows.

Использование gMSA, служб или администраторов служб не требует управления синхронизацией паролей между экземплярами службы. GMSA поддерживает узлы, которые хранятся в автономном режиме в течение расширенного периода времени, а также Управление узлами участников для всех экземпляров службы. Это означает, что можно развертывать ферму серверов, поддерживающую единое удостоверение, по которому существующие клиентские компьютеры могут проверять подлинность без идентификации экземпляра службы, к которому они подключаются.

Отказоустойчивые кластеры не поддерживают групповые управляемые учетные записи служб. При этом групповую или автономную учетную запись службы могут использовать службы, работающие поверх службы кластеров и представляющие собой службу Windows, пул приложений или назначенную задачу либо поддерживающие такие учетные записи изначально.

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Требования к программному обеспечению

\-Для выполнения команд Windows PowerShell, которые используются для администрирования gmsa, требуется битовая архитектура 64.

Управляемая учетная запись службы зависит от поддерживаемых протоколом Kerberos типов шифрования. Если проверка подлинности клиентского компьютера на сервере выполняется с помощью Kerberos, контроллер домена создает билет службы Kerberos, защищенный шифром, который поддерживают и контроллер, и сервер. Контроллер домена использует атрибут msDS суппортеденкриптионтипес учетной записи, \- чтобы определить, какое шифрование поддерживает сервер, и, если атрибут отсутствует, предполагается, что клиентский компьютер не поддерживает более надежные типы шифрования. Если узел настроен для поддержки алгоритма RC4, проверка подлинности всегда завершится ошибкой. Поэтому стандарт AES всегда должен быть явным образом настроен для поддержки MSA.

> [!NOTE]
> Начиная с версии Windows Server 2008 R2, стандарт DES отключен по умолчанию. Дополнительные сведения о поддерживаемых типах шифрования см. в статье [Изменения в проверке подлинности Kerberos](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560670(v=ws.10)).

Gmsa не применимы к операционным системам Windows до Windows Server 2012.

## <a name="server-manager-information"></a>Сведения о диспетчере сервера
Нет действий по настройке, необходимых для реализации MSA и gMSA с помощью диспетчер сервера или \- командлета Install WindowsFeature.

## <a name="see-also"></a><a name="BKMK_LINKS"></a> См. также
В следующей таблице представлены ссылки на дополнительные ресурсы, связанные с управляемыми учетными записями служб и групповыми управляемыми учетными записями служб.

|Тип содержимого|Ссылки|
|--------|-------|
|**Оценка продукта**|[What's New for Managed Service Accounts](what-s-new-for-managed-service-accounts.md)<p>[Документация по управляемым учетным записям служб для Windows 7 и Windows Server 2008 R2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff641731(v=ws.10))<p>[Пошаговое руководств по учетным записям служб \- \-](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd548356(v=ws.10))|
|**Планирование**|Пока недоступно|
|**Развертывание**|Пока недоступно|
|**Операции**|[Управляемые учетные записи служб в Active Directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd378925(v=ws.10))|
|**Устранение неполадок**|Пока недоступно|
|**Ознакомительная версия**|[начало работы с групповыми управляемыми учетными записями службы](getting-started-with-group-managed-service-accounts.md)|
|**Средства и параметры**|[Управляемые учетные записи служб в доменных службах Active Directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd378925(v=ws.10))|
|**Ресурсы сообщества**|[Управляемые учетные записи служб: общие сведения, реализация, рекомендации и устранение неполадок](/archive/blogs/askds/managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting)|
|**Связанные технологии**|[Обзор доменных служб Active Directory](active-directory-domain-services-overview.md)|