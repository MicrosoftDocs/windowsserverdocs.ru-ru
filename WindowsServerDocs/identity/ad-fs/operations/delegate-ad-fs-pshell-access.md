---
title: Делегирование доступа к командлету Powershell AD FS пользователям без прав администратора
description: В этом документе десЦирбес, как делегировать разрешения не являющимся администраторами для AD FS PowerShell котором описана.
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: zhvolosh
ms.date: 01/31/2019
ms.topic: article
ms.openlocfilehash: 836a40ffa9df8fa308d1005fbac3a9e087488949
ms.sourcegitcommit: 52a8d5d7e969eaa07fd3a45ed6d3cb5a5173b6d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "88970631"
---
# <a name="delegate-ad-fs-powershell-commandlet-access-to-non-admin-users"></a>Делегирование доступа к командлету Powershell AD FS пользователям без прав администратора
По умолчанию AD FS администрирование с помощью PowerShell может быть выполнено только администратором AD FS. Во многих крупных организациях это может не быть реальной рабочей моделью при работе с другими персонажами, такими как персонал службы поддержки.

Благодаря достаточному администрированию (JEA) клиенты теперь могут делегировать определенные командлеты различным группам персонала.
Хорошим примером этого варианта использования является разрешение сотрудникам службы поддержки запрашивать AD FS состояние блокировки учетной записи и сбрасывать состояние блокировки учетной записи в AD FS после того, как пользователь проверены. В этом случае командлеты, которые должны быть делегированы, — это:
- `Get-ADFSAccountActivity`
- `Set-ADFSAccountActivity`
- `Reset-ADFSAccountLockout`

Мы используем этот пример в оставшейся части этого документа. Тем не менее, можно настроить таким же настройку, чтобы разрешить делегирование установки свойств проверяющих сторон и передать их владельцам приложений в Организации.


##  <a name="create-the-required-groups-necessary-to-grant-users-permissions"></a>Создание необходимых групп, необходимых для предоставления пользователям разрешений
1. Создайте [групповую управляемую учетную запись службы](../../../security/group-managed-service-accounts/group-managed-service-accounts-overview.md). Учетная запись gMSA используется для предоставления пользователю JEA доступа к сетевым ресурсам в качестве других компьютеров или веб-служб. Он предоставляет удостоверение домена, которое можно использовать для проверки подлинности ресурсов на любом компьютере в домене. Учетная запись gMSA предоставляет необходимые административные права позже в программе установки. В этом примере мы вызываем учетную запись **гмсаконтосо**.
2. Создание группы Active Directory может быть заполнено пользователями, которым должны быть предоставлены права на делегированные команды. В этом примере сотрудникам службы поддержки предоставляются разрешения на чтение, обновление и сброс состояния блокировки ADFS. Мы будем называть эту группу по всему примеру как **жеаконтосо**.

### <a name="install-the-gmsa-account-on-the-adfs-server"></a>Установите учетную запись gMSA на сервере ADFS:
Создайте учетную запись службы с правами администратора на серверах ADFS. Это может быть выполнено на контроллере домена или удаленно при условии, что пакет AD RSAT установлен.Учетная запись службы должна быть создана в том же лесу, что и сервер ADFS.
Измените примеры значений в конфигурации фермы.

```powershell
 # This command should only be run if this is the first time gMSA accounts are enabled in the forest
Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10)) 

# Run this on every node that you want to have JEA configured on
$adfsServer = Get-ADComputer server01.contoso.com

# Run targeted at domain controller
$serviceaccount = New-ADServiceAccount gMSAcontoso -DNSHostName <FQDN of the domain containing the KDS key> - PrincipalsAllowedToRetrieveManagedPassword $adfsServer –passthru

# Run this on every node
Add-ADComputerServiceAccount -Identity server01.contoso.com -ServiceAccount $ServiceAccount
```

Установите учетную запись gMSA на сервере ADFS.Это необходимо выполнить на каждом узле ADFS в ферме.

```powershell
Install-ADServiceAccount gMSAcontoso
```

### <a name="grant-the-gmsa-account-admin-rights"></a>Предоставление прав администратора учетной записи gMSA
Если ферма использует делегированное администрирование, предоставьте права администратора учетной записи gMSA, добавив ее в существующую группу с делегированным доступом администратора.

Если ферма не использует делегированное администрирование, предоставьте права администратора учетной записи gMSA, сделав ее локальной группой администрирования на всех серверах ADFS.


### <a name="create-the-jea-role-file"></a>Создание файла роли JEA

На AD FS сервере создайте роль JEA в файле блокнота. Инструкции по созданию роли предоставляются в разделе [возможности роли JEA](https://docs.microsoft.com/powershell/scripting/learn/remoting/jea/role-capabilities).

Командлеты, делегированный в этом примере, — это `Reset-AdfsAccountLockout, Get-ADFSAccountActivity, and Set-ADFSAccountActivity` .

Пример роли JEA, делегирующий доступ к параметрам "Reset-Адфсаккаунтлоккаут", "Get-Адфсаккаунтактивити" и "Set-Адфсаккаунтактивити" командлеты:

```powershell
@{
GUID = 'b35d3985-9063-4de5-81f8-241be1f56b52'
ModulesToImport = 'adfs'
VisibleCmdlets = 'Reset-AdfsAccountLockout', 'Get-ADFSAccountActivity', 'Set-ADFSAccountActivity'
}
```


### <a name="create-the-jea-session-configuration-file"></a>Создание файла конфигурации сеанса JEA
Следуйте инструкциям по созданию файла [конфигурации сеанса JEA](https://docs.microsoft.com/powershell/scripting/learn/remoting/jea/session-configurations) . Файл конфигурации определяет, кто может использовать конечную точку JEA, и какие возможности они имеют к ним доступ.

На возможности роли ссылается неструктурированное имя (имя файла без расширения) файла возможностей роли. Если в системе доступно несколько возможностей роли с одинаковыми неструктурированными именами, PowerShell использует неявный порядок поиска, чтобы выбрать эффективный файл возможностей роли. Он не предоставляет доступ ко всем файлам возможностей роли с тем же именем.

Чтобы указать файл возможностей роли с путем, используйте `RoleCapabilityFiles` аргумент. Для вложенной папки JEA ищет допустимые модули PowerShell, содержащие `RoleCapabilities` вложенную папку, где `RoleCapabilityFiles` аргумент должен быть изменен на `RoleCapabilities` .

Пример файла конфигурации сеанса:

```powershell
@{
SchemaVersion = '2.0.0.0'
GUID = '54c8d41b-6425-46ac-a2eb-8c0184d9c6e6'
SessionType = 'RestrictedRemoteServer'
GroupManagedServiceAccount =  'CONTOSO\gMSAcontoso'
RoleDefinitions = @{ JEAcontoso = @{ RoleCapabilityFiles = 'C:\Program Files\WindowsPowershell\Modules\AccountActivityJEA\RoleCapabilities\JEAAccountActivityResetRole.psrc' } }
}
```

Сохраните файл конфигурации сеанса.

Настоятельно рекомендуется [протестировать файл конфигурации сеанса](/powershell/module/microsoft.powershell.core/test-pssessionconfigurationfile) , если вы редактировали файл pssc вручную с помощью текстового редактора, чтобы убедиться в правильности синтаксиса. Если файл конфигурации сеанса не прошел проверку, он не будет успешно зарегистрирован в системе.

### <a name="install-the-jea-session-configuration-on-the-ad-fs-server"></a>Установка конфигурации сеанса JEA на сервере AD FS

Установка конфигурации сеанса JEA на сервере AD FS

```powershell
Register-PSSessionConfiguration -Path .\JEASessionConfig.pssc -name "AccountActivityAdministration" -force
```
## <a name="operational-instructions"></a>Операционные инструкции
После настройки можно использовать ведение журнала JEA и аудит, чтобы определить, имеют ли правильные пользователи доступ к конечной точке JEA.

Чтобы использовать делегированные команды, выполните следующие действия.

```powershell
Enter-pssession -ComputerName server01.contoso.com -ConfigurationName "AccountActivityAdministration" -Credential <User Using JEA>
Get-AdfsAccountActivity <User>


```
