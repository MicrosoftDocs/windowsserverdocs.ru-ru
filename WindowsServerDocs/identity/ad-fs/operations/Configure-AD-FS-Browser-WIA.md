---
title: Настройка браузеров для использования встроенной проверки подлинности Windows (WIA) с AD FS
description: В этом документе описывается настройка браузеров для использования WIA с AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/20/2020
ms.topic: article
ms.openlocfilehash: e8a7b99ff18091266dd3ef7fdbe54ca641f4c556
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956501"
---
# <a name="configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>Настройка браузеров для использования встроенной проверки подлинности Windows (WIA) с AD FS

По умолчанию встроенная проверка подлинности Windows (WIA) включена в службы федерации Active Directory (AD FS) (AD FS) в Windows Server 2012 R2 для запросов проверки подлинности, которые выполняются в внутренней сети организации для любого приложения, использующего браузер для проверки подлинности.

AD FS 2016 теперь имеет усовершенствованный параметр по умолчанию, который позволяет браузеру пограничной работать с WIA, не выполняя при этом неправильное и неверное перехват Windows Phone:

```
=~Windows\s*NT.*Edge
```

Приведенное выше означает, что больше не нужно настраивать отдельные строки агента пользователя для поддержки распространенных сценариев пограничных устройств, несмотря на то, что они обновляются довольно часто.

Для других браузеров настройте свойство AD FS **виасуппортедусеражентс** , чтобы добавить необходимые значения в зависимости от используемых браузеров.  Вы можете использовать приведенные ниже процедуры.

### <a name="view-wiasupporteduseragent-settings"></a>Просмотр параметров Виасуппортедусеражент

**Виасуппортедусеражентс** определяет агенты пользователя, поддерживающие WIA. AD FS анализирует строку агента пользователя при выполнении входа в браузере или элементе управления браузера.

Текущие параметры можно просмотреть с помощью следующего примера PowerShell:

```powershell
Get-AdfsProperties | select -ExpandProperty WiaSupportedUserAgents
```

![Поддержка WIA](../operations/media/Configure-AD-FS-Browser-WIA/wiasupport.png)

### <a name="change-wiasupporteduseragent-settings"></a>Изменить параметры Виасуппортедусеражент
По умолчанию при установке новой AD FS создается набор строк агента пользователя. Однако они могут устареть в зависимости от изменений в браузерах и устройствах. В частности, устройства Windows имеют аналогичные строки агента пользователя с дополнительными вариациями в маркерах. Следующий пример Windows PowerShell предоставляет лучшие рекомендации для текущего набора устройств на рынке, поддерживающих беспрепятственное WIA:

Если у вас AD FS на Windows Server 2012 R2 или более ранней версии:

```powershell
Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client", "Edg/79.0.309.43")
```

Если у вас AD FS на Windows Server 2016 или более поздней версии:

```powershell
Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client", "Edg/*")
```

Приведенная выше команда обеспечит AD FS только для следующих вариантов использования WIA:

|Агенты пользователя|Варианты использования|
|-----|-----|
|MSIE 6,0|IE 6,0|
|MSIE 7,0; Windows NT|IE 7, IE в зоне интрасети. Фрагмент "Windows NT" отправляется операционной системой рабочего стола.|
|MSIE 8,0|IE 8,0 (устройства не отправляются, поэтому необходимо сделать более конкретным).|
|MSIE 9,0|IE 9,0 (устройства не отправляются, поэтому нет необходимости делать это более конкретным).|
|MSIE 10,0; Windows NT 6|IE 10,0 для Windows XP и более новых версий настольной операционной системы</br></br>Устройства Windows Phone 8,0 (с установленным параметром "мобильные") исключаются, так как они отправляют</br></br>Агент пользователя: Mozilla/5.0 (совместимый; MSIE 10,0; Windows Phone 8,0; Trident/6.0; Иемобиле/10.0; АКТИВАЦИИ Персонифицирован КЛАВИАТУРА Lumia 920)|
|Windows NT 6,3; Trident/7.0</br></br>Windows NT 6,3; Платформе х Trident/7.0</br></br>Windows NT 6,3; WOW64 Trident/7.0| Windows 8.1 классических операционных систем, различных платформ|
|Windows NT 6,2; Trident/7.0</br></br>Windows NT 6,2; Платформе х Trident/7.0</br></br>Windows NT 6,2; WOW64 Trident/7.0|Операционная система Windows 8 Desktop, различные платформы|
|Windows NT 6,1; Trident/7.0</br></br>Windows NT 6,1; Платформе х Trident/7.0</br></br>Windows NT 6,1; WOW64 Trident/7.0|Операционная система Windows 7 Desktop, различные платформы|
|Едг/79.0.309.43 | Microsoft ребро (Chromium) для Windows Server 2012 R2 или более ранней версии |
|Едг/*| Microsoft ребро (Chromium) для Windows Server 2016 или более поздней версии|
|MSIPC| Клиент Microsoft технология защиты и контроля информации|
|Клиент Windows Rights Management|Клиент Windows Rights Management|

### <a name="additional-links"></a>Дополнительные ссылки

[Документация по Microsoft Edge](/microsoft-edge/web-platform/user-agent-string)
