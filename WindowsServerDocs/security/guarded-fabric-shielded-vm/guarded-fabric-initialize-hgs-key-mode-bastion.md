---
title: Инициализация кластера HGS с помощью режима ключей в лесу бастиона
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: b526895f9b9e819523ee459701c2f09988565544
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966001"
---
# <a name="initialize-the-hgs-cluster-using-key-mode-in-an-existing-bastion-forest"></a>Инициализация кластера HGS с помощью режима ключей в существующем лесу бастиона

> Область применения: Windows Server 2019
>
> [!div class="step-by-step"]
> [«Установка HGS в новом лесу](guarded-fabric-install-hgs-in-a-bastion-forest.md) 
>  [Создать ключ узла»](guarded-fabric-create-host-key.md)

Домен Active Directory службы будут установлены на компьютере, но должны остаться ненастроенными.

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

Прежде чем продолжить, убедитесь, что объекты кластера предварительно подготовлены для службы защиты узла и предоставил вошедшему в систему пользователю **полный контроль** над объектами VCO и CNO в Active Directory.
Имя объекта виртуального компьютера должно быть передано в `-HgsServiceName` параметр, а имя кластера — в `-ClusterName` параметр.

> [!TIP]
> Прежде чем продолжить, проверьте контроллеры доменов AD, чтобы убедиться, что объекты кластера реплицированы на все контроллеры домена.

Если вы используете сертификаты на основе PFX, выполните на сервере HGS следующие команды:

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustHostKey
```

Если вы используете сертификаты, установленные на локальном компьютере (например, сертификаты с HSM-защитой и неэкспортируемые сертификаты), используйте `-SigningCertificateThumbprint` `-EncryptionCertificateThumbprint` вместо этого параметры и.

