---
title: Установка роли Hyper-V в Windows Server
description: Содержит инструкции по установке Hyper-V с помощью диспетчер сервера или Windows PowerShell.
manager: dongill
ms.topic: get-started-article
ms.assetid: 8e871317-09d2-4314-a6ec-ced12b7aee89
author: kbdazure
ms.author: kathydav
ms.date: 12/02/2016
ms.openlocfilehash: 32632e7af3db0c3b390606bc784b929e76b2892f
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997595"
---
# <a name="install-the-hyper-v-role-on-windows-server"></a>Установка роли Hyper-V в Windows Server

>Область применения. Windows Server 2016, Windows Server 2019

Чтобы создать и запустить виртуальные машины, установите роль Hyper-V в Windows Server с помощью диспетчер сервера или командлета **Install-WindowsFeature** в Windows PowerShell.
Для Windows 10 см. статью [Установка Hyper-V в Windows 10](/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).

Дополнительные сведения о Hyper-V см. в статье [Обзор технологии Hyper-v](../Hyper-V-Technology-Overview.md). Чтобы испытать Windows Server 2019, можно скачать и установить ознакомительную версию. См. [Центр оценки](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019).

Перед установкой Windows Server или добавлением роли Hyper-V убедитесь, что:
- Оборудование компьютера совместимо. Дополнительные сведения см. в разделе [требования к системе для Windows Server](../../../get-started/System-Requirements.md) и [требования к системе для Hyper-V в Windows Server](../System-requirements-for-Hyper-V-on-Windows.md).
- Вы не планируете использовать сторонние приложения виртуализации, использующие те же функции процессора, которые требуются Hyper-V. Примеры включают VMWare Workstation и VirtualBox. Вы можете установить Hyper-V без удаления этих приложений. Но если вы попытаетесь использовать их для управления виртуальными машинами при запуске гипервизора Hyper-V, виртуальные машины могут не запускаться или могут работать ненадежно. Дополнительные сведения и инструкции по отключению низкоуровневой оболочки Hyper-V при необходимости использования одного из этих приложений см. в статье [приложения виртуализации не работают вместе с Hyper-V, Device Guard и Credential Guard](https://support.microsoft.com/help/3204980/virtualization-applications-do-not-work-together-with-hyper-v-device-g).

Если вы хотите установить только средства управления, такие как диспетчер Hyper-V, см. раздел [Удаленное управление узлами Hyper-v с помощью диспетчера Hyper-v](../Manage/Remotely-manage-Hyper-V-hosts.md).

## <a name="install-hyper-v-by-using-server-manager"></a>Установка Hyper-V с помощью диспетчер сервера

1. В **диспетчере серверов** в меню **Управление** выберите **Добавить роли и компоненты**.

2. На странице **Приступая к работе** убедитесь, что конечный сервер и сетевое окружение подготовлены к установке нужной вам роли или компонента. Щелкните **Далее**.

3. На странице **Выбор типа установки** выберите **Установка ролей или компонентов** и нажмите кнопку **Далее**.

4. На странице **Выбор целевого сервера** выберите сервер из пула серверов и нажмите кнопку **Далее**.

5. На странице **Выбор ролей сервера** выберите **Hyper-V**.

6. Чтобы добавить средства для создания виртуальных машин и управления ими, щелкните **Добавить компоненты**. На странице "Компоненты" нажмите кнопку **Далее**.

7. Выберите нужные параметры на страницах **Создание виртуальных коммутаторов**, **Миграция виртуальной машины** и **Хранилища по умолчанию**.

8. На странице **Подтверждение выбранных элементов для установки** выберите **Автоматический перезапуск конечного сервера, если требуется** и нажмите кнопку **Установить**.

9. После завершения установки убедитесь, что Hyper-V установлен правильно. Откройте страницу **все серверы** в Диспетчер сервера и выберите сервер, на котором установлена Hyper-V. Просмотрите плитку **роли и компоненты** на странице выбранного сервера.

## <a name="install-hyper-v-by-using-the-install-windowsfeature-cmdlet"></a>Установка Hyper-V с помощью командлета Install-WindowsFeature

1. На рабочем столе Windows нажмите кнопку "Пуск" и введите любую часть имени **Windows PowerShell**.

2. Щелкните правой кнопкой мыши Windows PowerShell и выберите команду **Запуск от имени администратора**.

3. Чтобы установить Hyper-V на сервере, к которому вы подключены удаленно, выполните следующую команду и замените `<computer_name>` именем сервера.

    ```powershell
    Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart
    ```

    Если вы подключены локально к серверу, выполните команду без `-ComputerName <computer_name>` .

4. После перезагрузки сервера можно увидеть, что роль Hyper-V установлена и узнать, какие другие роли и компоненты установлены, выполнив следующую команду:

    ```powershell
    Get-WindowsFeature -ComputerName <computer_name>
    ```

    Если вы подключены локально к серверу, выполните команду без `-ComputerName <computer_name>` .

> [!NOTE]
> Если установить эту роль на сервере, на котором выполняется параметр установки Server Core в Windows Server 2016 и использовать параметр `-IncludeManagementTools` , устанавливается только модуль Hyper-V для Windows PowerShell. Для удаленного управления узлом Hyper-V, работающим в установке Server Core, можно использовать средство управления графического интерфейса пользователя (диспетчер Hyper-V) на другом компьютере. Инструкции по удаленному подключению см. в статье [Удаленное управление узлами Hyper-v с помощью диспетчера Hyper-v](../Manage/Remotely-manage-Hyper-V-hosts.md).

## <a name="additional-references"></a>Дополнительные ссылки

- [Install-WindowsFeature](/powershell/module/Microsoft.Windows.ServerManager.Migration/Install-WindowsFeature)