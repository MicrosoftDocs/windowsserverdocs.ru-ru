---
title: Подготовка среды для Windows Admin Center
description: Подготовка среды для Windows Admin Center (Project Honolulu)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5506918ed8da3a71c5ca078ce84502a3d889a386
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997454"
---
# <a name="prepare-your-environment-for-windows-admin-center"></a>Подготовка среды для Windows Admin Center

> Применяется к: Windows Admin Center, ознакомительная версия Windows Admin Center

Существует несколько версий Windows Server, которые требуют дополнительной подготовки, прежде чем ими можно будет управлять с помощью Windows Admin Center:

- [Windows Server 2012 и 2012 R2](#prepare-windows-server-2012-and-2012-r2)
- [Microsoft Hyper-V Server 2016](#prepare-microsoft-hyper-v-server-2016)
- [Microsoft Hyper-V Server 2012 R2](#prepare-microsoft-hyper-v-server-2012-r2)

Также есть некоторые сценарии, в которых нужно изменить [конфигурацию портов на целевом сервере](#port-configuration-on-the-target-server), прежде чем выполнять управление с помощью Windows Admin Center.

## <a name="prepare-windows-server-2012-and-2012-r2"></a>Подготовка Windows Server 2012 и 2012 R2

### <a name="install-wmf-version-51-or-higher"></a>Установка WMF версии 5.1 или более поздней версии

Для платформы Windows Admin Center нужны функции PowerShell, которые не входят в состав Windows Server 2012 и 2012 R2R2 по умолчанию. Для управления Windows Server 2012 или 2012 R2 с помощью Windows Admin Center необходимо установить WMF версии 5.1 или более поздней версии на эти серверы.

Введите `$PSVersiontable` в PowerShell, чтобы проверить, что платформа WMF установлена, и что используется версия 5.1 или более поздняя версия.

Если она не установлена, можно [скачать и установить WMF 5.1](/powershell/scripting/wmf/setup/install-configure).

## <a name="prepare-microsoft-hyper-v-server-2016"></a>Подготовка Microsoft Hyper-V Server 2016

Чтобы можно было управлять Microsoft Hyper-V Server 2016 с помощью Windows Admin Center, необходимо включить некоторые роли Windows Server.

### <a name="to-manage-microsoft-hyper-v-server-2016-with-windows-admin-center"></a>Для управления Microsoft Hyper-V Server 2016 с помощью Windows Admin Center выполните следующие действия.

1. Включите удаленное управление.
2. Включите роль файлового сервера.
3. Включите модуль Hyper-V для PowerShell.

### <a name="step-1-enable-remote-management"></a>**Шаг 1.** Включение удаленного управления

Для включения удаленного управления в Hyper-V Server выполните следующие действия.

1. Войдите в Hyper-V Server.
2. В средстве **Настройка сервера** (SCONFIG) введите **4**, чтобы настроить удаленное управление.
3. Введите **1**, чтобы включить удаленное управление.
4. Введите **4** для возврата в главное меню.

### <a name="step-2-enable-file-server-role"></a>**Шаг 2**. Включение роли файлового сервера

Чтобы включить роль файлового сервера для обеспечения базовых возможностей обмена файлами и удаленного управления, выполните следующие действия.

1. В меню **Сервис** выберите пункт **Роли и компоненты**.
2. В разделе **Роли и компоненты** найдите пункт **Файловые службы и службы хранилища** и установите флажки **Файловые службы и службы iSCSI** и **Файловый сервер**:

![Снимок экрана с оснасткой "Роли и компоненты", где отображается выбранный файл и роль служб iSCSI](../media/prepare-environment/prepare-your-environment-image-1.png)

### <a name="step-3-enable-hyper-v-module-for-powershell"></a>**Шаг 3.** Включение модуля Hyper-V для PowerShell

Чтобы включить модуль Hyper-V для функций PowerShell, выполните следующие действия.

1. В меню **Сервис** выберите пункт **Роли и компоненты**.
2. В разделе **Роли и компоненты** найдите пункт **Средства удаленного администрирования сервера** и установите флажки **Средства администрирования ролей** и **Модуль Hyper-V для PowerShell**.

![Снимок экрана с оснасткой "Роли и компоненты", где выбраны роли Hyper-V](../media/prepare-environment/prepare-your-environment-image-2.png)

Теперь сервер Microsoft Hyper-V Server 2016 готов к управлению через Windows Admin Center.

## <a name="prepare-microsoft-hyper-v-server-2012-r2"></a>Подготовка Microsoft Hyper-V Server 2012 R2

Чтобы управлять Microsoft Hyper-V Server 2012 R2 через Windows Admin Center, необходимо включить некоторые роли Windows Server.  Кроме того, необходимо установить WMF версии 5.1 или более поздней версии.

### <a name="to-manage-microsoft-hyper-v-server-2012-r2-with-windows-admin-center"></a>Для управления Microsoft Hyper-V Server 2012 R2 с помощью Windows Admin Center выполните следующие действия.

1. Установите Windows Management Framework (WMF) версии 5.1 или более поздней версии
2. Включение удаленного управления
3. Включение роли файлового сервера
4. Включение модуля Hyper-V для PowerShell

### <a name="step-1-install-windows-management-framework-51"></a>Шаг 1. Установка Windows Management Framework 5.1

Для платформы Windows Admin Center нужны функции PowerShell, которые не входят в состав Microsoft Hyper-V Server 2012 R2 по умолчанию. Для управления Microsoft Hyper-V Server 2012 R2 с помощью Windows Admin Center необходимо установить WMF версии 5.1 или более поздней версии.

Введите `$PSVersiontable` в PowerShell, чтобы проверить, что платформа WMF установлена, и что используется версия 5.1 или более поздняя версия.

Если она не установлена, вы можете [скачать WMF 5.1](/powershell/scripting/wmf/setup/install-configure).

### <a name="step-2-enable-remote-management"></a>Шаг 2. Включение удаленного управления

Для включения удаленного управления Hyper-V Server выполните следующие действия.

1. Войдите в Hyper-V Server.
2. В средстве **Настройка сервера** (SCONFIG) введите **4**, чтобы настроить удаленное управление.
3. Введите **1**, чтобы включить удаленное управление.
4. Введите **4** для возврата в главное меню.

### <a name="step-3-enable-file-server-role"></a>Шаг 3. Включение роли файлового сервера

Чтобы включить роль файлового сервера для обеспечения базовых возможностей обмена файлами и удаленного управления, выполните следующие действия.

1. В меню **Сервис** выберите пункт **Роли и компоненты**.
2. В разделе **Роли и компоненты** найдите пункт **Файловые службы и службы хранилища** и установите флажки **Файловые службы и службы iSCSI** и **Файловый сервер**:

![Снимок экрана с оснасткой "Роли и компоненты", где отображается выбранный файл и роль служб iSCSI](../media/prepare-environment/prepare-your-environment-image-1.png)

### <a name="step-4-enable-hyper-v-module-for-powershell"></a>Шаг 4. Включение модуля Hyper-V для PowerShell

Чтобы включить модуль Hyper-V для функций PowerShell, выполните следующие действия.

1. В меню **Сервис** выберите пункт **Роли и компоненты**.
2. В разделе **Роли и компоненты** найдите пункт **Средства удаленного администрирования сервера** и установите флажки **Средства администрирования ролей** и **Модуль Hyper-V для PowerShell**.

![Снимок экрана с оснасткой "Роли и компоненты", где выбраны средства удаленного администрирования сервера](../media/prepare-environment/prepare-your-environment-image-2.png)

Теперь сервером Microsoft Hyper-V Server 2012 R2 можно управлять с помощью Windows Admin Center.

## <a name="port-configuration-on-the-target-server"></a>Настройка портов на целевом сервере

Windows Admin Center использует протокол общего доступа к файлам SMB для некоторых задач копирования файлов, например при импорте сертификата на удаленном сервере. Чтобы эти операции копирования файлов прошли успешно, брандмауэр на удаленном сервере должен разрешать входящие подключения через порт 445.  Вы можете с помощью средства брандмауэра в Windows Admin Center убедиться, что настроено входящее правило "File Server Remote Management (SMB-In)" (Удаленное управление файловым сервером SMB-in), которое разрешает доступ через этот порт.

> [!Tip]
> Готовы к установке Windows Admin Center? [Скачать](../overview.md#download-now)