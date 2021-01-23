---
title: Настройка шифрования для виртуальной сети
description: Узнайте, как создать сертификат шифрования, создать учетные данные сертификата и настроить виртуальную сеть для шифрования.
manager: grcusanz
ms.topic: how-to
ms.assetid: 378213f5-2d59-4c9b-9607-1fc83f8072f1
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/08/2018
ms.openlocfilehash: 15f47d48ca0e3873433fcaa3e6dd7160bc0f9126
ms.sourcegitcommit: fb2ae5e6040cbe6dde3a87aee4a78b08f9a9ea7c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2021
ms.locfileid: "98716610"
---
# <a name="configure-encryption-for-a-virtual-subnet"></a>Настройка шифрования для виртуальной подсети

>Применяется к: Windows Server 2019, Windows Server 2016

Шифрование виртуальной сети обеспечивает шифрование трафика виртуальной сети между виртуальными машинами, взаимодействующими друг с другом в подсетях, помеченных как "шифрование включено". Для шифрования пакетов с помощью этой возможности также используется протокол DTLS в виртуальной подсети. Протокол DTLS обеспечивает защиту от перехвата, несанкционированных изменений и подделки со стороны любых лиц, имеющих доступ к физической сети.

Для шифрования виртуальной сети требуется:
- Сертификаты шифрования, установленные на каждом узле Hyper-V с поддержкой SDN.
- Объект учетных данных в сетевом контроллере, ссылающийся на отпечаток этого сертификата.
- Конфигурация каждой из виртуальных сетей содержит подсети, для которых требуется шифрование.

После включения шифрования в подсети весь сетевой трафик в этой подсети шифруется автоматически, в дополнение к любому шифрованию на уровне приложения, которое также может выполняться.  Трафик, который пересекается между подсетями, даже если он помечен как зашифрованный, автоматически отправляется в незашифрованном виде. Любой трафик, который пересекает границу виртуальной сети, также отправляется в незашифрованном виде.

>[!NOTE]
>При взаимодействии с другой виртуальной машиной в той же подсети, подключенной в данный момент или подключенной позже, трафик шифруется автоматически.

>[!TIP]
>Если необходимо ограничить приложения для обмена данными только с зашифрованной подсетью, можно использовать списки управления доступом (ACL) только для обеспечения взаимодействия в текущей подсети. Дополнительные сведения см. [в статье Использование списков управления доступом (ACL) для управления потоком сетевого трафика центра обработки данных](../manage/use-acls-for-traffic-flow.md).


## <a name="step-1-create-the-encryption-certificate"></a>Шаг 1. Создание сертификата шифрования
На каждом узле должен быть установлен сертификат шифрования. Вы можете использовать один и тот же сертификат для всех клиентов или создать уникальный для каждого клиента.

1.  Создание сертификата

    ```
    $subjectName = "EncryptedVirtualNetworks"
    $cryptographicProviderName = "Microsoft Base Cryptographic Provider v1.0";
    [int] $privateKeyLength = 1024;
    $sslServerOidString = "1.3.6.1.5.5.7.3.1";
    $sslClientOidString = "1.3.6.1.5.5.7.3.2";
    [int] $validityPeriodInYear = 5;

    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"
    $name.Encode("CN=" + $SubjectName, 0)

    #Generate Key
    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"
    $key.ProviderName = $cryptographicProviderName
    $key.KeySpec = 1 #X509KeySpec.XCN_AT_KEYEXCHANGE
    $key.Length = $privateKeyLength
    $key.MachineContext = 1
    $key.ExportPolicy = 0x2 #X509PrivateKeyExportFlags.XCN_NCRYPT_ALLOW_EXPORT_FLAG
    $key.Create()

    #Configure Eku
    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $serverauthoid.InitializeFromValue($sslServerOidString)
    $clientauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $clientauthoid.InitializeFromValue($sslClientOidString)
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"
    $ekuoids.add($serverauthoid)
    $ekuoids.add($clientauthoid)
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"
    $ekuext.InitializeEncode($ekuoids)

    # Set the hash algorithm to sha512 instead of the default sha1
    $hashAlgorithmObject = New-Object -ComObject X509Enrollment.CObjectId
    $hashAlgorithmObject.InitializeFromAlgorithmName( $ObjectIdGroupId.XCN_CRYPT_HASH_ALG_OID_GROUP_ID, $ObjectIdPublicKeyFlags.XCN_CRYPT_OID_INFO_PUBKEY_ANY, $AlgorithmFlags.AlgorithmFlagsNone, "SHA512")


    #Request Certificate
    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"

    $cert.InitializeFromPrivateKey(2, $key, "")
    $cert.Subject = $name
    $cert.Issuer = $cert.Subject
    $cert.NotBefore = (get-date).ToUniversalTime()
    $cert.NotAfter = $cert.NotBefore.AddYears($validityPeriodInYear);
    $cert.X509Extensions.Add($ekuext)
    $cert.HashAlgorithm = $hashAlgorithmObject
    $cert.Encode()

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"
    $enrollment.InitializeFromRequest($cert)
    $certdata = $enrollment.CreateRequest(0)
    $enrollment.InstallResponse(2, $certdata, 0, "")
    ```

    После выполнения скрипта в хранилище My появится новый сертификат:

    ```
    PS D:\> dir cert:\\localmachine\my
    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    84857CBBE7A1C851A80AE22391EB2C39BF820CE7  CN=MyNetwork
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks
    ```

1. Экспортируйте сертификат в файл.<p>Вам понадобятся две копии сертификата: один с закрытым ключом, а другой — нет.

    ```
   $subjectName = "EncryptedVirtualNetworks"
   $cert = Get-ChildItem cert:\localmachine\my | ? {$_.Subject -eq "CN=$subjectName"}
   [System.io.file]::WriteAllBytes("c:\$subjectName.pfx", $cert.Export("PFX", "secret"))
   Export-Certificate -Type CERT -FilePath "c:\$subjectName.cer" -cert $cert
    ```

3. Установите сертификаты на каждом узле Hyper-v.

    ```
    PS C:\> dir c:\$subjectname.*

    Directory: C:\

    Mode                LastWriteTime         Length Name
    ----                -------------         ------ ----
    -a----        9/22/2017   4:54 PM            543 EncryptedVirtualNetworks.cer
    -a----        9/22/2017   4:54 PM           1706 EncryptedVirtualNetworks.pfx
    ```

1. Установка на узле Hyper-V

    ```
    $server = "Server01"

    $subjectname = "EncryptedVirtualNetworks"
    copy c:\$SubjectName.* \\$server\c$
    invoke-command -computername $server -ArgumentList $subjectname,"secret" {
        param (
            [string] $SubjectName,
            [string] $Secret
        )
        $certFullPath = "c:\$SubjectName.cer"

        # create a representation of the certificate file
        $certificate = new-object System.Security.Cryptography.X509Certificates.X509Certificate2
        $certificate.import($certFullPath)

        # import into the store
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("Root", "LocalMachine")
        $store.open("MaxAllowed")
        $store.add($certificate)
        $store.close()

        $certFullPath = "c:\$SubjectName.pfx"
        $certificate = new-object System.Security.Cryptography.X509Certificates.X509Certificate2
        $certificate.import($certFullPath, $Secret, "MachineKeySet,PersistKeySet")

        # import into the store
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My", "LocalMachine")
        $store.open("MaxAllowed")
        $store.add($certificate)
        $store.close()

        # Important: Remove the certificate files when finished
        remove-item C:\$SubjectName.cer
        remove-item C:\$SubjectName.pfx
    }
    ```

5. Повторите эти действия для каждого сервера в вашей среде.<p>После повторения для каждого сервера должен быть установлен сертификат в корневом и моем хранилище каждого узла Hyper-V.

6. Проверьте установку сертификата.<p>Проверьте сертификаты, проверив содержимое хранилищ сертификатов My и root:

    ```
    PS C:\> enter-pssession Server1

    [Server1]: PS C:\> get-childitem cert://localmachine/my,cert://localmachine/root | ? {$_.Subject -eq "CN=EncryptedVirtualNetworks"}

    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\root

    Thumbprint                                Subject
    ----------                                -------
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks
    ```

7. Запишите отпечаток.<p>Необходимо заметку отпечатка, так как она понадобится для создания объекта учетных данных сертификата в сетевом контроллере.

## <a name="step-2-create-the-certificate-credential"></a>Шаг 2. Создание учетных данных сертификата

После установки сертификата на каждом из узлов Hyper-V, подключенных к сетевому контроллеру, необходимо настроить сетевой контроллер для его использования.  Для этого необходимо создать объект учетных данных, содержащий отпечаток сертификата на компьютере с установленными модулями PowerShell сетевого контроллера.

```
///Replace with the thumbprint from your certificate
$thumbprint = "5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6"

$uri = "https://nc.contoso.com"

///Replace with your Network Controller URI
Import-module networkcontroller

$credproperties = new-object Microsoft.Windows.NetworkController.CredentialProperties
$credproperties.Type = "X509Certificate"
$credproperties.Value = $thumbprint
New-networkcontrollercredential -connectionuri $uri -resourceid "EncryptedNetworkCertificate" -properties $credproperties -force
```

> [!TIP]
> Вы можете повторно использовать эти учетные данные для каждой зашифрованной виртуальной сети или развернуть и использовать уникальный сертификат для каждого клиента.

## <a name="step-3-configuring-a-virtual-network-for-encryption"></a>Шаг 3. Настройка виртуальной сети для шифрования

В этом шаге предполагается, что вы уже создали имя виртуальной сети "Моя сеть" и содержит по крайней мере одну виртуальную подсеть.  Сведения о создании виртуальных сетей см. в [статье Создание, удаление или обновление виртуальных сетей клиента](../Manage/Create,-Delete,-or-Update-Tenant-Virtual-Networks.md).

>[!NOTE]
>При взаимодействии с другой виртуальной машиной в той же подсети, подключенной в данный момент или подключенной позже, трафик шифруется автоматически.

1.  Извлеките виртуальные сети и объекты учетных данных из сетевого контроллера:

    ```
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "MyNetwork"
    $certcred = Get-NetworkControllerCredential -ConnectionUri $uri -ResourceId "EncryptedNetworkCertificate"
    ```

2.  Добавьте ссылку на учетные данные сертификата и включите шифрование для отдельных подсетей.

    ```
    $vnet.properties.EncryptionCredential = $certcred

    # Replace the Subnets index with the value corresponding to the subnet you want encrypted.
    # Repeat for each subnet where encryption is needed
    $vnet.properties.Subnets[0].properties.EncryptionEnabled = $true
    ```

3.  Вставьте обновленный объект виртуальной сети в сетевой контроллер:

    ```
    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId $vnet.ResourceId -Properties $vnet.Properties -force
    ```

*Поздравляем!* * Все действия выполняются после выполнения этих действий.