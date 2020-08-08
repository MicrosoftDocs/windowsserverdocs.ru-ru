---
ms.assetid: fe05e52c-cbf8-428b-8176-63407991042f
title: Advanced Active Directory Replication and Topology Management Using Windows PowerShell (Level 200)
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 058e1ba1cd68c1d33aee6e85dfb0de572a480d26
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967981"
---
# <a name="advanced-active-directory-replication-and-topology-management-using-windows-powershell-level-200"></a>Advanced Active Directory Replication and Topology Management Using Windows PowerShell (Level 200)

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этом разделе подробно описываются новые командлеты для управления репликацией и топологией доменных служб Active Directory и приводятся дополнительные примеры. Общие сведения см. в статьях [Общие сведения об Active Directory репликации и управлении топологией с помощью Windows PowerShell &#40;уровня 100&#41;](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md).

1. [Введение](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Intro)

2. [Репликация и метаданные](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Repl)

3. [Get-ADReplicationAttributeMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplAttrMD)

4. [Get-ADReplicationPartnerMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_PartnerMD)

5. [Get-ADReplicationFailure](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplFail)

6. [Get-ADReplicationQueueOperation и Get-ADReplicationUpToDatenessVectorTable](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplQueue)

7. [Sync-ADObject](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Sync)

8. [Топология](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Topo)

## <a name="introduction"></a><a name="BKMK_Intro"></a>Введение
В Windows Server 2012 модуль Active Directory для Windows PowerShell расширен двадцатью пятью новыми командлетами, предназначенными для управления репликацией и топологией леса. До этого были вынуждены использовать существительные Generic ** \* -адобжект** или вызывайте функции .NET.

Как и все командлеты Windows PowerShell для Active Directory, эти новые командлеты требуют установки [службы шлюза управления Active Directory](https://www.microsoft.com/download/details.aspx?displaylang=en&id=2852) по крайней мере на одном контроллере домена (а лучше на всех).

В таблице ниже перечислены новые командлеты управления репликацией и топологией, добавленные в модуль Active Directory для Windows PowerShell.

| Командлет | Описание |
|--|--|
| Get-ADReplicationAttributeMetadata | Возвращает метаданные репликации атрибутов для объекта. |
| Get-ADReplicationConnection | Возвращает сведения об объекте подключения к контроллеру домена. |
| Get-ADReplicationFailure | Возвращает сведения о последнем сбое репликации для домена контроллера. |
| Get-ADReplicationPartnerMetadata | Возвращает конфигурацию репликации для контроллера домена. |
| Get-ADReplicationQueueOperation | Возвращает текущую невыполненную часть очереди репликации. |
| Get-ADReplicationSite | Возвращает сведения о сайте. |
| Get-ADReplicationSiteLink | Возвращает сведения о связи сайта. |
| Get-ADReplicationSiteLinkBridge | Возвращает сведения о мосте связей сайтов. |
| Get-ADReplicationSubnet | Возвращает сведения о подсети Active Directory. |
| Get-ADReplicationUpToDatenessVectorTable | Возвращает сведения о векторе UTD для контроллера домена. |
| Get-ADTrust | Возвращает сведения об отношении доверия между доменами или лесами. |
| New-ADReplicationSite | Создает сайт. |
| New-ADReplicationSiteLink | Создает связь сайтов. |
| New-ADReplicationSiteLinkBridge | Создает мост связей сайтов. |
| New-ADReplicationSubnet | Создает подсеть Active Directory. |
| Remove-ADReplicationSite | Удаляет сайт. |
| Remove-ADReplicationSiteLink | Удаляет связь сайтов. |
| Remove-ADReplicationSiteLinkBridge | Удаляет мост связей сайтов. |
| Remove-ADReplicationSubnet | Удаляет подсеть Active Directory. |
| Set-ADReplicationConnection | Изменяет подключение. |
| Set-ADReplicationSite | Изменяет сайт. |
| Set-ADReplicationSiteLink | Изменяет связь сайтов. |
| Set-ADReplicationSiteLinkBridge | Изменяет мост связей сайтов. |
| Set-ADReplicationSubnet | Изменяет подсеть Active Directory |
| Sync-ADObject | Принудительная репликация отдельного объекта. |

Большинство этих командлетов основаны на программе Repadmin.exe. Другие командлеты (не приведенные в списке) используют такие компоненты, как динамический контроль доступа и групповые управляемые учетные записи служб.

Чтобы просмотреть весь список командлетов Windows PowerShell для Active Directory, выполните указанную ниже команду.

```
Get-command -module ActiveDirectory
```

Чтобы просмотреть весь список аргументов командлетов Windows PowerShell для Active Directory, обратитесь к справке. Например:

```
Get-help New-ADReplicationSite

```

Загрузка и установка файлов справки с помощью командлета `Update-Help`

### <a name="replication-and-metadata"></a><a name="BKMK_Repl"></a>Репликация и метаданные
Программа Repadmin.exe проверяет состояние и согласованность репликации Active Directory. Repadmin.exe обеспечивает простые средства для манипуляции с данными, например некоторые аргументы поддерживают вывод данных в формате CSV. Но для автоматизации, как правило, требуется разбор содержимого текстовых файлов. Модуль Active Directory для Windows PowerShell — это первая попытка обеспечить настоящий контроль над возвращаемыми данными. Раньше приходилось создавать сценарии или использовать сторонние средства.

Кроме того, в следующих командлетах реализован новый набор параметров, включающий параметры **Target**, **Scope** и **EnumerationServer**:

- **Get-ADReplicationFailure**

- **Get-ADReplicationPartnerMetadata**

- **Get-ADReplicationUpToDatenessVectorTable**

Аргумент **Target** принимает разделенный запятыми список строк, которые определяют целевые серверы, сайты, домены или леса, указанные в аргументе **Scope**. Звездочка ( \* ) также является допустимой и означает все серверы в указанной области. Если область не указана, подразумевается использование всех серверов в лесу текущего пользователя. Аргумент **Scope** определяет диапазон поиска. Допустимые значения: **Server**, **Site**, **Domain** и **Forest**. Аргумент **EnumerationServer** определяет сервер, который перечисляет список контроллеров домена, указанных в аргументах **Target** и **Scope**. Он работает так же, как аргумент **Server**, и требует, чтобы на указанном сервере была запущена веб-служба Active Directory.

Для знакомства с новыми командлетами ниже приведено несколько примеров сценариев, в которых показаны возможности, недоступные в repadmin.exe. Эти примеры наглядно демонстрируют возможности для администраторов. Конкретные требования для использования командлета можно найти в справке по нему.

### <a name="get-adreplicationattributemetadata"></a><a name="BKMK_ReplAttrMD"></a>Get-ADReplicationAttributeMetadata
Этот командлет аналогичен команде **repadmin.exe /showobjmeta**. Он позволяет возвращать метаданные репликации, например время изменения атрибута, исходный контроллер домена, версию и информацию USN, а также данные атрибута. Этот командлет полезен для отслеживания времени и места внесения изменения.

В отличие от программы Repadmin, среда Windows PowerShell предоставляет гибкий контроль над поиском и выходными данными. Например, метаданные объекта "Администраторы домена" могут выводиться в виде упорядоченного читаемого списка:

```
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-list

```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMd.png)

Данные также можно упорядочить в виде таблицы, как они выводятся программой repadmin:

```
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-table -wrap

```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdTable.png)

Кроме того, можно получить метаданные для всего класса объектов, направив выходные данные командлета **Get-Adobject** в фильтр по конвейеру. Например, таким образом можно получить данные по всем группам за определенную дату. Конвейер — это канал, используемый несколькими командлетами для обмена данными. Чтобы просмотреть все группы, измененные каким-либо образом 13 января 2012 года, выполните указанную ниже команду.

```
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.lastoriginatingchangetime -like "*1/13/2012*" -and $_.attributename -eq "name"} | format-table object
```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdClass.png)

Дополнительные сведения о других операциях Windows PowerShell с конвейерами см. в разделе [Конвейерная передача и конвейер в Windows PowerShell](/previous-versions/windows/it-pro/windows-powershell-1.0/ee176927(v=technet.10)).

Чтобы узнать, в какие группы входит пользователь Tony Wang и когда каждая из этих групп была изменена в последний раз, выполните указанную ниже команду.

```
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | where-object {$_.attributevalue -like "*tony wang*"} | format-table object,LastOriginatingChangeTime,version -auto

```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter.png)

Чтобы найти все объекты, восстановленные принудительно с помощью резервной копии состояния системы в домене, на основе полученной искусственно новой версии, выполните указанную ниже команду.

```
get-adobject -filter 'objectclass -like "*"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.version -gt "100000" -and $_.attributename -eq "name"} | format-table object,LastOriginatingChangeTime
```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter2.png)

Чтобы отправить все метаданные пользователей в файл CSV для дальнейшего анализа в Microsoft Excel, выполните указанную ниже команду.

```
get-adobject -filter 'objectclass -eq "user"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | export-csv allgroupmetadata.csv
```

### <a name="get-adreplicationpartnermetadata"></a><a name="BKMK_PartnerMD"></a>Get-ADReplicationPartnerMetadata
Этот командлет возвращает сведения о конфигурации и состоянии репликации для контроллера домена, которые можно использовать для мониторинга, инвентаризации или устранения неполадок. В отличие от программы Repadmin.exe, среда Windows PowerShell позволяет просматривать только необходимые данные в удобном формате.

Например, так выглядит состояние репликации отдельного контроллера домена в удобном для восприятия формате:

```
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com
```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMd.png)

Так выглядят сведения о последней попытке внутренней репликации контроллера домена и репликации его партнеров в табличном формате:

```
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com | format-table lastreplicationattempt,lastreplicationresult,partner -auto
```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdTable.png)

Чтобы связаться со всеми контроллерами домена в лесу и получить сведения о тех из них, при последней попытке репликации которых произошел сбой по какой-либо причине, выполните указанную ниже команду:

```
Get-ADReplicationPartnerMetadata -target * -scope server | where {$_.lastreplicationresult -ne "0"} | ft server,lastreplicationattempt,lastreplicationresult,partner -auto

```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdFail.png)

### <a name="get-adreplicationfailure"></a><a name="BKMK_ReplFail"></a>Get-ADReplicationFailure
С помощью этого командлета можно получать информацию о последних ошибках репликации. Он аналогичен команде **Repadmin.exe /showreplsum**, но также обеспечивает более эффективный контроль благодаря среде Windows PowerShell.

Например, можно получить сведения о последних сбоях контроллера домена и партнерах, с которыми не удалось связаться:

```
Get-ADReplicationFailure dc1.corp.contoso.com
```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFail.png)

Чтобы получить таблицу с наиболее важными сведениями о всех серверах в определенном логическом сайте Active Directory, упорядоченными для более удобного просмотра, выполните указанную ниже команду:

```
Get-ADReplicationFailure -scope site -target default-first-site-name | format-table server,firstfailuretime,failurecount,lasterror,partner -auto

```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFailScoped.png)

### <a name="get-adreplicationqueueoperation-and-get-adreplicationuptodatenessvectortable"></a><a name="BKMK_ReplQueue"></a>Get-ADReplicationQueueOperation и Get-ADReplicationUpToDatenessVectorTable
Оба эти командлета возвращают дополнительные сведения об актуальном состоянии контроллера домена, включая текущие сведения о репликации и векторе версии.

### <a name="sync-adobject"></a><a name="BKMK_Sync"></a>Sync-ADObject
Этот командлет аналогичен команде **Repadmin.exe /replsingleobject**. Он очень полезен при внесении изменений, требующих отдельной репликации, особенно при устранении неполадок.

Например, если кто-то удалил учетную запись генерального директора, а затем восстановил ее с помощью корзины Active Directory, возможно, ее необходимо немедленно реплицировать на все контроллеры домена. Кроме того, возможно, это следует сделать без принудительной репликации изменений, внесенных в другие объекты, ведь именно для этого служит расписание репликации, позволяющее не перегружать каналы глобальной сети.

```
Get-ADDomainController -filter * | foreach {Sync-ADObject -object "cn=tony wang,cn=users,dc=corp,dc=contoso,dc=com" -source dc1 -destination $_.hostname}

```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSSyncAD.png)

### <a name="topology"></a><a name="BKMK_Topo"></a>Topology
Хотя программа Repadmin.exe — это эффективное средство для получения информации о топологии репликации, включая сайты, связи сайтов, мосты связей сайтов и подключения, она не предоставляет достаточно широкий набор аргументов для внесения изменений. По сути, в Windows до сих пор не было встроенной программы с поддержкой сценариев, предназначенной специально для создания и изменения топологии доменных служб Active Directory администраторами. С распространением служб Active Directory в средах миллионов клиентов потребность в массовом изменении логической информации Active Directory стала очевидной.

Например, после быстрого развертывания новых филиалов, сопровождающегося объединением существующих, может потребоваться внести сотни изменений в сайты в соответствии с их физическим расположением, характеристиками сети и новыми требованиями к емкости. Эти изменения можно внести не с помощью средств Dssites.msc и Adsiedit.msc, а автоматически. Это особенно удобно, если вам приходится действовать на основе таблиц с данными, предоставленными группами сетевой инфраструктуры и технического обслуживания.

Командлеты **Get- \\ адрепликатион*** возвращают сведения о топологии репликации и полезны для многоканального конвейера в командлеты ** \\ Set-адрепликатион***. Командлеты **Get** не изменяют данные, они показывают только данные или создают объекты сеанса Windows PowerShell, которые можно конвейерировать в командлеты **Set-адрепликатион \\ ***. Командлеты **New** и **Remove** полезны для создания и удаления объектов топологии Active Directory.

Например, можно создавать сайты с помощью файла CSV:

```
import-csv -path C:\newsites.csv | new-adreplicationsite
```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewSitesCSV.png)

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSImportCSV.png)

Чтобы создать связь между двумя существующими сайтами с настраиваемым интервалом репликации и стоимостью сайтов, выполните указанную ниже команду.

```
new-adreplicationsitelink -name "chicago<-->waukegan" -sitesincluded chicago,waukegan -cost 50 -replicationfrequencyinminutes 15
```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSite.png)

Чтобы найти каждый сайт в лесу и заменить его атрибут **Options** на флаг, включающий уведомления об изменениях между сайтами, с целью максимально быстрой репликации со сжатием, выполните указанную ниже команду.

```
get-adreplicationsitelink -filter * | set-adobject -replace @{options=$($_.options -bor 1)}
```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteLink.gif)

> [!IMPORTANT]
> Чтобы отключить сжатие для этих связей сайтов, задайте параметр **-bor 5**.

Чтобы найти все сайты с отсутствующими назначениями подсетей с целью сверки списка фактических подсетей для этих расположений, выполните указанную ниже команду.

```
get-adreplicationsite -filter * -property subnets | where-object {!$_.subnets -eq "*"} | format-table name
```

![Расширенное управление с помощью PowerShell](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteFiltrer.png)

## <a name="see-also"></a>См. также:
[Общие сведения об Active Directory репликации и управлении топологией с помощью Windows PowerShell &#40;уровня 100&#41;](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md)

