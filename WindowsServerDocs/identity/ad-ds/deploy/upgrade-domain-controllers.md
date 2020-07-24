---
title: Обновление контроллеров домена до Windows Server 2016
description: В этом документе описывается обновление с Windows Server 2012 R2 до Windows Server 2016
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 93b02f79753f4e861c141ced84b29efd078fd227
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961056"
---
# <a name="upgrade-domain-controllers-to-windows-server-2016"></a>Обновление контроллеров домена до Windows Server 2016

Область применения. Windows Server

В этом разделе содержатся фундаментальные сведения о службах домен Active Directory в Windows Server 2016 и объясняется процесс обновления контроллеров домена с Windows Server 2012 или Windows Server 2012 R2.

## <a name="pre-requisites"></a>Предварительные требования

Рекомендуемый способ обновления домена — повысить уровень контроллеров домена, на которых работают более новые версии Windows Server, и при необходимости понизить прежние контроллеры домена. Этот метод является предпочтительным для обновления операционной системы существующего контроллера домена. В этом списке описаны общие шаги, которые необходимо выполнить перед повышением уровня контроллера домена под управлением более новой версии Windows Server.

1. Убедитесь, что целевой сервер отвечает требованиям к системе.
1. Проверьте совместимость приложений.
1. Ознакомьтесь с рекомендациями по переходу на Windows Server 2016
1. Проверьте параметры безопасности. Дополнительные сведения см. [в разделе устаревшие функции и изменения в работе, связанные с AD DS в Windows Server 2016](../../../get-started/deprecated-features.md).
1. Проверьте подключение к целевому серверу с компьютера, где планируется установка.
1. Проверьте доступность необходимых ролей хозяина операций.
   - Чтобы установить первый контроллер домена под управлением Windows Server 2016 в существующем домене и лесу, на компьютере, где выполняется установка, необходимо подключиться к **хозяину схемы** , чтобы запустить adprep/forestprep и хозяин инфраструктуры для запуска Adprep/домаинпреп.
   - Чтобы установить первый контроллер домена в домене, где схема леса уже расширена, требуется подключение только к **хозяину инфраструктуры**.
   - Для установки или удаления домена в существующем лесу необходимо подключение к **хозяину именования доменов**.
   - Для установки контроллера домена также требуется подключение к **хозяину RID.**
   - Если вы устанавливаете первый контроллер домена только для чтения в существующем лесу, вам потребуется подключение к **хозяину инфраструктуры** для каждого раздела каталога приложений, также известного как контекст именования не в ДОМЕНЕ или нднк.

### <a name="installation-steps-and-required-administrative-levels"></a>Этапы установки и требуемые административные уровни

В следующей таблице приведена сводка этапов обновления и требования к разрешениям для выполнения этих действий.

|Действие установки|Требования к учетным данным|
| ----- | ----- |
|Установка нового леса|Локальный администратор на целевом сервере|
|Установка нового домена в существующем лесу|Администраторы предприятия|
|Установка дополнительного контроллера домена в существующем домене|Администраторы домена|
|Выполнение команды adprep /forestprep|Администраторы схемы, администраторы предприятия и администраторы домена|
|Выполнение команды adprep /domainprep|Администраторы домена|
|Выполнение команды adprep /domainprep /gpprep|Администраторы домена|
|Выполнение команды adprep /rodcprep|Администраторы предприятия|

Дополнительные сведения о новых возможностях Windows Server 2016 см. в статье [новые возможности Windows server 2016](../../../get-started/whats-new-in-windows-server-2016.md).

## <a name="supported-in-place-upgrade-paths"></a>Поддерживаемые варианты обновления на месте

Контроллеры домена под управлением 64-разрядных версий Windows Server 2012 или Windows Server 2012 R2 можно обновить до Windows Server 2016. Поддерживаются только обновления 64-разрядных версий, так как Windows Server 2016 поставляется только в виде 64-разрядной версии.

|Используемый выпуск|Доступно обновление до следующих выпусков|
| ----- | ----- |
|Windows Server 2012 Standard|Windows Server 2016 Standard или Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard или Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 Workgroup|Windows Storage Server 2016 Workgroup|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 R2 Workgroup|Windows Storage Server 2016 Workgroup|

Дополнительные сведения о поддерживаемых путях обновления см. в разделе [Поддерживаемые варианты обновления](../../../get-started/supported-upgrade-paths.md) .

## <a name="adprep-and-domainprep"></a>Adprep и domainprep

При выполнении обновления на месте существующего контроллера домена до операционной системы Windows Server 2016 необходимо выполнить adprep/forestprep и adprep/domainprep вручную.  Adprep/forestprep необходимо запустить в лесу только один раз.  Программа adprep/domainprep должна запускаться один раз в каждом домене, в котором имеются контроллеры домена, обновляемые до Windows Server 2016.

При повышении уровня нового сервера Windows Server 2016 вам не нужно запускать их вручную.  Они встроены в PowerShell и диспетчер сервера возможности.

Дополнительные сведения о запуске Adprep см. в разделе [Выполнение Adprep](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)) .

## <a name="functional-level-features-and-requirements"></a>Возможности режимов работы и требования

Для Windows Server 2016 требуется функциональный уровень леса Windows Server 2003. Это значит, что перед добавлением контроллера домена под управлением Windows Server 2016 в существующий лес Active Directory в качестве функционального уровня леса необходимо использовать Windows Server 2003 или более поздней версии. Если в лесу есть контроллеры домена под управлением Windows Server 2003 или новее, но режим работы леса соответствует Windows 2000, то установка также блокируется.

Перед добавлением контроллеров домена Windows Server 2016 в лес необходимо удалить контроллеры домена Windows 2000. В этом случае порядок действий будет следующим.

1. Установите контроллеры домена под управлением Windows Server 2003 или более поздней версии. Эти контроллеры домена можно развертывать в ознакомительной версии Windows Server. Для этого шага нужно также запустить программу adprep.exe для соответствующей операционной системы.
1. Удалите контроллеры домена под управлением Windows 2000. В частности, надлежащим образом понизьте уровень контроллеров домена под управлением Windows Server 2000 или принудительно удалите их из домена и при помощи компонента "Пользователи и компьютеры Active Directory" удалите учетные записи для всех удаленных контроллеров домена.
1. Повысьте режим работы леса до Windows Server 2003 или выше.
1. Установите контроллеры домена под управлением Windows Server 2016.
1. Удалите контроллеры домена под управлением более ранних версий Windows Server.

### <a name="rolling-back-functional-levels"></a>Откат функциональных уровней

После настройки режима работы леса (FFL) на определенное значение невозможно выполнить откат или понижение режима работы леса, за исключением следующих:

- При обновлении с Windows Server 2012 R2 FFL можно уменьшить его до Windows Server 2012 R2.
- При обновлении с Windows Server 2008 R2 FFL можно уменьшить его до Windows Server 2008 R2.

После того как для режима работы домена задано определенное значение, откат или понижение режима работы домена невозможно, за исключением следующих:

- При повышении режима работы домена до Windows Server 2016, если режим работы леса — Windows Server 2012 или более ранняя, у вас есть возможность изменить режим работы домена на Windows Server 2012 или Windows Server 2012 R2.

Дополнительные сведения о возможностях, доступных при более низких режимах работы, см. в разделе [Общее представление о режимах работы доменных служб Active Directory (AD DS)](../active-directory-functional-levels.md).

## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a>Взаимодействие доменных служб Active Directory с другими ролями сервера и операционными системами Windows

Доменные службы Active Directory не поддерживаются в следующих операционных системах Windows:

- Windows MultiPoint Server
- Windows Server 2016 Essentials

Доменные службы Active Directory нельзя установить на сервере, на котором выполняются следующие роли или службы ролей:

- Microsoft Hyper-V Server 2016
- Посредник подключений к удаленному рабочему столу

## <a name="administration-of-windows-server-2016-servers"></a>Администрирование серверов Windows Server 2016

Используйте средства удаленного администрирования сервера для Windows 10, чтобы управлять контроллерами домена и другими серверами под управлением Windows Server 2016. Средства удаленного администрирования сервера Windows Server 2016 можно запустить на компьютере под управлением Windows 10.

## <a name="step-by-step-for-upgrading-to-windows-server-2016"></a>Пошаговые инструкции по обновлению до Windows Server 2016

Ниже приведен простой пример обновления леса contoso с Windows Server 2012 R2 до Windows Server 2016.

![Обновление](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade1.png)

1. Присоедините новый сервер Windows Server 2016 к лесу. При появлении запроса перезагрузите компьютер.

   ![Обновление](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade2.png)

1. Войдите на новый сервер Windows Server 2016 с учетной записью администратора домена.
1. В **Диспетчер сервера**в разделе **Добавление ролей и компонентов**установите **службы домен Active Directory** на новом сервере Windows Server 2016. Программа Adprep будет автоматически запущена в лесу и домене 2012 R2.

   ![Обновление](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade3.png)

1. В **Диспетчер сервера**щелкните желтый треугольник и в раскрывающемся списке выберите **повысить уровень сервера до контроллера домена**.

   ![Обновление](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade4.png)

1. На экране **Конфигурация развертывания** выберите **Добавить контроллер домена в существующий лес** и нажмите кнопку Далее.

   ![Обновление](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade5.png)

1. На экране **параметры контроллера домена** введите пароль в **режиме восстановления служб каталогов (DSRM)** и нажмите кнопку Далее.
1. В оставшейся части экрана нажмите кнопку **Далее**.
1. На экране **Проверка готовности** нажмите кнопку **установить**. После завершения перезагрузки можно снова войти в систему.
1. На сервере Windows Server 2012 R2 в **Диспетчер сервера**в разделе средства выберите **Active Directory модуль для Windows PowerShell**.

   ![Обновление](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade6.png)

1. В Windows PowerShell используйте Move-Аддиректорисервероператионмастерроле для перемещения ролей FSMO. Можно ввести имя каждого параметра-Оператионмастерроле или использовать числа, чтобы указать роли. Дополнительные сведения см. в разделе [Move-аддиректорисервероператионмастерроле](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)) .

    ``` powershell
    Move-ADDirectoryServerOperationMasterRole -Identity "DC-W2K16" -OperationMasterRole 0,1,2,3,4
    ```

    ![Обновление](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade7.png)

1. Убедитесь, что роли перемещены, перейдя на сервер Windows Server 2016, в **Диспетчер сервера**в разделе **средства**выберите **Active Directory модуль для Windows PowerShell**. Используйте `Get-ADDomain` `Get-ADForest` командлеты и для просмотра владельцев ролей FSMO.

    ![Обновление](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade8.png)

    ![Обновление](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade9.png)

1. Понизьте и удалите контроллер домена Windows Server 2012 R2. Сведения о понижении роли контроллера домена см. в статье [понижение роли контроллеров доменов и доменов](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md) .
1. После понижения и удаления сервера можно повысить функциональные уровни леса и функциональных уровней домена до Windows Server 2016.

## <a name="next-steps"></a>Дальнейшие шаги

- [Новые возможности при установке и удалении доменных служб Active Directory](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md)
- [Установка домен Active Directory Services &#40;&#41;уровня 100](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)
- [Режимы работы Windows Server 2016](../active-directory-functional-levels.md)  
