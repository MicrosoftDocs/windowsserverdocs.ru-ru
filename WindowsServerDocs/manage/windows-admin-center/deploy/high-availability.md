---
title: Развертывание Windows Admin Center с высоким уровнем доступности
description: Развертывание Windows Admin Center с высоким уровнем доступности (проект Honolulu)
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.openlocfilehash: 132f566e8467179c1a58e3555d26ab834dae7129
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970861"
---
# <a name="deploy-windows-admin-center-with-high-availability"></a>Развертывание Windows Admin Center с высоким уровнем доступности

>Область применения. Windows Admin Center, ознакомительная версия Windows Admin Center

Windows Admin Center можно развернуть в отказоустойчивом кластере, чтобы обеспечить высокий уровень доступности для службы шлюза Windows Admin Center. Мы предлагаем решение типа "активный/пассивный", в котором активным является только один экземпляр Windows Admin Center. В случае сбоя одного из узлов кластера Windows Admin Center корректно переключается на другой узел, сохраняя для вас возможность управлять серверами в своей среде.

[Сведения о других вариантах развертывания Windows Admin Center.](../plan/installation-options.md)

## <a name="prerequisites"></a>Предварительные условия

- Отказоустойчивый кластер с двумя или более узлами под управлением Windows Server 2016 или 2019. [Сведения о развертывании отказоустойчивого кластера](../../../failover-clustering/failover-clustering-overview.md).
- Общий том кластера (CSV) для Windows Admin Center, где будут храниться постоянные данные, доступные со всех узлов кластера. Для общего тома кластера достаточно размера 10 ГБ.
- Скрипт развертывания Windows Admin Center с высоким уровнем доступности в виде [ZIP-файла](https://aka.ms/WACHAScript). Скачайте ZIP-файл с этим скриптом на локальный компьютер и скопируйте нужный скрипт в соответствии с приведенными ниже инструкциями.
- Рекомендуется, но необязательно: подписанный сертификат в PFX-файле и пароль к нему. Вам не нужно предварительно устанавливать этот сертификат на узлах кластера, скрипт сделает это автоматически. Если сертификат не указан, скрипт установки создаст самозаверяющий сертификат со сроком действия 60 дней.

## <a name="install-windows-admin-center-on-a-failover-cluster"></a>Установка Windows Admin Center в отказоустойчивом кластере

1. Скопируйте скрипт ```Install-WindowsAdminCenterHA.ps1``` на любой узел кластера. Скачайте или скопируйте MSI-файл для Windows Admin Center на тот же узел.
2. Подключитесь к этому узлу про протоколу удаленного рабочего стола и запустите на нем скрипт ```Install-WindowsAdminCenterHA.ps1``` со следующими параметрами.
    - `-clusterStorage`: локальный путь к общему тому кластера для хранения данных Windows Admin Center.
    - `-clientAccessPoint`: имя, которое будет использоваться для доступа к Windows Admin Center. Например, выполнив этот скрипт с параметром `-clientAccessPoint contosoWindowsAdminCenter`, для доступа к службе Windows Admin Center нужно будет использовать адрес `https://contosoWindowsAdminCenter.<domain>.com`.
    - `-staticAddress`: Необязательный параметр. Один или несколько статических адресов для универсальной службы кластера.
    - `-msiPath`: Путь к MSI-файлу для Windows Admin Center.
    - `-certPath`: Необязательный параметр. Путь к PFX-файлу сертификата.
    - `-certPassword`: Необязательный параметр. Пароль SecureString для PFX-файла сертификата, указанный в параметре `-certPath`.
    - `-generateSslCert`: Необязательный параметр. Если вы не хотите предоставлять подписанный сертификат, включите в параметры этот флаг, чтобы создать самозаверяющий сертификат. Обратите внимание, что срок действия самозаверяющего сертификата истекает через 60 дней.
    - `-portNumber`: Необязательный параметр. Если порт не указан, служба шлюза развертывается на порту 443 (HTTPS). Чтобы использовать другой порт, укажите его в этом параметре. Обратите внимание, что при использовании настраиваемого порта (отличного от 443) вам придется обращаться к Windows Admin Center по адресу https://\<clientAccessPoint\>:\<port\>.

> [!NOTE]
> Скрипт ```Install-WindowsAdminCenterHA.ps1``` поддерживает параметры ```-WhatIf ``` и ```-Verbose```.

### <a name="examples"></a>Примеры

#### <a name="install-with-a-signed-certificate"></a>Установка с подписанным сертификатом:

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### <a name="install-with-a-self-signed-certificate"></a>Установка с самозаверяющим сертификатом:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## <a name="update-an-existing-high-availability-installation"></a>Обновление существующей установки с высоким уровнем доступности

Тот же самый скрипт ```Install-WindowsAdminCenterHA.ps1``` позволяет обновить развертывание с высоким уровнем доступности, не теряя данные подключения.

### <a name="update-to-a-new-version-of-windows-admin-center"></a>Обновление до новой версии Windows Admin Center

При выпуске новой версии Windows Admin Center просто запустите скрипт ```Install-WindowsAdminCenterHA.ps1``` с одним параметром ```msiPath```:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### <a name="update-the-certificate-used-by-windows-admin-center"></a>Обновление сертификата, используемого в Windows Admin Center

Вы можете в любое время обновить сертификат, используемый в развертывании Windows Admin Center с высоким уровнем доступности, указав PFX-файл и пароль нового сертификата.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

Вы также можете обновить сертификат одновременно с обновлением платформы Windows Admin Center с помощью нового MSI-файла.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

## <a name="uninstall"></a>Uninstall

Чтобы удалить из отказоустойчивого кластера развертывание Windows Admin Center с высоким уровнем доступности, передайте в скрипт ```Install-WindowsAdminCenterHA.ps1``` параметр ```-Uninstall```.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## <a name="troubleshooting"></a>Диагностика

Журналы сохраняются в папке temp на общем томе кластера (например, C:\ClusterStorage\Volume1\temp).