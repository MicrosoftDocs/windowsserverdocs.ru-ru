---
title: Настройка дополнительных узлов HGS
description: 'Дополнительные сведения: Настройка дополнительных узлов HGS'
ms.topic: article
ms.assetid: 227f723b-acb2-42a7-bbe3-44e82f930e35
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 01/14/2020
ms.openlocfilehash: 6bb3db6df690c56b6062134d735da70f026aed7b
ms.sourcegitcommit: 65b6de6b44d41f1180c45db11cdd60cb2a093b46
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/10/2020
ms.locfileid: "97049932"
---
# <a name="configure-additional-hgs-nodes"></a>Настройка дополнительных узлов HGS

>Область применения: Windows Server 2019, Windows Server (половина ежегодного канала), Windows Server 2016

В рабочей среде HGS следует настроить в кластере с высоким уровнем доступности, чтобы обеспечить возможность включения экранированных виртуальных машин даже в том случае, если узел HGS выйдет из строя. Для тестовых сред дополнительные узлы HGS не требуются.

Используйте один из этих методов для добавления узлов HGS, которые лучше всего подходят для вашей среды.

| Среда | Вариант 1 | Вариант 2 |
|--|--|--|
| Новый лес HGS | [Использование PFX-файлов](#dedicated-hgs-forest-with-pfx-certificates) | [Использование отпечатков сертификатов](#dedicated-hgs-forest-with-certificate-thumbprints) |
| Существующий лес бастиона | [Использование PFX-файлов](#existing-bastion-forest-with-pfx-certificates) | [Использование отпечатков сертификатов](#existing-bastion-forest-with-certificate-thumbprints) |

## <a name="prerequisites"></a>Предварительные требования

Убедитесь, что каждый дополнительный узел:
- Имеет ту же конфигурацию оборудования и программного обеспечения, что и основной узел
- Подключен к той же сети, что и другие серверы HGS
- Может разрешать другие серверы HGS по их DNS-именам

## <a name="dedicated-hgs-forest-with-pfx-certificates"></a>Выделенный лес HGS с сертификатами PFX

1. Повышение уровня узла HGS до контроллера домена
2. Инициализация сервера HGS

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>Повышение уровня узла HGS до контроллера домена

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)]

### <a name="initialize-the-hgs-server"></a>Инициализация сервера HGS

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)]

## <a name="dedicated-hgs-forest-with-certificate-thumbprints"></a>Выделенный лес HGS с отпечаткой сертификатов

1. Повышение уровня узла HGS до контроллера домена
2. Инициализация сервера HGS
3. Установка закрытых ключей для сертификатов

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>Повышение уровня узла HGS до контроллера домена

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)]

### <a name="initialize-the-hgs-server"></a>Инициализация сервера HGS

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)]

### <a name="install-the-private-keys-for-the-certificates"></a>Установка закрытых ключей для сертификатов

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="existing-bastion-forest-with-pfx-certificates"></a>Существующий лес бастиона с сертификатами PFX

1. Присоединение узла к существующему домену
2. Предоставьте компьютеру права на получение пароля gMSA и запуск Install-ADServiceAccount
3. Инициализация сервера HGS

### <a name="join-the-node-to-the-existing-domain"></a>Присоединение узла к существующему домену

1. Убедитесь, что по крайней мере одна сетевая карта на узле настроена для использования DNS-сервера на первом сервере HGS.
2. Присоедините новый узел HGS к тому же домену, что и ваш первый узел HGS.

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>Предоставьте компьютеру права на получение пароля gMSA и запуск Install-ADServiceAccount

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)]

### <a name="initialize-the-hgs-server"></a>Инициализация сервера HGS

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)]

## <a name="existing-bastion-forest-with-certificate-thumbprints"></a>Существующий лес бастиона с отпечаткой сертификатов

1. Присоединение узла к существующему домену
2. Предоставьте компьютеру права на получение пароля gMSA и запуск Install-ADServiceAccount
3. Инициализация сервера HGS
4. Установка закрытых ключей для сертификатов

### <a name="join-the-node-to-the-existing-domain"></a>Присоединение узла к существующему домену

1. Убедитесь, что по крайней мере одна сетевая карта на узле настроена для использования DNS-сервера на первом сервере HGS.
2. Присоедините новый узел HGS к тому же домену, что и ваш первый узел HGS.

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>Предоставьте компьютеру права на получение пароля gMSA и запуск Install-ADServiceAccount

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)]

### <a name="initialize-the-hgs-server"></a>Инициализация сервера HGS

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)]

Шифрование и подпись сертификатов с первого сервера HGS для репликации на этот узел займет до 10 минут.

### <a name="install-the-private-keys-for-the-certificates"></a>Установка закрытых ключей для сертификатов

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="configure-hgs-for-https-communications"></a>Настройка HGS для обмена данными по протоколу HTTPS

Если вы хотите защитить конечные точки HGS с помощью SSL-сертификата, необходимо настроить SSL-сертификат на этом узле, а также каждый другой узел в кластере HGS.
Сертификаты SSL *не* реплицируются службой HGS и не требуют использования одинаковых ключей для каждого узла (т. е. для каждого узла можно использовать разные SSL-сертификаты).

При запросе SSL-сертификата убедитесь, что полное доменное имя кластера (как показано в выходных данных `Get-HgsServer` ) является либо общим именем субъекта сертификата, либо включенным в качестве альтернативного DNS-имени субъекта.
После получения сертификата из центра сертификации можно настроить HGS для его использования с помощью [Set-HgsServer](/powershell/module/hgsserver/set-hgsserver).

```powershell
$sslPassword = Read-Host -AsSecureString -Prompt "SSL Certificate Password"
Set-HgsServer -Http -Https -HttpsCertificatePath 'C:\temp\HgsSSLCertificate.pfx' -HttpsCertificatePassword $sslPassword
```

Если вы уже установили сертификат в локальное хранилище сертификатов и хотите сослаться на него по отпечатку, выполните следующую команду:

```powershell
Set-HgsServer -Http -Https -HttpsCertificateThumbprint 'A1B2C3D4E5F6...'
```

HGS всегда будет предоставлять порты HTTP и HTTPS для обмена данными.
Удаление привязки HTTP в IIS не поддерживается, однако можно использовать брандмауэр Windows или другие технологии сетевого брандмауэра, чтобы блокировать обмен данными через порт 80.

## <a name="decommission-an-hgs-node"></a>Списание узла HGS

Чтобы списать узел HGS, сделайте следующее:

1. [Очистите конфигурацию HGS](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration).

   Это приведет к удалению узла из кластера и удалению службы аттестации и защиты ключей.
   Если это последний узел в кластере,-Force требуется, чтобы указать, что нужно удалить последний узел и уничтожить кластер в Active Directory.

   Если HGS развертывается в лесу бастиона (по умолчанию), это единственный шаг.
   При необходимости можно отсоединить компьютер от домена и удалить учетную запись gMSA из Active Directory.

2. Если HGS создала собственный домен, следует также [Удалить HGS](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration) , чтобы отменить присоединение к домену и понизить контроллер домена.
