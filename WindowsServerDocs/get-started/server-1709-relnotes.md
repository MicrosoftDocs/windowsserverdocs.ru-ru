---
title: Примечания к выпуску. Важные проблемы в Windows Server версии 1709
description: Сводные данные о критических проблемах, требующих обходных действий во избежание аварийного завершения, "зависания", ошибки установки и потери данных.
ms.prod: windows-server
ms.date: 04/23/2018
ms.technology: server-general
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: fea4b259986d1ca6e2f992168f7b0c2e1a177916
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826107"
---
# <a name="release-notes-important-issues-in-windows-server-version-1709"></a>Заметки о выпуске. Важные проблемы в Windows Server версии 1709

>Область применения. Windows Server, Semi-Annual Channel

В этих примечаниях к выпуску кратко изложены наиболее критические проблемы в операционной системе Windows Server&reg;, включая способы их устранения или обхода, если они известны. Информацию об изменениях структуры, новых компонентах и исправлениях в этом выпуске см. в статье [Новые возможности Windows Server версии 1709](whats-new-in-windows-server-1709.md) и в сообщениях групп разработчиков конкретных компонентов. Если не указано иное, эти заметки распространяются на все выпуски и варианты установки Windows Server 2016.  

Этот документ постоянно обновляется. По мере обнаружения критических проблем, определения обходных путей и выпуска исправлений в документ добавляются соответствующие сведения.  
  
## <a name="storage-spaces-direct"></a>Дисковые пространства прямого подключения
[comment]: # (ИД: неизвестно; Отправитель: stevenek; Состояние: утверждено)  
Локальные дисковые пространства не входят в состав Windows Server версии 1709. Если вызвать командлет *Enable-ClusterStorageSpacesDirect* или его псевдоним *Enable-ClusterS2D* на сервере с Windows Server версии 1709, отобразится сообщение об ошибке "Запрошенная операция не поддерживается".

Также она не поддерживается при добавлении серверов с Windows Server версии 1709 в среду локальных дисковых пространств Windows Server 2016.

Модель выпуска Windows Server предлагает новый вариант установки с целью обеспечения соответствия сходным моделям выпуска и обслуживания для [Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview) и [Office 365 профессиональный плюс](https://support.office.com/article/Overview-of-the-upcoming-changes-to-Office-365-ProPlus-update-management-78b33779-9356-4cdf-9d2c-08350ef05cca?ui=en-US&rs=en-US&ad=US). Выпуски Semi-Annual Channel предоставляют новые возможности пользователям, которым необходимы быстрые циклы обновления; они будут выходить дважды в год — весной и осенью.

Выпуск Semi-Annual Channel для Windows Server предназначен для контейнеров и сценариев приложений, в которых используются более быстрые инновации, дополнительные сведения см. в этом [блоге](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update). Клиентам, которые ищут инфраструктурные роли, такие как локальные дисковые пространства, следует использовать выпуски Long-Term Servicing Channel, например Windows Server 2016 (доступных сейчас) или [Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (ожидается в этом году). Мы стремимся создать лучшую платформу для гиперконвергентной инфраструктуры и продолжаем разрабатывать новые функции и улучшать существующие на основе ваших отзывов. 

Локальные дисковые пространства впервые появились в Windows Server 2016 и они лежат в основе нашей гиперконвергентной платформы. Мы рады тому, насколько положительно пользователи приняли гиперконвергентную платформу Майкрософт и делаем для них все возможное.

Мы прислушиваемся к отзывам клиентов и разрабатываем [следующий набор нововведений](https://blogs.technet.microsoft.com/windowsserver/2017/09/07/sneak-peek-2-windows-server-version-1709-hyper-converged-infrastructure/) для нашей гиперконвергентной платформы. Эти возможности уже доступны в сборках для [участников программы предварительной оценки Windows](https://insider.windows.com/for-business/), и мы хотим, чтобы вы тоже ознакомились с ними и поделились своим мнением. Клиентам, которым нужно проверенное гиперконвергентное решение, мы рекомендуем программу [Windows Server Software Defined](https://microsoft.com/wssd).
