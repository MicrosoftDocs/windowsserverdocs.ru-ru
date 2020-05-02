---
title: reg export
description: Справочный раздел по * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ad9526f-1e29-4fa5-9d2d-feaa92f12d7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b2c697595d5d19c953ef85f7a2e334c6fe05329d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722562"
---
# <a name="reg-export"></a>reg export



Копирует указанные подразделы, записи и значения локального компьютера в файл для перемещения на другие серверы.



## <a name="syntax"></a>Синтаксис

```
Reg export KeyName FileName [/y]
```

### <a name="parameters"></a>Параметры

|Параметр|Описание|
|---------|-----------|
|\<KeyName>|Указывает полный путь к подразделу. Операция экспорта работает только с локальным компьютером. KeyName должен содержать допустимый корневой ключ. Допустимые корневые ключи: HKLM, HKCU, HKCR, HKU и ХККК.|
|\<Имя файла>|Указывает имя и путь к файлу, который будет создан во время операции. Файл должен иметь расширение reg.|
|/y|Перезаписывает существующий файл с именем *filename* без запроса подтверждения.|
|/?|Отображает справку по **экспорту реестра** в командной строке.|

## <a name="remarks"></a>Примечания

В следующей таблице перечислены возвращаемые значения для операции **reg export** .

|Значение|Описание|
|-----|-----------|
|0|Успех|
|1|Сбой|

## <a name="examples"></a>Примеры

Чтобы экспортировать содержимое всех подразделов и значений раздела MyApp в файл Аппбкуп. reg, введите:
```
reg export HKLM\Software\MyCo\MyApp AppBkUp.reg
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)