---
title: Установка Windows Admin Center
description: Сведения об установке Windows Admin Center на компьютер или на сервер с Windows, чтобы несколько пользователей могли получить доступ к Windows Admin Center с помощью веб-браузера.
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: df5e7e2c23b9120a890b34448868ec4d5b1c99b3
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997407"
---
# <a name="install-windows-admin-center"></a>Установка Windows Admin Center

> Применяется к: Windows Admin Center, ознакомительная версия Windows Admin Center

В этой статье описывается установка Windows Admin Center на компьютер или на сервер с Windows, чтобы несколько пользователей могли получить доступ к Windows Admin Center с помощью веб-браузера.

> [!Tip]
> Только начинаете знакомство с Windows Admin Center?
> [Узнайте дополнительные сведения о Windows Admin Center](../overview.md) или [скачайте платформу](https://aka.ms/windowsadmincenter).

## <a name="determine-your-installation-type"></a>Определение типа установки

Просмотрите [варианты установки](../plan/installation-options.md), в том числе [поддерживаемые операционные системы](../plan/installation-options.md#installation-supported-operating-systems). Чтобы установить Windows Admin Center на виртуальной машине в Azure, обратитесь к статье о [развертывании Windows Admin Center в Azure](../azure/deploy-wac-in-azure.md).

## <a name="install-on-windows-10"></a>Установка в Windows 10

При установке в Windows 10 платформа Windows Admin Center будет использовать порт 6516 по умолчанию, однако вы можете указать другой порт. Вы также можете создать ярлык для рабочего стола и разрешить Windows Admin Center управлять вашими доверенными узлами TrustedHosts.

> [!NOTE]
> Изменение доверенных узлов необходимо в среде рабочей группы или при использовании учетных данных локального администратора в домене. Если вы решили отказаться от этого параметра, необходимо [вручную настроить доверенные узлы](../support/troubleshooting.md#configure-trustedhosts).

При запуске Windows Admin Center из меню **Пуск** платформа откроется в браузере по умолчанию.

При запуске Windows Admin Center в первый раз вы увидите значок в области уведомлений на рабочем столе. Щелкните его правой кнопкой мыши и выберите команду **Открыть**, чтобы открыть инструмент в браузере по умолчанию, или выберите **Выход** для завершения фонового процесса.

## <a name="install-on-windows-server-with-desktop-experience"></a>Установка в ОС Windows Server с возможностями рабочего стола

В среде Windows Server платформа Windows Admin Center устанавливается как сетевая служба. Необходимо указать порт для прослушивания. Кроме того, требуется сертификат для протокола HTTPS. Установщик может создать самозаверяющий сертификат для тестирования. Вы также можете предоставить отпечаток сертификата, уже установленного на компьютере. Если вы используете созданный сертификат, он должен соответствовать DNS-имени сервера. Если вы используете собственный сертификат, убедитесь, что указанное в нем имя совпадает с именем компьютера (групповые сертификаты не поддерживаются). Вы также вы получаете возможность разрешить Windows Admin Center управлять доверенными узлами.

> [!NOTE]
> Изменение доверенных узлов необходимо в среде рабочей группы или при использовании учетных данных локального администратора в домене. Если вы решили отказаться от этого параметра, необходимо [вручную настроить доверенные узлы](../support/troubleshooting.md#configure-trustedhosts).

После завершения установки откройте браузер с удаленного компьютера и перейдите по URL-адресу, представленному на последнем шаге установки.

> [!WARNING]
> Срок действия автоматически созданных сертификатов — 60 дней после установки.

## <a name="install-on-server-core"></a>Установка в среде основных серверных компонентов

Если у вас установлены основные серверные компоненты Windows Server, вы можете установить Windows Admin Center из командной строки (с правами администратора). Укажите порт и SSL-сертификат с использованием аргументов `SME_PORT` и `SSL_CERTIFICATE_OPTION` соответственно. Если вы собираетесь использовать существующий сертификат, укажите его отпечаток с помощью `SME_THUMBPRINT`.

> [!WARNING]
> Установка Windows Admin Center приведет к перезапуску службы WinRM, которая завершит все удаленные сеансы PowerShell. Установку рекомендуется выполнять из локальной командной строки или PowerShell. Если вы выполняете установку с использованием решения автоматизации, которое будет прервано перезапуском службы WinRM, можно добавить параметр ```RESTART_WINRM=0``` к аргументам установки, но для работы Windows Admin Center следует перезапустить WinRM.

Выполните следующую команду, чтобы установить Windows Admin Center и автоматически создать самозаверяющий сертификат.

```
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SSL_CERTIFICATE_OPTION=generate
```

Выполните следующую команду для установки Windows Admin Center с существующим сертификатом.

```
msiexec /i <WindowsAdminCenterInstallerName>.msi /qn /L*v log.txt SME_PORT=<port> SME_THUMBPRINT=<thumbprint> SSL_CERTIFICATE_OPTION=installed
```

> [!WARNING]
> Не вызывайте `msiexec` из PowerShell с использованием относительной нотации пути (например, `.\<WindowsAdminCenterInstallerName>.msi`). Эта нотация не поддерживается. В результате установка завершится ошибкой. Удалите префикс `.\` или укажите полный путь к MSI-файлу.

## <a name="upgrading-to-a-new-version-of-windows-admin-center"></a>Обновление до новой версии Windows Admin Center

Вы можете обновить версии Windows Admin Center (не ознакомительные), используя Центр обновления Майкрософт или установив их вручную.

При обновлении до новой версии Windows Admin Center ваши параметры сохраняются. Корпорация Майкрософт официально не поддерживает обновление версий Windows Admin Center типа Insider Preview. Рекомендуется выполнить чистую установку, но это не обязательно.

## <a name="updating-the-certificate-used-by-windows-admin-center"></a>Обновление сертификата, используемого Windows Admin Center

При развертывании Windows Admin Center в качестве службы необходимо предоставить сертификат для протокола HTTPS. Чтобы обновить этот сертификат позже, повторно запустите установщик и выберите ```change```.