---
title: Обновление Windows Server 2008 и Windows Server 2008 R2
description: Поддержка Windows Server 2008 и 2008 R2 вскоре будет прекращена. Из этой статьи вы узнаете, как выполнить обновление в локальной среде или разместить эти ОС в Azure.
ms.mktglfcycl: manage
ms.sitesec: library
author: JasonGerend
ms.author: thierryp
ms.date: 07/12/2018
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: a77d65ccf61b424f6a87d9d110dcabe8acf4a173
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101828025"
---
# <a name="upgrade-windows-server-2008-and-windows-server-2008-r2"></a>Обновление Windows Server 2008 и Windows Server 2008 R2

Расширенная поддержка для Windows Server 2008 и Windows Server 2008 R2 закончится 14 января 2020 г. Мы предлагаем два пути модернизации: обновление в локальной среде или перенос путем повторного размещения в Azure. **При повторном размещении в Azure вы можете перенести имеющиеся образы Server бесплатно.**

![Блок-схема с описанием путей обновления Windows Server 2008](media/WS08_upgrade_paths.png)


## <a name="on-premises-upgrade"></a>Локальное обновление
Если требуется оставить серверы в локальной среде и если вы используете Windows Server 2008 или Windows Server 2008 R2, необходимо будет выполнить [обновление до Windows Server 2012/2012 R2](installation-and-upgrade.md#upgrading-to-windows-server-2012-r2), прежде чем вы сможете выполнить [обновление до Windows Server 2016](installation-and-upgrade.md#upgrading-to-windows-server-2016). В ходе обновления у вас останется возможность выполнить перенос в Azure путем повторного размещения.

Подробные сведения о вариантах локального обновления см. в разделе [Upgrading from Windows Server 2008 R2 or Windows Server 2008](installation-and-upgrade.md#upgrading-from-windows-server-2008-r2-or-windows-server-2008) (Обновление с Windows Server 2008 R2 или Windows Server 2008).

Если вы используете Windows Server 2003, необходимо выполнить [обновление до Windows Server 2008](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff972408(v%3dws.10)). Подробные сведения о вариантах локального обновления см. в статье [Windows Server 2008 R2 Upgrade Paths](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/dd979563(v=ws.10)) (Пути обновления для Windows Server 2008 R2).


## <a name="migrate-to-azure"></a>Перенос в Azure
Вы можете перенести локальные серверы Windows Server 2008 и Windows Server 2008 R2 в Azure и продолжить использовать их на виртуальных машинах. В Azure вы обеспечите соответствие нормативным требованиям, повысите уровень защиты и сможете использовать в своей работе преимущества облачных технологий. Преимущества переноса в Azure:

- Обновления системы безопасности в Azure.
- В течение трех дополнительных лет вы будете получать важные обновления системы безопасности для Windows Server 2008 R2 или 2008 без дополнительной платы.
- Бесплатные обновления в Azure.
- Внедрение дополнительных облачных служб по мере готовности.
- При переносе SQL Server в управляемые экземпляры или на виртуальные машины Azure в течение трех дополнительных лет вы будете получать важные обновления системы безопасности для Windows Server 2008 R2 или 2008 без дополнительной платы.
- Только в Azure вы сможете использовать имеющиеся лицензии на SQL Server и Windows Server для экономии на облачных ресурсах.

[![Приступите к переносу в Azure с помощью специализированного образа](./media/WS08-image-banner-small.png)](uploading-specialized-WS08-image-to-azure.md)

Сведения о том, как приступить к переносу, см. в статье [Upload a Windows Server 2008/2008 R2 specialized image to Azure](uploading-specialized-WS08-image-to-azure.md) (Отправка специализированного образа Windows Server 2008 или 2008 R2 в Azure).

Сведения о том, как анализировать имеющиеся ИТ-ресурсы, оценить то, что у вас уже есть, определить преимущества переноса конкретных служб и приложений в облако по сравнению с сохранением рабочих нагрузок в локальной среде, а также понять, какую выгоду вы получите от обновления до последней версии Windows Server, см. в [руководстве по переносу для Windows Server](https://go.microsoft.com/fwlink/?linkid=872689).

## <a name="upgrade-sql-server-20082008-r2-in-parallel-with-your-windows-servers"></a>Обновление SQL Server 2008 или 2008 R2 параллельно с серверами Windows Server

![Логотип SQL Server](media/sqlr2.jpg)

Если вы используете SQL Server 2008 или 2008 R2, вы можете выполнить обновление до SQL Server [2016](/sql/sql-server/sql-server-technical-documentation?view=sql-server-2016&preserve-view=true) или [2017](/sql/sql-server/sql-server-technical-documentation?view=sql-server-2017&preserve-view=true).


## <a name="additional-resources"></a>Дополнительные ресурсы
[Microsoft Azure](/azure/#pivot=products)
