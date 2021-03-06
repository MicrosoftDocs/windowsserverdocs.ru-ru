---
title: Создание виртуального коммутатора для виртуальных машин Hyper-V
description: Содержит инструкции по созданию виртуального коммутатора с помощью диспетчера Hyper-V или Windows PowerShell.
ms.topic: how-to
ms.assetid: fdc8063c-47ce-4448-b445-d7ff9894dc17
ms.author: benarm
author: BenjaminArmstrong
ms.date: 10/04/2016
ms.openlocfilehash: da1082a90f5d028ae6be0581245d298f3a4c00d0
ms.sourcegitcommit: 40905b1f9d68f1b7d821e05cab2d35e9b425e38d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/06/2021
ms.locfileid: "97946900"
---
# <a name="create-a-virtual-switch-for-hyper-v-virtual-machines"></a>Создание виртуального коммутатора для виртуальных машин Hyper-V

> Область применения: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Виртуальный коммутатор позволяет виртуальным машинам, созданным на узлах Hyper-V, взаимодействовать с другими компьютерами. Виртуальный коммутатор можно создать при первой установке роли Hyper-V в Windows Server. Чтобы создать дополнительные виртуальные коммутаторы, используйте диспетчер Hyper-V или Windows PowerShell. Дополнительные сведения о виртуальных коммутаторах см. в статье [виртуальный коммутатор Hyper-V](../../hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).

Сеть виртуальных машин может быть сложной темой. И существует несколько новых функций виртуального коммутатора, которые можно использовать, например, [объединение внедренных коммутаторов (Set)](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md#switch-embedded-teaming-set). Но основная сеть довольно проста. В этом разделе описывается достаточно просто, чтобы можно было создавать сетевые виртуальные машины в Hyper-V. Чтобы узнать больше о том, как можно настроить сетевую инфраструктуру, ознакомьтесь с документацией по [сети](../../../networking/index.yml) .

## <a name="create-a-virtual-switch-by-using-hyper-v-manager"></a>Создание виртуального коммутатора с помощью диспетчера Hyper-V

1. Откройте диспетчер Hyper-V и выберите имя компьютера узла Hyper-V.

2. Выберите **действие**  >  **Диспетчер виртуальных коммутаторов**.

    ![Снимок экрана, показывающий действие пункта меню > диспетчера виртуальных коммутаторов](../media/Hyper-V-Action-VSwitchManager.png)

3. Выберите тип нужного виртуального коммутатора.

    | Тип подключения | Описание |
    | --------------- | ----------- |
    |     External    | Предоставляет виртуальным машинам доступ к физической сети для взаимодействия с серверами и клиентами во внешней сети. Позволяет виртуальным машинам на одном сервере Hyper-V взаимодействовать друг с другом. |
    |     Внутренние    | Разрешает обмен данными между виртуальными машинами на одном сервере Hyper-V, а также между виртуальными машинами и операционной системой узла управления. |
    |     Личные     | Разрешает обмен данными только между виртуальными машинами на одном сервере Hyper-V. Частная сеть изолирована от всего внешнего сетевого трафика на сервере Hyper-V. Этот тип сети полезен, если необходимо создать изолированную сетевую среду, например изолированный тестовый домен. |

4. Выберите **создать виртуальный коммутатор**.

5. Добавьте имя для виртуального коммутатора.

6. Если выбран параметр внешний, выберите сетевой адаптер, который вы хотите использовать, и любые другие параметры, описанные в следующей таблице.

    ![Снимок экрана, на котором показаны параметры внешней сети](../media/Hyper-V-NewVSwitch-ExternalOptions.png)

    | Имя параметра | Описание: |
    | ------------ | ----------- |
    | Разрешить управляющей операционной системе предоставлять общий доступ к этому сетевому адаптеру | Выберите этот параметр, если вы хотите разрешить узлу Hyper-V совместно использовать виртуальный коммутатор и сетевую карту или группу сетевых адаптеров с виртуальной машиной. Если этот параметр включен, узел может использовать любые параметры, настроенные для виртуального коммутатора, такие как параметры качества обслуживания (QoS), параметры безопасности или другие функции виртуального коммутатора Hyper-V. |
    | Включить виртуализацию SR-IOV | Выберите этот параметр, только если вы хотите разрешить трафику виртуальной машины обходить коммутатор виртуальной машины и перейти непосредственно к физическому сетевому адаптеру. Дополнительные сведения см. в [статье Виртуализация ввода-вывода с единым корнем](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn641211(v=ws.11)#Sec4) в справочнике по основам для плакатов: сети Hyper-V. |

7. Если вы хотите изолировать сетевой трафик от операционной системы узла управления Hyper-V или других виртуальных машин, использующих один и тот же виртуальный коммутатор, выберите параметр **включить идентификацию виртуальной локальной сети для операционной системы управления**. Можно изменить идентификатор виртуальной ЛС на любое число или оставить значение по умолчанию. Это идентификационный номер виртуальной локальной сети, который будет использоваться операционной системой управления для всех сетевых подключений через этот виртуальный коммутатор.

    ![Снимок экрана, на котором показаны параметры идентификатора виртуальной ЛС](../media/Hyper-V-NewSwitch-VLAN.png)

8. Нажмите кнопку **OK**.

9. Нажмите кнопку **Да**.

    ![Снимок экрана, показывающий сообщение "ожидающие изменения могут нарушить подключение к сети"](../media/Hyper-V-NewVSwitch-DisruptNetwork.png)

## <a name="create-a-virtual-switch-by-using-windows-powershell"></a>Создание виртуального коммутатора с помощью Windows PowerShell

1. На рабочем столе Windows нажмите кнопку "Пуск" и введите любую часть имени **Windows PowerShell**.

2. Щелкните правой кнопкой мыши Windows PowerShell и выберите команду **Запуск от имени администратора**.

3. Найдите существующие сетевые адаптеры, выполнив командлет [Get-NetAdapter](https://docs.microsoft.com/powershell/module/netadapter/get-netadapter) . Запишите имя сетевого адаптера, который вы хотите использовать для виртуального коммутатора.

    ```PowerShell
    Get-NetAdapter
    ```

4. Создайте виртуальный коммутатор с помощью командлета [New-VMSwitch](https://docs.microsoft.com/powershell/module/hyper-v/new-vmswitch) . Например, чтобы создать внешний виртуальный коммутатор с именем Екстерналсвитч, используя сетевой адаптер Ethernet и **разрешить операционной системе управления включить общий доступ к этому сетевому адаптеру** , выполните следующую команду.

    ```PowerShell
    New-VMSwitch -name ExternalSwitch  -NetAdapterName Ethernet -AllowManagementOS $true
    ```

    Чтобы создать внутренний коммутатор, выполните следующую команду.

    ```PowerShell
    New-VMSwitch -name InternalSwitch -SwitchType Internal
    ```

    Чтобы создать частный коммутатор, выполните следующую команду.

    ```PowerShell
    New-VMSwitch -name PrivateSwitch -SwitchType Private
    ```

Дополнительные сценарии Windows PowerShell, посвященные усовершенствованным или новым функциям виртуального коммутатора в Windows Server 2016, см. в разделе [Удаленный доступ к памяти и переключение на объединение внедренных](../../hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)элементов.


## <a name="next-step"></a>Следующий шаг

[Создание виртуальной машины в Hyper-V](Create-a-virtual-machine-in-Hyper-V.md)
