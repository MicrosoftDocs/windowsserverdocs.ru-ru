---
title: Основные решения поддержки для Windows Server
description: Получите ссылки на решения для проблем с Windows Server
manager: alant
ms.date: 03/16/2018
ms.topic: article
author: kaushika-msft
ms.author: elizapo
ms.openlocfilehash: 7bc533063c52af2087d822a428458ba8efab94fc
ms.sourcegitcommit: d08965d64f4a40ac20bc81b14f2d2ea89c48c5c8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2020
ms.locfileid: "96864673"
---
# <a name="top-support-solutions-for-windows-server-2016"></a>Основные решения поддержки для Windows Server 2016

Корпорация Майкрософт регулярно выпускает обновления и решения для Windows Server. Необходимо вовремя обновлять серверы, чтобы они могли получать будущие обновления, в том числе обновления безопасности. Полный список выпущенных обновлений см. в разделе [Журнал обновлений Windows 10 и Windows Server 2016](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history).

Это лучшие решения службы поддержки Майкрософт для наиболее распространенных проблем при использовании Windows Server 2016. Ниже представлены ссылки на статьи базы знаний и библиотеки, а также на обновления.

>[!TIP]
> Ищете дополнительные сведения о предыдущих версиях Windows Server? Ознакомьтесь с другими нашими [библиотеками Windows Server](/previous-versions/windows/) на сайте docs.microsoft.com. Кроме того, вы можете найти нужную информацию [на этом сайте](/search/index?dataSource=previousVersions&search=Windows+Server).

## <a name="solutions-for-installing-or-upgrading-windows-server"></a>Решения для установки или обновления Windows Server

- [Устранение ошибок при обновлении до Windows 10: технические сведения для ИТ-специалистов](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors)
- [Обновление стека обслуживания для Windows 10 версии 1607 и Windows Server 2016: 8 августа 2017 г.](https://support.microsoft.com/help/4035631)
- [Обновление совместимости для обновления до Windows 10 версии 1607 и Windows Server 2016: 3 августа 2017 г.](https://support.microsoft.com/help/4033524)
- [На виртуальных машинах Azure на базе Windows обновление системы на месте не поддерживается](https://support.microsoft.com/help/4014997)
- [Варианты обновления и преобразования для Windows Server 2016](../get-started/supported-upgrade-paths.md)
- [Матрица обновления и миграции ролей сервера для Windows Server 2016](../get-started/server-role-upgradeability-table.md)
- [Установка и обновление Windows Server](../get-started/installation-and-upgrade.md)
- [Заметки о выпуске. Важные проблемы в Windows Server 2016](../get-started/windows-server-2016-ga-release-notes.md)
- [Рекомендации по переходу на Windows Server 2016](../get-started/recommendations-moving-to-server2016.md)

## <a name="solutions-for-volume-activation"></a>Решения для активации корпоративных лицензий
- [Активация Windows Server 2016](../get-started/server-2016-activation.md)
- [Просмотр и выбор методов активации](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134256(v=ws.11))
- [Коды ошибок активации при активации корпоративных лицензий](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn502528(v=ws.11))
- [Устранение неполадок в службе управления ключами (KMS)](/previous-versions/tn-archive/ee939272(v=technet.10))
- [Устранение проблем с активацией корпоративных лицензий](/previous-versions/tn-archive/ff793439(v=technet.10))
- [Коды ошибок активации](/previous-versions/ff793399(v=technet.10))
- [Установка Windows может завершиться с ошибкой "указанный ключ продукта не соответствует ни одному из образов Windows, доступных для установки. Введите другой ключ продукта "](https://support.microsoft.com/help/2796988/windows-8-or-windows-server-2012-installation-may-fail-with-error-mess)

## <a name="solutions-related-to-dcpromo-and-installing-domain-controllers"></a>Решения, связанные с DCPromo и установкой контроллера домена
- [Требования к портам для Active Directory и доменных служб Active Directory](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772723(v=ws.10))
- [Active Directory порты брандмауэра — Давайте попробуем сделать это простым](http://blogs.msmvps.com/acefekay/2011/11/01/active-directory-firewall-ports-let-s-try-to-make-this-simple/)
- [Поддержки Exchange Server для Windows Server 2016](/Exchange/plan-and-deploy/supportability-matrix)
- [Использование Ntdsutil.exe для переноса или изменения размера ролей FSMO в контроллере домена](https://support.microsoft.com/kb/255504)
- [Устранение неполадок с развертыванием контроллера домена](../identity/ad-ds/deploy/troubleshooting-domain-controller-deployment.md)
- [Troubleshooting Active Directory Installation Wizard Problems](/previous-versions/windows/it-pro/windows-2000-server/bb727058(v=technet.10)) (Устранение неполадок с мастером установки Active Directory)
- [Известные проблемы при установке и удалении AD DS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754463(v=ws.10))

## <a name="solutions-for-active-directory-federation-services-ad-fs"></a>Решения для служб федерации Active Directory (AD FS)
- [Как настроить автоматическую регистрацию присоединенных к домену устройств Windows в Azure Active Directory](/azure/active-directory/active-directory-conditional-access-automatic-device-registration-setup)
- [Настройка выдачи утверждений](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup#step-2-setup-issuance-of-claims)
- [Настройка AD FS для аутентификации пользователей, хранящихся в каталогах LDAP](../identity/ad-fs/operations/configure-ad-fs-to-authenticate-users-stored-in-ldap-directories.md)
- [Поддержка привязки альтернативного имени узла для аутентификации сертификата в AD FS](../identity/ad-fs/operations/ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)
- [Защита от атак на пароли](/archive/blogs/tspring/federated-to-microsoft-cloud-and-account-lockouts)
- [Обновление до AD FS в Windows Server 2016 с помощью базы данных WID](../identity/ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md)
- [Вход в Windows 10: включение аутентификации с использованием AD FS](../identity/ad-fs/operations/configure-device-based-conditional-access-on-premises.md)
- [Управление SSL-сертификатами в AD FS и WAP в Windows Server 2016](../identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap.md)
- [Политики управления доступом в Windows Server 2016 AD FS](../identity/ad-fs/operations/access-control-policies-in-ad-fs.md)

## <a name="solutions-related-to-active-directory-replication"></a>Решения, связанные с репликацией Active Directory

- [Устранение неполадок с репликацией Active Directory](../identity/ad-ds/manage/troubleshoot/troubleshooting-active-directory-replication-problems.md)
- [Скачайте средство определения состояния репликации Active Directory в Центре загрузки Майкрософт](https://www.microsoft.com/en-in/download/details.aspx?id=30005)
- [E2E: устранение распространенных ошибок репликации Active Directory.](https://support.microsoft.com/kb/3108513)
- [Устранение ошибки репликации AD 8606: задано недостаточно атрибутов для создания объекта](https://support.microsoft.com/kb/2028495)
- [События с идентификаторами 2108 и 1084 происходят при входящей репликации Active Directory в Windows 2000 Server и Windows Server 2003](https://support.microsoft.com/kb/837932)
- [Устранение ошибки репликации 8451: произошла ошибка базы данных при выполнении репликации](https://support.microsoft.com/kb/2645996)
- [Устранение ошибки репликации 1127: зафиксирован многократный сбой операции при обращении к жесткому диску](https://support.microsoft.com/kb/2025726)
- [Очистка метаданных сервера](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816907(v=ws.10))
