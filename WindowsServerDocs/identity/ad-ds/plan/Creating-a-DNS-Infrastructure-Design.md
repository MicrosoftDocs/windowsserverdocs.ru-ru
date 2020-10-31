---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: Создание проекта инфраструктуры DNS
ms.author: daveba
author: iainfoulds
manager: daveba
ms.date: 08/08/2018
ms.topic: article
ms.openlocfilehash: a0052c791a0af7184845be7bbdbc52db6e66f6f0
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93068907"
---
# <a name="creating-a-dns-infrastructure-design"></a>Создание проекта инфраструктуры DNS

> Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

После создания леса Active Directory и доменных проектов необходимо разработать инфраструктуру системы доменных имен (DNS) для поддержки логической структуры Active Directory. DNS позволяет пользователям использовать понятные имена, которые легко запомнить для подключения к компьютерам и другим ресурсам в IP-сетях. Для домен Active Directory служб (AD DS) в Windows Server 2008 требуется DNS.

Процесс проектирования DNS для поддержки AD DS зависит от того, имеет ли ваша организация уже существующую службу DNS-сервера или вы развертываете новую службу DNS-сервера:

- Если у вас уже есть инфраструктура DNS, необходимо интегрировать пространство имен Active Directory в эту среду. Дополнительные сведения см. [в статье интеграция AD DS в существующую инфраструктуру DNS](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md).
- Если у вас нет инфраструктуры DNS, необходимо разработать и развернуть новую инфраструктуру DNS для поддержки AD DS. Дополнительные сведения см. в разделе [развертывание службы доменных имен (DNS)](/previous-versions/windows/it-pro/windows-server-2003/cc780661(v=ws.10)).

Если ваша организация имеет существующую инфраструктуру DNS, необходимо убедиться, что вы понимаете, как инфраструктура DNS будет взаимодействовать с пространством имен Active Directory. Для листа, который поможет вам документировать существующую структуру инфраструктуры DNS, скачайте Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip из [комплекта вспомогательных средств для Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608) и откройте оснастку "Инвентаризация DNS" (DSSLOGI_8.doc).

> [!NOTE]
> Кроме адресов IP версии 4 (IPv4), Windows Server также поддерживает адреса IP версии 6 (IPv6). Сведения о том, как получить список IPv6-адресов, в которых описывается метод рекурсивного разрешения имен в текущей структуре DNS, см. [в приложении a. Инвентаризация DNS](../../ad-ds/plan/Appendix-A--DNS-Inventory.md).

Прежде чем приступить к проектированию инфраструктуры DNS для поддержки AD DS, можно прочитать сведения об иерархии DNS, процессе разрешения имен DNS и о том, как DNS поддерживает AD DS. Дополнительные сведения об иерархии DNS и процессе разрешения имен см. в [техническом справочнике по DNS](/previous-versions/windows/it-pro/windows-server-2003/cc779926(v=ws.10)). Дополнительные сведения о том, как DNS поддерживает AD DS, см. в статье [поддержка DNS для Active Directory технического справочника](/previous-versions/windows/it-pro/windows-server-2003/cc781627(v=ws.10)).

## <a name="in-this-section"></a>В этом разделе

- [Общие сведения о понятиях DNS](../../ad-ds/plan/Reviewing-DNS-Concepts.md)
- [DNS и доменные службы Active Directory](../../ad-ds/plan/DNS-and-AD-DS.md)
- [Назначение DNS для роли владельца доменных служб Active Directory](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)
- [Интеграция доменных служб Active Directory в существующую инфраструктуру DNS](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)
