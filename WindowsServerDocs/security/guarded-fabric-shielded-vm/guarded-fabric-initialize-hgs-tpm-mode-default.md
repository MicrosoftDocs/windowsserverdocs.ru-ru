---
description: 'Дополнительные сведения: инициализация кластера HGS с помощью режима TPM в новом выделенном лесу (по умолчанию)'
title: Инициализация кластера HGS с помощью режима TPM в новом выделенном лесу (по умолчанию)
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: eb63af4feb13b519906b8898a1eb9a352bf91d27
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97047342"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-a-new-dedicated-forest-default"></a>Инициализация кластера HGS с помощью режима TPM в новом выделенном лесу (по умолчанию)

> Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  Выполните команду [Initialize-HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/initialize-hgsserver) в окне PowerShell с повышенными привилегиями на первом узле HGS. Синтаксис этого командлета поддерживает множество различных входных данных, но 2 наиболее распространенные вызовы приведены ниже:

    -   Если вы используете PFX-файлы для сертификатов подписывания и шифрования, выполните следующие команды:

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
        ```

    -   Если вы используете неэкспортируемые сертификаты, установленные в локальном хранилище сертификатов, выполните следующую команду. Если вы не знакомы с отпечаткой сертификатов, можно вывести список доступных сертификатов, выполнив `Get-ChildItem Cert:\LocalMachine\My` .

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' -TrustTpm
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Установка корневых сертификатов доверенного платформенного модуля](guarded-fabric-install-trusted-tpm-root-certificates.md)
