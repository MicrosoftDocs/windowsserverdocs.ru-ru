---
title: manage-bde
description: Справочная статья по команде Manage-bde, которая включает или выключает BitLocker, задает механизмы снятия блокировки, обновляет методы восстановления и разблокирует диски данных, защищенные BitLocker.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 276a7841-7289-48d4-a57d-bc7c300affbb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 480f44c6467587918ad347413315b208c874f8cd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922123"
---
# <a name="manage-bde"></a>manage-bde

Включает или выключает BitLocker, задает механизмы разблокировки, обновляет методы восстановления и разблокирует диски данных, защищенные BitLocker.

> [!NOTE]
> Это средство командной строки можно использовать вместо элемента панели управления **Шифрование диска BitLocker** .

## <a name="syntax"></a>Синтаксис

```
manage-bde [-status] [–on] [–off] [–pause] [–resume] [–lock] [–unlock] [–autounlock] [–protectors] [–tpm]
[–setidentifier] [-forcerecovery] [–changepassword] [–changepin] [–changekey] [-keypackage] [–upgrade] [-wipefreespace] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
| --------- |------------ |
| [Управление — состояние BDE](manage-bde-status.md) | Предоставляет сведения обо всех дисках на компьютере независимо от того, защищены ли они с помощью BitLocker. |
| [Управление — BDE в](manage-bde-on.md) | Шифрует диск и включает BitLocker. |
| [Manage-bde выкл.](manage-bde-off.md) | Расшифровывает диск и отключает BitLocker. Все предохранители ключа удаляются после завершения расшифровки. |
| [Управление — приостановка BDE](manage-bde-pause.md) | Приостанавливает шифрование или расшифровку. |
| [Управление — возобновление BDE](manage-bde-resume.md) | Возобновляет шифрование или расшифровку. |
| [Управление — блокировка BDE](manage-bde-lock.md) | Предотвращает доступ к данным, защищенным BitLocker. |
| [Управление-BDE Unlock](manage-bde-unlock.md) | Разрешает доступ к данным, защищенным BitLocker, с помощью пароля восстановления или ключа восстановления. |
| [Управление — автоматическое разблокирование BDE](manage-bde-autounlock.md) | Управляет автоматическим разблокировкой дисков данных. |
| [Управление — предохранители BDE](manage-bde-protectors.md) | Управляет методами защиты для ключа шифрования. |
| [Управление — TPM BDE](manage-bde-tpm.md) | Настраивает доверенный платформенный модуль (TPM) компьютера (TPM). Эта команда не поддерживается на компьютерах под управлением Windows 8 или **win8_server_2**. Для управления доверенным платформенным модулем на этих компьютерах используйте оснастку MMC "Управление TPM" или командлеты управления TPM для Windows PowerShell. |
| [Управление — BDE сетидентифиер](manage-bde-setidentifier.md)   | Задает для поля "идентификатор диска" значение, указанное в поле **Укажите уникальные идентификаторы для вашей организации** групповая политика параметр. |
| [Управление — BDE Форцерековери](manage-bde-forcerecovery.md) | Принудительное перезагрузку диска, защищенного с помощью BitLocker, в режим восстановления. Эта команда удаляет из диска все предохранители ключей, связанные с TPM. При перезапуске компьютера для разблокировки диска можно использовать только пароль восстановления или ключ восстановления. |
| [Manage-bde ChangePassword](manage-bde-changepassword.md) | Изменяет пароль для диска данных. |
| [Управление — BDE чанжепин](manage-bde-changepin.md) | Изменяет ПИН-код для диска операционной системы. |
| [Управление — BDE чанжекэй](manage-bde-changekey.md) | Изменяет ключ запуска для диска операционной системы. |
| [Управление — BDE Кэйпаккаже](manage-bde-keypackage.md) | Создает пакет ключей для диска. |
| [Управление обновлением BDE](manage-bde-upgrade.md) | Обновляет версию BitLocker. |
| [Управление — BDE Випефриспаце](manage-bde-wipefreespace.md) | Очищает свободное место на диске. |
| -? или/? | Отображает краткую справку в командной строке. |
| -Help или-h | Отображает полную справку в командной строке. |

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Включение BitLocker с помощью командной строки](https://technet.microsoft.com/library/dd894351(v=ws.10).aspx)
