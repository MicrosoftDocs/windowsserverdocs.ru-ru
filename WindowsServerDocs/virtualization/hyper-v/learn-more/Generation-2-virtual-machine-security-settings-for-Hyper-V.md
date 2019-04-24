---
title: Параметры безопасности виртуальной машины поколения 2 для Hyper-V
description: Описание параметров безопасности, доступные в диспетчере Hyper-V для виртуальных машин поколения 2
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 06ab4f5f-6b8e-4058-8108-76785aa93d4c
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 90a2b7234ee55d8469b6e02ba3de3a0efc080a3e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889505"
---
# <a name="generation-2-virtual-machine-security-settings-for-hyper-v"></a>Параметры безопасности виртуальной машины поколения 2 для Hyper-V

>Область применения. Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019 г., Microsoft Hyper-V Server 2019 г.

Используйте настройки безопасности виртуальной машины в диспетчере Hyper-V для защиты данных и состояние виртуальной машины. Виртуальные машины можно защитить от проверки, кражи и подмены от обоих вредоносных программ, которая может выполняться на узле и администраторам центров обработки данных. Уровень безопасности, которые вы получаете зависит от оборудования размещающей, при запуске, поколение виртуальной машины, и ли настроить службу, служба защиты узла, который авторизует узлы для запуска экранированных виртуальных машин.  

Служба защиты узла — это новая роль в Windows Server 2016. Идентифицирует допустимые узлы Hyper-V, а также разрешает им запускать определенной виртуальной машины. Чаще всего, будет Настройка службы защиты узла для центра обработки данных. Но вы можете создать экранированной виртуальной машины, чтобы запустить его локально без настройки службы защиты узла. Позже вы можете распределить экранированной виртуальной машины к структуре защиты узла.  

Если вы еще не настроили службы защиты узла или используете его в локальном режиме на узле Hyper-V, и у узла есть защитный ключ файла владелец виртуальной машины, можно изменить параметры, описанные в этом разделе.   Владельцем ключа защиты является организация, которая создает и общих папок, закрытого или открытого ключа, который будет владельцем всех виртуальных машин, созданных с помощью этого ключа.  

Чтобы узнать, как сделать ваши виртуальные машины более безопасным при использовании службы защиты узла, см. следующие ресурсы.  

- [Усиление защиты структуры: Защита секретов клиента в Hyper-V (Ignite видео)](https://go.microsoft.com/fwlink/?LinkId=746379)
- [Защищенная структура и экранированные виртуальные машины](https://go.microsoft.com/fwlink/?LinkId=746381)

## <a name="secure-boot-setting-in-hyper-v-manager"></a>Защиты загрузки в диспетчере Hyper-V  

Безопасная загрузка является это функция, доступная с виртуальными машинами поколения 2, помогает избежать несанкционированного, операционных систем или драйверов Unified Extensible Firmware Interface (UEFI) (также известный как ПЗУ) во время запуска системы. Безопасная загрузка включена по умолчанию. Безопасная загрузка можно использовать с виртуальными машинами поколения 2 под управлением операционных систем Windows или Linux распространения.  

Сертификаты, которые необходимо проверить целостность процесса загрузки см. шаблоны, описанные в следующей таблице.  

|Имя шаблона|Описание|  
|-----------------|---------------|  
|Microsoft Windows|Выберите для безопасной загрузки виртуальной машины для операционной системы Windows.|  
|Центр сертификации Microsoft UEFI|Выберите для безопасной загрузки виртуальной машины для операционной системы Linux распространения.|  
|С открытым исходным кодом экранированной виртуальной Машины|Этот шаблон используется для безопасной загрузки для [под управлением Linux экранированных виртуальных машин](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template).|

Дополнительные сведения см. в следующих статьях.  

- [Общие сведения о безопасности Windows 10](https://docs.microsoft.com/windows/security/threat-protection/overview-of-threat-mitigations-in-windows-10)  
- [Следует ли создавать виртуальные машины поколения 1 или 2 в Hyper-V?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  
- [Linux и виртуальные машины FreeBSD в Hyper-V](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Параметры поддержки шифрования в диспетчере Hyper-V

Можно защитить данные и состояние виртуальной машины, выбрав следующие параметры поддержки шифрования.  

- **Включить доверенный платформенный модуль** -этот параметр делает доступными для виртуальной машины виртуализированных микросхемы доверенного платформенного модуля (TPM). Это разрешает гостевой системе шифрование диска виртуальной машины с помощью BitLocker.
  - Если на узле Hyper-V работает под управлением Windows 10 1511, вам нужно включить режим изолированного пользователя. 
- **Шифрование трафика миграции состояния и виртуальной Машины** — шифрует состояние виртуальной машины сохранены и трафика динамической миграции.

### <a name="enable-isolated-user-mode"></a>Включить режим изолированного пользователя

При выборе **включить доверенный платформенный модуль** на узлах Hyper-V под управлением версии Windows более ранней, чем Юбилейное обновление Windows 10, необходимо включить в изолированном режиме пользователя. Не нужно выполнить для узлов Hyper-V, запуска Windows Server 2016 и Юбилейное обновление Windows 10 или более поздней версии.

Изолированный режим пользователя — это среда, на котором размещена безопасности приложений в виртуальном безопасном режиме на узле Hyper-V. Виртуальный безопасный режим используется для обеспечения безопасности и защиты состояния микросхему виртуального доверенного платформенного МОДУЛЯ.  

Для перехода в режим изолированного пользователя на узле Hyper-V, управлением предыдущих версий Windows 10  

1.  Откройте Windows PowerShell от имени администратора.  

2.  Выполните следующие команды:  

    ```  
    Enable-WindowsOptionalFeature -Feature IsolatedUserMode -Online  
    New-Item -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Force  
    New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name EnableVirtualizationBasedSecurity -Value 1 -PropertyType DWord -Force  

    ```  

Можно перенести виртуальную машину с помощью виртуального доверенного платформенного МОДУЛЯ, включить любой узел, на котором выполняется Windows Server 2016, Windows 10 сборки 10586 или более поздней версии. Но при переходе на другой узел, может не смогут запустить его. Необходимо обновить предохранители ключа для этой виртуальной машине для авторизации на новый узел для запуска виртуальной машины. Дополнительные сведения см. в разделе [Защищенная структура и экранированные виртуальные машины](https://go.microsoft.com/fwlink/?LinkId=746381) и [требования к системе для Hyper-V в Windows Server](../System-requirements-for-Hyper-V-on-Windows.md).  

## <a name="security-policy-in-hyper-v-manager"></a>Политика безопасности в диспетчере Hyper-V  
Для повышения безопасности виртуальной машины, используйте **Включение экранирования** возможность отключения функции управления, например подключение к консоли, PowerShell Direct и некоторые компоненты интеграции. Если выбран этот параметр, **безопасной загрузки**, **включить доверенный платформенный модуль**, и **трафика миграции состояния Encrypt и виртуальной Машины** выбраны и применяются параметры.   

Экранированной виртуальной машины можно запустить локально без настройки службы защиты узла. Но при переходе на другой узел, может не смогут запустить его. Необходимо обновить предохранители ключа для этой виртуальной машине для авторизации на новый узел для запуска виртуальной машины. Дополнительные сведения см. в разделе [Защищенная структура и экранированные виртуальные машины](https://go.microsoft.com/fwlink/?LinkId=746381).  

Дополнительные сведения о безопасности в Windows Server, см. в разделе [безопасность и контроль](../../../security/Security-and-Assurance.md).  