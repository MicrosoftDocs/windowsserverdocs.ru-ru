---
title: Предварительные требования для развертывания DirectAccess
description: В этом разделе приводятся предварительные требования для развертывания DirectAccess в Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 57c7e039-42ef-4909-867a-b5f669c9e74e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2025c2d90d9eef679bf8f51c18c9e1ba32123441
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87994953"
---
# <a name="prerequisites-for-deploying-directaccess"></a>Предварительные требования для развертывания DirectAccess

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

В следующей таблице перечислены предварительные требования, необходимые для использования мастеров настройки для развертывания DirectAccess.

|Сценарий|Предварительные требования|
|-|-|
|[Развертывание одного сервера DirectAccess с помощью мастера начало работы](../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|— Брандмауэр Windows должен быть включен для всех профилей.<p>— Поддерживается только для клиентов под управлением Windows 10 &reg; , <br />              Windows &reg; 8 и windows &reg; 8,1 Enterprise.<p>— Инфраструктура открытых ключей не требуется.<p>— Не поддерживается для развертывания двухфакторной проверки подлинности. Для проверки подлинности требуются учетные данные домена.<p>— Автоматически развертывает DirectAccess на всех мобильных компьютерах в текущем домене.<p>— Трафик к Интернету не проходит через DirectAccess. Конфигурация принудительного туннелирования не поддерживается.<p>— Сервер DirectAccess — это сервер сетевых расположений.<p>— Защита доступа к сети (NAP) не поддерживается.<p>-Изменение политик с помощью компонента, отличного от консоли управления DirectAccess или командлетов Windows PowerShell, не поддерживается.<p>— Для многосайтовой конфигурации, сейчас или в будущем, сначала следуйте указаниям в статье [развертывание одного сервера DirectAccess с дополнительными параметрами](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).|
|[Развертывание одного сервера DirectAccess с расширенными параметрами](../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)|— Инфраструктура открытых ключей должна быть развернута.<br /> Дополнительные сведения см. в разделе [тест лабораторного руководства мини-модуль: базовый PKI для Windows Server 2012](/answers/topics/windows-server-2012.html).<p>— Брандмауэр Windows должен быть включен для всех профилей.<p>Следующие серверные операционные системы поддерживают DirectAccess.<p>— Можно развернуть все версии Windows Server 2016 в качестве клиента DirectAccess или сервера DirectAccess.<br />— Можно развернуть все версии Windows Server 2012 R2 в качестве клиента DirectAccess или сервера DirectAccess.<br />— Можно развернуть все версии Windows Server 2012 в качестве клиента DirectAccess или сервера DirectAccess.<br />— Можно развернуть все версии Windows Server 2008 R2 в качестве клиента DirectAccess или сервера DirectAccess.<p>Следующие клиентские операционные системы поддерживают DirectAccess.<p>— Windows 10 &reg; Корпоративная<br />— Windows 10 &reg; корпоративная 2015 Long Term Servicing Branch (LTSB)<br />— Windows &reg; 8 и 8,1 Enterprise<br />— Windows &reg; 7 Максимальная<br />— Windows &reg; 7 Корпоративная<p>— Конфигурация принудительного туннелирования не поддерживается при проверке подлинности Кербпрокси.<p>-Изменение политик с помощью компонента, отличного от консоли управления DirectAccess или командлетов Windows PowerShell, не поддерживается.<p>-Разделение ролей NAT64, DNS64 и IPHTTPS сервера на другом сервере не поддерживается.|