---
title: Установка и настройка серверов содержимого
description: Эта статья является частью руководства по развертыванию BranchCache для Windows Server 2016, в котором показано, как развернуть BranchCache в распределенном и размещенном режимах кэша для оптимизации использования пропускной способности глобальной сети в филиалах.
manager: brianlic
ms.topic: get-started-article
ms.assetid: e753c56b-8902-4610-9c53-381e77bf29ab
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c1efeb5d63be8ce5b91c814825b68f9f43ae4049
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954120"
---
# <a name="install-and-configure-content-servers"></a>Установка и настройка серверов содержимого

>Применяется к: Windows Server (Semi-Annual Channel), Windows Server 2016

При развертывании BranchCache в режиме распределенного кэша или в режиме размещенного кэша необходимо развернуть один или несколько серверов содержимого в главном офисе или в облаке. Серверы содержимого, являющиеся веб-серверами или серверами приложений, используют функцию BranchCache. Серверы содержимого, являющиеся файловыми серверами, используют службу роли BranchCache для сетевых файлов роли сервера файловых служб в Windows Server 2016.

Сведения о развертывании серверов содержимого см. в следующих разделах.

-   [Установка серверов содержимого, использующих функцию BranchCache](../../branchcache/deploy/Install-Content-Servers-that-Use-the-BranchCache-Feature.md)

-   [Установка серверов содержимого файловых служб](../../branchcache/deploy/Install-File-Services-Content-Servers.md)



