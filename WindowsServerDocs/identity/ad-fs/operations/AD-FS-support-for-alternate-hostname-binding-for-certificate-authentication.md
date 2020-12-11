---
description: 'Дополнительные сведения: AD FS поддержка альтернативного привязывания имени узла для проверки подлинности на сертификате'
ms.assetid: 4b71b212-7e5b-4fad-81ee-75b3d1f27869
title: Поддержка привязки альтернативного имени узла для проверки подлинности сертификата в AD FS
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 468e6934dc69ef2f6f83f052ad288860d7fed46e
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97046612"
---
# <a name="ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication"></a>Поддержка привязки альтернативного имени узла для проверки подлинности сертификата в AD FS

Во многих сетях локальные политики брандмауэра могут запрещать трафик через нестандартные порты, например 49443. Это стало проблемой при попытке выполнить проверку подлинности на сертификате с AD FS до AD FS в Windows Server 2016. Это связано с тем, что для проверки подлинности устройства и проверки подлинности сертификата пользователя на одном узле не могут быть настроены разные привязки. Порт по умолчанию 443 связан с получением сертификатов устройств и не может быть изменен для поддержки нескольких привязок в одном канале. В результате проверка подлинности смарт-карты не будет работать, и пользователи не знают, что произошло, так как это не означает, что произошло.

В Windows Server 2016 это можно сделать с помощью AD FS.

В AD FS на Windows Server 2016 это изменилось. Теперь мы поддерживаем два режима, первый использует тот же узел (например, adfs.contoso.com) с разными портами (443, 49443). Второй использует различные узлы (adfs.contoso.com и certauth.adfs.contoso.com) с одним и тем же портом (443). Для этого потребуется SSL-сертификат для поддержки "цертаус. <ADFS — Service-Name>" в качестве альтернативного имени субъекта. Это можно сделать во время создания фермы или позднее с помощью PowerShell.

## <a name="how-to-configure-alternate-host-name-binding-for-certificate-authentication"></a>Настройка альтернативной привязки имени узла для проверки подлинности сертификата
Существует два способа добавления привязки имени альтернативного узла для проверки подлинности сертификата. Во-первых, при настройке новой фермы AD FS с AD FS для Windows Server 2016, если сертификат содержит альтернативное имя субъекта (SAN), он будет автоматически настроен для использования второго метода, упомянутого выше. То есть он автоматически настраивает два разных узла (sts.contoso.com и certauth.sts.contoso.com с одним и тем же портом). Если сертификат не содержит SAN, вы увидите предупреждение о том, что альтернативные имена субъектов сертификатов не поддерживают цертаус. *. См. снимки экрана ниже. В первой показана установка с сертификатом SAN, а второй — сертификатом, который не был.

![альтернативная привязка имени узла](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_1.png)

![альтернативная привязка имени узла](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_2.png)

Кроме того, после развертывания AD FS в Windows Server 2016 можно использовать командлет PowerShell Set-Адфсалтернатетлсклиентбиндинг.

```powershell
Set-AdfsAlternateTlsClientBinding -Member ADFS1.contoso.com -Thumbprint '<thumbprint of cert>'
```

При появлении запроса нажмите кнопку Да для подтверждения.  И это должно быть.

![альтернативная привязка имени узла](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_3.png)

## <a name="additional-references"></a>Дополнительная справка

* [Управление SSL-сертификатами в AD FS и WAP в Windows Server 2016](./manage-ssl-certificates-ad-fs-wap.md)
