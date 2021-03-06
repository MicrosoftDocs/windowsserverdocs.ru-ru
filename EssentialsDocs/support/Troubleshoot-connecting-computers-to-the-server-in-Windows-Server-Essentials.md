---
title: Устранение неполадок при подключении компьютеров к серверу в Windows Server Essentials
description: Узнайте, как устранять неполадки, которые могут возникнуть при подключении компьютера к серверу под Windows Server Essentials.
ms.date: 10/03/2016
ms.topic: article
ms.assetid: e45b3d89-c057-4c70-a627-86fb06dd22aa
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: cfb7cd5b31e86fcbed9e92e8f82f1da4437f380d
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810141"
---
# <a name="troubleshoot-connecting-computers-to-the-server-in-windows-server-essentials"></a>Устранение неполадок при подключении компьютеров к серверу в Windows Server Essentials

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

 В этом разделе содержатся рекомендации по устранению неполадок, которые могут возникнуть при подключении компьютера к серверу под Windows Server Essentials или Windows Server Essentials.

> [!NOTE]
>  Для получения последних сведений об устранении неполадок из сообщества Windows Server Essentials и Windows Server Essentials мы рекомендуем посетить [форум Windows Server Essentials](/answers/topics/windows-server-essentials.html). Форум Windows Server Essentials — это отличный ресурс, на котором можно получить помощь или задать вопрос.

 В этом разделе представлены решения следующих проблем.


-   Выпуск 1. [выпуск 1](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)

-   Выпуск 2. [выпуск 2](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)

-   Вопрос 3. [выпуск 3](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)

-   Выпуск 4. [выпуск 4](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)

-   Причина 5: [Выпуск 5](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)

-   Вопрос 6. [Выпуск 6](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)

-   Выпуск 7. [Выпуск 7](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)

-   Ошибка 8. [Ошибка 8](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)

-   Выпуск 9. [Выпуск 9](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)

-   Выпуск 10: [выпуск 10](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)

-   Выпуск 11. [выпуск 11](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)


##  <a name="issue-1"></a><a name="BMRK_Package"></a> Выпуск 1
 **Проблема**

 Не удалось установить пакет. Попробуйте установить соединитель Windows Server Essentials еще раз. Если проблема не исчезнет, обратитесь к администратору сети при подключении компьютера к серверу.

 **Описание**

 Эта проблема может возникать при подключении компьютера к серверу под Windows Server Essentials, в то время как другие обновления Windows или приложения ожидают установки соединителя.

 **Решение**

 Завершите все обновления или установки приложений. При появлении соответствующего запроса перезагрузите компьютер.

##  <a name="issue-2"></a><a name="BKMK_ConnectorIssue2"></a> Выпуск 2
 **Проблема**

 Не удается присоединить компьютер к Windows Server Essentials

 **Описание**

 Компьютеры, которые не имеют символов ASCII в имени компьютера, не могут быть присоединены к Windows Server Essentials. Если имя компьютера содержит символы, отличные от ASCII, выводится сообщение об ошибке: "Произошла непредвиденная ошибка".

 **Решение**

 Переименуйте клиентский компьютер, указав имя, содержащее только символы ASCII, и повторите попытку добавить компьютер в Windows Server Essentials.

##  <a name="issue-3"></a><a name="BKMK_ConnectorIssue2a"></a> Выпуск 3
 **Проблема**

 Я получаю сообщение об установке программного обеспечения соединителя отменено при подключении компьютера к серверу.

 **Описание**

 Для подключения компьютера к серверу СИСТЕМная учетная запись должна иметь разрешения на полный доступ к серверным папкам, отображаемым на панели мониторинга Windows Server Essentials. Если необходимые разрешения не были предоставлены, будет показано сообщение "Установка программного обеспечения Connector отменена".

 **Решение**

 Убедитесь, что системная учетная запись имеет разрешения **Полный доступ** к каждой папке сервера.

#### <a name="to-grant-the-system-account-full-control-permissions-on-a-server-folder"></a>Предоставление системной учетной записи разрешений полного доступа к папкам сервера

1.  Откройте панель мониторинга Windows Server Essentials.

2.  Нажмите кнопку **Хранение**, а затем **Папки сервера**.

3.  Щелкните правой кнопкой мыши папку, затем выберите **Открыть папку**. (Если команда **Открыть папку** отсутствует, задавать разрешения на доступ к папке не требуется.)

4.  В сетевом пути в верхней части проводника Windows выберите общий ресурс сервера, чтобы отобразить общие папки на сервере. Например, в пути **Сети > Server01 > Архивы журналов файлов** щелкните **Server01**.

5.  Щелкните правой кнопкой мыши папку сервера, а затем выберите пункт **Свойства**.

6.  Перейдите на вкладку **Безопасность** .

7.  Если для системной учетной записи разрешение **Полный доступ** запрещено, нажмите кнопку **Изменить**, а затем — **СИСТЕМА**. В разделе **Разрешения для системы** установите флажок **Разрешить** рядом с вариантом **Полный доступ**.

8.  Дважды нажмите **ОК**, чтобы обновить разрешения и закрыть окно **Свойства**.

##  <a name="issue-4"></a><a name="BKMK_ConnectorIssueNetFramework"></a> Выпуск 4
 **Проблема**

 Для запуска этого приложения необходимо установить одну из следующих версий .NET Framework: V 4.5.50709 "ошибка при подключении компьютера к серверу

 **Описание**

 При подключении компьютера к серверу под управлением Windows Server Essentials или Windows Server Essentials мастер пытается установить .NET Framework версии 4.5.50709 на компьютере. Однако при наличии более ранней версии .NET Framework версии 4,5 невозможно установить обновленный выпуск, и попытка подключения завершится ошибкой: чтобы запустить это приложение, необходимо установить одну из следующих версий .NET Framework: V 4.5.50709. Обратитесь к издателю выделения, чтобы получить инструкции по получению соответствующей версии .NET Framework.

 **Решение**

 Удалите .NET Framework 4.5 с компьютера, а затем подключите компьютер к серверу.

#### <a name="to-uninstall-net-framework-45"></a>Удаление .NET Framework 4.5

1.  На странице **Пуск** клиентского компьютера откройте **панель управления**.

2.  На панели управления в разделе **Программы** щелкните **Удаление программы**.

3.  Щелкните правой кнопкой мыши **Microsoft .NET Framework 4.5** и выберите команду **Удалить**.

4.  После успешного удаления .NET Framework 4.5 подключите компьютер к серверу. Нужная версия .NET Framework 4.5 устанавливается вместе с ПО Connector.

##  <a name="issue-5"></a><a name="BKMK_Time"></a> Выпуск 5
 **Проблема**

 Я получаю, что сервер недоступен. Чтобы устранить эту проблему, обратитесь к лицу, ответственному за вашу сеть. сетевому администратору".

 **Описание**

 Это может произойти, если дата и время на подключенном компьютере не синхронизированы с датой и временем на сервере.  Windows Server Essentials и Windows Server Essentials используют службу синхронизации времени для синхронизации даты и времени компьютеров, работающих в сети Windows Server Essentials или Windows Server Essentials. Синхронизация времени очень важна еще потому, что серверное время используется в установленном по умолчанию протоколе проверки подлинности как часть процесса проверки подлинности. Например, если часы на клиентском компьютере не синхронизированы с правильными датой и временем, проверка подлинности Windows Server Essentials или Windows Server Essentials может ошибочно интерпретировать запрос на вход в систему в качестве попытки вторжения и запретить доступ пользователю.

 Это может произойти, если объем свободной памяти сервера меньше 5%.

 Это может произойти, если имеется VPN-подключение к Windows Essentials Server и предпринимается попытка настройки ПО Connector во внешней среде с помощью адреса домена.

 **Решение**

1.  Синхронизируйте дату и время на клиентском компьютере с датой и временем на сервере. Затем подключите компьютер к серверу.

2.  Закройте некоторые приложения на стороне сервера и подключите компьютер к серверу.

3.  Закройте VPN-подключение, а затем подключите компьютер к серверу.

#### <a name="to-change-the-date-and-time-on-the-client-computer"></a>Изменение даты и времени на клиентском компьютере

1. На начальной странице клиентского компьютера откройте **панель управления**.

2. В панели управления щелкните **Часы, язык и регион** и **Дата и время**.

3. Щелкните **Изменить дату и время**, установите правильную дату и время и нажмите кнопку **ОК**.

4. Нажмите кнопку **ОК** и закройте панель управления.

5. Повторите попытку подключения клиентского компьютера к серверу. Инструкции см. в подразделе "Подключение компьютеров к серверу".

   Если по-прежнему не удается подключить клиентский компьютер к серверу, убедитесь, что на сервере установлены правильная дата и время. Если дата и время неверны, измените их.

#### <a name="to-change-the-date-and-time-on-the-server"></a>Изменение даты и времени на сервере

1.  Войдите на сервер, используя пароль, настроенный во время установки и настройки Windows Server Essentials или Windows Server Essentials.

    > [!NOTE]
    >  При удаленном администрировании сервера для входа на сервер необходимо использовать удаленное подключение к рабочему столу.

2.  На **начальной странице** откройте **Панель управления**.

3.  В панели управления щелкните **Часы, язык и регион** и **Дата и время**.

4.  Щелкните **Изменить дату и время**, установите правильную дату и время и нажмите кнопку **ОК**.

5.  Нажмите кнопку **ОК** и закройте панель управления.

6.  На клиентском компьютере повторите попытку подключения клиентского компьютера к серверу. Инструкции см. в подразделе "Подключение компьютеров к серверу".

##  <a name="issue-6"></a><a name="BKMK_ServiceStopped"></a> Выпуск 6
 **Проблема**

 Возникла непредвиденная ошибка. Чтобы устранить эту проблему, обратитесь к лицу, ответственному за вашу сеть. сетевому администратору".

 **Описание**

 Если отображается это сообщение об ошибке, возможно, не запущена веб-служба сертификатов WSS.

 **Решение**

 Запустите веб-службу сертификатов WSS.

#### <a name="to-start-the-wss-certificate-web-service"></a>Запуск веб-службы сертификатов WSS

1.  На **начальной** странице сервера откройте компонент **Администрирование**.

     В компоненте **Администрирование** правой кнопкой мыши щелкните **Internet Information Services (IIS)** и выберите **Открыть**.

2.  В области навигации щелкните **Веб-службы сертификатов WSS**.

3.  На панели **Действия** нажмите кнопку **Начать**.

##  <a name="issue-7"></a><a name="BKMK_ConnectorIssueReconnect"></a> Выпуск 7
 **Проблема**

 Когда я пытаюсь снова подключить компьютер к серверу после неудачной попытки подключения, я получаю предупреждение о том, что компьютер с таким именем уже подключен к серверу.

 **Описание**

 Если предыдущая попытка подключения компьютера к серверу была прервана или прервана, при попытке подключения может появиться следующее предупреждение: компьютер с таким именем уже подключен к серверу. Это происходит потому, что сертификат был выдан при первой попытке подключения к серверу.

 **Решение**. Если вы уверены, что никакой другой компьютер с таким же именем не подключен к серверу, нажмите кнопку **Далее** и следуйте инструкциям для завершения работы мастера **подключения компьютера к серверу**.

##  <a name="issue-8"></a><a name="BKMK_JoinWin7"></a> Выпуск 8
 **Проблема**

 При попытке подключения клиентского компьютера под управлением ОС Windows 7 Домашняя к серверу открывается веб-страница для запуска ПО Connector, но клиентский компьютер не может подключиться к серверу.

 **Описание**

 Если на маршрутизаторе в сети включена многоадресная рассылка, обмен данными между сервером и клиентским компьютером под управлением ОС Windows 7 Домашняя базовая или Windows 7 Домашняя осуществляется неправильно.

 **Решение**

 Отключите многоадресную рассылку на маршрутизаторе. На некоторых маршрутизаторах, возможно, потребуется отключить протокол маршрутизации RIP-2M. Дополнительные сведения см. в документации, предоставленной производителем маршрутизатора.

##  <a name="issue-9"></a><a name="BKMK_ConnectorIssueAutologon"></a> Выпуск 9
 **Проблема**

 После подключения компьютера к серверу перестал работать автоматический вход.

 **Описание**

 Если для учетной записи пользователя задан автоматический вход во время подключения компьютера к Windows Server Essentials, этот параметр перезаписывается при установке программного обеспечения соединителя на компьютере.

 **Решение**. Чтобы устранить эту проблему, при подключении компьютера к серверу запишите пароль, который используется для учетной записи пользователя. После установки ПО Connector настройте автоматический вход для этой учетной записи.

> [!NOTE]
>  Для учетной записи домена Windows Server Essentials требуется пароль, соответствующий требованиям политики паролей по умолчанию.

##  <a name="issue-10"></a><a name="BKMK_ConnectorIssueOldLogs"></a> Выпуск 10
 **Проблема**

 Удаление предварительной версии ПО Connector не приводит к удалению существующих журналов.

 **Описание**

 После обновления предварительной версии (бета-версия или RC) Windows Server Essentials до выпущенной версии необходимо удалить программное обеспечение соединителя с каждого компьютера, подключенного к серверу, а затем снова подключить компьютер, чтобы установить выпущенную версию программного обеспечения соединителя.

 Однако при удалении ПО Connector с сетевого компьютера существующие файлы журнала в папке %ProgramData%\Microsoft\Windows Server\Logs\ на этом компьютере не удаляются. Если не удалить папку Logs, файлы журнала могут быть повреждены при подключении компьютера к выпущенной версии Windows Server Essentials.

 **Решение**. Во избежание повреждения файлов журнала вручную удалите папку журналов до повторного подключения клиентского компьютера к обновленному серверу.

#### <a name="to-reconnect-a-computer-after-a-server-update-without-corrupting-the-log-files"></a>Повторное подключение компьютера после обновления сервера без повреждения файлов журналов

1.  Удалите ПО Connector с клиентского компьютера.

2.  Удалите папку журналов из папки %ProgramData%\Microsoft\Windows Server\.

3.  Повторное подключение компьютера к серверу. Будет установлена окончательная версия ПО Connector и создана новая папка журналов и файлы журналов.

##  <a name="issue-11"></a><a name="BKMK_UpgradeClientOS"></a> Выпуск 11
 **Проблема**

 Необходимо обновить операционную систему на клиентском компьютере.

 **Описание**

 Во время установки ПО Connector в операционной системе клиента выполняется ряд проверок, чтобы обеспечить соответствие клиента требованиям Connector. Если операционная система клиента обновляется после установки ПО Connector, некоторые необходимые компоненты могут отсутствовать и ПО Connector на клиенте может завершиться ошибкой.

 **Решение**

 Перед обновлением клиентской операционной системы до другой версии (например, обновление Windows XP до Windows Vista или Windows Vista до Windows 7) следует удалить ПО Connector. Используйте компонент **Установка и удаление программ** на панели управления. После завершения обновления клиентской операционной системы можно переустановить соединитель клиента, открыв http://<*server*>/Коннект в веб-браузере, где <*Server*> — это имя сервера Windows Server Essentials.

 Если клиент уже был обновлен путем установки программного обеспечения Connector, воспользуйтесь компонентом **Установка и удаление программ** или **Программы и компоненты**, чтобы удалить программное обеспечение Connector. Затем установите программное обеспечение Connector еще раз.

## <a name="additional-references"></a>Дополнительные ссылки

- [Управление Windows Server Essentials](../manage/Manage-Windows-Server-Essentials.md)

- [Устранение неполадок в Windows 2012 Server Essentials Коннекткомпутер]()