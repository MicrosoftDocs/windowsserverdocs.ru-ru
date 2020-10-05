---
title: Добавление необходимых тегов метаданных в статью, связанную с Windows Server
description: Список сведений, которые необходимо добавить в качестве тегов метаданных, в начало статей, посвященных Windows Server. Необходимые теги могут изменяться в зависимости от требований к отчетности и команде.
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: 7728d6e9bb2c1e5a6ad53f638f253c53a0720059
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/05/2020
ms.locfileid: "91717751"
---
# <a name="add-the-required-metadata-tags-to-your-windows-server-related-article"></a>Добавление необходимых тегов метаданных в статью, связанную с Windows Server

В начале каждой статьи есть определенные метаданные, которые необходимо включать в целях отслеживания и SEO. Необходимые теги могут быть изменены в зависимости от требований к отчетам. Однако если необходимо добавить или удалить какие-либо поля, необходимо получать уведомления.

Он должен выглядеть следующим образом, включая три дефиса (---) в верхней и нижней части:

```markdown
---
title: Required. The title of the article should go here. This is used in SEO and search results.
description: Required. A description for the article should go here. This is used in search results, to provide users with information about whether the article has the information they're looking for.
author: Required. Your GitHub alias
ms.author: Required. Your Microsoft alias
manager: Optional. Your manager's Microsoft alias
ms.reviewer: Optional. The Microsoft alias for the primary PM for the feature/functionality
ms.topic: Type of article, including conceptual, how-to, hub-page, overview, quickstart, reference, sample, troubleshooting, or tutorial
ms.date: Date of change (MM/DD/YYYY)

---
```

## <a name="example"></a>Пример

```markdown
---
title: What is Windows Admin Center?
description: Learn about the Windows Admin Center, a locally-deployed, browser-based management tool set that lets you manage your Windows Servers with no Azure or cloud dependency.
author: danielle-github
ms.author: danielle
manager: alainch
ms.reviewer: alainch
ms.topic: overview
ms.date: 07/06/2019

---
```