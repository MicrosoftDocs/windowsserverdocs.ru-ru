---
title: Удаленное управление узлами Hyper-V
description: Содержит описание совместимости версии узлов Hyper-V и диспетчера Hyper-V и способ подключения к удаленным узлам в различных средах, включая между доменами и автономный.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2d34e98c-6134-479b-8000-3eb360b8b8a3
author: KBDAzure
ms.author: kathydav
ms.date: 12/06/2016
ms.openlocfilehash: df66f308ee7999f97fe7e57a8b52256f2561faa2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870235"
---
# <a name="remotely-manage-hyper-v-hosts-with-hyper-v-manager"></a>Удаленное управление узлами Hyper-V с помощью диспетчера Hyper-V

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1

В этой статье перечислены поддерживаемые сочетания узлов Hyper-V и диспетчера Hyper-V версий и описывается, как подключиться к удаленных и локальных узлов Hyper-V, чтобы ими можно управлять. 

Диспетчер Hyper-V позволяет управлять небольшое количество узлов Hyper-V, удаленных и локальных. Он устанавливается при установке средств управления Hyper-V, это можно сделать либо с помощью полной установки Hyper-V или только для средства установки. Это средство установки только для инструментов можно использовать средства на компьютерах, которые не соответствуют требования к оборудованию для узлов Hyper-V. Дополнительные сведения об оборудовании для узлов Hyper-V см. в разделе [требования к системе](..\System-requirements-for-Hyper-V-on-Windows.md).

Если диспетчер Hyper-V не установлена, см. в разделе [инструкции](#install-hyper-v-manager) ниже.

## <a name="supported-combinations-of-hyper-v-manager-and-hyper-v-host-versions"></a>Поддерживаемые сочетания диспетчера Hyper-V и версии узлов Hyper-V

В некоторых случаях можно использовать другую версию диспетчера Hyper-V, чем версия Hyper-V на узле, как показано в таблице. При этом Диспетчер Hyper-V предоставляет функции, доступные для версии Hyper-V на узле, которыми вы управляете. Например при использовании версии диспетчера Hyper-V в Windows Server 2012 R2 на удаленном узле под управлением Hyper-V в Windows Server 2012, нельзя будет использовать функции, доступные в Windows Server 2012 R2 на этом узле Hyper-V.

В следующей таблице показаны, какие версии узлов Hyper-V, вы можете управлять из определенной версии диспетчера Hyper-V. Поддерживается только перечислены версии операционной системы. Дополнительные сведения о состоянии поддержки версии конкретной операционной системе, используйте **жизненного цикла продукта поиска** , нажмите кнопку [политика жизненного цикла Майкрософт](https://support.microsoft.com/lifecycle) страницы. Как правило более старые версии диспетчера Hyper-V можно управлять только на узле Hyper-V под управлением той же версии или сравнить версии Windows Server.

|Версия диспетчера Hyper-V | Версия узла Hyper-V|
|---|---|
|Windows 2016, Windows 10|— Windows Server 2016 — все выпусками и вариантами установки, включая Nano Server и соответствующей версией Hyper-V Server <br>— Windows Server 2012 R2 — все выпуски и варианты установки и соответствующей версией Hyper-V Server <br>— Windows Server 2012 — все выпуски и варианты установки и соответствующей версией Hyper-V Server <br> — Windows 10 <br> — Windows 8.1  |
| Windows Server 2012 R2, Windows 8.1 | — Windows Server 2012 R2 — все выпуски и варианты установки и соответствующей версией Hyper-V Server <br>— Windows Server 2012 — все выпуски и варианты установки и соответствующей версией Hyper-V Server <br>— Windows 8.1
| Windows Server 2012 | — Windows Server 2012 — все выпуски и варианты установки и соответствующей версией Hyper-V Server
| Windows Server 2008 R2 с пакетом обновления 1, Windows 7 с пакетом обновления 1 | — Windows Server 2008 R2 — все выпуски и варианты установки и соответствующей версией Hyper-V Server
| Windows Server 2008, Windows Vista с пакетом обновления 2 | — Windows Server 2008 — все выпуски и варианты установки и соответствующей версией Hyper-V Server

>[!NOTE]
>Поддержка пакета обновления прекращена для Windows 8 с 12 января 2016 г. Дополнительные сведения см. в разделе [вопросы и ответы по Windows 8.1](https://support.microsoft.com/help/18581).

## <a name="connect-to-a-hyper-v-host"></a>Подключиться к узлу Hyper-V

Чтобы соединиться с узлом Hyper-V в диспетчере Hyper-V, щелкните правой кнопкой мыши **диспетчера Hyper-V** в левой области, а затем нажмите кнопку **соединение с сервером**.

## <a name="manage-hyper-v-on-a-local-computer"></a>Управление Hyper-V на локальном компьютере

Диспетчер Hyper-V не перечисляет все компьютеры, на которых размещены Hyper-V, пока вы не добавите на компьютере, включая локального компьютера. Выполните указанные ниже действия.

1. В левой области щелкните правой кнопкой мыши **диспетчера Hyper-V**.
2. Нажмите кнопку **соединиться с сервером**.
3. Из **Выбор компьютера**, нажмите кнопку **локального компьютера** и нажмите кнопку **ОК**.

Если не удается подключиться:

* Вполне возможно, что установлены средства Hyper-V. Чтобы проверить, что установлена платформа Hyper-V, найдите службу управления виртуальными машинами. \(Откройте приложение службы рабочего стола: щелкните **запустить**, нажмите кнопку **начать поиск** введите **services.msc**и нажмите клавишу **ввод**. Если служба управления виртуальными машинами нет в списке, установите платформу Hyper-V, следуя инструкциям в [Установка Hyper-V](..\get-started\Install-the-Hyper-V-role-on-Windows-Server.md).\)
* Проверьте, что оборудование соответствует требованиям. См. в разделе [требования к системе](..\System-requirements-for-Hyper-V-on-Windows.md).
* Убедитесь, что учетная запись пользователя принадлежит к группе администраторов или группы администраторов Hyper-V.

## <a name="manage-hyper-v-hosts-remotely"></a>Удаленное управление узлами Hyper-V  

Чтобы управлять удаленными узлами Hyper-V, включите удаленное управление на локальном компьютере и удаленном узле.

Откройте диспетчер сервера на Windows Server, \> **локального сервера** \> **удаленного управления** и нажмите кнопку **разрешить удаленные подключения к этому компьютеру**. 

Или, под управлением операционной системы, откройте Windows PowerShell от имени администратора и запустите: 

```
Enable-PSRemoting
```

### <a name="connect-to-hosts-in-the-same-domain"></a>Подключаться к узлам в одном домене

Windows 8.1 и более ранних версиях удаленного управления работает только в том случае, если узел находится в том же домене и учетной записи локального пользователя также находится на удаленном узле.

Чтобы добавить удаленный узел Hyper-V в диспетчере Hyper-V, выберите **другой компьютер** в **Выбор компьютера** диалоговое окно и введите имя узла удаленного узла, NetBIOS-имя или полное доменное имя \(Полное доменное имя\).

Диспетчер Hyper-V в Windows Server 2016 и Windows 10 предлагает дополнительные типы подключения к удаленному предыдущих версий, описанных в следующих разделах.  

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-as-a-different-user"></a>Подключение к удаленному узлу Windows 2016 или Windows 10, от имени другого пользователя

Это позволяет подключиться к узлу Hyper-V, если не выполняется на локальном компьютере как пользователь, являющийся членом группы администраторов Hyper-V или в группу администраторов на узле Hyper-V. Выполните указанные ниже действия.

1. В левой области щелкните правой кнопкой мыши **диспетчера Hyper-V**.
1. Нажмите кнопку **соединиться с сервером**.
1. Выберите **подключиться от имени другого пользователя** в **Выбор компьютера** диалоговое окно.
1. Выберите **задание пользователя**.

>[!NOTE]
> Это работает только для Windows Server 2016 или Windows 10 **удаленного** узлов.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-using-ip-address"></a>Подключение к Windows 2016 или Windows 10 удаленному узлу, используя IP-адрес

Выполните указанные ниже действия.

1. В левой области щелкните правой кнопкой мыши **диспетчера Hyper-V**.
1. Нажмите кнопку **соединиться с сервером**.
1. Введите IP-адрес в **другой компьютер** текстовое поле.

>[!NOTE]
> Это работает только для Windows Server 2016 или Windows 10 **удаленного** узлов.

### <a name="connect-to-a-windows-2016-or-windows-10-remote-host-outside-your-domain-or-with-no-domain"></a>Подключение к Windows 2016 или Windows 10 удаленного узла за пределами вашего домена или без домена

Выполните указанные ниже действия.

1. На управляемом узле Hyper-V откройте сеанс Windows PowerShell от имени администратора.

1. Создайте правила брандмауэра, необходимые для частной сети зон:   
   
   ```
   Enable-PSRemoting
   ```

2. Чтобы разрешить удаленный доступ для общедоступных зон, включите правила брандмауэра для CredSSP и WinRM:
  
   ```
   Enable-WSManCredSSP -Role server
   ```

    Дополнительные сведения см. в разделе [Enable-PSRemoting](https://technet.microsoft.com/library/hh849694.aspx) и [Enable-WSManCredSSP](https://technet.microsoft.com/library/hh849872.aspx).

Настройте компьютер, которые будут использоваться для управления на узле Hyper-V.

1. Откройте сеанс Windows PowerShell от имени администратора.
1. Выполните следующие команды:

     ```
     Set-Item WSMan:\localhost\Client\TrustedHosts -Value "fqdn-of-hyper-v-host"
     ```
     ```
     Enable-WSManCredSSP -Role client -DelegateComputer "fqdn-of-hyper-v-host"
     ```
1. Может также потребоваться настроить следующую групповую политику: 
    * **Конфигурация компьютера** \> **административные шаблоны** \> **системы** \> **учетные данные делегирования** \> **Разрешить передачу новых учетных данных с проверкой подлинности NTLM-только для сервера**
    * Нажмите кнопку **включить** и добавьте *wsman или полное доменное имя — от hyper-v узла*.
1. Откройте **диспетчера Hyper-V**.
1. В левой области щелкните правой кнопкой мыши **диспетчера Hyper-V**.
1. Нажмите кнопку **соединиться с сервером**.

>[!NOTE]
> Это работает только для Windows Server 2016 или Windows 10 **удаленного** узлов.

Сведения о командлете, см. в разделе [Set-Item](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.management/set-item) и [Enable-WSManCredSSP](https://technet.microsoft.com/library/hh849872.aspx).

## <a name="install-hyper-v-manager"></a>Установка диспетчера Hyper-V

Чтобы использовать средство пользовательского интерфейса, выберите то, для операционной системы на компьютере, откуда будет запускаться Hyper-V Manager:

Откройте диспетчер сервера на Windows Server, \> **управление** \> **Добавить роли и компоненты**. Переместить **функции** странице и разверните **средства удаленного администрирования сервера** \> **средства администрирования ролей** \>  **Средства управления Hyper-V**. 

В Windows, можно найти в диспетчере Hyper-V [любой операционной системе Windows, которая включает Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_compatibility).

1. На рабочем столе Windows нажмите кнопку "Пуск" и начните вводить **программы и компоненты**. 
1. В результатах поиска щелкните **программы и компоненты**.
1. В левой области щелкните **или отключение компонентов Windows включить**.
1. Разверните папку Hyper-V, и **щелкните средства управления Hyper-V**.
1. Чтобы установить Диспетчер Hyper-V, щелкните **средства управления Hyper-V**. Если вы хотите также установить модуль Hyper-V, щелкните соответствующий параметр.

Чтобы использовать Windows PowerShell, выполните следующую команду от имени администратора:

```
add-windowsfeature rsat-hyper-v-tools
```

## <a name="see-also"></a>См. также  
 
[Установка Hyper-V](..\get-started\Install-the-Hyper-V-role-on-Windows-Server.md) 
