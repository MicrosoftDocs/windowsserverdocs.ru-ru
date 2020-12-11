---
description: Дополнительные сведения см. в статье инициализация кластера HGS с помощью режима TPM в существующем лесу бастиона.
title: Инициализация кластера HGS с помощью режима TPM в лесу бастиона
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: de96fa3a0ad8ce4b76bd4b3c0d484bc448906ae6
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049752"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-an-existing-bastion-forest"></a>Инициализация кластера HGS с помощью режима TPM в существующем лесу бастиона

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016

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

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
```

Если вы используете сертификаты, установленные на локальном компьютере (например, сертификаты с HSM-защитой и неэкспортируемые сертификаты), используйте `-SigningCertificateThumbprint` `-EncryptionCertificateThumbprint` вместо этого параметры и.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Установка корневых сертификатов доверенного платформенного модуля](guarded-fabric-install-trusted-tpm-root-certificates.md)
