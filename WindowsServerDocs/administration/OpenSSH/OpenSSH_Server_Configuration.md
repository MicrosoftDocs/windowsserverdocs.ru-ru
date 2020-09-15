---
title: Конфигурация сервера OpenSSH для Windows
description: Сведения о конфигурации сервера OpenSSH для Windows 10 1809 и Windows Server 2019.
ms.date: 09/27/2018
ms.topic: conceptual
ms.author: damaerte
author: maertendmsft
ms.openlocfilehash: e24ba7d0cef92d700b9078422069c8c0461cf516
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078331"
---
# <a name="openssh-server-configuration-for-windows-10-1809-and-server-2019"></a>Конфигурация сервера OpenSSH для Windows 10 версии 1809 и Windows Server 2019

В этой статье описывается настройка сервера OpenSSH (sshd) для ОС Windows.

Для OpenSSH предоставляется подробная документация по параметрам конфигурации на веб-сайте [OpenSSH.com](https://www.openssh.com/manual.html), и мы не намерены дублировать ее в этом пакете документации.

## <a name="configuring-the-default-shell-for-openssh-in-windows"></a>Настройка стандартной оболочки OpenSSH для Windows

Стандартная оболочка командной строки предоставляет пользователю интерфейс, который он увидит при подключении к серверу по протоколу SSH.
По умолчанию в среде Windows изначально используется командная оболочка Windows (cmd.exe).
Кроме того, Windows включает PowerShell и Bash, и вы можете настроить в качестве оболочки по умолчанию для сервера любую из оболочек командной строки сторонних производителей, которые предоставляются для Windows.

Чтобы задать командную оболочку по умолчанию, для начала убедитесь, что папка установки OpenSSH находится в системном пути.
В среде Windows по умолчанию она устанавливается в папку SystemDrive:WindowsDirectory\System32\openssh.
Следующие команды позволяют узнать текущее значение пути (переменную среды path) и добавить к нему стандартную папку установки OpenSSH.

Командная оболочка | Используемая команда
------------- | --------------
Команда | путь
PowerShell | $env:path

Настройка оболочки SSH по умолчанию выполняется в реестре Windows, где вам нужно добавить полный путь к исполняемому файлу оболочки в строковое значение DefaultShell в разделе Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH.

Например, следующая команда PowerShell устанавливает PowerShell.exe в качестве оболочки по умолчанию:

```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## <a name="windows-configurations-in-sshd_config"></a>Конфигурация Windows в файле sshd_config

В среде Windows программа sshd по умолчанию считывает данные конфигурации из файла %programdata%\ssh\sshd_config, но вы можете указать другой файл конфигурации, запустив команду sshd.exe с параметром -f.
Если указанный файл отсутствует, sshd создаст новый файл с конфигурацией по умолчанию при запуске службы.

Ниже перечислены элементы конфигурации специально для среды Windows, которые можно указать в sshd_config.
Существуют и другие параметры конфигурации, которые здесь не перечислены, так как они подробно описаны в [документации по OpenSSH для Win32](https://github.com/powershell/win32-openssh/wiki) в Интернете.


### <a name="allowgroups-allowusers-denygroups-denyusers"></a>AllowGroups, AllowUsers, DenyGroups, DenyUsers

Управление тем, какие пользователи и группы могут подключаться к серверу, осуществляется с помощью директив AllowGroups, AllowUsers, DenyGroups и DenyUsers.
Директивы разрешения и запрета обрабатываются в следующем порядке: DenyUsers, AllowUsers, DenyGroups и наконец AllowGroups.
Все имена учетных записей должны быть указаны в нижнем регистре.
Дополнительные сведения о шаблонах с подстановочными знаками вы найдете в разделе PATTERNS непосредственно в файле ssh_config.

При настройке правил для пользователей и (или) групп в домене используйте следующий формат: ``` user?domain* ```.
Windows поддерживает несколько форматов для указания субъектов домена, но многие из них конфликтуют со стандартными шаблонами в Linux.
По этой причине добавлен символ *, чтобы поддерживать полные доменные имена.
Кроме того, этот подход использует "?" вместо "\@", чтобы избежать конфликтов с форматом username@host.

Пользователи и группы, входящие в рабочие группы, а также подключенные к Интернету учетные записи всегда разрешаются в имена локальных учетных записей (без сегмента домена, примерно как стандартные имена в UNIX).
Пользователи и группы домена строго разрешаются в формат [NameSamCompatible](/windows/desktop/api/secext/ne-secext-extended_name_format), то есть "короткое_имя_домена\имя_пользователя".
Все правила конфигурации для пользователей и групп должны соответствовать этому формату.

Примеры для пользователей и групп домена

```
DenyUsers contoso\admin@192.168.2.23 : blocks contoso\admin from 192.168.2.23
DenyUsers contoso\* : blocks all users from contoso domain
AllowGroups contoso\sshusers : only allow users from contoso\sshusers group
```

Примеры для локальных пользователей и групп

```
AllowUsers localuser@192.168.2.23
AllowGroups sshusers
```

### <a name="authenticationmethods"></a>AuthenticationMethods

Для OpenSSH в Windows поддерживаются только методы проверки подлинности "password" и "publickey".

### <a name="authorizedkeysfile"></a>AuthorizedKeysFile

По умолчанию используется значение .ssh/authorized_keys .ssh/authorized_keys2. Если путь не является абсолютным, он вычисляется относительно основного каталога пользователя (или пути к образу профиля). Например: c:\users\user. Обратите внимание, что если пользователь входит в группу администраторов, используется %programdata%/ssh/administrators_authorized_keys.

### <a name="chrootdirectory-support-added-in-v7700"></a>ChrootDirectory (добавлена поддержка в версии 7.7.0.0)

Эта директива поддерживается только для сеансов SFTP. Удаленный сеанс подключения к cmd.exe не учитывает ее. Чтобы настроить сервер chroot только для SFTP, укажите параметр ForceCommand со значением internal-sftp. Вы также можете настроить SCP с поддержкой chroot, реализовав пользовательскую оболочку, которая допускает только SCP и SFTP.

### <a name="hostkey"></a>HostKey

По умолчанию используются значения %programdata%/ssh/ssh_host_ecdsa_key, %programdata%/ssh/ssh_host_ed25519_key, %programdata%/ssh/ssh_host_dsa_key и %programdata%/ssh/ssh_host_rsa_key. Если эти файлы отсутствуют, sshd автоматически создает их при запуске службы.

### <a name="match"></a>Сопоставление

Обратите внимание на правила шаблона в этом разделе. Имена пользователей и групп должны быть в нижнем регистре.

### <a name="permitrootlogin"></a>PermitRootLogin

Неприменимо в ОС Windows. Чтобы предотвратить вход администратора, примените для группы Administrators директиву DenyGroups.

### <a name="syslogfacility"></a>SyslogFacility

Если вам требуется ведение журнала в файле, используйте LOCAL0. Журналы создаются в папке %programdata%\ssh\logs.
Любое другое значение, включая используемое по умолчанию AUTH, направляет журналы в ETW. Дополнительные сведения см. в статье о возможностях по ведению журнала в Windows.

### <a name="not-supported"></a>Не поддерживается

Следующие параметры конфигурации недоступны в версии OpenSSH, которая поставляется в составе Windows Server 2019 и Windows 10 версии 1809:

* AcceptEnv
* AllowStreamLocalForwarding
* AuthorizedKeysCommand
* AuthorizedKeysCommandUser
* AuthorizedPrincipalsCommand
* AuthorizedPrincipalsCommandUser
* сжатие;
* ExposeAuthInfo
* GSSAPIAuthentication
* GSSAPICleanupCredentials
* GSSAPIStrictAcceptorCheck
* HostbasedAcceptedKeyTypes
* HostbasedAuthentication
* HostbasedUsesNameFromPacketOnly
* IgnoreRhosts
* IgnoreUserKnownHosts
* KbdInteractiveAuthentication
* KerberosAuthentication
* KerberosGetAFSToken
* KerberosOrLocalPasswd
* KerberosTicketCleanup
* PermitTunnel
* PermitUserEnvironment
* PermitUserRC
* PidFile
* PrintLastLog
* RDomain
* StreamLocalBindMask
* StreamLocalBindUnlink
* StrictModes
* X11DisplayOffset
* X11Forwarding
* X11UseLocalhost
* XAuthLocation