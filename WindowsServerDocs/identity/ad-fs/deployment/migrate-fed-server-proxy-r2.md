---
title: Перенос прокси-сервера федерации AD FS 2,0
description: Содержит сведения о миграции AD FS прокси-сервера на Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.openlocfilehash: a8345f587e7fe4119e46dc390e9240dee6071ce6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940837"
---
# <a name="migrate-the-active-directory-federation-services-proxy-server-to-windows-server-2012-r2"></a>Миграция службы федерации Active Directory (AD FS) прокси-сервера на Windows Server 2012 R2

В службы федерации Active Directory (AD FS) (AD FS) в Windows Server 2012 R2 роль прокси-сервера федерации обрабатывается новой службой роли удаленного доступа, именуемой прокси-сервером веб приложения. В Windows Server 2012 R2, чтобы обеспечить доступность AD FS для доступа за пределами корпоративной сети, можно развернуть один или несколько прокси веб-приложений. Однако вы не можете перенести прокси-сервер федерации, работающий на Windows Server 2008 R2 или Windows Server 2012, в прокси веб – приложения, работающего на Windows Server 2012 R2.

> [!IMPORTANT]
>  Миграция прокси-сервера федерации, работающего на Windows Server 2008, Windows Server 2008 R2 или Windows Server 2012, к прокси веб приложения, работающему под Windows Server 2012 R2, не поддерживается.

Если вы хотите настроить AD FS в перенесенной ферме Windows Server 2012 R2 для доступа к экстрасети, необходимо выполнить новое развертывание одного или нескольких компьютеров прокси-сервера приложений в рамках инфраструктуры AD FS.

При планировании развертывания прокси-сервера веб-приложения можно использовать сведения в следующих разделах.

- [Планирование инфраструктуры прокси веб-приложения](/previous-versions/orphan-topics/ws.11/dn383648(v=ws.11))

- [Планирование прокси-сервера веб-приложений](/previous-versions/orphan-topics/ws.11/dn383647(v=ws.11))

  При развертывании прокси-сервера веб-приложения можно следовать процедурам в следующих разделах.

- [Настройка инфраструктуры прокси-сервера веб-приложений](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383644(v=ws.11))

- [Установка и настройка прокси-сервера веб-приложений](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383662(v=ws.11))

## <a name="next-steps"></a>Next Steps
 [Миграция служб ролей службы федерации Active Directory (AD FS) в Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md) [Подготовка к переносу сервера федерации AD FS](prepare-migrate-ad-fs-server-r2.md) [Миграция AD FS сервер федерации,](migrate-ad-fs-fed-server-r2.md) [проверяющий миграцию AD FS на Windows Server 2012 R2](verify-ad-fs-migration.md)
