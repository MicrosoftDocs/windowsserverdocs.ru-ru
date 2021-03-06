---
ms.assetid: 5b9fc9c1-5d12-4ad4-8ddc-3b8a6d45b217
title: Создание отношения доверия с проверяющей стороной
description: Узнайте, как создать отношение доверия с проверяющей стороной вручную и использовать метаданные федерации.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 949ff74ea3fbb4518b1463709d798c945d1a3b5b
ms.sourcegitcommit: 6717decb5839aa340c81811d6fde020aabaddb3b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/26/2021
ms.locfileid: "98781905"
---
# <a name="create-a-relying-party-trust"></a>Создание отношения доверия с проверяющей стороной


Следующий документ содержит сведения о создании отношения доверия с проверяющей стороной вручную и использовании метаданных федерации.

## <a name="to-create-a-claims-aware-relying-party-trust-manually"></a>Создание отношения доверия с проверяющей стороной с поддержкой утверждений вручную

Чтобы добавить новое отношение доверия с проверяющей стороной с помощью оснастки управления AD FS \- в и вручную настроить параметры, выполните следующую процедуру на сервере федерации.

Для выполнения этой процедуры требуется членство в группе **Администраторы** или в эквивалентной группе на локальном компьютере.  Просмотрите сведения об использовании соответствующих учетных записей и членстве в группах в [локальной среде и группах домена по умолчанию](https://go.microsoft.com/fwlink/?LinkId=83477).

1. В диспетчере сервера щелкните **Средства** и выберите **Управление AD FS**.

2. В разделе **действия** щелкните **Добавить отношение доверия с проверяющей стороной**.

    ![Снимок экрана: диалоговое окно AD FS с параметром добавить отношение доверия с проверяющей стороной в области действий с именем out.](media/Create-a-Relying-Party-Trust/addtrust1.PNG)

3. На странице **приветствия** выберите **Claims aware** (Поддерживающие утверждения) и нажмите кнопку **Начало**.

    ![Снимок экрана: страница приветствия мастера добавления отношения доверия с проверяющей стороной с выбранным параметром "с учетом утверждений".](media/Create-a-Relying-Party-Trust/addtrust2.PNG)

4. На странице **Выбор источника данных** щелкните **Ввод данных о проверяющей стороне вручную** и нажмите кнопку **Далее**.

    ![Снимок экрана: страница "Выбор источника данных" мастера добавления отношения доверия с проверяющей стороной, показывающая параметр "ввести данные о проверяющей стороне вручную".](media/Create-a-Relying-Party-Trust/addtrust3.PNG)

5. На странице **Specify Display Name** (Указание отображаемого имени) введите имя в поле **Отображаемое имя**. В поле **Примечания** введите описание для этого отношения доверия с проверяющей стороной и нажмите кнопку **Далее**.

    ![Снимок экрана: страница "укажите отображаемое имя" мастера добавления отношения доверия с проверяющей стороной.](media/Create-a-Relying-Party-Trust/addtrust4.PNG)

6. На странице **Настройка сертификата** при наличии необязательного сертификата шифрования маркеров нажмите кнопку **Обзор** , чтобы найти файл сертификата, а затем нажмите кнопку **Далее**.

    ![Снимок экрана: страница "Настройка сертификата" мастера добавления отношения доверия с проверяющей стороной с вызываемой кнопкой "Обзор".](media/Create-a-Relying-Party-Trust/addtrust5.PNG)

7. На странице **Настройка URL-адреса** выполните одно или оба следующих действия, нажмите кнопку **Далее**, а затем перейдите к шагу 8.

    - Установите флажок **включить поддержку \- пассивного протокола WS Federation** . В поле **\- URL-адрес пассивного протокола WS Federation проверяющей** стороны введите URL-адрес для этого отношения доверия с проверяющей стороной и нажмите кнопку **Далее**.

    - Установите флажок **Включить поддержку протокола WebSSO SAML 2.0** . В разделе **URL-адрес службы saml 2,0 SSO проверяющей** стороны введите \( язык разметки зявлений системы безопасности (SAML) \) URL-адрес конечной точки службы SAML для этого отношения доверия с проверяющей стороной, а затем нажмите кнопку **Далее**.

    ![Снимок экрана: страница "Настройка сертификата" мастера добавления отношения доверия с проверяющей стороной, в которой показана описанная выше конфигурация.](media/Create-a-Relying-Party-Trust/addtrust6.PNG)

8. На странице **Настройка удостоверений** укажите один или несколько идентификаторов этой проверяющей стороны, нажмите кнопку **Добавить**, чтобы добавить их в список, а затем нажмите кнопку **Далее**.

    ![Снимок экрана: страница "Настройка идентификаторов" мастера добавления отношений доверия с проверяющей стороной, отображающая идентификаторы, добавленные в раздел идентификаторы доверия проверяющей стороны.](media/Create-a-Relying-Party-Trust/addtrust8.PNG)

9. На странице **Choose Access Control Policy** (Выбрать политику управления доступом) выберите политику и нажмите кнопку **Далее**.  Дополнительные сведения о политиках управления доступом см. [в разделе политики управления доступом в AD FS](Access-Control-Policies-in-AD-FS.md).

    ![Снимок экрана: страница "Выбор политики контроля доступа" мастера добавления отношений доверия с проверяющей стороной, в которой отображается параметр "разрешить всем и требовать MFA".](media/Create-a-Relying-Party-Trust/addtrust9.PNG)

10. На странице **Готовность для добавления отношения доверия** проверьте параметры, а затем нажмите кнопку **Далее**, чтобы сохранить сведения об отношениях доверия с проверяющей стороной.

    ![Снимок экрана со страницей "готово к добавлению доверия" мастера добавления отношений доверия с проверяющей стороной.](media/Create-a-Relying-Party-Trust/addtrust10.PNG)

11. На странице **Готово** нажмите кнопку **Закрыть**. После этого автоматически откроется диалоговое окно **Изменение правил утверждений**.

    ![Снимок экрана: страница "завершение" мастера добавления отношения доверия с проверяющей стороной.](media/Create-a-Relying-Party-Trust/addtrust11.PNG)

## <a name="to-create-a-claims-aware-relying-party-trust-using-federation-metadata"></a>Создание отношения доверия с проверяющей стороной с поддержкой утверждений с помощью метаданных федерации

Чтобы добавить новое отношение доверия с проверяющей стороной, используя оснастку управления AD FS, автоматически импортируя данные конфигурации партнера из метаданных федерации, опубликованных партнером в локальной сети или в Интернете, выполните следующую процедуру на сервере федерации в организации партнера по учетным записям.

>[!NOTE]
>Хотя распространенной практикой является использование сертификатов с неполными именами узлов https://myserver , например, эти сертификаты не имеют значения безопасности и могут позволить злоумышленнику олицетворять служба Федерации, который публикует метаданные федерации. Поэтому при запросе метаданных федерации следует использовать только полное доменное имя, например https://myserver.contoso.com .

Для выполнения этой процедуры требуется членство в группе **Администраторы** или в эквивалентной группе на локальном компьютере.  Просмотрите сведения об использовании соответствующих учетных записей и членстве в группах в [локальной среде и группах домена по умолчанию](https://go.microsoft.com/fwlink/?LinkId=83477).

1. В диспетчере сервера щелкните **Средства** и выберите **Управление AD FS**.

2. В разделе **действия** щелкните **Добавить отношение доверия с проверяющей стороной**.

    ![Еще один снимок экрана диалогового окна AD FS с параметром добавить отношение доверия с проверяющей стороной в области действия вызываемая.](media/Create-a-Relying-Party-Trust/addtrust1.PNG)

3. На странице **приветствия** выберите **Claims aware** (Поддерживающие утверждения) и нажмите кнопку **Начало**.

    ![Еще один снимок экрана страницы приветствия мастера добавления отношения доверия с проверяющей стороной с выбранным параметром с поддержкой утверждений.](media/Create-a-Relying-Party-Trust/addtrust2.PNG)

4. На странице **Выбор источника данных** щелкните **Импорт данных о поставщике утверждений, опубликованных в Интернете или локальной сети**. В поле **Адрес метаданных федерации (имя узла или URL-адрес)** введите URL-адрес метаданных федерации или имя узла для партнера, а затем нажмите кнопку **Далее**.

    ![Снимок экрана: страница "Выбор источника данных" мастера добавления отношения доверия с проверяющей стороной, на которой отображаются данные импорта проверяющей стороны, опубликованной в Интернете или в локальной сети.](media/Create-a-Relying-Party-Trust/addtrust12.PNG)

5. На странице Указание отображаемого имени введите имя в поле **Отображаемое** имя, в разделе Заметки введите описание отношения доверия с проверяющей стороной и нажмите кнопку **Далее**.

6. На странице Выбор правил авторизации выдачи выберите **Разрешить всем пользователям доступ к этой проверяющей стороне** или **Отказать всем пользователям в доступе к этой проверяющей стороне**, а затем нажмите кнопку **Далее**.

7. На странице Ready to Add Trust (Готовность для добавления отношения доверия) проверьте параметры и нажмите кнопку **Далее**, чтобы сохранить сведения об отношении доверия с проверяющей стороной.

8. На странице Готово нажмите кнопку **Закрыть**. После этого автоматически откроется диалоговое окно Изменение правил утверждений. Дополнительные сведения о добавлении правил утверждения для отношений доверия с этой проверяющей стороной см. в разделе "Дополнительные материалы".




## <a name="see-also"></a>См. также:
[Операции AD FS](../ad-fs-operations.md)
