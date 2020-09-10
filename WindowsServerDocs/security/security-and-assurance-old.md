---
title: Безопасность и контроль
description: Обзор обеспечения безопасности в Windows Server 2016
ms.topic: article
ms.date: 07/27/2018
ms.assetid: b886b2fd-3567-4f0a-8aa3-4ba7923d2d21
ms.author: lizross
author: eross-msft
manager: mtillman
ms.localizationpriority: medium
ms.openlocfilehash: 86011cbe4ba748347e049699a716ec38d462a788
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89641198"
---
# <a name="security-and-assurance-in-windows-server"></a>Безопасность и контроль в Windows Server

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

>[!TIP]
> Ищете дополнительные сведения о предыдущих версиях Windows Server? Ознакомьтесь с другими нашими [библиотеками Windows Server](/previous-versions/windows/) на сайте docs.microsoft.com. Кроме того, вы можете найти нужную информацию [на этом сайте](/search/index?dataSource=previousVersions&search=Windows+Server).

<img src="../media/landing-icons/security.png" style='float:left; padding:.5em;' alt="Icon representing a lock"> Положитесь на новые уровни защиты, встроенные в операционную систему для дополнительной защиты от брешей в системе безопасности. Обеспечьте блокировку вредоносных атак и повысьте безопасность виртуальных машин, приложений и данных.


### <a name="windows-server-security-blog-post"></a>[Запись в блоге о службе безопасности Windows Server](https://blogs.technet.microsoft.com/windowsserver/2016/04/25/ten-reasons-youll-love-windows-server-2016-8-security/)
В этой записи блога команда специалистов по обеспечению безопасности в Windows Server дает краткое описание многих улучшений, реализованных в Windows Server, повышающих безопасность сред размещения и гибридного облака.

### <a name="datacenter-and-private-cloud-security-blog"></a>[Datacenter and Private Cloud Security Blog (Блог о безопасности центров обработки данных и частных облаков)](/archive/blogs/datacentersecurity/)
Это центральный сайт для блогов, в которых представлена техническая информация от специалистов Microsoft по обеспечению безопасности центров обработки данных и частных облаков.

### <a name="addressing-emerging-threats-and-landscape-shifts"></a>[Addressing emerging threats and landscape shifts (Реагирование на возникающие угрозы и изменение условий)](https://www.youtube.com/watch?v=B5JMYxYWx1k&feature=youtu.be)
В этом 6-минутном видео Андерс Вайнберг (Anders Vinberg) дает общее представление о стратегии безопасности и контроля корпорации Майкрософт, а также описывает появляющиеся в отрасли тенденции, связанные с безопасностью. Затем он рассматривает ключевые инициативы корпорации Майкрософт по защите рабочих нагрузок из базовой структуры и защите от прямых атак из привилегированных учетных записей. В конце он объясняет, как новые возможности обнаружения и анализа могут способствовать лучшему определению угроз.

### <a name="protecting-your-datacenter-and-cloud-from-emerging-threats-blog-post"></a>[Protecting Your Datacenter and Cloud from Emerging Threats blog post (Запись блога. Защита центра обработки данных и облака от возникающих угроз)](https://blogs.technet.com/b/windowsserver/archive/2015/11/18/protecting-your-datacenter-and-cloud-november-update.aspx)
В этой публикации описываются методы применения технологий Майкрософт для защиты центров обработки данных и облачных хранилищ от возникающих угроз.

### <a name="security-and-assurance-overview-session-at-ignite"></a>[Обзорный семинар по безопасности и контролю на конференции Ignite](https://channel9.msdn.com/events/ignite/2015/brk2482)
В этом видео с конференции Ignite речь пойдет о постоянных угрозах, внутренних нарушениях системы безопасности, организованной киберпреступности, а также об обеспечении безопасности облачной платформы Майкрософт (локальных и подключенных служб в Azure). Здесь приведены сценарии для защиты рабочих нагрузок, крупных корпоративных клиентов и поставщиков услуг.

## <a name="secure-virtualization-with-shielded-vms"></a>Безопасная виртуализация с использованием экранированных виртуальных машин

### <a name="shielded-vm-in-channel-9"></a>[Экранированная виртуальная машина в Channel 9](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
Пошаговое описание технологии и преимуществ экранированных виртуальных машин.

### <a name="shielded-vm-demo"></a>[Демонстрация экранированной виртуальной машины](https://www.youtube.com/watch?v=xip5Qtk-7d8)
В этом 4-минутном видео описывается предназначение экранированных виртуальных машин, а также различия между экранированными и неэкранированными виртуальными машинами.

### <a name="shielded-virtual-machines-in-windows-server-video-walkthrough"></a>[Видеоруководство по использованию экранированных виртуальных машин в Windows Server](http://microsoft-cloud.cloudguides.com/Guides/Shielded Virtual Machines in Windows Server.htm)
В этом пошаговом видеоруководстве показано, как служба защиты узла включает экранированные виртуальные машины, обеспечивая защиту конфиденциальных данных от несанкционированного доступа администраторов узла Hyper-V.

### <a name="harden-the-fabric-protecting-tenant-secrets-in-hyper-v-ignite-video"></a>[Видео с конференции Microsoft Ignite. Усиление защиты структуры: защита секретных данных клиента в Hyper-V](https://channel9.msdn.com/events/ignite/2015/brk3457)

В этой презентации Ignite обсуждаются дополнительные улучшения Hyper-V и диспетчера виртуальных машин, а также новая роль сервера-защитника узла для запуска экранированных виртуальных машин.

### <a name="guarded-fabric-deployment-guide"></a>[Руководство по развертыванию защищенной структуры](./guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview.md)
В этом руководстве содержится информация об установке и проверке Windows Server и System Center Virtual Machine Manager для узлов защищенной структуры и экранированных виртуальных машин.

### <a name="shielded-vm-and-guarded-fabric-in-branch-offices"></a>[Экранированная виртуальная машина и защищенная структура в филиалах](./guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office.md)
В этом руководстве содержатся советы и рекомендации по запуску экранированных виртуальных машин в филиалах, а также другие дистанционные сценарии, в которых узлы Hyper-V могут работать в условиях ограниченной возможности подключения к HGS.

### <a name="shielded-vm-and-guarded-fabric-troubleshooting-guide"></a>[Руководство по поиску и устранению неисправностей при использовании экранированной виртуальной машины и защищенной структуры](./guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-overview.md)
Это руководство содержит информацию о способах решения проблем, с которыми вы можете столкнуться в среде экранированной виртуальной машины.

### <a name="shielded-vm-article"></a>[Статья об экранированных виртуальных машинах](http://windowsitpro.com/hyper-v/super-secure-hyper-v-environments-shielded-vms-2016)
В этом техническом документе содержатся общие сведения о том, каким образом экранированные виртуальные машины повышают общий уровень безопасности для предотвращения мошенничества.

## <a name="privileged-access-management"></a>Privileged Access Management (Защита Windows и Microsoft Azure Active Directory с помощью управления привилегированным доступом)
### <a name="securing-privileged-access"></a>[Обеспечение безопасности привилегированного доступа](../identity/securing-privileged-access/securing-privileged-access.md)
Схема по обеспечению безопасности привилегированного доступа. В этой схеме учтен совокупный опыт группы по безопасности серверов, ИТ-отдела корпорации Майкрософт, группы Azure и службы консультаций Майкрософт

### <a name="just-in-time-administration-with-microsoft-identity-manager"></a>[JIT-администрирование с помощью Microsoft Identity Manager](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services)
В этой статье рассматриваются функции и возможности Microsoft Identity Manager, включая поддержку управления JIT-управления привилегированным доступом.

### <a name="protecting-windows-and-microsoft-azure-active-directory-with-privileged-access-management"></a>[Защита Windows и Microsoft Azure Active Directory с помощью Privileged Access Management](https://channel9.msdn.com/events/ignite/2015/brk3873)
В этой презентации Ignite описаны стратегии и инвестиции корпорации Майкрософт в Windows Server, PowerShell, Active Directory, Identity Manager и Azure Active Directory для устранения рисков доступа администратора с помощью более надежной проверки подлинности и управления доступом с использованием технологий администрирования Just in Time (JIT) и Just Enough Administration (JEA).

### <a name="just-enough-administration-article"></a>[Статья о технологии Just Enough Administration](https://aka.ms/JEA)
В этом документе представлена концепция и технические детали технологии Just Enough Administration — инструментария PowerShell для предприятий, предназначенного для сокращения рисков путем ограничения доступа операторам. Доступ предоставляется только к определенным ресурсам, необходимым для решения поставленных задач.

### <a name="just-enough-administration-demo-video"></a>[Демонстрационное видео по Just Enough Administration](https://www.youtube.com/watch?v=xnBrbkY9P20)
Демонстрационное пошаговое руководство по Just Enough Administration.
## <a name="credential-protection"></a>Защита учетных данных

### <a name="protect-derived-domain-credentials-with-credential-guard"></a>[Защита извлеченных учетных данных домена с помощью Credential Guard](/windows/security/identity-protection/credential-guard/credential-guard)
Для защиты секретов Credential Guard использует безопасность на основе виртуализации, чтобы только привилегированное системное ПО могло получать доступ к этим данным. Несанкционированный доступ к этим секретам может привести к атакам с хищением учетных данных, таким как Pass-the-Hash или Pass-a-Ticket. Credential Guard предотвращает такие атаки, защищая хэши паролей NTLM и билеты для предоставления билетов Kerberos.

### <a name="protect-remote-desktop-credentials-with-remote-credential-guard"></a>[Защита учетных данных удаленного рабочего стола с помощью Remote Credential Guard](/windows/security/identity-protection/remote-credential-guard)
Remote Credential Guard позволяет защитить учетные данные через подключение к удаленному рабочему столу путем перенаправления запросов Kerberos обратно к устройству, запрашивающему соединение. Remote Credential Guard также предоставляет единый вход пользователей в систему для сеансов доступа к удаленному рабочему столу.                                                                                                        |
### <a name="credential-guard-demo-video"></a>[Демонстрационное видео по Credential Guard](https://www.youtube.com/watch?v=eUpKOGSl7yk)
В этом 5-минутном видео демонстрируется Credential Guard и удаленный Credential Guard.

## <a name="hardening-the-os-and-applications"></a>Усиление защиты ОС и приложений
### <a name="windows-defender-application-control-wdac-deployment-guide"></a>[Руководство по развертыванию компонента "Управление приложениями в Защитнике Windows" (WDAC)](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)
WDAC — это политика настраиваемой целостности кода (CI), которая помогает предприятиям контролировать приложения, выполняющиеся в их средах. К этому компоненту не предъявляются особые аппаратные или программные требования, за исключением необходимости использования Windows 10.

### <a name="device-guard-demo-video"></a>[Демонстрационное видео по Device Guard](https://www.youtube.com/watch?v=F-pTkesjkhI)
Device Guard — это сочетание WDAC и службы целостности кода с защищенной низкоуровневой оболочкой (HVCI). Это 7-минутное видео описывает Device Guard и его использование в Windows Server.

### <a name="transport-layer-security-registry-settings"></a>[Параметры реестра безопасности транспортного уровня (протокол TLS)](./tls/tls-registry-settings.md)
Сведения о поддерживаемых параметрах реестра для реализации в Windows протокола TLS и протокола SSL.

### <a name="control-flow-guard"></a>[Защита потока управления](/windows/desktop/SecBP/control-flow-guard)
Защита потока управления обеспечивает встроенную защиту от некоторых видов атак, основанных на повреждении памяти.

### <a name="windows-defender"></a>[Защитник Windows](./windows-defender/windows-defender-overview-windows-server.md)
Защитник Windows обеспечивает возможности активного обнаружения для блокировки известных вредоносных программ. Защитник Windows включен по умолчанию и оптимизирован для поддержки различных ролей сервера в Windows Server.

## <a name="detecting-and-responding-to-threats"></a>Обнаружение угроз и реагирование на них
### <a name="security-threat-analysis-using-microsoft-operations-management-suite"></a>[Анализ угроз безопасности с помощью Microsoft Operations Management Suite](https://channel9.msdn.com/events/ignite/2015/brk3464)
В этой презентации Ignite обсуждается вопрос использования оперативной аналитики для анализа угроз безопасности.

### <a name="microsoft-operations-management-suite-oms"></a>[Microsoft Operations Management Suite (OMS)](https://www.microsoft.com/server-cloud/operations-management-suite/overview.aspx)
Решение Microsoft Operations Management Suite (OMS) по безопасности и аудиту обрабатывает журналы безопасности и события брандмауэра, поступающие от локальных ресурсов и из облачной среды. Эти данные используются для анализа и обнаружения вредоносной деятельности.

### <a name="oms-and-windows-server"></a>[OMS и Windows Server](https://www.youtube.com/watch?v=_SaDw1dRy2k)
Это 3-минутное видео показывает, как OMS может помочь в обнаружении потенциально вредоносного поведения, блокируемого Windows Server.

### <a name="microsoft-advanced-threat-analytics"></a>[Microsoft Advanced Threat Analytics](https://blogs.technet.com/b/ad/archive/2015/07/22/microsoft-advanced-threat-analytics-coming-next-month.aspx)
В этой записи блога рассматривается служба Microsoft Advanced Threat Analytics — локальный продукт, который использует сетевой трафик Active Directory и данные SIEM для выявления потенциальных угроз и предупреждения о них.

### <a name="microsoft-advanced-threat-analytics"></a>[Microsoft Advanced Threat Analytics](https://www.youtube.com/watch?v=0nA9FeTRZFw&list=PL8nfc9haGeb5IZGM8HvmRozetHRpBDKSw)
В этом трехминутном видео рассказывается о новых функциях для анализа угроз безопасности в Windows Server.                                                                                 |

## <a name="network-security"></a>Сетевая безопасность

### <a name="datacenter-firewall-overview"></a>[Обзор брандмауэра центра обработки данных](/previous-versions/windows/server/dn920240(v=ws.12))
В этом обзоре рассматривается брандмауэр центра обработки данных сетевого уровня с пятью кортежами (протокол, номера начального и конечного портов, начальный и конечный IP-адреса), с функцией отслеживания состояния и поддержкой нескольких клиентов.

### <a name="whats-new-in-dns-in-windows-server"></a>[Новые возможности службы DNS в Windows Server](../networking/dns/what-s-new-in-dns-server.md)
В этой обзорной статье дано краткое описание новых возможностей службы DNS, а также полезные ссылки для получения дополнительных сведений.

## <a name="mapping-security-features-to-compliance-regulations"></a>Сопоставление функций безопасности с требованиями по обеспечению соответствия

Соответствие является важным аспектом реализации функций безопасности. Мы даем квалифицированный совет по обеспечению соответствия, поясняем, что значит соответствие для ваших доверенных консультантов, а также предлагаем начальное сопоставление, которое вы можете использовать при оценке Windows Server.

-   [Технический документ по сопоставлению соответствия для экранированных виртуальных машин Hyper-V](https://download.microsoft.com/download/6/D/0/6D06E149-B4C1-4EED-ACD5-DF6066E93CC0/Coalfire_Branded_Hyper_V_Shielded_VMs_Whitepaper_EN_US.pdf)

-   [Технический документ по сопоставлению соответствия для JEA и JIT](https://download.microsoft.com/download/2/7/A/27A2B5BB-6B52-4482-87C1-DA9D6B6D8C8D/Coalfire_Branded_Privileged_Identity_Manager_Whitepaper_EN_US.pdf)

-   [Технический документ по сопоставлению соответствия для Device Guard](https://download.microsoft.com/download/6/9/D/69D9E610-D23C-4F7E-A8CC-D65B87CEB4F8/Coalfire_Branded_Device_Guard_Whitepaper_EN_US.pdf)

-   [Технический документ по сопоставлению соответствия для Credential Guard](https://download.microsoft.com/download/8/1/2/812009C9-E4B8-4D4B-AADD-FDC373D0A076/Coalfire_Branded_Credential_Guard_Whitepaper_EN_US.pdf)

-   [Технический документ по сопоставлению соответствия для Защитника Windows](https://download.microsoft.com/download/C/7/7/C778B7BB-0783-42D7-93A9-B86DFB5A7BAD/Coalfire_Branded_Windows_Defender_Whitepaper_EN_US.pdf)