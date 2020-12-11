---
description: Дополнительные сведения о развертывании защищенных узлов
title: Развертывание защищенных узлов
ms.topic: article
ms.assetid: 2379ca26-b32d-4055-8b4b-99d1f2df37e1
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: fb3d189ce0817d52a536af8f25fd9b78fda719e5
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049882"
---
# <a name="deploy-guarded-hosts"></a>Развертывание защищенных узлов

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016

В подразделах этого раздела описываются шаги, необходимые администратору структуры для настройки узлов Hyper-V для работы со службой защиты узла (HGS). Прежде чем вы сможете выполнить эти действия, необходимо настроить хотя бы один узел в [кластере HGS](guarded-fabric-setting-up-the-host-guardian-service-hgs.md).

**Для аттестации, доверенной для доверенного платформенного модуля**:
1. [Настройка DNS-сервера структуры](guarded-fabric-configuring-fabric-dns.md). указывает, как настроить сервер пересылки DNS из домена структуры в домен HGS.
2. [Запись сведений, необходимых для HGS](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md): сведения о том, как записывать идентификаторы доверенного платформенного модуля (также называемые идентификаторами платформы), создавать политику целостности кода и создавать базовые показатели TPM. Затем эти сведения будут предоставлены администратору HGS для настройки аттестации.
3. [Подтверждение аттестации защищенных узлов](guarded-fabric-confirm-hosts-can-attest-successfully.md)

**Для аттестации ключа узла**:
1. [Создание ключа узла](guarded-fabric-create-host-key.md#create-a-host-key): указывает, как настроить сервер пересылки DNS из домена структуры в домен HGS.
2. [Добавление ключа узла в службу аттестации](guarded-fabric-create-host-key.md#add-the-host-key-to-the-attestation-service): сведения о настройке группы безопасности Active Directory в домене структуры, добавлении защищенных узлов в качестве членов этой группы и предоставлении идентификатора группы администратору HGS.
3. [Подтверждение аттестации защищенных узлов](guarded-fabric-confirm-hosts-can-attest-successfully.md)


**Для аттестации, доверенной для администраторов**:
1. [Настройка DNS-сервера структуры](guarded-fabric-configuring-fabric-dns.md). указывает, как настроить сервер пересылки DNS из домена структуры в домен HGS.
2. [Создание группы безопасности](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md). сведения о настройке группы безопасности Active Directory в домене структуры, добавлении защищенных узлов в качестве членов этой группы и предоставлении идентификатора группы администратору HGS.
3. [Подтверждение аттестации защищенных узлов](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="additional-references"></a>Дополнительные ссылки

- [Задачи развертывания для защищенных структур и экранированных виртуальных машин](guarded-fabric-deploying-hgs-overview.md#deployment-tasks-for-guarded-fabrics-and-shielded-vms)
