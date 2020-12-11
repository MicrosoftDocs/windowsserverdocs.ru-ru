---
description: Дополнительные сведения см. в техническом справочном приложении по виртуальному контроллеру домена
ms.assetid: 73a4deba-7da6-4eae-8fdd-2a4d369f9cbb
title: Приложение технического справочника по виртуализированным контроллерам домена
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 3f59760b5519d636ad879e11e692ddcbdc6c3129
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97045022"
---
# <a name="virtualized-domain-controller-technical-reference-appendix"></a>Приложение технического справочника по виртуализированным контроллерам домена

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этой статье рассматриваются следующие вопросы.

-   [Терминология](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_Terms)

-   [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)

## <a name="terminology"></a><a name="BKMK_Terms"></a>Терминология

-   **Snapshot** — состояние виртуальной машины в определенный момент времени. Он зависит от цепочки предыдущих моментальных снимков на оборудовании и на платформе виртуализации.

-   **Клонирование** — полная и отдельная копия виртуальной машины. Это зависит от виртуального оборудования (гипервизора).

-   **Полное клонирование** — полное клонирование — это независимая копия виртуальной машины, которая не использует ресурсы с родительской виртуальной машиной после операции клонирования. Текущая операция полного клона полностью отделена от родительской виртуальной машины.

-   **Разностный диск** — копия виртуальной машины, которая постоянно использует виртуальные диски с родительской виртуальной машиной. Обычно это экономит место на диске и позволяет нескольким виртуальным машинам использовать одну и ту же установку программного обеспечения.

-   **Копия виртуальной машины**— копия всех связанных файлов и папок виртуальной машины в файловой системе.

-   **Копирование** VHD-файлов — копия виртуального жесткого диска виртуальной машины

-   **Идентификатор создания виртуальной машины** — 128-разрядное целое число, заданное для виртуальной машины гипервизором. Этот идентификатор хранится в памяти и сбрасывается каждый раз при применении моментального снимка. В проекте используется механизм, не зависящий от гипервизора, для отображая идентификатора VM-Generation на виртуальной машине. Реализация Hyper-V предоставляет идентификатор в таблице ACPI виртуальной машины.

-   Функция **импорта и экспорта** — компонент Hyper-V, позволяющий пользователю сохранить всю виртуальную машину (файлы виртуальной машины, VHD и конфигурацию компьютера). Затем он позволяет пользователям использовать этот набор файлов, чтобы вернуть компьютер на тот же компьютер, что и ту же ВИРТУАЛЬную машину (восстановление), на другом компьютере, где находится та же ВИРТУАЛЬная машина (переместить), или новую виртуальную машину (копию).

## <a name="fixvdcpermissionsps1"></a><a name="BKMK_FixPDCPerms"></a>FixVDCPermissions.ps1

```
# Unsigned script, requires use of set-executionpolicy remotesigned -force
# You must run the Windows PowerShell console as an elevated administrator

# Load Active Directory Windows PowerShell Module and switch to AD DS drive
import-module activedirectory
cd ad:

## Get Domain NC
$domainNC = get-addomain

## Get groups and obtain their SIDs
$dcgroup = get-adgroup "Cloneable Domain Controllers"

$sid1 = (get-adgroup $dcgroup).sid

## Get the DACL of the domain
$acl = get-acl $domainNC

## The following object specific ACE grants extended right 'Allow a DC to create a clone of itself' for the CDC group to the Domain NC
## 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e is the schemaIDGuid for 'DS-Clone-Domain-Controller"

$objectguid = new-object Guid 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e
$ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid1,"ExtendedRight","Allow",$objectguid

## Add the ACE in the ACL and set the ACL on the object

$acl.AddAccessRule($ace1)
set-acl -aclobject $acl $domainNC
write-host "Done writing new VDC permissions."
cd c:
```



