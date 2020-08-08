---
ms.assetid: 4d21d27d-5523-4993-ad4f-fbaa43df7576
title: Advanced AD DS Management Using Active Directory Administrative Center (Level 200)
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.openlocfilehash: 56792ce9c5a98e923627be4d98eba8404e046b46
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971141"
---
# <a name="advanced-ad-ds-management-using-active-directory-administrative-center-level-200"></a>Advanced AD DS Management Using Active Directory Administrative Center (Level 200)

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этой статье рассматривается обновленный Центр администрирования Active Directory и приводится более подробное описание новой корзины Active Directory, детальной политики паролей и средства просмотра журнала Windows PowerShell, включая их архитектуру, примеры задач и информацию об устранении неполадок. Общие сведения см. [в статье Введение в центр администрирования Active Directory улучшения &#40;уровня 100&#41;](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md).

- [Архитектура центра администрирования Active Directory](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Arch)
- [Активация и администрирование новой корзины Active Directory через Центр администрирования Active Directory](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_EnableRecycleBin)
- [Настройка и администрирование детальной политики паролей через Центр администрирования Active Directory](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_FGPP)
- [Использование средства просмотра журнала Windows PowerShell в Центре администрирования Active Directory](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_HistoryViewer)
- [Устранение неполадок в управлении доменными службами Active Directory](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Tshoot)

## <a name="active-directory-administrative-center-architecture"></a><a name="BKMK_Arch"></a>Архитектура центра администрирования Active Directory

### <a name="active-directory-administrative-center-executables-dlls"></a>Центр администрирования Active Directory исполняемых файлов, DLL

Модуль и базовая архитектура Центра администрирования Active Directory с появлением новой корзины Active Directory, детальной политики паролей и средства просмотра журнала не изменились,

- Microsoft.ActiveDirectory.Management.UI.dll
- Microsoft.ActiveDirectory.Management.UI.resources.dll
- Microsoft.ActiveDirectory.Management.dll
- Microsoft.ActiveDirectory.Management.resources.dll
- ActiveDirectoryPowerShellResources.dll

Базовый Windows PowerShell и слой операций для новой корзины представлены ниже:

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/adds_adrestore.png)

## <a name="enabling-and-managing-the-active-directory-recycle-bin-using-active-directory-administrative-center"></a><a name="BKMK_EnableRecycleBin"></a>Активация и администрирование новой корзины Active Directory через Центр администрирования Active Directory

### <a name="capabilities"></a>Характеристики

- Центр администрирования Active Directory Windows Server 2012 или более поздней версии позволяет настраивать корзину Active Directory и управлять ею для любого раздела домена в лесу. Для активации корзины Active Directory или восстановления объектов в разделы доменов больше не нужно использовать Windows PowerShell или Ldp.exe.
- В Центре администрирования Active Directory есть расширенные условия фильтрации, упрощающие адресное восстановление в крупных средах с большим количеством удаленных объектов.

### <a name="limitations"></a>Ограничения

- Поскольку Центр администрирования Active Directory позволяет управлять только разделами доменов, он не может восстанавливать удаленные объекты из разделов "Конфигурация", "DNS-домен" и "DNS-лес" (удалять объекты из раздела "Схема" нельзя). Для восстановления объектов из разделов, не принадлежащих к домену, используйте командлет [Restore-ADObject](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee617262(v=technet.10)).

- Центр администрирования Active Directory не позволяет восстанавливать поддеревья объектов за одно действие. Например, если вы удалите организационное подразделение с вложенными подразделениями, пользователями, группами и компьютерами, то при восстановлении этого организационного подразделения дочерние объекты восстановлены не будут.

    > [!NOTE]
    > Центр администрирования Active Directory операция восстановления пакетной службы выполняет «наилучшую» сортировку удаленных объектов *в выделенном фрагменте* , чтобы родители были упорядочены до дочерних элементов списка восстановления. В простых тестовых случаях поддеревья объектов можно восстановить одним действием. Но в угловых случаях, например при выборе, содержащем частичные деревья деревьев, с некоторыми удаленными родительскими узлами или с ошибками, например при пропуске дочерних объектов, когда происходит сбой при восстановлении родительского объекта, может не работать должным образом. В связи с этим поддеревья объектов необходимо восстанавливать только после восстановления родительских объектов.

Для корзины Active Directory требуется режим работы леса Windows Server 2008 R2. необходимо быть членом группы "Администраторы предприятия". Активированную корзину Active Directory отключить нельзя. Корзина Active Directory увеличивает размер базы данных Active Directory (NTDS.DIT) на каждом контроллере домена в лесу. Объекты сохраняются в корзине вместе со всеми соответствующими данными атрибутов, поэтому со временем она занимает все больше места на диске.

### <a name="enabling-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Активация корзины Active Directory через Центр администрирования Active Directory

Чтобы включить корзину Active Directory, откройте **Центр администрирования Active Directory** и щелкните имя своего леса на панели управления На панели **Задачи** выберите команду **Включить корзину**.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBin.png)

В Центре администрирования Active Directory откроется диалоговое окно **Подтверждение включения корзины**. Оно содержит предупреждение о том, что операция включения корзины необратима. Нажмите кнопку **ОК**, чтобы включить корзину Active Directory. В Центре администрирования Active Directory откроется другое диалоговое окно с сообщением о том, что корзина Active Directory не будет функционировать полностью, пока изменения в конфигурации не будут реализованы на всех контроллерах доменов.

> [!IMPORTANT]
> Параметр включения корзины Active Directory недоступен, если:
>
> - функциональный уровень леса ниже Windows Server 2008 R2;
> - корзина уже включена.

Эквивалент Active Directory командлета Windows PowerShell:

```powershell
Enable-ADOptionalFeature
```

Дополнительные сведения об использовании Windows PowerShell для включения корзины Active Directory см. в статье [Пошаговое руководство по использованию корзины Active Directory](./introduction-to-active-directory-administrative-center-enhancements--level-100-.md#active-directory-recycle-bin-step-by-step).

### <a name="managing-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Управление корзиной Active Directory через Центр администрирования Active Directory

В этом разделе в качестве примера используется существующий домен **corp.contoso.com**. Он объединяет пользователей в организационное подразделение **UserAccounts**. Организационное подразделение **UserAccounts** содержит три подразделения, каждое из которых, в свою очередь, содержит свои подразделения, пользователей и группы.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBinExampleOU.png)

#### <a name="storage-and-filtering"></a>Хранение и фильтрация

Все объекты, удаленные в лесу, попадают в корзину Active Directory. Объекты хранятся в соответствии с атрибутом **msDS-deletedObjectLifetime**, который по умолчанию совпадает с атрибутом **tombstoneLifetime** леса. В любом лесу, созданном с помощью Windows Server 2003 SP1 или более поздней версии, значение атрибута **tombstoneLifetime** по умолчанию устанавливается равным 180 дням. В любом лесу, обновленном с Windows 2000 или установленном с помощью Windows Server 2003 (без пакетов обновления), атрибут tombstoneLifetime по умолчанию НЕ УСТАНАВЛИВАЕТСЯ, поэтому Windows использует внутреннее значение по умолчанию, равное 60 дням. Все эти параметры можно настраивать. Для восстановления объектов, удаленных из разделов доменов в лесу, можно использовать Центр администрирования Active Directory. Для восстановления объектов, удаленных из других разделов, например из раздела "Конфигурация", используйте командлет **Restore-ADObject**. При включении корзины Active Directory под каждым разделом домена в Центре администрирования Active Directory появляется контейнер **Удаленные объекты**.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_DeletedObjectsContainer.png)

Контейнер **Удаленные объекты** содержит список всех доступных для восстановления объектов в этом разделе домена. Удаленные объекты с превышенным значением атрибута **msDS-deletedObjectLifetime** называются утилизированными. Центр администрирования Active Directory не показывает утилизированные объекты и не позволяет их восстановить.

Более подробно архитектура и принципы работы корзины описываются в статье [Корзина Active Directory: общие сведения, реализация, рекомендации и устранение неполадок](/archive/blogs/askds/the-ad-recycle-bin-understanding-implementing-best-practices-and-troubleshooting).

Центр администрирования Active Directory искусственно ограничивает количество отображаемых в контейнере объектов до 20 000 штук. Чтобы увеличить этот лимит до 100 000 объектов, откройте меню **Управление** и выберите пункт **Параметры списка управления**.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_MgmtList.png)

#### <a name="restoration"></a>Восстановление

##### <a name="filtering"></a>Фильтрация

Центр администрирования Active Directory предлагает эффективные критерии поиска и параметры фильтрации, которые необходимо изучить до того, как они вам потребуются в реальной жизни. Домены специально удаляют множество объектов с истекшим сроком хранения. Учитывая, что срок хранения объектов обычно составляет 180 дней, в случае инцидента вы просто не сможете восстановить все объекты.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_AddCriteria.png)

Вместо того чтобы составлять сложные фильтры LDAP и конвертировать значения UTC в даты и время, составьте список соответствующих объектов с помощью простого и расширенного меню **Фильтр**. Если вы знаете дату удаления, названия объектов или другие ключевые данные, используйте их в качестве фильтра. Для переключения расширенных параметров фильтрации используйте шевроны справа от поля поиска.

Операция восстановления поддерживает все стандартные параметры фильтрации точно так же, как и другие поисковые службы. Из встроенных фильтров для восстановления объектов обычно используются следующие:

- *ANR (разрешение неоднозначных имен — не указано в меню, но используется при вводе в поле * * * * Фильтр * * * *)*
- Последнее изменение между заданными датами
- Объект — пользователь, InetOrgPerson, компьютер, группа или организационное подразделение
- name
- Дата удаления
- Последний известный родительский объект
- Тип
- Описание
- Город
- Страна или регион
- отдел;
- Код сотрудника
- Имя
- Должность
- Фамилия
- SAMaccountname
- Область, республика, край, округ
- Номер телефона
- Имя участника-пользователя
- почтовый индекс

Можно добавить несколько критериев. Например, можно найти все объекты-пользователи, удаленные 24 сентября 2012 из Чикаго, Иллинойс с заголовком должности менеджер.

Вы также можете добавить, изменить или переупорядочить заголовки столбцов, чтобы получить больше данных для выбора объектов к восстановлению.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ColumnHeaders.png)

Дополнительные сведения о разрешении неоднозначных имен см. в разделе [Атрибуты ANR](/windows/win32/adschema/attributes-anr).

##### <a name="single-object"></a>Один объект

Восстановление удаленных объектов всегда выполнялось в одно действие.  Центр администрирования Active Directory упрощает эту операцию. Чтобы восстановить удаленный объект, например отдельного пользователя, выполните указанные ниже действия.

1. Щелкните имя домена на панели управления Центра администрирования Active Directory.
2. Дважды щелкните **Удаленные объекты** в списке управления.
3. Щелкните нужный объект правой кнопкой мыши и выберите команду **Восстановить** или выберите команду **Восстановить** на панели **Задачи**.

Объект вернется в свое исходное расположение.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreSingle.gif)

Нажмите кнопку **восстановить в...** , чтобы изменить расположение для восстановления. Это полезно, если родительский контейнер удаленного объекта также был удален, но вы не хотите восстанавливать его.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreToSingle.gif)

##### <a name="multiple-peer-objects"></a>Несколько аналогичных объектов

Вы можете восстановить сразу несколько объектов одного уровня, например всех пользователей организационного подразделения. Удерживая клавишу CTRL, щелкните один или несколько удаленных объектов, которые нужно восстановить. Щелкните **Восстановить** на панели задач. Вы также можете выбрать все указанные объекты, нажав комбинацию клавиш CTRL+A, или определенный диапазон объектов, нажав и удерживая клавишу SHIFT, а затем первый и последний искомые объекты.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestorePeers.png)

##### <a name="multiple-parent-and-child-objects"></a>Несколько дочерних и родительских объектов

Центр администрирования Active Directory не позволяет восстанавливать вложенные деревья удаленных объектов за одно действие, поэтому восстанавливать объекты нужно в определенном порядке.

1. Восстановите верхний удаленный объект в дереве.
2. Восстановите дочерние элементы этого родительского объекта.
3. Восстановите дочерние элементы этих родительских объектов.
4. Повторяйте процедуру, пока не будут восстановлены все объекты.

Восстановить дочерний объект можно только после того, как будет восстановлен родительский, в противном случае система выдаст следующую ошибку:

**Эта операция не может быть выполнена, т.к. родитель объекта либо не подтвержден, либо удален.**

Родительские отношения каждого объекта обозначаются атрибутом **Последний известный родительский объект**. При обновлении Центра администрирования Active Directory после восстановления родительского объекта атрибут **Последний известный родительский объект** переносится из удаленного в восстановленное расположение. Таким образом, можно восстановить этот дочерний объект, если расположение родительского объекта больше не показывает различающееся имя контейнера удаленных объектов.

Предположим, что администратор случайно удалил организационное подразделение Sales, содержащее дочерние подразделения и пользователей.

Сначала обратите внимание на значение **последнего известного родительского** атрибута для всех удаленных пользователей и как он считывает **OU = Sales\0ADEL:*<GUID + Deleted Objects различающееся имя контейнера> * * *:

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParent.gif)

Отфильтруйте неоднозначное имя Sales. Вы получите список удаленных подразделений, которые затем нужно будет восстановить:

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSales.png)

Обновите центр администрирования Active Directory, чтобы увидеть, что последний известный родительский атрибут объекта User изменился на восстановленное различающееся имя подразделения продаж:

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesRestored.gif)

Отфильтруйте всех пользователей подразделения Sales. Нажмите комбинацию клавиш CTRL+A, чтобы выбрать всех удаленных пользователей подразделения Sales. Щелкните **Восстановить**, чтобы перенести объекты из контейнера **Удаленные объекты** в организационное подразделение Sales с теми же атрибутами и членством в группах.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesUndelete.png)

Если организационное подразделение **Sales** включало дочерние подразделения, восстановите сначала эти подразделения, а затем их дочерние объекты и т. д.

Порядок восстановления всех вложенных удаленных объектов путем указания удаленного родительского контейнера см. в [Приложении Б. Восстановление сразу нескольких удаленных объектов Active Directory (образец сценария)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379504(v=ws.10)).

Командлет Active Directory в Windows PowerShell, предназначенный для восстановления удаленных объектов, выглядит следующим образом:

```powershell
Restore-adobject
```

Командлет **Restore-ADObject** в Windows Server 2008 R2 и Windows Server 2012 работает одинаково.

##### <a name="server-side-filtering"></a>Фильтрация на стороне сервера

С течением времени число объектов в контейнере "Удаленные объекты" в средних и крупных организациях может вырасти до 20 000 (и даже 100 000), после чего возникнут сложности с отображением полного списка объектов. Поскольку механизм фильтрации в Центре администрирования Active Directory использует фильтрацию на стороне клиента, он не может отображать объекты сверх установленного лимита. Чтобы обойти это ограничение, выполните поиск на стороне сервера согласно приведенным ниже инструкциям.

1. Щелкните контейнер **Удаленные объекты** правой кнопкой мыши и выберите команду **Искать в этом узле**.
2. Щелкните шеврон, чтобы открыть меню **Добавить условия**, а затем выберите и добавьте параметр **Последнее изменение между заданными датами**. Последнее изменение между заданными датами (атрибут **whenChanged**) будет приближено к времени удаления, а в некоторых средах эти значения будут идентичны. Этот запрос запускает поиск на стороне сервера.
3. Выберите удаленные объекты для восстановления с помощью дополнительной фильтрации, сортировки и других действий с результатами поиска, а затем восстановите объекты как обычно.

## <a name="configuring-and-managing-fine-grained-password-policies-using-active-directory-administrative-center"></a><a name="BKMK_FGPP"></a>Настройка и администрирование детальной политики паролей через Центр администрирования Active Directory

### <a name="configuring-fine-grained-password-policies"></a>Настройка детальной политики паролей

Центр администрирования Active Directory позволяет создавать объекты детальной политики паролей (FGPP) и управлять такими объектами. Функция FGPP была представлена в Windows Server 2008, но первый графический интерфейс для управления этой функцией появился только в Windows Server 2012. Детальная политика паролей настраивается на уровне домена и позволяет перезаписывать единый пароль домена, предусмотренный в Windows Server 2003. При создании различных FGPP с различными параметрами отдельные пользователи или группы получают различные политики паролей в домене.

Информацию о детальной политике паролей см. в [пошаговом руководстве по детальной настройке политик блокировки учетных записей и паролей доменных служб Active Directory (Windows Server 2008 R2)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770842(v=ws.10)).

На панели навигации выберите представление в виде дерева, щелкните свой домен, **Система**, **Контейнер параметров паролей**, а затем на панели "Задачи" щелкните **Создать** и **Параметры пароля**.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_PasswordSettings.png)

### <a name="managing-fine-grained-password-policies"></a>Управление детальной политикой паролей

При создании новой или редактировании уже существующей детальной политики паролей открывается редактор **Параметры пароля**. Здесь можно настроить все желаемые политики паролей как Windows Server 2008 или Windows Server 2008 R2, но только в специальном редакторе.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_CreatePasswordSettings.png)

Заполните все обязательные (отмеченные звездочкой) и желаемые дополнительные поля и щелкните **Добавить**, чтобы указать, к каким пользователям или группам необходимо применить эту политику. FGPP перезаписывает параметры политики домена по умолчанию для выбранных субъектов безопасности. На представленном выше рисунке максимально ограничивающая политика применяется только к встроенной учетной записи администратора, чтобы предотвратить компрометацию. Эта политика слишком сложна для ее соблюдения стандартными пользователями, но идеально подходит для учетной записи высокого риска, которой пользуются только специалисты.

Также необходимо указать очередность применения и выбрать пользователей и группы для применения политики в соответствующем домене.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_Precedence.png)

Командлет Active Directory в Windows PowerShell, предназначенный для настройки детальной политики паролей, выглядит следующим образом:

```powershell
Add-ADFineGrainedPasswordPolicySubject
Get-ADFineGrainedPasswordPolicy
Get-ADFineGrainedPasswordPolicySubject
New-ADFineGrainedPasswordPolicy
Remove-ADFineGrainedPasswordPolicy
Remove-ADFineGrainedPasswordPolicySubject
Set-ADFineGrainedPasswordPolicy
```

Командлет для настройки детальной политики паролей в Windows Server 2008 R2 и Windows Server 2012 работает одинаково. На приведенном ниже рисунке обозначены соответствующие атрибуты для этих командлетов:

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPP.gif)

Центр администрирования Active Directory позволяет также найти результирующую детальную политику паролей, примененную к конкретному пользователю. Щелкните правой кнопкой мыши любого пользователя и выберите пункт **просмотреть результирующие параметры пароля...** , чтобы открыть страницу *параметров пароля* , которая применяется к этому пользователю при явном или неявном назначении:

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RSOP.png)

В разделе **Свойства** вы найдете **Напрямую связанные параметры пароля** — параметры детальной политики пароля, назначенные соответствующему пользователю или группе напрямую:

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPPSettings.gif)

Неявное назначение ФГПП здесь не отображается; для этого необходимо использовать параметр **просмотреть результирующие параметры пароля...** .

## <a name="using-the-active-directory-administrative-center-windows-powershell-history-viewer"></a><a name="BKMK_HistoryViewer"></a>Использование средства просмотра журнала Windows PowerShell в Центре администрирования Active Directory

Будущее управления Windows связано с Windows PowerShell. Благодаря размещению графических средств поверх платформы автоматизации задач управление сложнейшими распределенными системами стало последовательным и эффективным. Зная принципы работы Windows PowerShell, вы сможете полностью раскрыть свой потенциал и извлечь максимальную пользу из своих инвестиций в компьютерное оборудование.

Теперь Центр администрирования Active Directory позволяет просматривать историю выполнения всех командлетов Windows PowerShell, включая их аргументы и значения. При этом историю командлетов можно скопировать для дальнейшего изучения или изменения и повторного использования. Вы можете создавать примечания к задачам и описывать, какой результат команды Центра администрирования Active Directory дали в Windows PowerShell. Также можно фильтровать историю на предмет интересных моментов.

Средство просмотра журнала Windows PowerShell в Центре администрирования Active Directory позволяет учиться на основе практического опыта.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_HistoryViewer.gif)

Чтобы открыть средство просмотра журнала Windows PowerShell, нажмите на шеврон (стрелку).

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RaiseViewer.png)

Затем создайте пользователя или измените членство в группе. Средство просмотра журнала постоянно обновляется — в нем появляется свернутое представление каждого командлета, выполненного Центром администрирования Active Directory, и указываются его аргументы.

Разверните любую интересующую вас строку, чтобы увидеть значения всех аргументов командлета:

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ViewArgs.png)

Откройте меню **Запустить задачу** и создайте заметку, а затем воспользуйтесь Центром администрирования Active Directory для создания, изменения или удаления объекта. Укажите свои действия.  Закончив внесение изменений, выберите команду **Закончить задачу**. В заметке к задаче все выполненные действия будут представлены в виде свернутого примечания, позволяющего лучше понять суть задачи.

Например, все команды Windows PowerShell, которые использовались для изменения пароля пользователя и удаления пользователя из группы, будут выглядеть следующим образом:

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RemoveUser.gif)

Если установить флажок "Показать все", в окне появятся также командлеты Windows PowerShell с глаголом Get-*, предназначенные только для извлечения данных.

![Расширенное управление AD DS](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ShowAll.png)

В средстве просмотра журнала отображаются тексты всех команд, выполненных Центром администрирования Active Directory, и может показаться, что некоторые команды выполняются без причины. Например, создать нового пользователя можно с помощью команды:

```powershell
new-aduser
```

и нет необходимости использовать команды:

```powershell
set-adaccountpassword
enable-adaccount
set-aduser
```

Структура Центра администрирования Active Directory предусматривает минимальное использование кодов и модулей. Таким образом, вместо отдельных наборов функций для создания новых пользователей и изменения уже существующих он выполняет каждую задачу по минимуму, а затем соединяет их воедино с помощью командлетов. Помните об этом при изучении модуля Active Directory в Windows PowerShell. Эту особенность можно также использовать как способ изучения, показывающий, как просто выполнять отдельные задачи с помощью Windows PowerShell.

## <a name="troubleshooting-ad-ds-management"></a><a name="BKMK_Tshoot"></a>Устранение неполадок в управлении доменными службами Active Directory

### <a name="introduction-to-troubleshooting"></a>Общие сведения об устранении неполадок

Ввиду относительной новизны и небольшого опыта применения в реальных условиях доступные в Центре администрирования Active Directory варианты устранения неполадок довольно ограниченны.

### <a name="troubleshooting-options"></a>Способы устранения неполадок

#### <a name="logging-options"></a>Параметры ведения журнала

Центр администрирования Active Directory теперь содержит встроенное ведение журнала в составе файла конфигурации трассировки. Создайте или измените следующий файл, расположенный в той же папке, что и файл dsac.exe:

**dsac.exe.config**

Создайте следующее содержимое:

```xml
<appSettings>
  <add key="DsacLogLevel" value="Verbose" />
</appSettings>
<system.diagnostics>
 <trace autoflush="false" indentsize="4">
  <listeners>
   <add name="myListener"
    type="System.Diagnostics.TextWriterTraceListener"
    initializeData="dsac.trace.log" />
   <remove name="Default" />
  </listeners>
 </trace>
</system.diagnostics>
```

Уровни детализации для параметра **DsacLogLevel** — это **None **(Нет), **Error **(Ошибки), **Warning** (Предупреждения), **Info** (Информация) и **Verbose** (Подробно). Выходной файл записывается в папку с файлом dsac.exe, и его можно переименовать. Выходные данные позволяют узнать больше о том, как работает ADAC, с какими контроллерами доменов устанавливается связь, что делают команды Windows PowerShell, какие ответы были получены и другие данные.

Например, при использовании уровня детализации INFO (Информация) выдаются все результаты, кроме данных на уровне трассировки:

- Запускается файл DSAC.exe.
- Начинается ведение журнала.
- Запрашиваются исходные данные домена с контроллера домена.

   ```
   [12:42:49][TID 3][Info] Command Id, Action, Command, Time, Elapsed Time ms (output), Number objects (output)
   [12:42:49][TID 3][Info] 1, Invoke, Get-ADDomainController, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] Get-ADDomainController-Discover:$null-DomainName:"CORP"-ForceDiscover:$null-Service:ADWS-Writable:$null
   ```

- Домен Corp возвращает контроллер домена DC1.
- Загружается виртуальный диск PS AD.

   ```
   [12:42:49][TID 3][Info] 1, Output, Get-ADDomainController, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] Found the domain controller 'DC1' in the domain 'CORP'.
   [12:42:49][TID 3][Info] 2, Invoke, New-PSDrive, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] New-PSDrive-Name:"ADDrive0"-PSProvider:"ActiveDirectory"-Root:""-Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 2, Output, New-PSDrive, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 3, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49
   ```

- Извлекаются данные домена Root DSE.

   ```
   [12:42:49][TID 3][Info] Get-ADRootDSE -Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 3, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 4, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49
   ```

- Извлекаются данные корзины Active Directory.

   ```
   [12:42:49][TID 3][Info] Get-ADOptionalFeature -LDAPFilter:"(msDS-OptionalFeatureFlags=1)" -Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 4, Output, Get-ADOptionalFeature, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 5, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] Get-ADRootDSE -Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 5, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 6, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] Get-ADRootDSE -Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 6, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 7, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] Get-ADOptionalFeature -LDAPFilter:"(msDS-OptionalFeatureFlags=1)" -Server:"dc1.corp.contoso.com"
   [12:42:50][TID 3][Info] 7, Output, Get-ADOptionalFeature, 2012-04-16T12:42:50, 1
   [12:42:50][TID 3][Info] 8, Invoke, Get-ADForest, 2012-04-16T12:42:50
   ```

- Извлекается лес Active Directory.

   ```
   [12:42:50][TID 3][Info] Get-ADForest -Identity:"corp.contoso.com" -Server:"dc1.corp.contoso.com"
   [12:42:50][TID 3][Info] 8, Output, Get-ADForest, 2012-04-16T12:42:50, 1
   [12:42:50][TID 3][Info] 9, Invoke, Get-ADObject, 2012-04-16T12:42:50
   ```

- Извлекаются данные схемы по поддерживаемым типам шифрования, детальная политика паролей, данные определенных пользователей.

   ```
   [12:42:50][TID 3][Info] Get-ADObject
   -LDAPFilter:"(|(ldapdisplayname=msDS-PhoneticDisplayName)(ldapdisplayname=msDS-PhoneticCompanyName)(ldapdisplayname=msDS-PhoneticDepartment)(ldapdisplayname=msDS-PhoneticFirstName)(ldapdisplayname=msDS-PhoneticLastName)(ldapdisplayname=msDS-SupportedEncryptionTypes)(ldapdisplayname=msDS-PasswordSettingsPrecedence))"
   -Properties:lDAPDisplayName
   -ResultPageSize:"100"
   -ResultSetSize:$null
   -SearchBase:"CN=Schema,CN=Configuration,DC=corp,DC=contoso,DC=com"
   -SearchScope:"OneLevel"
   -Server:"dc1.corp.contoso.com"
   [12:42:50][TID 3][Info] 9, Output, Get-ADObject, 2012-04-16T12:42:50, 7
   [12:42:50][TID 3][Info] 10, Invoke, Get-ADObject, 2012-04-16T12:42:50
   ```

- Извлекается вся информация об объекте домена, которая будет показываться администратору при выборе заголовка домена.

   ```
   [12:42:50][TID 3][Info] Get-ADObject
   -IncludeDeletedObjects:$false
   -LDAPFilter:"(objectClass=*)"
   -Properties:allowedChildClassesEffective,allowedChildClasses,lastKnownParent,sAMAccountType,systemFlags,userAccountControl,displayName,description,whenChanged,location,managedBy,memberOf,primaryGroupID,objectSid,msDS-User-Account-Control-Computed,sAMAccountName,lastLogonTimestamp,lastLogoff,mail,accountExpires,msDS-PhoneticCompanyName,msDS-PhoneticDepartment,msDS-PhoneticDisplayName,msDS-PhoneticFirstName,msDS-PhoneticLastName,pwdLastSet,operatingSystem,operatingSystemServicePack,operatingSystemVersion,telephoneNumber,physicalDeliveryOfficeName,department,company,manager,dNSHostName,groupType,c,l,employeeID,givenName,sn,title,st,postalCode,managedBy,userPrincipalName,isDeleted,msDS-PasswordSettingsPrecedence
   -ResultPageSize:"100"
   -ResultSetSize:"20201"
   -SearchBase:"DC=corp,DC=contoso,DC=com"
   -SearchScope:"Base"
   -Server:"dc1.corp.contoso.com"
   ```

Выбранный уровень Verbose (Подробно) включает стеки .NET для каждой функции, однако отражаемые данные могут пригодиться только при устранении неполадок с файлом Dsac.exe, связанных с нарушением прав доступа или аварийным сбоем. Такая проблема может возникнуть по двум причинам:

- На одном из запрашиваемых контроллеров доменов не запущена веб-служба Active Directory.
- Сетевая связь блокируется службой ADWS с компьютера, на котором выполняется центр администрирования Active Directory.

> [!IMPORTANT]
> Существует также отдельная версия этой службы, которая называется [Active Directory Management Gateway](https://www.microsoft.com/download/en/details.aspx?displaylang=en&id=2852)и работает в среде Windows Server 2008 с пакетом обновления 2 (SP2) и Windows Server 2003 с пакетом обновления 2 (SP2).
>

В отсутствие доступных экземпляров веб-служб Active Directory отображаются следующие ошибки:

|Ошибка|Операция|
| --- | --- |
|"Не удается подключиться к какому-либо домену. Обновите состояние или попробуйте еще раз, когда подключение станет доступным".|Отображается при запуске приложения "Центр администрирования Active Directory".|
|"Не удается найти доступный сервер в *<NetBIOS domain name>* домене, на котором выполняется веб-служба Active Directory (ADWS)"|Отображается при попытке выбора узла домена в приложении "Центр администрирования Active Directory"|

Для решения этой проблемы выполните указанные ниже действия.

1. Убедитесь в том, что веб-служба Active Directory запущена хотя бы на одном контроллере домена (а лучше на всех контроллерах доменов в лесу). Убедитесь в том, что на всех контроллерах доменов настроен автоматический запуск веб-службы.
2. С компьютера, на котором запущено приложение "Центр администрирования Active Directory", проверьте возможность связи с сервером, на котором выполняется веб-служба Active Directory, выполнив команды NLTest.exe:

   ```
   nltest /dsgetdc:<domain NetBIOS name> /ws /force
   nltest /dsgetdc:<domain fully qualified DNS name> /ws /force
   ```

   Если связь не устанавливается несмотря на то, что веб-служба Active Directory запущена, то проблема связана с разрешением имен или LDAP, а не с Центром администрирования Active Directory. Если веб-служба Active Directory не запущена ни на одном контроллере домена, выдается ошибка "1355 0x54B ERROR_NO_SUCH_DOMAIN", тем не менее прежде чем делать какие-то выводы, проверьте все еще раз.

3. На контроллере домена, полученном после выполнения команды NLTest, введите дамп списка портов прослушивания с помощью следующей команды:

   ```
   Netstat -anob > ports.txt
   ```

   Изучите файл ports.txt и убедитесь в том, что веб-служба Active Directory прослушивает порт 9389. Пример

   ```
   TCP    0.0.0.0:9389    0.0.0.0:0    LISTENING    1828
   [Microsoft.ActiveDirectory.WebServices.exe]

   TCP    [::]:9389       [::]:0       LISTENING    1828
   [Microsoft.ActiveDirectory.WebServices.exe]
   ```

   Если порт прослушивается, проверьте правила брандмауэра Windows — они должны разрешать входящий трафик по TCP-порту 9389. По умолчанию контроллеры доменов включают правило "Веб-службы Active Directory (TCP-входящий)". Если порт не прослушивается, еще раз проверьте, запущена ли служба на этом сервере, и перезапустите ее. Проверьте, не прослушивают ли порт 9389 какие-либо другие процессы.

4. Установите NetMon или другую утилиту для записи сетевых данных на компьютер с запущенным Центром администрирования Active Directory и на контроллер домена, выданный командой NLTEST. Запустите запись сетевых данных на обоих компьютерах с компьютера, где запущен Центр администрирования Active Directory, посмотрите ошибки и остановите запись. Убедитесь в том, что клиент способен отправлять и принимать данные с контроллера домена через порт TCP 9389. Если пакеты отправляются, но не поступают, а также если пакеты поступают, а ответы контроллера домена не достигают клиента, скорее всего, между компьютерами в сети существует брандмауэр, который теряет пакеты в этом порту. Брандмауэр может быть программным или аппаратным, а может входить в программу защиты (антивирус) стороннего разработчика.

## <a name="see-also"></a>См. также:

[Корзина AD, детальная политика паролей и журнал PowerShell](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md)
