---
title: Что нового в клиенте для Windows Desktop
description: Узнайте больше о последних изменениях в клиенте Удаленного рабочего стола для Windows Desktop.
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 02/23/2021
ms.localizationpriority: medium
ms.openlocfilehash: 0f33e5df5878ab58b74622610409c5e2a83a7336
ms.sourcegitcommit: db4c35ebe56d561768d2a657da9e6d6a791457bd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "101830340"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Что нового в клиенте для Windows Desktop

Более подробные сведения о клиенте рабочего стола Windows можно найти в статье [Приступая к работе с клиентом для Windows Desktop](windowsdesktop.md). В этой статье вы найдете последние обновления для клиента.

## <a name="supported-client-versions"></a>Поддерживаемые версии клиента

Клиент можно настроить для разных [групп пользователей](windowsdesktop-admin.md#configure-user-groups). В следующей таблице перечислены текущие версии, доступные для каждой из групп пользователей.

|Группа пользователей |Последняя версия  |Минимальная поддерживаемая версия |
|-----------|----------------|--------------------------|
|Общие     |1.2.1755        |1.2.945                   |
|Предварительная оценка    |1.2.1755        |1.2.945                   |

## <a name="updates-for-version-121755"></a>Обновления для версии 1.2.1755

*Дата публикации: 23.02.2021*

Скачать: [Windows (64-разрядная версия)](https://go.microsoft.com/fwlink/?linkid=2139233), [Windows (32-разрядная версия)](https://go.microsoft.com/fwlink/?linkid=2139144), [Windows (ARM64)](https://go.microsoft.com/fwlink/?linkid=2139368)

- Добавлена точка доступа монитора взаимодействия в меню значка на панели задач.
- Исправлена проблема, из-за которой при вводе адреса электронной почты на вкладке Subscribe to a Workplace (Подписка на рабочее место) приложение переставало отвечать.
- Исправлена проблема, из-за которой клиент иногда не отправлял события EventHub и Diagnostics.
- Реализованы обновления для команд в подключаемом модуле Виртуального рабочего стола Windows, в том числе:
  - Улучшена производительность синхронизации аудио и видео, а также добавлена возможность аппаратно ускоренного декодирования, уменьшающая загрузку ЦП в клиенте.
  - Устранены наиболее распространенные причины проблем, из-за которых появляется черный экран, когда пользователь присоединяется к звонку или встрече с включенным видео, предоставляет общий доступ к экрану или включает либо отключает камеру.
  - Повышено качество переключения активного докладчика в одном представлении видео за счет уменьшения времени, требуемого на отображение нового видео, и сокращения периодических появлений черного экрана при переключении потоков видео на другого пользователя.
  - Исправлена проблема, при которой устройства со специальными знаками иногда были недоступны в Teams.

## <a name="updates-for-version-121672"></a>Обновления для версии 1.2.1672

*Дата публикации: 26.01.2021*

Скачать: [Windows (64-разрядная версия)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4MntP), [Windows (32-разрядная версия)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4MntQ), [Windows (ARM64)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4MntO)

- Добавлена поддержка функции для защиты от записи экрана для конечных точек Windows 10. Дополнительные сведения см. в разделе [Рекомендации по безопасности узла сеансов](/azure/virtual-desktop/security-guide#session-host-security-best-practices).
- Добавлена поддержка прокси-серверов, требующих проверки подлинности для подписки на веб-канал.
- Теперь в клиенте отображается уведомление с возможностью повторить попытку, если обновление не удалось скачать.
- Устранены некоторые проблемы со специальными возможностями, касающиеся фокуса клавиатуры и режима высокой контрастности.

## <a name="updates-for-version-121525"></a>Обновления для версии 1.2.1525

*Дата публикации: 01.12.2020*

- Добавлено представление списка для удаленных ресурсов, чтобы длинные имена приложений были читабельными.
- Добавлен значок уведомления, который появляется при наличии обновления для клиента.

## <a name="updates-for-version-121446"></a>Обновления для версии 1.2.1446

*Дата публикации: 27.10.2020*

- Добавлена функция автоматического обновления, которая позволяет клиенту автоматически устанавливать последние обновления.
- Теперь клиент различает разные веб-каналы в центре подключений.
- Исправлена проблема, из-за которой учетная запись подписки не совпадала с учетной записью, с помощью которой пользователь выполнил вход.
- Исправлена ошибка, из-за которой некоторые пользователи не могли получать доступ к удаленным приложениям через скачанный файл.
- Исправлена проблема с перенаправлением смарт-карт.

## <a name="updates-for-version-121364"></a>Обновления для версии 1.2.1364

*Дата публикации: 22.09.2020*

- Исправлена ошибка, из-за которой единый вход не работал в Windows 7.
- Исправлена ошибка подключения, которая возникла при вызове или присоединении к звонку Teams, в то время как другое приложение открывает аудиопоток в монопольном режиме, и при включении для команд оптимизации мультимедиа.
- Исправлена ошибка при перечислении аудио-или видеоустройств в Teams при включенной оптимизации мультимедиа для Teams.
- Добавлена ссылка Need help with settings? (Нужна помощь с параметрами?) на страницу параметров рабочего стола.
- Исправлена проблема с кнопкой "Подписаться", которая возникла при использовании темных тем с высокой контрастностью.

## <a name="updates-for-version-121275"></a>Обновления для версии 1.2.1275

*Дата публикации: 25.08.2020*

- Добавлены функции для автоматического обнаружения независимых облаков из удостоверения пользователя.
- Добавлены функции для включения настраиваемых подписок URL-адресов для всех пользователей.
- Исправлена проблема с закреплением приложений на панели задач веб-канала.
- Исправлено аварийное завершение при подписке с URL-адресом.
- Улучшена работа при перетаскивании окон удаленных приложений с помощью сенсорного ввода или пера.
- Исправлена ошибка, связанная с локализацией.

## <a name="updates-for-version-121186"></a>Обновления для версии 1.2.1186

*Дата публикации: 28.07.2020*

- Теперь вы можете подписываться на рабочие области с несколькими учетными записями пользователей, используя меню переполнения ( **...** ) на панели команд в верхней части клиента. Чтобы вы могли различать рабочие области, их имена теперь включают имя пользователя, как и все ярлыки приложений.
- В сообщения об ошибках, связанных с подпиской, добавлены дополнительные сведения, чтобы оптимизировать процесс устранения неполадок.
- Свернутое или развернутое состояние рабочих областей теперь сохраняется во время обновления.
- В диалоговом окне **Сведения о подключении** добавлена кнопка **Send Diagnostics and Close** (Отправить диагностику и закрыть).
- Исправлена проблема, связанная с использованием клавиш CTRL+SHIFT в удаленных сеансах.

## <a name="updates-for-version-121104"></a>Обновления для версии 1.2.1104

*Дата публикации: 23.06.2020*

- Обновлена логика автоматического обнаружения для параметра **подписки**, и теперь поддерживается версия Виртуального рабочего стола Windows, интегрированная с Azure Resource Manager. Клиентам, у которых есть только ресурсы Виртуального рабочего стола Windows, больше не нужно предоставлять согласие для использования Виртуального рабочего стола Windows (классическая версия).
- Улучшена поддержка устройств с высоким разрешением и коэффициентом масштабирования до 400 %.
- Устранена проблема, из-за которой не отображалось диалоговое окно отключения.
- Устранена проблема, из-за которой подсказки в панели команд оставались видимыми дольше, чем ожидалось.
- Исправлена ошибка, происходившая при попытке подписаться сразу после обновления.
- Исправлена ошибка неправильного анализа даты и времени на некоторых языках.

## <a name="updates-for-version-121026"></a>Обновления для версии 1.2.1026

*Дата публикации: 27.05.2020*

- Теперь при оформлении подписки можно выбрать учетную запись, а не вводить адрес электронной почты.
- Добавлен новый параметр **Подписка по URL-адресу**, который позволяет указать URL-адрес рабочей области, на которую вы подписываетесь, или использовать [обнаружение электронной почты](../rds-email-discovery.md), если оно доступно, в случаях, когда не удается автоматически найти ресурсы. Аналогичные возможности применяются в процессе подписки в других клиентах удаленного рабочего стола. Их можно использовать для создания подписки непосредственно на рабочие области Виртуального рабочего стола Windows.
- Добавлена поддержка подписки на рабочую область с помощью новой [схемы URI](remote-desktop-uri.md), которую можно отправить пользователям по электронной почте или добавить на веб-сайт поддержки.
- Добавлено новое диалоговое окно **Сведения о подключении**, в котором приведены сведения о клиенте, сети и сервере для сеансов удаленного рабочего стола и приложений. Доступ к диалоговому окну можно получить на панели подключения в полноэкранном режиме или в системном меню при появлении окна.
- Сеансы рабочего стола, запущенные в оконном режиме, при разворачивании окна теперь всегда разворачиваются вместо перехода в полноэкранный режим. Используйте параметр **Полноэкранный режим** системного меню, чтобы перейти в полноэкранный режим.
- Теперь в запросе отмены подписки отображется значок предупреждения и перечисляются имена рабочих областей в виде маркированного списка.
- Добавлен раздел сведений в дополнительные диалоговые окна ошибок, чтобы помочь диагностировать проблемы.
- Добавлена метка времени в раздел сведений диалоговых окон ошибок.
- Исправлена проблема с неправильной работой параметра RDP-файла **Идентификатор размера рабочего стола**.
- Исправлена проблема, из-за которой параметр дисплея **Обновление разрешения при изменении размера** не применялся после запуска сеанса.
- Исправлены ошибки локализации на панели параметров рабочего стола.
- Исправлен размер поля фокуса при переходе по элементам управления на панели параметров рабочего стола.
- Исправлена проблема, из-за которой имена ресурсов были плохо различимы в режиме высокой контрастности.
- Исправлена проблема, из-за которой уведомление об обновлении в центре уведомлений отображалось более одного раза в день.

## <a name="updates-for-version-12945"></a>Обновления для версии 1.2.945

*Дата публикации: 28.04.2020*

- Добавлены новые параметры настройки экрана для подключений к рабочему столу при щелчке правой кнопкой мыши значка рабочего стола в Центре подключений.
  - Теперь доступны три варианта конфигурации экрана: **All displays** (Все экраны), **Single display** (Один экран), **Select displays** (Выбор экранов).
  - При выборе конфигурации экрана теперь отображаются только доступные параметры.
  - В режиме выбора экранов новый параметр **Maximize to current displays** (Развернуть на текущие экраны) позволяет динамически менять используемые для сеанса экраны без переподключения. При включении этого параметра изображение разворачивается во весь экран на всех экранах, связанных с окном сеанса.
  - Мы добавили параметр **Single display when windowed** (Один экран в оконном режиме) в режимы всех экранов и выбора экранов. При выборе этого параметра сеанс автоматически переключается на один экран при выходе из полноэкранного режима и автоматически возвращается к отображению на нескольких экранах при разворачивании окна.
- В системное меню, отображаемое при щелчке правой кнопкой мыши заголовка окна сеанса рабочего стола, мы добавили группу **Display settings** (Параметры экрана). Она позволяет динамически изменять некоторые параметры во время сеанса. В частности, вы можете изменять новые параметры **Single display mode when windowed** (Один экран в оконном режиме) и **Maximize to current displays** (Развернуть на текущие экраны).
- При выходе из полноэкранного режима окно сеанса возвращается в исходное расположение до перехода в полноэкранный режим.
- Интервал между обновлениями рабочих областей в фоновом режиме теперь составляет не один час, а четыре. Теперь при запуске клиента автоматически выполняется обновление.
- При сбросе пользовательских данных на странице со сведениями о программе теперь происходит переход в Центр подключений, а не закрытие клиента.
- Изменен порядок пунктов системного меню подключений к удаленному рабочему столу. Раздел справки теперь указывает на документацию по клиенту.
- Устранены некоторые проблемы с доступом при переходе по вкладкам и средствами чтения с экрана.
- Исправлена проблема, из-за которой диалоговое окно проверки подлинности Azure Active Directory появлялось за окном сеанса.
- Устранена проблема с мерцанием и сжатием при перетаскивании окна сеанса рабочего стола между экранами с разным разрешением.
- Устранена ошибка, возникающая при перенаправлении камер.
- Устранены ошибки, приводившие к сбоям, что повысило надежность работы.

## <a name="updates-for-version-12790"></a>Обновления для версии 1.2.790

*Дата публикации: 24.03.2020*

- Действие Update (Обновить) для рабочих областей переименовано на Refresh (Обновить) для согласованности с другими клиентами удаленного рабочего стола.
- Теперь рабочую область можно обновить прямо из контекстного меню.
- Обновление рабочей области вручную гарантирует обновление всего локального содержимого.
- Для сброса данных пользователя в клиенте на странице "О программе" не нужно удалять приложение.
- Можно также сбросить данные пользователя в клиенте с помощью команды msrdcw.exe /reset с необязательным параметром /f, который позволяет пропустить запрос.
- Теперь при переходе на страницу "О программе" выполняется автоматический поиск обновлений.
- Изменен цвет кнопок для согласованности.

## <a name="updates-for-version-12675"></a>Обновления для версии 1.2.675

*Дата публикации: 25.02.2020*

- Подключения к Виртуальному рабочему столу Windows теперь блокируются, если в RDP-файле отсутствует подпись или одно из свойств signscope изменено.
- Центр соединений больше не отображается как пустой, если рабочая область пуста или удалена.
- Чтобы оптимизировать устранение неполадок, добавлен идентификатор действия и код ошибки в сообщениях об отключении. Вы можете скопировать сообщение в диалоговом окне, нажав клавиши **CTRL+C**.
- Исправлена проблема, из-за которой в параметрах подключения к рабочему столу не обнаруживались экраны.
- Обновления клиента больше не приводят к автоматическому перезапуску компьютера.
- Значки без окон больше не отображаются на панели задач.

## <a name="updates-for-version-12605"></a>Обновления для версии 1.2.605

*Дата публикации: 29.01.2020*

- Теперь можно выбрать, какие рабочие столы будут использоваться для подключений к рабочему столу. Чтобы изменить этот параметр, щелкните правой кнопкой мыши значок подключения к рабочему столу и выберите **Параметры**.
- Исправлена проблема, из-за которой параметры подключения не отображали правильные коэффициенты масштабирования.
- Исправлена проблема, из-за которой экранный диктор не мог прочитать сведения в диалоговом окне, отображаемом при инициировании подключения.
- Исправлена проблема, из-за которой имя пользователя отображалось неправильно, если имена в Azure Active Directory и Active Directory не совпадали.
- Исправлена проблема, из-за которой клиент переставал отвечать во время инициирования подключения при отсутствии подключения к сети.
- Исправлена проблема, из-за которой клиент переставал отвечать при подключении гарнитуры.

## <a name="updates-for-version-12535"></a>Обновления для версии 1.2.535

*Дата публикации: 04.12.2019*

- Теперь вы можете получать доступ к сведениям об обновлениях непосредственно с помощью кнопки "Дополнительные параметры" на панели команд в верхней части клиента.
- Теперь вы можете отправлять отчеты об обратной связи с панели команд клиента.
- Параметр обратной связи теперь отображается, только если доступен Центр отзывов.
- Убедитесь, что уведомление об обновлении не отображается, если уведомления отключены с помощью политики.
- Исправлена проблема, из-за которой не удавалось запускать некоторые файлы RDP.
- Исправлена ошибка с запуском клиента из-за повреждения некоторых постоянных параметров.

## <a name="updates-for-version-12431"></a>Обновления для версии 1.2.431

*Дата публикации: 12.11.2019*

- Теперь доступны версии клиента для 32-разрядной платформы и платформы ARM64.
- Теперь клиент сохраняет любые изменения панели подключения (например, ее расположение, размер и закрепленное состояние) и применяет их в сеансах.
- Обновлены диалоговые окна сведений о шлюзе и состояния подключения.
- Устранена проблема, из-за которой при попытке подключиться после истечения срока действия маркера Azure Active Directory появлялись сразу два запроса учетных данных.
- В Windows 7 теперь правильно запрашиваются учетные данные у пользователей, если у них есть сохраненные учетные данные, а сервер запрещает это.
- Теперь при повторном подключении запрос Azure Active Directory отображается перед окном подключения.
- Элементы, закрепленные на панели задач, теперь обновляются во время обновления веб-канала.
- Улучшена прокрутка с помощью сенсорного ввода в центре подключений.
- Из раскрывающегося меню "Разрешение" удалена пустая строка.
- Удалены ненужные записи из диспетчера учетных данных Windows.
- Теперь при выходе из полноэкранного режима окна сеансов рабочего стола имеют правильный размер.
- Диалоговое окно отключения удаленного приложения RemoteApp теперь отображается на переднем плане при возобновлении сеанса после перехода в спящий режим.
- Устранены проблемы со специальными возможностями, например, при навигации с помощью клавиатуры.

## <a name="updates-for-version-12247"></a>Обновления для версии 1.2.247

*Дата публикации: 17.09.2019*

- Улучшены резервные языки для локализованной версии. (Например, FR-CA будет правильно отображаться на французском, а не на английском языке.)
- Теперь при удалении подписки клиент правильно удаляет сохраненные учетные данные из диспетчера учетных данных.
- Теперь процесс обновления клиента выполняется автоматически после запуска, а по завершении клиент перезапускается.
- Теперь клиент можно использовать в S-режиме в Windows 10.
- Устранена проблема, из-за которой происходил сбой процесса обновления для пользователей с пробелом в имени пользователя.
- Устранен сбой, возникавший при аутентификации во время подключения.
- Устранен сбой, который происходил при закрытии клиента.
