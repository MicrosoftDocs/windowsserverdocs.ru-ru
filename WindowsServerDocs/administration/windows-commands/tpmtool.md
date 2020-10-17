---
title: tpmtool
description: Справочная статья по команде тпмтул, которая получает сведения о доверенный платформенный модуль (TPM).
ms.topic: reference
author: ashleytqy
ms.author: asteoh
manager: raigner
ms.date: 05/07/2019
ms.openlocfilehash: bc0aaa4bc4bd9c23e0cf22b0315335287867d8cd
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156430"
---
# <a name="tpmtool"></a>tpmtool

Эту служебную программу можно использовать для получения сведений о [доверенный платформенный модуль (TPM) (TPM)](/windows/security/information-protection/tpm/trusted-platform-module-overview).

>[!IMPORTANT]
>Некоторые сведения могут быть связаны с предварительной версией продукта, которая может быть значительно изменена до выпуска коммерческой версии. Майкрософт не дает никаких гарантий, явных или подразумеваемых, в отношении предоставленной здесь информации.

## <a name="syntax"></a>Синтаксис

```
tpmtool /parameter [<arguments>]
```

### <a name="parameters"></a>Параметры

| Параметр | Описание |
|--|--|
| жетдевицеинформатион | Отображает основные сведения о доверенном платформенном модуле. Сведения о значениях флагов сведений см. в статье [Параметры метода Win32_Tpm:: исреадинформатион](/windows/win32/secprov/win32-tpm-isreadyinformation#parameters) . |
| гасерлогс [путь к выходному каталогу] | Собирает журналы TPM и помещает их в указанный каталог. Если этот каталог не существует, он будет создан. По умолчанию файлы журналов помещаются в текущий каталог. Ниже перечислены возможные создаваемые файлы.<ul><li>Тпмевентс. evtx</li><li>TpmInformation.txt</li><li>Сртмбут. dat</li><li>Сртмресуме. dat</li><li>Дртмбут. dat</li><li>Дртмресуме. dat</li></ul> |
| дривертраЦинг `[start | stop]` | Запускает или останавливает сбор трассировок драйверов TPM. Журнал трассировки *тпмтраце. ETL*создается и помещается в текущий каталог. |
| /? | Отображение справки в командной строке. |

## <a name="examples"></a>Примеры

Чтобы отобразить основные сведения о TPM, введите:

```
tpmtool getdeviceinformation
```

Чтобы получить журналы TPM и поместить их в текущий каталог, введите:

```
tpmtool gatherlogs
```

Чтобы получить журналы TPM и поместить их в `C:\Users\Public` , введите:

```
tpmtool gatherlogs C:\Users\Public
```

Чтобы получить информацию о трассировках драйверов TPM, введите:

```
tpmtool drivertracing start
# Run scenario
tpmtool drivertracing stop
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)

- [Коды ошибок COM (TPM, PLA, ФВЕ)](/windows/win32/com/com-error-codes-6)
