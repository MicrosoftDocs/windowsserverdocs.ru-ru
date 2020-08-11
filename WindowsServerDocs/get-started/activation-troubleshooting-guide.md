---
title: Устранение неполадок с активацией корпоративных лицензий Windows
description: Список ресурсов, содержащих рекомендации по активации корпоративных лицензий и сведения об устранении неполадок, связанных с активацией.
ms.topic: troubleshooting
ms.date: 09/24/2019
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: ce6c2e830e7c30e24112854b54e12909c43fa6f7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972331"
---
# <a name="troubleshooting-windows-volume-activation"></a>Устранение неполадок с активацией корпоративных лицензий Windows

Активация продукта — это проверка программного обеспечения после того, как оно было установлено на конкретном компьютере. Активация подтверждает, что продукт является подлинной копией и что ключ или серийный номер продукта действительны и не были скомпрометированы или аннулированы. Активация также устанавливает связь между ключом продукта и установленной копией.

Активация корпоративных лицензий — это процесс активации продуктов с корпоративной лицензией. Чтобы иметь возможность выполнять корпоративное лицензирование, организации необходимо заключить с корпорацией Майкрософт соглашение о корпоративном лицензировании. Корпорация Майкрософт предлагает программы корпоративного лицензирования, соответствующие размеру и покупательским предпочтениям организации. Дополнительные сведения см. на веб-сайте [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx).

[Руководство по активации Windows Server 2016](server-2016-activation.md) преимущественно посвящено технологии активации с помощью службы управления ключами (KMS). В этом разделе рассматриваются распространенные проблемы, а также рекомендации по устранению неполадок KMS и ряда других технологий активации корпоративных лицензий.

## <a name="best-practices-for-volume-activation"></a>Рекомендации оп активации корпоративных лицензий

В следующих статьях содержатся технические сведения и рекомендации по технологиям активации корпоративных лицензий корпорации Майкрософт.

### <a name="key-management-service-kms"></a>Служба управления ключами (KMS).

- [Планирование активации корпоративных лицензий](/windows/deployment/volume-activation/plan-for-volume-activation-client)
- [Общие сведения о KMS](/previous-versions/tn-archive/ff793434(v=technet.10))
- [Развертывание активации KMS](/previous-versions/tn-archive/ff793409%28v=technet.10%29)
- [Настройка узлов KMS](/previous-versions/tn-archive/ff793407%28v%3dtechnet.10%29)
- [Настройка DNS](/previous-versions/tn-archive/ff793405%28v%3dtechnet.10%29)
- [Активация с помощью службы управления ключами](/windows/deployment/volume-activation/activate-using-key-management-service-vamt)

### <a name="active-directory-based-activation-adba"></a>Активация с помощью Active Directory (ADBA)

- [Развертывание активации с помощью Active Directory](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn502534%28v%3dws.11%29)
- [Активация с помощью Active Directory](/windows/deployment/volume-activation/activate-using-active-directory-based-activation-client)
- [Общие сведения об активации с помощью Active Directory](/windows/deployment/volume-activation/active-directory-based-activation-overview)

### <a name="multiple-activation-key-mak-activation"></a>Активация с помощью ключей многократной активации (MAK)

- [Активация с помощью MAK](/previous-versions/tn-archive/ff793438%28v=technet.10%29)
- [Общие сведения об активации с помощью MAK](/previous-versions/tn-archive/ff793435%28v%3dtechnet.10%29)
- [Активация клиентов MAK](/previous-versions/tn-archive/ff793398%28v%3dtechnet.10%29)

### <a name="subscription-activation"></a>Активация подписки

- [Активация подписки Windows 10](/windows/deployment/windows-10-subscription-activation)
- [Развертывание лицензий Windows 10 Корпоративная](/windows/deployment/deploy-enterprise-licenses)
- [Windows 10 Корпоративная E3 в CSP](/windows/deployment/windows-10-enterprise-e3-overview)

## <a name="resources-for-troubleshooting-activation-issues"></a>Материалы по устранению проблем с активацией

В следующих статьях приводятся рекомендации и сведения о средствах устранения неполадок, связанных с активацией корпоративных лицензий.

- [Рекомендации по устранению неполадок службы управления ключами (KMS)](activation-troubleshoot-kms-general.md)
- [Параметры Slmgr.vbs для получения сведений об активации корпоративных лицензий](activation-slmgr-vbs-options.md)
- [Пример. Устранение неполадок клиентов ADBA, которые не активируются](activation-troubleshoot-adba-clients.md)

В следующих статьях приведены рекомендации по устранению конкретных проблем с активацией.

- [Разрешение распространенных кодов ошибок активации](activation-error-codes.md)
- [Активация KMS: известные проблемы](activation-troubleshoot-KMS-issues.md)
- [Активация MAK: известные проблемы](activation-troubleshoot-MAK-issues.md)
- [Рекомендации по устранению проблем с активацией, связанных с DNS](common-troubleshooting-procedures-kms-dns.md)
- [Как перестроить файл Tokens.dat](activation-rebuild-tokens-dat-file.md)
