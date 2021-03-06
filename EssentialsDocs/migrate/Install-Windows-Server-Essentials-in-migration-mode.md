---
title: Установка Windows Server Essentials в режиме миграции
description: Узнайте, как установить Windows Server Essentials в режиме миграции.
ms.date: 04/29/2020
ms.topic: article
ms.assetid: fd7196ac-cfa6-46a5-ba77-6962b47a825e
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.custom:
- CI ID 117135
- CSSTroubleshoot
ms.openlocfilehash: 288a3a3c6680da8f595cb55d77637b6d64678667
ms.sourcegitcommit: 9e19436bd8b20af60284071ab512405aebfbec83
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/29/2020
ms.locfileid: "97810951"
---
# <a name="install-windows-server-essentials-in-migration-mode"></a>Установка Windows Server Essentials в режиме миграции

> Область применения: Windows Server 2012 Essentials

В сети может быть только один сервер, на котором работает Windows Server Essentials, и этот сервер должен быть контроллером домена для сети.

 При установке Windows Server Essentials в режиме миграции мастер установки выполняет следующие задачи:

1.  Устанавливает и настраивает серверное программное обеспечение Windows Server Essentials на целевом сервере.

2.  Обновляет схему домена до самой последней версии.

3.  Присоединяет конечный сервер к существующему домену. Исходный и конечный сервер могут быть присоединены к одному домену до завершения процесса миграции. После завершения миграции необходимо удалить исходный сервер из сети в течение 21 дня.

    > [!WARNING]
    >  Каждый день в течение 21-дневного льготного периода в журнал событий добавляется сообщение об ошибке, пока вы не удалите исходный сервер из сети. Это сообщение содержит следующий текст: "Проверка роли FSMO обнаружила в данной среде условие, несовместимое с политикой лицензирования. Сервер управления должен выполнять роли Active Directory первичного контроллера домена и хозяина именования доменов. Перенесите роли Active Directory на сервер управления. Работа этого сервера будет автоматически завершена, если проблема не будет устранена в течение 31 дня с момента первого обнаружения этого условия". По истечении 21-дневного льготного периода работа исходного сервера завершается.

4.  Переносит роли хозяев операций (также известные, как гибкие операции с единым хозяином или FSMO) с исходного сервера на конечный. Роли хозяина операций — это специализированные задачи контроллера домена, которые используются, когда стандартные методы обновлений и передачи данных неэффективны. Когда конечный сервер становится контроллером домена, он должен выполнять роли хозяина операций.

5.  Настраивает конечный сервер в качестве сервера глобального каталога. Сервер глобального каталога — это контроллер домена, который управляет репозиторием распределенных данных. В нем содержится частичная репрезентация с возможностью поиска каждого объекта в каждом домене леса Active Directory.

6.  Настраивает конечный сервер в качестве сервера лицензирования использования.

##  <a name="install-windows-server-essentials-on-the-destination-server"></a><a name="BKMK_Install"></a> Установка Windows Server Essentials на целевом сервере
 Чтобы установить и настроить Windows Server Essentials на целевом сервере в режиме миграции, выполните следующую процедуру.

#### <a name="to-install-windows-server-essentials-on-the-destination-server"></a>Установка Windows Server Essentials на целевом сервере

1. Включите целевой сервер и вставьте Windows Server Essentials DVD1 в DVD-дисковод. Если отображается сообщение с запросом на загрузку с компакт-диска или DVD-диска, нажмите любую клавишу для выполнения этой операции.

   > [!NOTE]
   >  Если целевой сервер поддерживает загрузку с флэш-накопителя USB, можно использовать **средство загрузки USB-или DVD** -диска для Windows 7, чтобы создать загрузочный USB-накопитель из файла ISO Windows Server Essentials. Применение накопителя USB позволяет существенно ускорить процесс установки, поскольку скорость чтения данных у флэш-памяти гораздо выше, чем у DVD-дисков. После создания загрузочного накопителя USB можно добавить на него файл ответов. Вы можете [загрузить средство загрузки USB-или DVD для Windows 7](https://go.microsoft.com/fwlink/p/?LinkId=248282) бесплатно на веб-сайте Microsoft Store.

   > [!NOTE]
   >  Если конечный сервер не загружается с DVD-диска, перезагрузите компьютер и проверьте настройку BIOS, чтобы убедиться, что **DVD-ROM** стоит первым в последовательности загрузки. Дополнительные сведения о способах изменения последовательности загрузки BIOS см. в документации изготовителя оборудования.

2. Щелкните элемент **Новая установка**.

3. Если у вас есть внутренний жесткий диск, который не отображается в списке, нажмите кнопку **Загрузить драйверы** и установите необходимые драйверы перед продолжением.

4. Установите флажок, подтверждающий удаление всех файлов и папок на основном жестком диске, и нажмите кнопку **Установить**.

5. На странице **Выбор режима установки сервера** щелкните элемент **Миграция сервера** и введите необходимые сведения о миграции.

6. После отображения сообщения **Миграция сервера выполнена успешно** нажмите кнопку **Закрыть**.

   После завершения установки выполняется автоматический вход в систему с использованием учетной записи и пароля администратора, указанные в файле ответов для миграции.

> [!NOTE]
>  Чтобы разблокировать рабочий стол во время установки Windows Server Essentials, используйте встроенную учетную запись администратора и оставьте поле пароля пустым.

##  <a name="verify-the-health-of-the-domain-controller"></a><a name="BKMK_VerifyTheHealthOfDC"></a> Проверка работоспособности контроллера домена
 Прежде чем продолжить миграцию, убедитесь, что контроллер домена и сеть Windows Server Essentials работоспособны.

 В следующей таблице перечислены средства, которые помогут выявить проблемы с конечным сервером, сетью и доменом:

|Инструмент|Описание|
|----------|-----------------|
|Netdiag|Помогает изолировать проблемы с сетью и подключением. Для получения дополнительных сведений и загрузки см. раздел [Netdiag](https://go.microsoft.com/fwlink/?LinkId=217388).|
|Dcdiag.exe|Анализирует состояние контроллеров домена в лесу или на предприятии и сообщает о проблемах, помогая в устранении неполадок. Для получения дополнительных сведений и загрузки см. раздел [Dcdiag](https://go.microsoft.com/fwlink/?LinkId=217389).|
|Repadmin.exe|Содействует в диагностике проблем с репликацией между контроллерами домена. Для запуска этого средства необходимо задавать параметры командной строки. Для получения дополнительных сведений и загрузки см. раздел [Repadmin](https://go.microsoft.com/fwlink/?LinkId=217387).|

 Перед продолжением миграции следует устранить все проблемы, обнаруженные этими средствами.

> [!NOTE]
>  Если вы планируете перенести электронную почту на другой локальный сервер Exchange Server, ознакомьтесь со статьей [Интеграция локального сервера Exchange Server с Windows Server Essentials](../manage/Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md) для получения сведений о настройке локального сервера Exchange Server.
