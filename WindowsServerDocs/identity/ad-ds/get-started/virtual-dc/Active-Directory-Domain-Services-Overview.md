---
ms.assetid: f052dfcd-dace-4485-8d0a-cc7df5cf3751
title: Обзор доменных служб Active Directory
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 13d32a4fc11611f030006ad9628d2e84a045e511
ms.sourcegitcommit: c710fea2c0591febfc1bc9a705d59979be6f699b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/20/2020
ms.locfileid: "83705568"
---
# <a name="active-directory-domain-services-overview"></a>Обзор доменных служб Active Directory

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


Каталог — это иерархическая структура, в которой хранятся сведения об объектах в сети. Служба каталогов, например домен Active Directory Services (AD DS), предоставляет методы для хранения данных каталога и предоставления доступа к этим данным сетевым пользователям и администраторам. Например, AD DS хранит сведения об учетных записях пользователей, таких как имена, пароли, Номера телефонов и т. д., а также позволяет другим полномочным пользователям в той же сети получить доступ к этим сведениям.

Active Directory хранит сведения об объектах в сети и предоставляет эту информацию администраторам и пользователям, которые могут легко найти и использовать ее. Active Directory использует структурированное хранилище данных в качестве основы для логической иерархической организации сведений в каталоге.

Это хранилище данных, также называемое каталогом, содержит сведения об Active Directoryных объектах. Обычно эти объекты включают в себя общие ресурсы, такие как серверы, тома, принтеры, учетные записи пользователей и компьютеров сети. Дополнительные сведения о Active Directory хранилище данных см. в разделе [хранилище данных каталога](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc736627(v=ws.10)).

Безопасность интегрирована с Active Directory путем проверки подлинности входа и управления доступом к объектам в каталоге. С одним сетевым входом администраторы могут управлять данными каталога и Организацией по всей сети, а полномочные пользователи сети могут получать доступ к ресурсам в любой точке сети. Администрирование на основе политики облегчает управление даже очень сложной сетью. Дополнительные сведения о Active Directory безопасности см. в разделе [Общие сведения о безопасности](../../plan/security-best-practices/best-practices-for-securing-active-directory.md).

Active Directory также включает:
* Набор правил, **схема**, определяющая классы объектов и атрибутов, содержащихся в каталоге, ограничения и ограничения для экземпляров этих объектов и формат их имен. Дополнительные сведения о схеме см. в разделе Schema.


* **Глобальный каталог** , содержащий сведения о каждом объекте в каталоге. Это позволяет пользователям и администраторам находить данные каталога независимо от того, какой домен в каталоге действительно содержит данные. Дополнительные сведения о глобальном каталоге см. в статье роль глобального каталога.


* **Механизм запросов и индексов**, чтобы объекты и их свойства могли быть опубликованы и найдены сетевыми пользователями или приложениями. Дополнительные сведения о запросах к каталогу см. в разделе Поиск сведений о каталоге.


* **Служба репликации** , которая распределяет данные каталога по сети. Все контроллеры домена в домене участвуют в репликации и содержат полную копию всех данных каталога для своего домена. Любые изменения данных каталога реплицируются в домене на все контроллеры домена. Дополнительные сведения о репликации Active Directory см. в разделе Общие сведения о репликации.

## <a name="understanding-active-directory"></a>Основные сведения о Active Directory
 В этом разделе приводятся ссылки на основные понятия Active Directory:
 
* [Технологии структуры и хранения Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759186(v=ws.10))
* [Роли контроллера домена](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc786438(v=ws.10)) 
* [Схема Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771796(v=ws.10))
* [Представление о довериях](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771568(v=ws.10)) 
* [Технологии репликации Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc776877(v=ws.10)) 
* [Технологии поиска и публикации Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc775686(v=ws.10)) 
* [Взаимодействие с DNS и групповая политика](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197486(v=ws.10))
* [Основные сведения о схеме](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10)) 

Подробный список концепций Active Directory см. в разделе [Общие сведения о Active Directory](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc781408(v=ws.10)). 


