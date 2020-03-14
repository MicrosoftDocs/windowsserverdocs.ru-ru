---
title: Создание ключа узла и добавление его в HGS
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 2aea6c8416a0f3af04ad6056c5d09a4d07708eaa
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322016"
---
# <a name="create-a-host-key-and-add-it-to-hgs"></a>Создание ключа узла и добавление его в HGS

>Область применения: Windows Server 2019


В этом разделе описывается подготовка узлов Hyper-V к защищенным узлам с помощью аттестации ключа узла (режим ключей). Вы создадите пару ключей узла (или используйте существующий сертификат) и добавите открытую половину ключа в HGS.

## <a name="create-a-host-key"></a>Создание ключа узла

1.  Установите Windows Server 2019 на компьютере узла Hyper-V.
2.  Установите компоненты поддержки Hyper-V для Hyper-V и службы защиты узла:

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ``` 

3.  Автоматическое создание ключа узла или выбор существующего сертификата. Если вы используете пользовательский сертификат, он должен иметь по крайней мере 2048-разрядный ключ RSA, EKU проверки подлинности клиента и использование ключа цифровой подписи.

    ```powershell
    Set-HgsClientHostKey
    ```

    Кроме того, можно указать отпечаток, если вы хотите использовать собственный сертификат. 
    Это может быть полезно, если требуется предоставить общий доступ к сертификату на нескольких компьютерах или использовать сертификат, привязанный к доверенному платформенному модулю или HSM. Ниже приведен пример создания сертификата, привязанного к доверенному платформенному модулю (который предотвращает кражу и использование закрытого ключа на другом компьютере и требует только доверенного платформенного модуля 1,2):

    ```powershell
    $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
    Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
    ```

4.  Получите открытую половину ключа, чтобы предоставить серверу HGS. Можно использовать следующий командлет или, если у вас есть сертификат, хранящийся в других местах, укажите CER-элемент, содержащий открытую половину ключа. Обратите внимание, что мы сохраняем и проверяем только открытый ключ в HGS; Мы не храним сведения о сертификате и не проверили цепочку сертификатов или дату истечения срока действия.

    ```powershell
    Get-HgsClientHostKey -Path "C:\temp\$env:hostname-HostKey.cer"
    ```

5.  Скопируйте CER файл на сервер HGS.

## <a name="add-the-host-key-to-the-attestation-service"></a>Добавление ключа узла в службу аттестации

Этот шаг выполняется на сервере HGS и позволяет узлу запускать экранированные виртуальные машины. Рекомендуется присвоить имени полное доменное имя или идентификатор ресурса хост-компьютера, чтобы можно было легко указывать на узел, на котором установлен ключ.

```powershell
Add-HgsAttestationHostKey -Name MyHost01 -Path "C:\temp\MyHost01-HostKey.cer"
``` 

## <a name="next-step"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Подтверждение успешной аттестации узлов](guarded-fabric-confirm-hosts-can-attest-successfully.md)

## <a name="see-also"></a>См. также:

- [Развертывание службы защиты узла для защищенных узлов и экранированных виртуальных машин](guarded-fabric-deploying-hgs-overview.md)
