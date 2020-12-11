---
description: 'Дополнительные сведения: инициализация кластера HGS с помощью режима AD в новом выделенном лесу (по умолчанию)'
title: Инициализация кластера HGS с помощью режима AD в новом выделенном лесу (по умолчанию)
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: a477ae4010c201b5dec89f5c3d938fd25991245d
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97047372"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-a-new-dedicated-forest-default"></a>Инициализация кластера HGS с помощью режима AD в новом выделенном лесу (по умолчанию)

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

>[!IMPORTANT]
>Служба аттестации, доверенная для администраторов (режим AD), устарела, начиная с Windows Server 2019. Для сред, в которых невозможно подтвердить аттестацию доверенного платформенного модуля, настройте [аттестацию ключа узла](guarded-fabric-initialize-hgs-key-mode-default.md). Аттестация ключа узла обеспечивает аналогичные гарантии в режиме AD и проще в настройке.

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]
2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  Выполните команду [Initialize-HgsServer](https://technet.microsoft.com/library/mt652185.aspx) в окне PowerShell с повышенными привилегиями на первом узле HGS. Синтаксис этого командлета поддерживает множество различных входных данных, но 2 наиболее распространенные вызовы приведены ниже:

    -   Если вы используете PFX-файлы для сертификатов подписывания и шифрования, выполните следующие команды:

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
        ```

    -   Если вы используете неэкспортируемые сертификаты, установленные в локальном хранилище сертификатов, выполните следующую команду. Если вы не знакомы с отпечаткой сертификатов, можно вывести список доступных сертификатов, выполнив `Get-ChildItem Cert:\LocalMachine\My` .

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' --TrustActiveDirectory
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Настройка DNS структуры](guarded-fabric-configuring-fabric-dns-ad.md)
