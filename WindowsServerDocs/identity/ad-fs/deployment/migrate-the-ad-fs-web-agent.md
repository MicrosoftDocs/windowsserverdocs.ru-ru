---
title: Перенос веб-агента AD FS
description: Предоставляет сведения о веб-агенте AD FS для Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: 23e80eee87eb5faac875298f4264607df65253c3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940746"
---
# <a name="migrate-the-ad-fs-web-agent"></a>Перенос веб-агента AD FS

Чтобы перенести агент на основе маркеров Windows AD FS 1,1 или агент AD FS 1,1 с поддержкой утверждений, установленный вместе с Windows Server 2008 R2 или Windows Server 2008 до Windows Server 2012, выполните обновление операционной системы компьютера, на котором размещается агент, на Windows Server 2012. Дополнительные сведения см. в разделе [Установка Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11)). Дальнейшая настройка не требуется.

> [!IMPORTANT]
>  Перенесенный агент AD FS 1.1, использующий токены Windows, работает только со службой федерации AD FS 1.1, которая устанавливается с Windows Server 2008 R2 или Windows Server 2008. Дополнительные сведения см. в разделе [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md).
>
>  Перенесенный веб-агент по утверждениям AD FS 1.1 функционирует со следующими системами:
>
> - службой федерации AD FS 1.1, установленной с Windows Server 2008 R2 или Windows Server 2008;
>   -   службой федерации AD FS 2.0, установленной в Windows Server 2008 R2 или Windows Server 2008;
>   -   AD FS Служба федерации, установленная с Windows Server 2012
>
>   Дополнительные сведения см. в разделе [Interoperating with AD FS 1.x](Interoperating-with-AD-FS-1.x.md).


## <a name="next-steps"></a>Next Steps
 [Подготовка к переносу сервера федерации AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) [Подготовка к переносу AD FS 2,0 прокси-](prepare-to-migrate-ad-fs-fed-proxy.md) сервер федерации миграция [сервера AD FS 2,0 сервер федерации](migrate-the-ad-fs-fed-server.md) миграция [AD FS 2,0 прокси-сервер](migrate-the-ad-fs-2-fed-server-proxy.md) [AD FS 1,1](migrate-the-ad-fs-web-agent.md)
