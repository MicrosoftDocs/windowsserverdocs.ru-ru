---
title: Установка HGS в существующем лесу бастиона
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 358fae9a9ee477537d3ee929ff81920175d58298
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766417"
---
# <a name="install-hgs-in-an-existing-bastion-forest"></a>Установка HGS в существующем лесу бастиона

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016


## <a name="join-the-hgs-server-to-the-existing-domain"></a>Присоединение сервера HGS к существующему домену

В существующем лесу бастиона необходимо добавить HGS в корневой домен. Используйте диспетчер сервера или [Add-Computer](https://go.microsoft.com/fwlink/?LinkId=821564) , чтобы присоединить сервер HGS к корневому домену.

## <a name="add-the-hgs-server-role"></a>Добавление роли сервера HGS

Выполните все команды в этом разделе в сеансе PowerShell с повышенными привилегиями.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)]

Если в центре обработки данных есть защищенный лес бастиона, в котором нужно присоединить узлы HGS, выполните следующие действия.
Эти действия также можно использовать для настройки 2 или более независимых кластеров HGS, присоединенных к одному и тому же домену.

## <a name="join-the-hgs-server-to-the-existing-domain"></a>Присоединение сервера HGS к существующему домену

Используйте диспетчер сервера или [Add-Computer](https://go.microsoft.com/fwlink/?LinkId=821564) , чтобы присоединить серверы HGS к нужному домену.

## <a name="prepare-active-directory-objects"></a>Подготовка Active Directory объектов

Создайте групповую управляемую учетную запись службы и 2 группы безопасности.
Вы также можете предварительно разместить объекты кластера, если у учетной записи, с помощью которой выполняется HGS, нет разрешения на создание объектов-компьютеров в домене.

## <a name="group-managed-service-account"></a>Групповая управляемая учетная запись службы

Групповая управляемая учетная запись службы (gMSA) — это удостоверение, используемое службой HGS для получения и использования своих сертификатов. Для создания gMSA используйте [New-адсервицеаккаунт](/powershell/module/addsadministration/new-adserviceaccount?view=win10-ps) .
Если это первый gMSA в домене, необходимо добавить корневой ключ службы распространения ключей.

Каждому узлу HGS необходимо разрешить доступ к паролю gMSA.
Самый простой способ настроить это — создать группу безопасности, содержащую все узлы HGS, и предоставить этой группе безопасности доступ для получения пароля gMSA.

Необходимо перезагрузить сервер HGS после его добавления в группу безопасности, чтобы убедиться, что он получает новое членство в группе.

```powershell
# Check if the KDS root key has been set up
if (-not (Get-KdsRootKey)) {
    # Adds a KDS root key effective immediately (ignores normal 10 hour waiting period)
    Add-KdsRootKey -EffectiveTime ((Get-Date).AddHours(-10))
}

# Create a security group for HGS nodes
$hgsNodes = New-ADGroup -Name 'HgsServers' -GroupScope DomainLocal -PassThru

# Add your HGS nodes to this group
# If your HGS server object is under an organizational unit, provide the full distinguished name instead of "HGS01"
Add-ADGroupMember -Identity $hgsNodes -Members "HGS01"

# Create the gMSA
New-ADServiceAccount -Name 'HGSgMSA' -DnsHostName 'HGSgMSA.yourdomain.com' -PrincipalsAllowedToRetrieveManagedPassword $hgsNodes
```

Для gMSA потребуется право на создание событий в журнале безопасности на каждом сервере HGS.
Если для настройки назначения прав пользователя используется групповая политика, убедитесь, что учетной записи gMSA предоставлено разрешение на [Создание событий аудита](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn221956%28v=ws.11%29) на серверах HGS.

> [!NOTE]
> Групповые управляемые учетные записи служб доступны начиная с схемы Active Directory Windows Server 2012.
> Дополнительные сведения см. в разделе [требования к групповой управляемой учетной записи службы](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431(v=ws.11)).

## <a name="jea-security-groups"></a>Группы безопасности JEA

При настройке HGS конечная точка PowerShell [достаточно простого администрирования (JEA)](/powershell/scripting/learn/remoting/jea/overview) разрешает администраторам управлять HGS без необходимости полных прав локального администратора.
Для управления HGS не требуется использовать JEA, но ее необходимо настроить при запуске команды Initialize-HgsServer.
Конфигурация конечной точки JEA состоит из двух групп безопасности, которые содержат администраторов HGS и проверяющих HGS.
Пользователи, входящие в группу администраторов, могут добавлять, изменять и удалять политики в HGS. Рецензенты могут только просматривать текущую конфигурацию.

Создайте 2 группы безопасности для этих групп JEA с помощью средств администрирования Active Directory или [New-ADGroup](/powershell/module/addsadministration/new-adgroup?view=win10-ps).

```powershell
New-ADGroup -Name 'HgsJeaReviewers' -GroupScope DomainLocal
New-ADGroup -Name 'HgsJeaAdmins' -GroupScope DomainLocal
```

## <a name="cluster-objects"></a>Объекты кластера

Если учетная запись, используемая для настройки HGS, не имеет разрешения на создание новых объектов-компьютеров в домене, необходимо предварительно разместить объекты кластера.
Эти шаги описаны в разделе [Предварительная настройка объектов компьютеров кластера в домен Active Directory Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn466519(v=ws.11)).

Чтобы настроить первый узел HGS, необходимо создать один объект имени кластера (CNO) и один объект виртуального компьютера (VCO).
CNO представляет имя кластера и используется в основном для внутренних целей посредством отказоустойчивой кластеризации.
Объект VCO представляет службу HGS, которая находится на вершине кластера и будет являться именем, зарегистрированным на DNS-сервере.

> [!IMPORTANT]
> Пользователь, который будет запускаться, `Initialize-HgsServer` должен иметь **полный контроль** над объектами CNO и VCO в Active Directory.

Чтобы быстро подготовить CNO и VCO, у администратора Active Directory выполните следующие команды PowerShell:

```powershell
# Create the CNO
$cno = New-ADComputer -Name 'HgsCluster' -Description 'HGS CNO' -Enabled $false -Passthru

# Create the VCO
$vco = New-ADComputer -Name 'HgsService' -Description 'HGS VCO' -Passthru

# Give the CNO full control over the VCO
$vcoPath = Join-Path "AD:\" $vco.DistinguishedName
$acl = Get-Acl $vcoPath
$ace = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $cno.SID, "GenericAll", "Allow"
$acl.AddAccessRule($ace)
Set-Acl -Path $vcoPath -AclObject $acl

# Allow time for your new CNO and VCO to replicate to your other Domain Controllers before continuing
```

## <a name="security-baseline-exceptions"></a>Исключения базовых показателей безопасности

Если вы развертываете HGS в сильно заблокированной среде, некоторые параметры групповая политика могут препятствовать нормальной работе HGS.
Проверьте объекты групповая политика на наличие следующих параметров и следуйте указаниям, если они затрагиваются.

### <a name="network-logon"></a>Вход в сеть

**Путь политики:** Конфигурация компьютера \ параметры безопасности \ локальные политики \ назначение прав Policies\User

**Имя политики:** Запретить доступ к этому компьютеру из сети

**Обязательное значение:** Убедитесь, что значение не блокирует вход в сеть для всех локальных учетных записей. Однако вы можете безопасно блокировать учетные записи локального администратора.

**Причина:** Отказоустойчивая кластеризация использует локальную учетную запись без прав администратора с именем КЛИУСР для управления узлами кластера. Блокировка сетевого входа для этого пользователя приведет к неправильной работе кластера.

### <a name="kerberos-encryption"></a>Шифрование Kerberos

**Путь политики:** Конфигурация компьютера \ параметры безопасности \ локальные режимы политики

**Имя политики:** Сетевая безопасность: Настройка типов шифрования, разрешенных для Kerberos

**Действие**. Если эта политика настроена, необходимо обновить учетную запись gMSA с помощью [Set-адсервицеаккаунт](/powershell/module/addsadministration/set-adserviceaccount?view=win10-ps) , чтобы использовать в этой политике только поддерживаемые типы шифрования. Например, если политика допускает только AES128 \_ HMAC \_ SHA1 и AES256 \_ HMAC \_ SHA1, следует запустить `Set-ADServiceAccount -Identity HGSgMSA -KerberosEncryptionType AES128,AES256` .



## <a name="next-steps"></a>Дальнейшие действия

- Дальнейшие действия по настройке аттестации на основе TPM см. в статье [Инициализация кластера HGS с помощью режима TPM в существующем лесу бастиона](guarded-fabric-initialize-hgs-tpm-mode-bastion.md).
- Дальнейшие действия по настройке аттестации ключа узла см. в статье [Инициализация кластера HGS с помощью режима ключей в существующем лесу бастиона](guarded-fabric-initialize-hgs-key-mode-bastion.md).
- Дальнейшие действия по настройке аттестации на основе администратора (не рекомендуется в Windows Server 2019) см. в статье [Инициализация кластера HGS с помощью режима AD в существующем лесу бастиона](guarded-fabric-initialize-hgs-ad-mode-bastion.md).