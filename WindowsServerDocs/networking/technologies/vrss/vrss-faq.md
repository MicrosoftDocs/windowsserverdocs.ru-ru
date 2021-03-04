---
title: Часто задаваемые вопросы по vRSS
description: В этом разделе вы найдете ответы на часто задаваемые вопросы об использовании vRSS.
ms.topic: article
ms.assetid: 61ae242e-82a8-430d-b07d-52b86c01e686
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: jgerend
author: JasonGerend
ms.openlocfilehash: a26ea69e9725d2fa0ac999a7ff61f908e7310f97
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101829949"
---
# <a name="vrss-frequently-asked-questions"></a>Часто задаваемые вопросы по vRSS

В этом разделе вы найдете ответы на часто задаваемые вопросы об использовании vRSS.

## <a name="what-are-the-requirements-for-the-physical-network-adapters-that-i-use-with-vrss"></a>Каковы требования для физических сетевых адаптеров, которые я использую с vRSS?

Сетевые адаптеры должны быть совместимы с очередь виртуальной машины \( VMQ \) и должны иметь скорость связи 10 Гбит/с или более.

Дополнительные сведения см. [в разделе Планирование использования vRSS](vrss-plan.md).

## <a name="does-vrss-work-with-hyper-threaded-processor-cores"></a>Работает ли vRSS с \- процессорными ядрами с Hyper Threading?

Нет. И vRSS, и VMQ игнорируют \- процессорные ядра Hyper.

## <a name="does-vrss-work-for-host-virtual-nics-vnics"></a>Работает ли vRSS для виртуальных сетевых адаптеров узла \( vNIC \) ?

Да. Используйте параметр **-манажементос** вместо \( имени ВМ виртуальной машины \) в команде **Set-VMNetworkAdapter** Windows PowerShell и **Enable-нетадаптеррсс** на узле vNIC.

Дополнительные сведения см. в разделе [команды Windows PowerShell для RSS и vRSS](vrss-wps.md).

## <a name="how-many-logical-processors-does-a-vm-need-to-use-vrss"></a>Сколько логических процессоров виртуальным машинам требуется использовать vRSS?

Виртуальным машинам требуются два или более логических процессора \( LPS \) , чтобы иметь возможность использовать vRSS.

Дополнительные сведения см. [в разделе Планирование использования vRSS](vrss-plan.md).

## <a name="is-vrss-compatible-with-nic-teaming"></a>Поддерживает ли vRSS объединение сетевых карт?

Да. Если вы используете объединение сетевых карт, важно правильно настроить VMQ для работы с параметрами объединения сетевых карт. Подробные сведения о развертывании и управлении с объединением сетевых карт см. в разделе [Объединение сетевых](../nic-teaming/nic-teaming.md)карт.

## <a name="vrss-is-enabled-but-how-do-i-know-if-it-is-working"></a>vRSS включен, но как узнать, работает ли оно?

Вы сможете сообщить, что vRSS работает, открыв диспетчер задач на виртуальной машине и просмотрев использование виртуального процессора. Если для виртуальной машины установлено несколько подключений, можно увидеть более одного ядра выше 0% использования.

Поскольку один сеанс TCP не может быть сбалансирован в нескольких логических процессорных ядрах, виртуальная машина должна получать несколько сеансов TCP, прежде чем можно будет определить, работает ли vRSS.

Если виртуальная машина получает несколько сеансов TCP, но вы не видите несколько ядер LP Core выше 0%, убедитесь, что выполнены все шаги подготовки, описанные в разделе [планирование использования vRSS](vrss-plan.md).

## <a name="im-looking-at-the-host-and-not-all-of-the-processors-are-being-used-it-looks-like-every-other-one-is-being-skipped"></a>Я ищу основное приложение, и не все процессоры используются. Такое впечатление, что каждый второй пропускается.

Проверьте, включена ли технология Hyper-Threading. Как VMQ, так и vRSS предназначены для пропуска \- потоков Hyper.

## <a name="are-there-different-windows-powershell-commands-for-rss-and-vrss"></a>Существуют ли разные команды Windows PowerShell для RSS и vRSS?

И да, и нет. Хотя вы используете одни и те же команды для RSS на собственных узлах и RSS в виртуальных машинах, vRSS также требует включения VMQ на физическом сетевом адаптере, а для виртуальной машины, а также для включения vRSS в порт коммутатора.

Дополнительные сведения см. в разделе [команды Windows PowerShell для RSS и vRSS](vrss-wps.md).

---