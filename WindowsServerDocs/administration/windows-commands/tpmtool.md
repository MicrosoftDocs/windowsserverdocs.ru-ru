---
title: tpmtool
description: Справочная статья по тпмтул, которая получает сведения о доверенный платформенный модуль (TPM).
ms.topic: reference
author: ashleytqy
ms.author: ashleytqy
manager: ronaldai
ms.date: 05/07/2019
ms.openlocfilehash: b0f234755eefdca15f214dad428f02631592e8c2
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027002"
---
# <a name="tpmtool"></a>tpmtool

Эту служебную программу можно использовать для получения сведений о [доверенный платформенный модуль (TPM) (TPM)](/windows/security/information-protection/tpm/trusted-platform-module-overview).

>[!IMPORTANT]
>Некоторые сведения относятся к предварительным версиям продуктов, в которые перед коммерческим выпуском могут быть внесены существенные изменения. Майкрософт не предоставляет никаких гарантий, явных или подразумеваемых, относительно приведенных здесь сведений.

В разделе [Примеры](#tpmtool_examples) показан принцип использования этой команды.

## <a name="syntax"></a>Синтаксис

```
tpmtool /parameter [<arguments>]
```
### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|жетдевицеинформатион|Отображает основные сведения о доверенном платформенном модуле. Значение флагов сведений можно найти [здесь](/windows/desktop/secprov/win32-tpm-isreadyinformation#parameters).|
|гасерлогс [путь к выходному каталогу]|Собирает журналы TPM и помещает их в указанный каталог. Если этот каталог не существует, он будет создан. По умолчанию они помещаются в текущий каталог. Ниже перечислены возможные создаваемые файлы. </br>-Тпмевентс. evtx</br>— TpmInformation.txt</br>-Сртмбут. dat</br>-Сртмресуме. dat</br>-Дртмбут. dat</br>-Дртмресуме. dat</br>|
|дривертраЦинг [запуск/завершение]|Запуск и завершение сбора трассировок драйверов TPM. Журнал трассировки ТПМТРАЦЕ. ETL будет создан и помещен в текущий каталог.|
|/?|Отображение справки в командной строке.|

## <a name="examples"></a><a name=tpmtool_examples></a>Примеры

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

## <a name="decoding-error-codes"></a>Коды ошибок декодирования

Коды ошибок, специфичные для TPM, описаны [здесь](/windows/desktop/com/com-error-codes-6).
