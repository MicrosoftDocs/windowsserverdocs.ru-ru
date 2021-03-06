---
description: Дополнительные сведения см. в статье ферма серверов федерации с помощью WID.
ms.assetid: 663a2482-33d1-4c19-8607-2e24eef89fcb
title: Ферма серверов AD FS Федерации с помощью WID
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: ffc15afdea63755689d78c6567ea6d0a4cb8af69
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97046962"
---
# <a name="federation-server-farm-using-wid"></a>Ферма серверов федерации с использованием WID

Топология по умолчанию для службы федерации Active Directory (AD FS) \( AD FS \) представляет собой ферму серверов федерации с помощью внутренней базы данных Windows \( WID \) , которая состоит из пяти серверов федерации, на которых размещена служба федерации организации. В этой топологии AD FS использует WID в качестве хранилища для базы данных конфигурации AD FS для всех серверов федерации, присоединенных к этой ферме. Ферма выполняет репликацию и обслуживание данных службы федерации в базе данных конфигурации на всех своих серверах.

При создании первого сервера федерации в ферме также создается новая служба федерации. При использовании WID для базы данных конфигурации AD FS первый сервер федерации, созданный в ферме, называется *основным сервером федерации*. Это означает, что на этом компьютере настроена копия базы данных конфигурации AD FS, предназначенная для чтения и \/ записи.

Все другие серверы федерации, настроенные для этой фермы, называются *дополнительными серверами федерации* , так как они должны реплицировать все изменения, внесенные на основном сервере федерации, в доступные только для чтения \- копии базы данных конфигурации AD FS, которые хранятся локально.

> [!NOTE]
> Рекомендуется использовать по крайней мере два сервера федерации в \- конфигурации с балансировкой нагрузки.

## <a name="deployment-considerations"></a>Рекомендации по развертыванию
В этом разделе описываются различные вопросы о предполагаемой аудитории, преимуществах и ограничениях, связанных с этой топологией развертывания.

### <a name="who-should-use-this-topology"></a>Кто должен использовать эту топологию?

-   Организации с 100 или менее настроенными доверительными отношениями, которые должны предоставить своим внутренним пользователям \( доступ к компьютерам, физически подключенным к корпоративной сети, \) с единым входом единого входа \- \( \) для федеративных приложений или служб.

-   Организации, желающие предоставить своим внутренним пользователям доступ с помощью единого входа к службам Microsoft Online Services или Microsoft Office 365

-   Небольшие организации, требующие избыточных масштабируемых служб

> [!NOTE]
> Организации с большими базами данных должны использовать [ферму серверов федерации, используя](Federation-Server-Farm-Using-SQL-Server.md) топологию развертывания SQL Server, которая описана далее в этом разделе. Организации с пользователями, которые входят за пределы сети, должны использовать [ферму серверов федерации, использующую топологию WID и учетные записи-посредники](Federation-Server-Farm-Using-WID-and-Proxies.md) или [ферму серверов федерации, используя](Federation-Server-Farm-Using-SQL-Server.md) топологию SQL Server.

### <a name="what-are-the-benefits-of-using-this-topology"></a>Каковы преимущества использования этой топологии?

-   Предоставляет единый доступ к внутренним пользователям

-   Данные и служба федерации избыточность на \( каждом сервере федерации реплицирует изменения на другие серверы федерации в той же ферме.\)

-   Ферму можно масштабировать, добавив до пяти серверов федерации

-   WID входит в состав Windows; Следовательно, нет необходимости покупать SQL Server

### <a name="what-are-the-limitations-of-using-this-topology"></a>Каковы ограничения использования этой топологии?

-   Ферма WID имеет ограничение в пять серверов федерации. Дополнительные сведения см. в разделе [Некоторые аспекты топологии развертывания AD FS](AD-FS-Deployment-Topology-Considerations.md).

-   Ферма WID не поддерживает определение воспроизведения маркеров или разрешение артефактов \( в \( \) протоколе язык разметки зявлений системы безопасности (SAML) SAML \) .

## <a name="server-placement-and-network-layout-recommendations"></a>Рекомендации по размещению и макету сети сервера
Когда вы будете готовы приступить к развертыванию этой топологии в сети, следует спланировать размещение всех серверов федерации в корпоративной сети за узлом балансировки сетевой нагрузки \( \) , который можно настроить для кластера балансировки сетевой нагрузки с выделенным \( DNS- \) именем и IP-адресом кластера.

> [!NOTE]
> Это DNS-имя кластера должно соответствовать имени служба федерации, например fs.fabrikam.com.

Узел балансировки сетевой нагрузки может использовать параметры, определенные в этом кластере балансировки сетевой нагрузки, для выделения клиентских запросов отдельным серверам федерации. На следующем рисунке показано, как вымышленная компания Fabrikam, Inc. компании настраивает первый этап развертывания, используя две \- фермы серверов федерации \( FS1 и FS2 \) с WID, а также размещение DNS-сервера и одного узла балансировки сетевой нагрузки, подключенного к корпоративной сети.

![ферма серверов, использующая WID](media/FarmWID.gif)

> [!NOTE]
> Если на данном узле балансировки сетевой нагрузки произошел сбой, пользователи не смогут получить доступ к федеративным приложениям или службам. Если требования бизнес-деятельности организации не допускают наличия подобных узких мест, добавьте дополнительные узлы балансировки сетевой нагрузки.

Дополнительные сведения о настройке сетевой среды для использования с серверами федерации см. в разделе [требования к разрешению имен для серверов федерации](Name-Resolution-Requirements-for-Federation-Servers.md) в AD FS руководство по проектированию.

## <a name="see-also"></a>См. также:
[Руководство по разработке служб федерации Active Directory в Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
