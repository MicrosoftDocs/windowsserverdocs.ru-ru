---
title: Общие сведения о Windows Admin Center
description: Сведения об управлении Windows Server с помощью Windows Admin Center (Project Honolulu)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 01/07/2020
ms.localizationpriority: high
ms.openlocfilehash: d6fa3e4535748b6c4d5b45755b0336dc26815bee
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766737"
---
# <a name="windows-admin-center"></a>Windows Admin Center

> Применяется к: Windows Admin Center, ознакомительная версия Windows Admin Center

Windows Admin Center представляет собой локально развертываемое браузерное приложение для управления серверами, кластерами, гиперконвергентной инфраструктурой Windows, а также ПК с Windows 10. Оно поставляется без дополнительной платы в составе Windows и готово для использования в рабочей среде.

Описание новых возможностей см. в [этой статье](support/release-history.md).

## <a name="download-now"></a>Скачать сейчас

**Скачайте [Windows Admin Center](https://www.microsoft.com/evalcenter/evaluate-windows-admin-center)** из Центра оценки Майкрософт. Хотя там отображается надпись Start your evaluation (Начните оценку), это общедоступная версия для производственного использования.

Сведения об установке см. в [этой статье](deploy/install.md). Советы по началу работы с Windows Admin Center см. в [этой статье](use/get-started.md).

Вы можете обновить версии Windows Admin Center (не предварительные), используя Центр обновления Майкрософт или скачав и установив Windows Admin Center вручную. Каждая версия Windows Admin Center (не ознакомительная) поддерживается в течение 30 дней после выпуска следующей версии (не ознакомительной). Дополнительные сведения см. в нашей [​​политике поддержки](support/index.md).

## <a name="windows-admin-center-scenarios"></a>Сценарии Windows Admin Center

Ниже приведены несколько действий, для выполнения которых вы можете использовать Windows Admin Center.

- **Упрощение управления серверами.** Управляйте серверами и кластерами с помощью модернизированных версий привычных инструментов, таких как диспетчер серверов. Установка занимает меньше пяти минут, и вы сразу можете приступать к управлению серверами в своей среде, дополнительная настройка не требуется. Дополнительные сведения см. в статье [Что такое Windows Admin Center?](understand/what-is.md).

- **Работа с гибридными решениями.** Интеграция с Azure позволяет дополнительно подключать локальные серверы к соответствующим облачным службам. Дополнительные сведения см. в статье [Подключение Windows Server к гибридным службам Azure](azure/index.md).

- **Упрощение гиперконвергентного управления.** Оптимизируйте управление гиперконвергентными кластерами Azure Stack HCI или Windows Server. Используйте упрощенные рабочие нагрузки для создания виртуальных машин, томов Локальных дисковых пространств, программно-определяемых сетей и многого другого, а также управления ими. Дополнительные сведения см. в статье [Manage Hyper-Converged Infrastructure with Windows Admin Center](use/manage-hyper-converged.md) (Управление гиперконвергентной инфраструктурой с помощью Windows Admin Center).

Ниже представлено видео с обзором, а после него — плакат с более подробной информацией.
> [!VIDEO https://www.youtube.com/embed/WCWxAp27ERk]

[![Плакат Windows Admin Center](media/WAC1910Poster_thumb_small.PNG)](media/WAC1910Poster_thumb.png)

[Скачать PDF](https://github.com/MicrosoftDocs/windowsserverdocs/raw/master/WindowsServerDocs/manage/windows-admin-center/media/WindowsAdminCenter1910Poster.pdf)

## <a name="contents-at-a-glance"></a>Краткий обзор основных понятий

<table>
    <tr></tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Общие сведения</h3>
            <ul>
            <li><a href="understand/what-is.md">Что такое Windows Admin Center?</a>
            <li><a href="understand/faq.md">Вопросы и ответы</a>
            <li><a href="understand/case-studies.md">Практические примеры</a>
            <li><a href="understand/related-management.md">Сопутствующие продукты для управления</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Планирование</h3>
            <ul>
            <li><a href="plan/installation-options.md">Какой тип установки подойдет именно вам?</a>
            <li><a href="plan/user-access-options.md">Варианты доступа пользователей</a>
            <br>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Развертывание</h3>
            <ul>
            <li><a href="deploy/prepare-environment.md">Подготовка среды</a>
            <li><a href="deploy/install.md">Установка Windows Admin Center</a>
            <li><a href="deploy/high-availability.md">Обеспечение высокой доступности</a>
         </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Настройка</h3>
            <ul>
            <li><a href="configure/settings.md">Параметры Windows Admin Center</a>
            <li><a href="configure/user-access-control.md">Управление доступом пользователей и разрешениями</a>
            <li><a href="configure/shared-connections.md">Общие подключения</a>
            <li><a href="configure/using-extensions.md">Расширения</a>
            <li><a href="configure/use-powershell.md">Автоматизация с помощью PowerShell</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Использование</h3>
            <ul>
            <li><a href="use/get-started.md">Запуск и добавление подключений</a>
            <li><a href="use/manage-servers.md">Управление серверами</a>
            <li><a href="use/deploy-hyperconverged-infrastructure.md">Развертывание гиперконвергентной инфраструктуры</a>
            <li><a href="use/manage-hyper-converged.md">Управление гиперконвергентной инфраструктурой</a>
            <li><a href="use/manage-failover-clusters.md">Управление отказоустойчивыми кластерами</a>
            <li><a href="use/manage-virtual-machines.md">Управление виртуальными машинами</a>
            <li><a href="use/logging.md">Ведение журнала</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Подключение к Azure</h3>
            <ul>
            <li><a href="azure/index.md">Гибридные службы Azure</a></li>
            <li><a href="azure/azure-integration.md">Подключение Windows Admin Center к Azure</a></li>
            <li><a href="azure/deploy-wac-in-azure.md">Развертывание Windows Admin Center в Azure</a></li>
            <li><a href="azure/manage-azure-vms.md">Управление виртуальными машинами Azure с помощью Windows Admin Center</a></li>
            </ul>
        </td>
    </tr>
    <tr>
            <td style="vertical-align: top;">
            <h3>Поддержка</h3>
            <ul>
            <li><a href="support/release-history.md">История выпусков</a>
            <li><a href="support/index.md">Политика поддержки</a>
            <li><a href="support/troubleshooting.md">Общие инструкции по устранению неполадок</a>
            <li><a href="support/known-issues.md">Известные проблемы</a>
            </ul>
        </td>
            <td style="vertical-align: top;">
            <h3>Расширение</h3>
            <ul>
            <li><a href="extend/extensibility-overview.md">Обзор расширений</a>
            <li><a href="extend/understand-extensions.md">Общие сведения о расширениях</a>
            <li><a href="extend/developing-extensions.md">Разработка расширения</a>
            <li><a href="extend/publish-extensions.md">Рекомендации</a>
            <li><a href="extend/publish-extensions.md">Публикация расширений</a>
            </ul>
        </td>
    </tr>

</table>

## <a name="video-based-learning"></a>Обучение на основе видео

Далее приводятся несколько ссылок на видеоролики из семинаров конференции Microsoft Ignite 2019.

- [Видео о Windows Admin Center, посвященное раскрытию возможностей гибридной среды Azure](https://aka.ms/WAC-BRK3165)
- [Видео о Windows Admin Center, посвященное новым возможностям и предстоящим переменам](https://aka.ms/WAC-BRK2048)
- [Видео об автоматическом отслеживании, защите и обновлении локальных серверов из Azure с помощью Windows Admin Center](https://aka.ms/WAC-THR2146)
- [Видео о повышении эффективности благодаря сторонним расширениям Windows Admin Center](https://aka.ms/WAC-THR2140)
- [Видео о дополнительных возможностях Windows Admin Center с рекомендациями по развертыванию, настройке и безопасности](https://aka.ms/WAC-THR2135)
- [Видео о Windows Admin Center, посвященное эффективному совместному использованию System Center и Microsoft Azure](https://aka.ms/WAC-THR2176)
- [Видео об использовании гибридных служб Microsoft Azure с Windows Admin Center и Windows Server](https://aka.ms/WAC-THR2073)
- [Видео из интерактивной сессии вопросов и ответов, посвященное управлению гибридной средой сервера с помощью Windows Admin Center](https://aka.ms/WAC-MLS1055)
- [Видео с предоставлением схемы обучения для гибридных технологий управления](https://aka.ms/WAC-HybridMgmtTech)
- [Практическое занятие по Windows Admin Center и гибридной среде](/learn/?WT.mc_id=sitertzn_homepage_learn-redirect-handsonlabs)

Далее приведено несколько ссылок на видеоролики из сеансов конференции Windows Server Summit 2019.

- [Видео о гибридной среде и Windows Admin Center](https://aka.ms/WAC-WSS2019-GoHybridWAC)
- [Видео, посвященное новым возможностям Windows Admin Center версии 1904](https://aka.ms/WAC-WSS2019-WhatsNewv1904)

А вот несколько дополнительных ресурсов:

- [Видео о переосмыслении управления сервером Windows Admin Center](https://aka.ms/WAC-ServerMgmtReimagined)
- [Видео об управлении серверами и виртуальными машинами в любом расположении с помощью Windows Admin Center](https://aka.ms/WAC-Webinar2019)
- [Как приступить к работе с Windows Admin Center](https://www.youtube.com/embed/PcQj6ZklmK0)

## <a name="see-how-customers-are-benefitting-from-windows-admin-center"></a>Узнайте, какую пользу приносит Windows Admin Center клиентам

|     |
| --- |
| "Windows Admin Center сократил время и усилия, которые мы затрачиваем на работу с системой управления, более чем на 75 %".<br> *(Рэнд Моримото (Rand Morimoto), президент, Convergent Computing)* |
| "Благодаря Windows Admin Center мы можем управлять оборудованием наших клиентов удаленно с помощью портала на HTML5 без каких-либо проблем, а полная интеграция с Azure Active Directory позволяет повысить безопасность благодаря многофакторной идентификации".<br/> *(Сильвио ди Бенедетто (Silvio Di Benedetto), основатель и старший консультант, Inside Technologies)* |
| "Мы смогли развертывать SKU [Server Core] более эффективным путем, повысив эффективность работы с ресурсами, безопасность и автоматизацию, при этом мы по-прежнему обеспечиваем хорошую производительность и снижаем число ошибок, которые могут возникнуть при использовании только сценариев". <br/> *(Гильельмо Менгора (Guglielmo Mengora), основатель и генеральный директор, VaiSulWeb)* |
| "Благодаря [Windows Admin Center] наши клиенты, особенно на рынке SMB, теперь имеют удобные средства для управления своей внутренней инфраструктурой. Это минимизирует административную работу и экономит много времени. А самое лучшее вот что: Windows Admin Center не требует дополнительных лицензионных выплат!" <br/> *(Гельмут Отто (Helmut Otto), управляющий директор, SecureGUARD)* |

[Узнайте больше о компаниях, использующих Windows Admin Center в своей рабочей среде.](understand/case-studies.md)

## <a name="related-products"></a>Похожие продукты

Windows Admin Center предназначен для управления одним сервером или кластером серверов. Это средство дополняет, но не заменяет существующие решения для мониторинга и администрирования Майкрософт, такие как средства удаленного администрирования сервера (RSAT), System Center, Intune или Azure Stack.

[Узнайте, как Windows Admin Center дополняет другие решения по управлению от Майкрософт.](understand/related-management.md)

## <a name="stay-updated"></a>Всегда будьте в курсе

[Следите за нашими новостями в Твиттере](https://twitter.com/servermgmt)

[Читайте наши блоги](https://techcommunity.microsoft.com/t5/windows-admin-center-blog/bg-p/Windows-Admin-Center-Blog)