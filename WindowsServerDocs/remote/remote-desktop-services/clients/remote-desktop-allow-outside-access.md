---
title: 'Удаленный рабочий стол: разрешение доступа к компьютеру извне сети'
description: Узнайте о возможностях удаленного доступа к своему компьютеру извне его сети.
ms.topic: article
author: haley-rowland
manager: dongill
ms.author: elizapo
ms.date: 04/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: a9cf5f32a2cffb52b56e619e42b22483e7cbe48a
ms.sourcegitcommit: f18097c21e50a09aef2f1937f52608b0042ef0e1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/07/2020
ms.locfileid: "96755391"
---
# <a name="remote-desktop---allow-access-to-your-pc-from-outside-your-pcs-network"></a>Удаленный рабочий стол: разрешение доступа к компьютеру извне его сети

>Применяется к: Windows 10,  Windows Server 2016

При подключении к своему компьютеру с помощью клиента удаленного рабочего стола вы создаете одноранговое подключение. Это означает, что требуется прямой доступ к компьютеру (иногда его называют "узлом"). Если вам нужно подключить к компьютеру извне сети, в которой он работает, необходимо разрешить этот доступ. Доступно несколько вариантов: использовать перенаправление портов или настроить виртуальную частную сеть (VPN).

## <a name="enable-port-forwarding-on-your-router"></a>Включение перенаправления портов на маршрутизаторе

Перенаправление портов просто сопоставляет порт для IP-адреса маршрутизатора (вашего общедоступного IP-адреса) с портом и IP-адресом компьютера, к которому необходимо получить доступ.

Конкретная последовательность действий для включения перенаправления портов зависит от маршрутизатора, который вы используете, поэтому необходимо найти в Интернете инструкции для своего маршрутизатора. Общие сведения об этих действиях см. на странице wikiHow [How to Set Up Port Forwarding on a Router](https://www.wikihow.com/Set-Up-Port-Forwarding-on-a-Router) (Как настроить перенаправление портов на маршрутизаторе).

Прежде чем сопоставить порт, потребуется следующее.

- Внутренний IP-адрес компьютера. Найдите его, выбрав **Параметры > Сеть и Интернет > Состояние > Просмотр свойств сети**. Найдите конфигурацию сети с состоянием "Работает" и получите **IPv4-адрес**.

   ![Конфигурация работающей сети](../media/rdclient-operational-network.png)

- Общедоступный IP-адрес (IP-адрес маршрутизатора). Существует много способов узнать его. Можно выполнить поиск "my IP" (в Bing или Google) или просмотреть [свойства сети Wi-Fi](https://binged.it/2Gwob34) (для Windows 10).
- Номер сопоставляемого порта. В большинстве случаев это 3389 — порт по умолчанию, используемый подключениями к удаленному рабочему столу.
- Административный доступ к маршрутизатору.

   >[!WARNING]
   > Вы открываете свой компьютер для доступа из Интернета, так что убедитесь, что на нем установлен надежный пароль.

После сопоставления порта вы сможете подключаться к компьютеру узла извне локальной сети, подключаясь к общедоступному IP-адресу маршрутизатора (см. второй пункт выше).

Вы можете изменить IP-адрес маршрутизатора. Ваш поставщик услуг Интернета (ISP) может назначить новый IP-адрес в любое время. Чтобы избежать этой проблемы, рассмотрите возможность использования динамических DNS-имен. Это позволит подключаться к компьютеру с помощью легко запоминающегося доменного имени, а не IP-адреса. Маршрутизатор автоматически обновит службу DDNS, если IP-адрес изменится.

В большинстве маршрутизаторов может определить, какой исходный IP-адрес или исходная сеть может использовать сопоставление портов. Поэтому, если известно, что вы собираетесь подключаться только с работы, можно добавить IP-адрес для своей рабочей сети. Это позволит избежать открытия порта для всего Интернета. Если на узле, которые вы используете для подключения, используется динамический IP-адрес, задайте ограничение источника, чтобы разрешить доступ из целого диапазона адресов, определенного поставщиком услуг Интернета.

Также рассмотрите возможность настройки статического IP-адреса на своем компьютере, чтобы внутренний IP-адрес не менялся. Если это сделать, то перенаправление портов маршрутизатора всегда будет указывать на правильный IP-адрес.


## <a name="use-a-vpn"></a>Использование VPN

При подключении к локальной сети с помощью виртуальной частной сети (VPN) не нужно открывать доступ к компьютеру из общедоступного Интернета. Вместо этого при подключении к VPN клиент удаленного рабочего стола действует так, будто он является частью той же сети и имеет доступ к компьютеру. Существует несколько служб VPN — можно найти и использовать ту, которая лучше всего подходит для вас.
