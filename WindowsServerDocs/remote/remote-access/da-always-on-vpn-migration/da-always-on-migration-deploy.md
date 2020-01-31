---
title: Миграция с DirectAccess на Always On VPN
description: Миграция с DirectAccess на Always On VPN требует определенного процесса миграции клиентов, что помогает свести к минимуму состояние гонки, возникающее из-за неупорядоченного выполнения этапов миграции.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 06/07/2018
ms.openlocfilehash: 2bcbc7030d54e96b4ac120b943cc1adc0513feca
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822646"
---
# <a name="migrate-to-always-on-vpn-and-decommission-directaccess"></a>Вывод профиля DirectAccess из эксплуатации и его перенос в постоянно подключенный VPN-профиль

>Область применения: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows 10

&#171;[ **Назад.** планирование DirectAccess для Always on миграции VPN](da-always-on-migration-planning.md)<br>

Миграция с DirectAccess на Always On VPN требует определенного процесса миграции клиентов, что помогает свести к минимуму состояние гонки, возникающее из-за неупорядоченного выполнения этапов миграции. На высоком уровне процесс миграции состоит из следующих четырех основных этапов:

1.  **Развертывание параллельной инфраструктуры VPN.** Определив этапы миграции и компоненты, которые необходимо включить в развертывание, инфраструктура VPN будет развернута параллельно с существующей инфраструктурой DirectAccess.  

2.  **Развертывание сертификатов и конфигурации на клиентах.**  Когда инфраструктура VPN будет готова, вы создадите и опубликуете необходимые сертификаты для клиента. Когда клиенты получили сертификаты, вы развертываете скрипт конфигурации VPN_Profile. ps1. Кроме того, для настройки VPN-клиента можно использовать Intune. Чтобы отслеживать успешные развертывания конфигурации VPN, используйте Configuration Manager или Microsoft Intune конечной точки Майкрософт.

3.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

Прежде чем начать процесс миграции с DirectAccess на Always On VPN, убедитесь, что вы планируете выполнить миграцию.  Если вы еще не запланировали миграцию, см. статью [Планирование DirectAccess для Always on миграции VPN](da-always-on-migration-planning.md).

>[!TIP] 
>Этот раздел не является пошаговым руководством по развертыванию Always On VPN, а предназначен для дополнения [Always on развертывания VPN для Windows Server и Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) и предоставления руководств по развертыванию, относящегося к миграции.

## <a name="deploy-a-side-by-side-vpn-infrastructure"></a>Развертывание параллельной инфраструктуры VPN

Инфраструктура VPN развертывается параллельно с существующей инфраструктурой DirectAccess.  Пошаговые инструкции см. в разделе [Always on развертывание VPN для Windows Server и Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md) для установки и настройки Always on инфраструктуры VPN. 

Параллельное развертывание включает следующие высокоуровневые задачи:

1.  Создайте группы VPN-пользователей, VPN-серверов и серверов политики сети.

2.  Создайте и опубликуйте необходимые шаблоны сертификатов.

3.  Регистрация сертификатов сервера.

4.  Установите и настройте службу удаленного доступа для Always On VPN.

5.  Установите и настройте NPS.

6.  Настройте DNS и правила брандмауэра для Always On VPN.

На следующем рисунке представлена визуальная ссылка на изменения инфраструктуры в рамках миграции с DirectAccess на Always On VPN.

![](../../media/DA-to-AlwaysOnVPN/6b64f322f945f837f22a32bf87a228f8.png)

## <a name="deploy-certificates-and-vpn-configuration-script-to-the-clients"></a>Развертывание сертификатов и скрипта конфигурации VPN для клиентов

Несмотря на то, что основная часть конфигурации VPN-клиента в разделе [Deploy Always on VPN](../vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment.md) , необходимо выполнить два дополнительных действия для завершения миграции с DirectAccess на успешное Always on VPN. 

Необходимо убедиться, что **VPN_Profile. ps1** приходит _после_ выдачи сертификата, чтобы VPN-клиент не пытался подключиться без него. Для этого выполните сценарий, добавляющий только тех пользователей, которые зарегистрированы в сертификате в группе готовности к развертыванию VPN, которая используется для развертывания конфигурации Always On VPN.

>[!NOTE] 
>Корпорация Майкрософт рекомендует протестировать этот процесс, прежде чем выполнять его на всех кольцах миграции пользователей.

1.  **Создайте и опубликуйте сертификат VPN и включите объект автоматической регистрации групповая политика объекта (GPO).** Для традиционных VPN-развертываний Windows 10 на основе сертификатов сертификат выдается либо устройству, либо пользователю, чтобы он мог проверить подлинность подключения. Когда новый сертификат проверки подлинности создается и публикуется для автоматической регистрации, необходимо создать и развернуть объект групповой политики с параметром автоматической регистрации, настроенным для группы "пользователи VPN". Действия по настройке сертификатов и автоматической регистрации см. в статье [Настройка серверной инфраструктуры](../vpn/always-on-vpn/deploy/vpn-deploy-server-infrastructure.md).

2.  **Добавьте пользователей в группу VPN-пользователей.** Добавьте пользователей, которые вы переносите в группу "пользователи VPN". Эти пользователи остаются в этой группе безопасности после миграции, чтобы они могли получать обновления сертификатов в будущем. Продолжайте добавлять пользователей в эту группу, пока вы не переместит каждого пользователя из DirectAccess в Always On VPN. 

3.  **Идентификация пользователей, получивших сертификат проверки подлинности VPN.** Вы выполняете миграцию из DirectAccess, поэтому необходимо добавить метод для определения момента получения клиентом необходимого сертификата и готовности к получению сведений о конфигурации VPN. Выполните сценарий **жетусерсвисцерт. ps1** , чтобы добавить пользователей, которые в данный момент выдавали неотозванные сертификаты, исходящие из указанного имени шаблона, в указанную группу безопасности AD DS. Например, после выполнения скрипта **жетусерсвисцерт. ps1** любой пользователь, выдавший действительный сертификат из шаблона сертификата проверки подлинности VPN, добавляется в группу готовности к развертыванию VPN.

    >[!NOTE] 
    >Если у вас нет метода для обнаружения того, когда клиент получил требуемый сертификат, можно развернуть конфигурацию VPN до выдачи сертификата пользователю, что приведет к сбою VPN-подключения. Чтобы избежать этой ситуации, запустите сценарий **жетусерсвисцерт. ps1** в центре сертификации или по расписанию, чтобы синхронизировать пользователей, получивших сертификат в группу "готовность к развертыванию VPN". Затем эта группа безопасности будет использоваться для развертывания конфигурации VPN в Microsoft Endpoint Configuration Manager или Intune, что гарантирует, что управляемый клиент не получит конфигурацию VPN до получения сертификата.
    
    ### <a name="getuserswithcertps1"></a>Жетусерсвисцерт. ps1
    
    ```powershell
    Import-module ActiveDirectory
    Import-Module AdcsAdministration
    
    $TemplateName = 'VPNUserAuthentication'##Certificate Template Name (not the friendly name)
    $GroupName = 'VPN Deployment Ready' ##Group you will add the users to
    $CSServerName = 'localhost\corp-dc-ca' ##CA Server Information
    
    $users= @()
    $TemplateID = (get-CATemplate | Where-Object {$_.Name -like $TemplateName} | Select-Object oid).oid
    $View = New-Object -ComObject CertificateAuthority.View
    $NULL = $View.OpenConnection($CSServerName)
    $View.SetResultColumnCount(3)
    $i1 = $View.GetColumnIndex($false, "User Principal Name")
    $i2 = $View.GetColumnIndex($false, "Certificate Template")
    $i3 = $View.GetColumnIndex($false, "Revocation Date")
    $i1, $i2, $i3 | %{$View.SetResultColumn($_) }
    $Row= $View.OpenView()
    
    while ($Row.Next() -ne -1){
    $Cert = New-Object PsObject
    $Col = $Row.EnumCertViewColumn()
    [void]$Col.Next()
    do {
    $Cert | Add-Member -MemberType NoteProperty $($Col.GetDisplayName()) -Value $($Col.GetValue(1)) -Force
          }
    until ($Col.Next() -eq -1)
    $col = ''
    
    if($cert."Certificate Template" -eq $TemplateID -and $cert."Revocation Date" -eq $NULL){
       $users= $users+= $cert."User Principal Name"
    $temp = $cert."User Principal Name"
    $user = get-aduser -Filter {UserPrincipalName -eq $temp} –Property UserPrincipalName
    Add-ADGroupMember $GroupName $user
       }
      }
    ```

4. Разверните Always On конфигурацию VPN. Когда выдаются сертификаты проверки подлинности VPN и выполняется сценарий **жетусерсвисцерт. ps1** , пользователи добавляются в группу безопасности "готовность к РАЗВЕРТЫВАНИю VPN".


| Если вы используете...  | То... |
| ---- | ---- |
| Configuration Manager | Создайте коллекцию пользователей на основе членства в этой группе безопасности.<br><br>![](../../media/DA-to-AlwaysOnVPN/b38723b3ffcfacd697b83dd41a177f66.png)\!|
| Intune | Просто нацеливание на группу безопасности непосредственно после ее синхронизации. |
|
    
Каждый раз при запуске скрипта конфигурации **жетусерсвисцерт. ps1** необходимо также запустить правило обнаружения AD DS, чтобы обновить членство в группе безопасности в Configuration Manager. Кроме того, убедитесь, что обновление членства для коллекции развертывания часто встречается достаточно (в соответствии с правилом скрипта и обнаружения).

Дополнительные сведения об использовании Configuration Manager или Intune для развертывания Always On VPN на клиентах Windows см. в статье [Always on развертывание VPN для Windows Server и Windows 10](../vpn/always-on-vpn/deploy/always-on-vpn-deploy.md). Однако следует убедиться, что для включения этих задач, связанных с миграцией.

>[!NOTE] 
>Включение этих задач, связанных с миграцией, является важным различием между простым Always On развертыванием VPN и миграцией из DirectAccess в Always On VPN. Не забудьте правильно определить коллекцию для группы безопасности, а не использовать метод в разделе руководств по развертыванию.


## <a name="remove-devices-from-the-directaccess-security-group"></a>Удаление устройств из группы безопасности DirectAccess

Когда пользователи получают сертификат проверки подлинности и сценарий настройки **VPN_Profile. ps1** , вы увидите соответствующие успешные развертывания скриптов конфигурации VPN в Configuration Manager или Intune. После каждого развертывания удалите устройство этого пользователя из группы безопасности DirectAccess, чтобы позже можно было удалить DirectAccess. Intune и Configuration Manager содержат сведения о назначении устройств пользователя, помогающие определить устройство каждого пользователя.

>[!NOTE] 
>При применении объектов групповой политики DirectAccess с помощью подразделений (OU), а не групп компьютеров, переместите объект компьютера пользователя из подразделения.

## <a name="decommission-the-directaccess-infrastructure"></a>Списание инфраструктуры DirectAccess

После завершения миграции всех клиентов DirectAccess на Always On VPN можно списать инфраструктуру DirectAccess и удалить параметры DirectAccess из групповая политика. Для корректного удаления DirectAccess из среды корпорация Майкрософт рекомендует выполнить следующие действия:

1.  [!INCLUDE [remove-config-settings-shortdesc-include](../includes/remove-config-settings-shortdesc-include.md)]

    ![](../../media/DA-to-AlwaysOnVPN/dbdc3d80e8dc1b8665f7b15d7d2ee1f6.png)

2.  [!INCLUDE [remove-da-security-group-shortdesc-include](../includes/remove-da-security-group-shortdesc-include.md)]

3.  **Очистите DNS.** Не забудьте удалить все записи из внутреннего DNS-сервера и общедоступного DNS-сервера, связанного с DirectAccess, например DA.contoso.com, DAGateway.contoso.com.

4.  [!INCLUDE [decommission-da-shortdesc-include](../includes/decommission-da-shortdesc-include.md)]

5.  **Удалите все сертификаты DirectAccess из служб Active Directory Certificate Services.** Если для реализации DirectAccess использовались сертификаты компьютеров, удалите опубликованные шаблоны из папки шаблоны сертификатов в консоли центра сертификации.

## <a name="next-step"></a>Далее
Миграция с DirectAccess выполнена на Always On VPN. 

---