---
title: Get-Аллсерверс
description: Справочная статья по Get-Аллсерверс, которая извлекает сведения обо всех серверах служб развертывания Windows.
ms.topic: article
ms.assetid: fe2e3c69-8f2e-457d-af55-d249ebf70f53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6218b3dba4e87758322a7d33865b9a1a69dcb9fa
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896385"
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

|   Параметр   |                                                                                                                 Описание:                                                                                                                  |
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