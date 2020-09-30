---
title: Развертывание инфраструктуры гиперконвергентном с помощью центра администрирования Windows
description: Развертывание инфраструктуры гиперконвергентном с помощью центра администрирования Windows.
ms.topic: article
author: cosmosdarwin
ms.author: cosdar
ms.date: 11/04/2019
ms.openlocfilehash: 1f8e8a5433b986333975f45009819a98d90b61fc
ms.sourcegitcommit: f89639d3861c61620275c69f31f4b02fd48327ab
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/29/2020
ms.locfileid: "91517510"
---
# <a name="deploy-hyperconverged-infrastructure-with-windows-admin-center"></a>Развертывание инфраструктуры гиперконвергентном с помощью центра администрирования Windows

> Применяется к: Windows Admin Center, ознакомительная версия Windows Admin Center

Для развертывания инфраструктуры гиперконвергентном с использованием двух или более подходящих серверов Windows можно использовать центр администрирования Windows [версии 1910](../overview.md) или более поздней. Эта новая функция имеет вид многоэтапного рабочего процесса, который поможет вам установить компоненты, настроить сеть, создать кластер и развернуть Локальные дисковые пространства и (или) программно-определяемую сеть (SDN), если они выбраны.

В центре администрирования Windows версии 2007 центр администрирования Windows поддерживает Azure Stack ХЦИ OS. Дополнительные сведения о [развертывании кластера в центре администрирования Windows см. в документации по Azure Stack хЦи](/azure-stack/hci/get-started). Несмотря на то, что эта документация посвящена Azure Stack ХЦИ, инструкции также обычно применяются к развертываниям Windows Server.

## <a name="undo-and-start-over"></a>Отменить и начать заново

Используйте эти командлеты Windows PowerShell, чтобы отменить изменения, внесенные рабочим процессом, и начать заново.

### <a name="remove-virtual-machines-or-other-clustered-resources"></a>Удаление виртуальных машин или других кластерных ресурсов

Если вы создали виртуальные машины или другие кластерные ресурсы, например сетевые контроллеры для программно-определяемой сети, сначала удалите их.

Например, чтобы удалить ресурсы по имени, используйте:

```PowerShell
Get-ClusterResource -Name "<NAME>" | Remove-ClusterResource
```

### <a name="undo-the-storage-steps"></a>Отмена действий хранилища

Если вы включили Локальные дисковые пространства, отключите ее с помощью этого сценария:

> [!Warning]
> Эти командлеты окончательно удаляют все данные в Локальные дисковые пространстваных томах. Это невозможно отменить.

```PowerShell
Get-VirtualDisk | Remove-VirtualDisk
Get-StoragePool -IsPrimordial $False | Remove-StoragePool
Disable-ClusterS2D
```

### <a name="undo-the-clustering-steps"></a>Отмена шагов кластеризации

Если вы создали кластер, удалите его с помощью этого командлета:

```PowerShell
Remove-Cluster -CleanUpAD
```

Чтобы также удалить отчеты о проверке кластера, выполните этот командлет на каждом сервере, который входит в состав кластера:

```PowerShell
Get-ChildItem C:\Windows\cluster\Reports\ | Remove-Item
```

### <a name="undo-the-networking-steps"></a>Отмена действий по работе с сетью

Выполните эти командлеты на каждом сервере, который входит в состав кластера.

Если вы создали виртуальный коммутатор Hyper-V, выполните следующие действия.

```PowerShell
Get-VMSwitch | Remove-VMSwitch
```

> [!Note]
> `Remove-VMSwitch`Командлет автоматически удаляет все виртуальные адаптеры и отменяет объединение физических адаптеров, внедренных в коммутаторы.

Если вы изменили свойства сетевого адаптера, такие как имя, IPv4-адрес и идентификатор виртуальной ЛС, выполните следующие действия.

> [!Warning]
> Эти командлеты удаляют имена сетевых адаптеров и IP-адреса. Убедитесь, что у вас есть сведения, необходимые для подключения, например адаптер для управления, который исключен из приведенного ниже сценария. Кроме того, убедитесь, что вы знаете, как соединяются серверы с точки зрения физических свойств, таких как MAC-адрес, а не только имени адаптера в Windows.

```PowerShell
Get-NetAdapter | Where Name -Ne "Management" | Rename-NetAdapter -NewName $(Get-Random)
Get-NetAdapter | Where Name -Ne "Management" | Get-NetIPAddress -ErrorAction SilentlyContinue | Where AddressFamily -Eq IPv4 | Remove-NetIPAddress
Get-NetAdapter | Where Name -Ne "Management" | Set-NetAdapter -VlanID 0
```

Теперь все готово для запуска рабочего процесса.

## <a name="additional-references"></a>Дополнительные ссылки

- [Привет, центр администрирования Windows](../overview.md)
- [Развертывание локальных дисковых пространств](../../../storage/storage-spaces/deploy-storage-spaces-direct.md)
