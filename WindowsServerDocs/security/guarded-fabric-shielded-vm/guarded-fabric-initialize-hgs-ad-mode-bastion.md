---
description: Дополнительные сведения см. в статье инициализация кластера HGS с помощью режима AD в существующем лесу бастиона.
title: Инициализация кластера HGS с помощью режима AD в лесу бастиона
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: a37ad77686b9a75704045a28ae6cccc21dbe891b
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049792"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-an-existing-bastion-forest"></a>Инициализация кластера HGS с помощью режима AD в существующем лесу бастиона

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016


>[!IMPORTANT]
>Служба аттестации, доверенная для администраторов (режим AD), устарела, начиная с Windows Server 2019. Для сред, в которых невозможно подтвердить аттестацию доверенного платформенного модуля, настройте [аттестацию ключа узла](guarded-fabric-initialize-hgs-key-mode-bastion.md). Аттестация ключа узла обеспечивает аналогичные гарантии в режиме AD и проще в настройке.

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

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
```

Если вы используете сертификаты, установленные на локальном компьютере (например, сертификаты с HSM-защитой и неэкспортируемые сертификаты), используйте `-SigningCertificateThumbprint` `-EncryptionCertificateThumbprint` вместо этого параметры и.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Настройка DNS структуры](guarded-fabric-configuring-fabric-dns-ad.md)

