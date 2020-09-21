---
title: Как правильно выбрать тип установки
description: Эта статья описывает несколько способов установки для Windows Admin Center, в том числе установку на компьютере под управлением Windows 10 или Windows Server для использования несколькими администраторами.
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 12/02/2019
ms.openlocfilehash: 403a0f68f559d72dfaa54e4b537a50a66fc3ec6a
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766727"
---
# <a name="what-type-of-installation-is-right-for-you"></a>Как правильно выбрать тип установки

Эта статья описывает несколько способов установки для Windows Admin Center, в том числе установку на компьютере под управлением Windows 10 или Windows Server для использования несколькими администраторами. Чтобы установить Windows Admin Center на виртуальной машине в Azure, обратитесь к статье о [развертывании Windows Admin Center в Azure](../azure/deploy-wac-in-azure.md).

## <a name="installation-types"></a>Установка. Типы

![img](../media/deployment-options/install-options.PNG)

| Локальный клиент                                | Сервер шлюза                                  | Управляемый сервер                               | Отказоустойчивый кластер                           |
|---------------------------------------------|-------------------------------------------------|----------------------------------------------|--------------------------------------------|
| [Установка](../deploy/install.md) на локальном клиенте Windows 10, который имеет подключение к управляемым серверам.  Это отличный способ для ознакомления и тестирования, для быстрого решения или небольшой системы. |[Установка](../deploy/install.md) на выделенном сервере шлюза с доступом через любой клиентский браузер, имеющий подключение к этому серверу шлюза.  Хорошо подходит для крупных развертываний. | [Установка](../deploy/install.md) непосредственно на управляемом сервере, которая позволит управлять самим этим сервером или кластером, в который он входит.  Идеальный вариант для распределенной системы. | [Развертывание](#high-availability) в отказоустойчивом кластере, которое обеспечит высокий уровень доступности службы шлюза. Отлично подходит для рабочих сред, чтобы повысить устойчивость службы управления. |

## <a name="installation-supported-operating-systems"></a>Установка. Поддерживаемые операционные системы

Windows Admin Center можно **установить** в следующих операционных системах Windows.

| **Платформа**                       | **Режим установки** |
| -----------------------------------| --------------------- |
| Windows 10                         | Локальный клиент |
| Windows Server, Semi-Annual Channel | Сервер шлюза, управляемый шлюз, отказоустойчивый кластер |
| Windows Server 2016                | Сервер шлюза, управляемый шлюз, отказоустойчивый кластер |
| Windows Server 2019                | Сервер шлюза, управляемый шлюз, отказоустойчивый кластер |

Для работы с Windows Admin Center потребуется следующее.

- **В сценарии с локальным клиентом.** Запустите шлюз Windows Admin Center через начальный экран и подключитесь к нему из клиентского веб-браузера по адресу `https://localhost:6516`.
- **В других сценариях.** Подключитесь к шлюзу Windows Admin Center, установленному на другом компьютере, через любой клиентский браузер по известному URL-адресу вида `https://servername.contoso.com`.

> [!WARNING]
> Установка Windows Admin Center на контроллере домена не поддерживается. [Дополнительные рекомендации по обеспечению безопасности контроллера домена](../../../identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack.md).

## <a name="installation-supported-web-browsers"></a>Установка. Поддерживаемые веб-браузеры

В среде Windows 10 тестируется и поддерживается работа из Microsoft Edge (включая [Microsoft Edge Insider](https://microsoftedgeinsider.com)) и Google Chrome. Другие веб-браузеры, в том числе Internet Explorer и Firefox, в настоящий момент не входят в нашу матрицу тестирования и поэтому *официально* не поддерживаются. В этих браузерах могут возникать проблемы с работой в Windows Admin Center. Например, Firefox использует собственное хранилище сертификатов, поэтому вам придется импортировать сертификат `Windows Admin Center Client` в Firefox, чтобы использовать Windows Admin Center в Windows 10. Дополнительные сведения см. в разделе [известные проблемы с разными браузерами](../support/known-issues.md#browser-specific-issues).

## <a name="management-target-supported-operating-systems"></a>Целевой объект управления. Поддерживаемые операционные системы

С помощью Windows Admin Center можно **управлять** следующими операционными системами Windows.

| Версия | Управление *узлом* через *диспетчер сервера* | Управление через *диспетчер кластера* |
| ------------------------- |--------------- | ----- |
| Windows 10 | Да (через "Управление компьютером") | Н/Д |
| Windows Server, Semi-Annual Channel | Да | Да |
| Windows Server 2019 | Да | Да |
| Windows Server 2016 | Да | Да, с [последним накопительным пакетом обновления](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | Да | Да |
| Windows Server 2012 R2 | Да | Да |
| Microsoft Hyper-V Server 2012 R2 | Да | Да |
| Windows Server 2012 | Да | Да |

> [!NOTE]
> Для Windows Admin Center требуются функции PowerShell, которые отсутствуют в Windows Server 2012 и 2012 R2. Если вы намерены применить Windows Admin Center для управления этими ОС, вам придется установить на этих серверах Windows Management Framework (WMF) 5.1 или более поздней версии.
>
> Введите `$PSVersiontable` в PowerShell, чтобы проверить, что платформа WMF установлена, и что используется версия 5.1 или более поздняя версия.
>
> Если WMF не установлена, вы можете [скачать WMF 5.1](https://www.microsoft.com/download/details.aspx?id=54616).

## <a name="high-availability"></a>Высокая доступность

Вы можете обеспечить высокий уровень доступности для службы шлюза, развернув Windows Admin Center в активно-пассивном режиме в отказоустойчивом кластере. В случае сбоя одного из узлов кластера Windows Admin Center корректно переключается на другой узел, сохраняя для вас возможность управлять серверами в своей среде.

[Сведения о развертывании Windows Admin Center с высоким уровнем доступности](../deploy/high-availability.md).

> [!Tip]
> Готовы к установке Windows Admin Center? [Скачать](../overview.md)