---
title: Get-Аллсерверс
description: Справочная статья по Get-Аллсерверс, которая извлекает сведения обо всех серверах служб развертывания Windows.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe2e3c69-8f2e-457d-af55-d249ebf70f53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a02515b138c9db6a1d320a4ad466700c15b84749
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935060"
---
# <a name="get-allservers"></a>Get-Аллсерверс

Извлекает сведения обо всех серверах служб развертывания Windows.

> [!NOTE]
> Выполнение этой команды может занять продолжительное время, если в среде имеется много серверов служб развертывания Windows или если сетевое подключение к серверу работает слишком долго.

## <a name="syntax"></a>Синтаксис

```
WDSUTIL [Options] /Get-AllServers /Show:{Config | Images | All} [/Detailed] [/Forest:{Yes | No}]
```

### <a name="parameters"></a>Параметры

|   Параметр   |                                                                                                                 Описание                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Show: {config |                                                                                                                    Изображения                                                                                                                    |
|  [/Детаилед]  | При использовании в сочетании с параметром **/Show: Images** или **/Show: ALL**возвращает все метаданные образа из каждого изображения. Если параметр **/детаилед** не указан, по умолчанию возвращается имя образа, описание и имя файла. |
| [/Forest: {Да |                                                                                                                     Нет}]                                                                                                                     |

## <a name="examples"></a>Примеры

Чтобы просмотреть сведения обо всех серверах, введите:
```
WDSUTIL /Get-AllServers /Show:Config
```
Чтобы просмотреть подробные сведения обо всех серверах, введите:
```
WDSUTIL /Verbose /Get-AllServers /Show:All /Detailed /Forest:Yes
```

## <a name="additional-references"></a>Дополнительные ссылки

- [Условные обозначения синтаксиса команд командной строки](command-line-syntax-key.md)