---
title: Устранение неполадок сервера Nano Server
description: Консоль восстановления, службы аварийного управления, отладка на уровне ядра
manager: DonGill
ms.date: 09/06/2017
ms.topic: article
ms.assetid: e427c66f-9571-4b8c-b65d-e7370d91544d
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 2eae28145013342718c6a0e83ca99311c6504f78
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87959232"
---
# <a name="troubleshooting-nano-server"></a>Устранение неполадок сервера Nano Server

>Область применения. Windows Server 2016

> [!IMPORTANT]
> Начиная с Windows Server версии 1709, сервер Nano Server будет доступен только в качестве [базового образа ОС контейнера](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image). Его описание см. в статье об [изменениях сервера Nano Server](nano-in-semi-annual-channel.md).

Этот раздел содержит сведения о средствах, которые можно использовать для подключения к установкам сервера Nano Server, их диагностики и восстановления.

## <a name="using-the-nano-server-recovery-console"></a>Использование агента восстановления Nano Server

Сервер Nano Server содержит агент восстановления, который гарантирует вам доступ к Nano Server, даже если этому препятствует неправильная конфигурация. Вы можете воспользоваться агентом восстановления для исправления сети, а затем применить привычные средства удаленного управления.

При загрузке сервера Nano Server на любую виртуальную машину или на физический компьютер с подключенным монитором и клавиатурой отображается полноэкранный текстовый режим входа в систему. Войдите в систему с помощью учетной записи администратора, чтобы узнать имя компьютера и IP-адрес сервера Nano Server. Для перемещения по консоли можно применить эти команды:

-   Используйте клавиши со стрелками для прокрутки

-   Используйте клавишу TAB для перемещения к любому тексту, который начинается с **>** ; затем нажмите клавишу ВВОД для выбора.

-   Для возврата на один экран или одну страницу назад нажмите клавишу ESC. Если нажать клавишу ESC на домашней странице, выполняется выход из системы.

-   Некоторые экраны предоставляют дополнительные возможности, указанные в последней строке экрана. Например, нажав клавишу F4 при просмотре сетевого адаптера, вы отключите его.

Агент восстановления позволяет просматривать и настраивать сетевые адаптеры и параметры TCP/IP, а также правила брандмауэра.
> [!NOTE]
> Агент восстановления поддерживает только базовые функции клавиатуры. Индикаторы клавиатуры, добавочные панели на 10 клавиш и переключение раскладки клавиатуры (например, клавиши CAPS LOCK и NUM LOCK) не поддерживается. Поддерживаются только английские буквы и кодировка.

## <a name="accessing-nano-server-over-a-serial-port-with-emergency-management-services"></a>Доступ к серверу Nano Server через последовательный порт с помощью служб аварийного управления
Службы аварийного управления (EMS) позволяют устранить основные неполадки, получить состояние сети и открыть консольные сеансы (включая CMD/PowerShell) с помощью эмулятора терминала через последовательный порт. Это устраняет потребность в клавиатуре и мониторе при устранении неполадок на сервере. Дополнительные сведения о службах EMS см. в разделе [Технический справочник по службам аварийного управления](/previous-versions/windows/it-pro/windows-server-2003/cc784411(v=ws.10)).

Чтобы включить EMS в образе Nano Server для использования в дальнейшем, запустите этот командлет:

`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\EnablingEMS.vhdx   -EnableEMS   -EMSPort 3   -EMSBaudRate 9600`

Этот пример включает EMS через последовательный порт 3 со скоростью 9600 бит/с. Если не указать эти параметры, по умолчанию используется порт 1 и скорость 115 200 бит/с. Чтобы использовать этот командлет для носителя VHDX, не забудьте включить функцию Hyper-V и соответствующие модули Windows PowerShell.

## <a name="kernel-debugging"></a>Отладка ядра
Можно настроить образ Nano Server для поддержки разных методов отладки ядра. Чтобы использовать отладку ядра с образом VHDX, не забудьте включить функцию Hyper-V и соответствующие модули Windows PowerShell. Дополнительные сведения об удаленной отладке ядра см. в статьях [Ручная настройка отладки в режиме ядра через сетевой кабель](/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection) и [Удаленная отладка с помощью WinDbg](/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection).

### <a name="debugging-using-a-serial-port"></a>Отладка с использованием последовательного порта
Используйте этот пример командлета, чтобы включить отладку образа через последовательный порт:

`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingSerial   -DebugMethod Serial   -DebugCOMPort 1   -DebugBaudRate 9600`

В этом примере включается отладка через последовательный порт 2 со скоростью 9600 бит/с. Если не указать эти параметры, по умолчанию используется порт 2 и скорость 115 200 бит/с. Если вы планируете использовать как EMS, так и отладку ядра, следует настроить для них два разных последовательных порта.

### <a name="debugging-over-a-tcpip-network"></a>Отладка по сети TCP/IP
Используйте этот пример командлета, чтобы включить отладку образа по сети TCP/IP:

`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingNetwork   -DebugMethod Net   -DebugRemoteIP 192.168.1.100   -DebugPort 64000`

Этот командлет включает отладку ядра таким образом, чтобы подключаться мог только компьютер с IP-адресом 192.168.1.100, при этом обмен данными осуществляется через порт 64 000. Параметры -DebugRemoteIP и -DebugPort являются обязательными при номере порта больше 49 152. В файле, хранящемся вместе с сформированным виртуальным жестким диском, этот командлет создает ключ шифрования, который требуется для обмена данными через порт. Кроме того, с помощью параметра -DebugKey можно указать собственный ключ, как показано в следующем примере:

`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingNetwork   -DebugMethod Net   -DebugRemoteIP 192.168.1.100   -DebugPort 64000   -DebugKey 1.2.3.4`

### <a name="debugging-using-the-ieee1394-protocol-firewire"></a>Отладка с использованием протокола IEEE1394 (Firewire)
Чтобы включить отладку через IEEE1394, используйте этот пример командлета:

`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingFireWire   -DebugMethod 1394   -DebugChannel 3`

Параметр -DebugChannel является обязательным.

### <a name="debugging-using-usb"></a>Отладка с использованием USB
Отладку через USB можно включить с помощью этого командлета:

`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingUSB   -DebugMethod USB   -DebugTargetName KernelDebuggingUSBNano`

При подключении удаленного отладчика к полученному серверу Nano Server укажите целевое имя в том виде, в котором оно задано в параметре -DebugTargetName.
