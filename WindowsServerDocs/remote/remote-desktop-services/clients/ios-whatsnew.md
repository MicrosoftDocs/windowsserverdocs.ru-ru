---
title: Что нового в клиенте iOS?
description: Дополнительные сведения о последних изменениях в клиенте удаленного рабочего стола для iOS
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 12/02/2020
ms.localizationpriority: medium
ms.openlocfilehash: ab03feb27e2f03f8765cd42b8acaec6b61836d3b
ms.sourcegitcommit: dce404a0a4500a693e294e0431c93f0ae90f8b13
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2020
ms.locfileid: "96563834"
---
# <a name="whats-new-in-the-ios-client"></a>Что нового в клиенте iOS?

Мы регулярно обновляем [клиент удаленного рабочего стола для iOS](remote-desktop-ios.md), добавляя новые компоненты и устраняя проблемы. На этой странице вы найдете последние обновления.

## <a name="how-to-report-issues"></a>Отправка сообщений о проблемах

Мы хотим сделать клиент удаленного рабочего стола для iOS максимально удобным, поэтому для нас важен ваш отзыв. Вы можете сообщить о проблемах, щелкнув **Справка** > **Сообщить о проблеме**.

## <a name="updates-for-version-1022"></a>Обновления для версии 10.2.2

*Дата публикации: 23.11.2020*

В этом выпуске мы устранили некоторые ошибки, затрагивающие пользователей iOS 14 и iPadOS 14.

## <a name="updates-for-version-1021"></a>Обновления для версии 10.2.1

*Дата публикации: 11.11.2020*

Вышло очередное небольшое обновление. В этой версии были внесены следующие изменения:

- Добавлена поддержка недавно выпущенных устройств iPhone и iPad.
- Устранена проблема, когда клиент выдает сообщение об ошибке 0x30000066 при подключении с помощью сервера шлюза удаленных рабочих столов.

## <a name="updates-for-version-1020"></a>Обновления для версии 10.2.0

*Дата публикации: 06.11.2020*

В этой версии мы устранили некоторые проблемы совместимости с iOS и iPadOS 14. Кроме того, мы добавили следующие исправления и обновления функций:

- Устранены сбои в iOS и iPadOS 14, которые возникали при вводе с клавиатуры.
- Добавлены сочетания клавиш Cmd+S и Cmd+N для доступа к процессам "Add Workspace" (Добавление рабочего пространства) и "Add PC" (Добавление ПК) соответственно.
- Добавлено сочетание клавиш Cmd+F для вызова пользовательского интерфейса поиска в Центре подключений.
- Добавлены команды "Развернуть все" и "Свернуть все" на вкладку "Workspaces" (Рабочие пространства).
- Устранена проблема, которая приводила к ошибке протокола 0xD06 при запуске Outlook в качестве удаленного приложения.
- Экранная клавиатура теперь скрывается при прокрутке результатов поиска в Центре подключений.
- Обновлена анимация, используемая при наведении указателя на значки рабочего пространства в iPadOS 14.

## <a name="updates-for-version-1014"></a>Обновления для версии 10.1.4

*Дата публикации: 06.11.2020*

Здесь приведены исправления ошибок и незначительные обновления компонентов для этого выпуска 10.1.4. Новые возможности:

- Устранена проблема, при которой клиент выдавал сообщение об ошибке 0x5000007 при попытке подключиться к серверу шлюза удаленных рабочих столов.
- Пароли учетных записей пользователей, обновленные в пользовательском интерфейсе учетных данных, теперь сохраняются после успешного входа.
- Устранена проблема, при которой выбор диапазона и множественный выбор с помощью мыши или сенсорной панели (SHIFT+щелчок и CTRL+щелчок) могли не срабатывать.
- Устранена проблема, при которой приложения, отображаемые в пользовательском интерфейсе переключателя сеанса, были рассинхронизированы с удаленным сеансом.
- Внесены некоторые косметические изменения в макет заголовков рабочих пространств в Центре подключений.
- Улучшена видимость кнопок экранной клавиатуры для темных фонов.
- Исправлена ошибка локализации в диалоговом окне отключения.

## <a name="updates-for-version-1013"></a>Обновления для версии 10.1.3

*Дата публикации: 06.11.2020*

Здесь приведены исправления ошибок и обновления компонентов для этого выпуска 10.1.3. Новые возможности:

- Режим ввода (указатель мыши или режим сенсорного ввода) теперь является глобальным для всех активных подключений ПК и удаленных приложений.
- Исправлена проблема, из-за которой перенаправление микрофона могло не срабатывать.
- Исправлена ошибка, из-за которой звук для воспроизведения направлялся на наушник iPhone, а не на внутренний динамик.
- Клиент теперь поддерживает автоматическую смену звуковых выходов между внутренними динамиками iPhone или iPad, Bluetooth-динамиками и наушниками Airpods.
- Звук теперь будет продолжать воспроизводиться в фоновом режиме при переключении с клиента на другое приложение или при блокировке устройства.
- Режим ввода автоматически переключается на сенсорный ввод при использовании мыши SwiftPoint с iPhone или iPad (без iPadOS версии 13.4 или более поздней).
- Устранены проблемы с выводом графики, которые возникали, если сервер был настроен для использования полноэкранного режима AVC444.
- Устранены некоторые ошибки с VoiceOver.
- Сдвиг окна сеанса с увеличенным масштабом теперь работает иначе при использовании внешней мыши или сенсорной панели. Чтобы сдвинуть окно сеанса с увеличенным масштабом с помощью внешней мыши, щелкните маркер сдвига и перетащите указатель, удерживая кнопку мыши. Чтобы выполнить сдвиг в сенсорном режиме, щелкните маркер сдвига и проведите пальцем. Окно сеанса будет следовать за маркером. В режиме указателя мыши выведите указатель виртуальной мыши за границы экрана.

## <a name="updates-for-version-1012"></a>Обновления для версии 10.1.2

*Дата публикации: 17.08.2020*

В этом обновлении мы устранили проблемы, о которых сообщили в обновлении версии 10.1.1.

- Исправлена ошибка, которая возникала для некоторых пользователей при подписке на канал виртуальных рабочих столов Windows с использованием аутентификации без посредника.
- Исправлено расположение значков рабочего пространства на устройствах iPhone X, iPhone XS и iPhone 11 Pro.

## <a name="updates-for-version-1011"></a>Обновления для версии 10.1.1

*Дата публикации: 06.11.2020*

Новое в этом выпуске:

- Исправлена ошибка, предотвращающая ввод на корейском языке.
- Добавлена поддержка клавиш F1–F12, Home, End, PgUp и PgDn на аппаратных клавиатурах.
- Устранена ошибка, которая усложняла перемещение указателя мыши в верхнюю часть экрана в режиме отображения с рамками на устройствах iPadOS.
- Устранена проблема, из-за которой после нажатия клавиши BACKSPACE после пробела выполнялось удаление двух символов.
- Исправлена ошибка, которая приводила к появлению указателя мыши iPadOS над указателем мыши клиента Удаленного рабочего стола в режиме "касание для щелчка".
- Устранена проблема, которая не позволила устанавливать подключения к некоторым серверам шлюзов удаленных рабочих столов (код ошибки 0x30000064).
- Исправлена ошибка, которая приводила к отображению указателя мыши в пользовательском интерфейсе переключателя сеанса на устройствах iOS при использовании мыши SwiftPoint.
- Изменен размер указателя мыши клиента удаленного рабочего стола для соответствия текущему коэффициенту масштабирования клиента.
- Клиент теперь проверяет наличие сетевого подключения перед запуском ресурса рабочего пространства или подключением к компьютеру.
- Нажатие переназначенной клавиши ESCAPE или клавиш Cmd+. теперь приводит к отмене любого запроса учетных данных.
- Мы добавили несколько улучшений и анимаций, которые отображаются при перемещении указателя мыши на iPad с iPadOS версии 13.4 или более поздней.

## <a name="updates-for-version-1010"></a>Обновления для версии 10.1.0

*Дата публикации: 06.11.2020*

Новое в этой версии:

- Если вы используете iPadOS 13.4 или более поздней версии, теперь вы можете управлять удаленным сеансом с помощью мыши или сенсорной панели.
- Клиент теперь поддерживает следующие жесты Apple Magic Mouse 2 и Apple Magic Trackpad 2: щелчок левой кнопкой, перетаскивание левой кнопкой, щелчок правой кнопкой, перетаскивание правой кнопкой, горизонтальная и вертикальная прокрутка и локальное изменение масштаба.
- Если вы используете внешние мыши, клиент теперь поддерживает щелчок левой кнопкой, перетаскивание левой кнопкой, щелчок правой кнопкой, перетаскивание правой кнопкой, щелчок средней кнопкой и вертикальную прокрутку.
- Клиент теперь поддерживает сочетания клавиш с CTRL, ALT или SHIFT и мыши или сенсорного экрана, в том числе при множественном выборе и выборе диапазона.
- Клиент теперь поддерживает функцию "касание для щелчка" для сенсорной панели.
- Мы изменили жест с щелчком правой кнопкой при использовании режима указателя мыши на нажатие и удерживание (а не нажатие, удерживание и отпускание). В клиенте iPhone мы добавили небольшой тактильный отклик при регистрации жеста с щелчком правой кнопкой.
- Добавлен параметр для отключения принудительного применения NLA в разделе **Параметры iOS** > **Клиент удаленного рабочего стола**.
- Клавиши CTRL+SHIFT+ESCAPE переназначены на CTRL+SHIFT+ESC, где ESCAPE регистрируется при нажатии переназначенной клавиши на iPadOS или Command+.
- Клавиши Command+F переназначены на CTRL+F.
- Исправлена проблема, при которой средняя кнопка мыши SwiftPoint не работала в iOS и iPadOS версии 13.3.1 и более ранних.
- Исправлены некоторые ошибки, которые блокировали распознавание клиентом URI "rdp:".
- Устранена проблема, при которой пользовательский интерфейс иммерсивного переключателя сеансов отображал устаревшие записи приложений, если отключение было инициировано сервером.
- Клиент теперь поддерживает версию Виртуального рабочего стола Windows, интегрированную с Azure Resource Manager.

## <a name="updates-for-version-1007"></a>Обновления для версии 10.0.7

*Дата публикации: 29.04.2020*

В этом обновлении мы добавили возможность сортировки представления списка компьютеров (доступно на iPhone) по имени или времени последнего подключения.

## <a name="updates-for-version-1006"></a>Обновления для версии 10.0.6

*Дата публикации: 31.03.2020*

Небольшое обновление с исправлениями нескольких ошибок. Что нового в этом выпуске:

- Устранен ряд проблем со специальными возможностями VoiceOver.
- Исправлена ошибка, из-за которой пользователям не удавалось подключиться с помощью учетных данных на турецком языке.
- Сеансы, отображаемые в пользовательском интерфейсе переключателя, теперь упорядочиваются по времени запуска.
- После нажатия кнопки "Назад" в Центре подключений теперь выполняется переход к последнему активному сеансу.
- Мыши Swiftpoint теперь освобождаются при переходе от клиента к другому приложению.
- Улучшено взаимодействие со службой "Виртуальный рабочий стол Windows."
- Исправлены сбои, которые отображались в отчетах об ошибках.

Мы ценим все комментарии, отправленные нам в App Store, с помощью функции отправки отзывов в приложениях и по электронной почте. Также выражаем благодарность всем, кто помогал нам диагностировать проблемы.

## <a name="updates-for-version-1005"></a>Обновления для версии 10.0.5

*Дата публикации: 09.03.2020*

Мы собрали исправления ошибок и обновления компонентов для этого выпуска 10.0.5. Новые возможности:

- Запущенные RDP-файлы теперь импортируются автоматически (переключатель находится в общих параметрах).
- Теперь вы можете запускать RDP-файлы на основе iCloud, которые еще не скачаны в приложении "Файлы".
- Теперь удаленный сеанс можно расширить под индикатором "Домой" на устройствах iPhone (переключатель находится в параметрах отображения).
- Реализована поддержка ввода составных символов, например é, с помощью нескольких нажатий клавиш.
- Реализована поддержка плавающей клавиатуры iPad на экране.
- Реализована поддержка настройки свойств перенаправленных камер из удаленного сеанса.
- Исправлена ошибка в распознавателе жестов, из-за которой клиент не отвечал при подключении к удаленному сеансу.
- Теперь, чтобы перейти в режим переключения приложений, достаточно провести пальцем (за исключением сенсорного режима с сеансом, расширенным в область индикатора "Домой").
- Теперь индикатор "Домой" будет автоматически скрываться при подключении к удаленному сеансу, появляясь только при касании экрана.
- Добавлено сочетание клавиш для перехода к параметрам приложения в Центре подключений (**COMMAND+,** ).
- Добавлено сочетание клавиш для обновления всех рабочих областей в Центре подключений (**COMMAND+R**).
- Добавлено системное сочетание клавиш для экранирования при подключении к удаленному сеансу (**COMMAND+.** ).
- Исправлен сценарий, когда экранная клавиатура Windows в удаленном сеансе была слишком мала.
- Реализован автоматический фокус клавиатуры в Центре подключений, чтобы сделать ввод данных более удобным.
- Нажатие **ВВОД** при запрашивании учетных данных теперь приводит к закрытию запроса и возобновлению текущего потока.
- Исправлен сценарий, когда происходил сбой клиента при нажатии клавиш SHIFT + OPTION + стрелка влево, вверх или вниз.
- Исправлена ошибка, возникающая при удалении устройства SwiftPoint.
- Исправлены другие ошибки, о которых нам сообщали пользователи с момента последнего выпуска.

Мы бы хотели поблагодарить всех, кто сообщал об ошибках и помогал нам диагностировать проблемы.

## <a name="updates-for-version-1004"></a>Обновления для версии 10.0.4

*Дата публикации: 03.02.2020*

Пора установить другое обновление! Мы бы хотели поблагодарить всех, кто сообщал об ошибках и помогал нам диагностировать проблемы. Что нового в этой версии:

- Теперь при удалении учетных записей пользователей и шлюзов отображается пользовательский интерфейс подтверждения.
- Пользовательский интерфейс поиска в Центре подключений переработан.
- Подсказка имени пользователя (при наличии) теперь отображается в пользовательском интерфейсе запроса учетных данных при запуске из RDP-файла или URI.
- Исправлена ошибка, из-за которой расширенная экранная клавиатура заходила под выступ под камеру на iPhone.
- Исправлена ошибка, из-за которой внешние клавиатуры прекращали работать после отключения и повторного подключения.
- Реализована поддержка клавиши ESC на внешних клавиатурах.
- Исправлена ошибка, из-за которой при вводе символов китайского письма отображались символы английского языка.
- Исправлена ошибка, из-за которой некоторые входные данные на китайском языке оставались в удаленном сеансе после удаления.
- Исправлены другие ошибки, о которых нам сообщали пользователи с момента последнего выпуска.

Мы ценим все ваши комментарии, отправленные нам в App Store, с помощью функции отправки отзывов в приложениях и по электронной почте. Мы и дальше будем работать над тем, чтобы с каждым выпуском это приложение становилось еще лучше.

## <a name="updates-for-version-1003"></a>Обновления для версии 10.0.3

*Дата публикации: 16.01.2020*

Наступил 2020 год, и пришло время выхода нашего первого выпуска, который включает новые функции и исправления ошибок. Вот что входит в это обновление:

- Поддержка запуска подключений из RDP-файлов и URI RDP.
- Заголовки рабочей области теперь можно свернуть.
- Одновременное прокручивание и панорамирование поддерживаются в режиме указателя мыши.
- Жест нажатия и удерживания в режиме указателя мыши теперь активирует щелчок правой кнопкой мыши в удаленном сеансе.
- Удален жест принудительного касания для щелчка правой кнопкой мыши в режиме указателя мыши.
- Экран переключателя во время сеанса теперь поддерживает отключение, даже если нет подключенных приложений.
- Теперь на экране переключателя во время сеанса поддерживается эффект исчезновения.
- Компьютеры и приложения больше не переупорядочиваются автоматически на экране переключателя во время сеанса.
- Увеличена область проверки нажатия для меню с многоточием в представлении эскизов ПК.
- На странице с параметрами входных устройств теперь содержится ссылка на поддерживаемые устройства.
- Исправлена ошибка, из-за которой пользовательский интерфейс разрешений Bluetooth многократно отображался при запуске для некоторых пользователей.
- Исправлены другие ошибки, о которых нам сообщали пользователи с момента последнего выпуска.

## <a name="updates-for-version-1002"></a>Обновления для версии 10.0.2

*Дата публикации: 20.12.2019*

Мы усердно работали над устранением ошибок и добавили полезные функции. Что нового в этом выпуске

- Поддержка ввода японских и китайских иероглифов на аппаратных клавиатурах.
- В представлении списка ПК теперь отображается понятное имя связанной учетной записи пользователя (при наличии).
- Пользовательский интерфейс разрешений при первом запуске теперь правильно отображается в светлом режиме.
- Исправлена ошибка, возникавшая каждый раз, когда пользователь одновременно нажимал клавишу OPTION и клавиши со стрелкой вверх или вниз на аппаратной клавиатуре.
- Обновлен макет экранной клавиатуры, используемый в пользовательском интерфейсе запроса пароля, чтобы проще было найти клавишу обратной косой черты.
- Исправлены другие ошибки, о которых нам сообщали пользователи с момента последнего выпуска.

## <a name="updates-for-version-1001"></a>Обновления для версии 10.0.1

*Дата публикации: 15.12.2019*

Что нового в этом выпуске:

- Поддержка службы виртуальных рабочих столов Windows.
- Обновлен пользовательский интерфейс центра подключений.
- Обновлен пользовательский интерфейс для работы во время сеанса.

## <a name="updates-for-version-1000"></a>Обновления для версии 10.0.0

*Дата публикации: 13.12.19*

Прошло уже больше года с момента последнего обновления клиента Удаленного рабочего стола для iOS. Но мы наконец выпустили новое обновление, и в будущем собираемся делать это регулярно. Что нового в выпуске 10.0.0:

- Поддержка службы виртуальных рабочих столов Windows.
- Новый пользовательский интерфейс Центра подключений.
- Новый пользовательский интерфейс в сеансе, который позволяет переключаться между подключенными компьютерами и приложениями.
- Новый макет вспомогательной экранной клавиатуры.
- Улучшенная поддержка внешней клавиатуры.
- Поддержка мыши SwiftPoint Bluetooth.
- Поддержка перенаправления микрофона.
- Поддержка перенаправления локального хранилища.
- Поддержка перенаправления камеры (доступна только для Windows 10 версии 1809 или более поздней).
- Поддержка новых устройств iPhone и iPad.
- Поддержка темной и светлой тем.
- Управление возможностью блокировки телефона при подключении к удаленному компьютеру или приложению.
- Теперь можно свернуть панель подключения в сеансе, нажав и удерживая кнопку с логотипом удаленного рабочего стола.

## <a name="updates-for-version-8142"></a>Обновления для версии 8.1.42

*Дата публикации: 20.06.2018*

- Исправления ошибок и повышение производительности.

## <a name="updates-for-version-8141"></a>Обновления для версии 8.1.41

*Дата публикации: 28.03.2018*

- Обновления для устранения проблемы шифрования CredSSP, описанные в CVE-2018-0886.
