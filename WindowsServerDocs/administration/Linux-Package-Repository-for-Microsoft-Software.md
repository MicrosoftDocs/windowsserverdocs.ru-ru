---
title: Репозиторий программного обеспечения Linux для продуктов Майкрософт
description: В этом документе описывается, как использовать и устанавливать программные пакеты Linux для продуктов Майкрософт.
manager: szark
ms.topic: article
ms.assetid: b5387444-595f-4f38-abb7-163a70ea1895
author: szarkos
ms.author: szark
ms.date: 08/14/2020
ms.openlocfilehash: 421518ffceb2fb5cab0ed84e9299004084311924
ms.sourcegitcommit: b18effcba95c85d6e08e7d29808b576491a5352e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/15/2020
ms.locfileid: "88243186"
---
# <a name="linux-software-repository-for-microsoft-products"></a>Репозиторий программного обеспечения Linux для продуктов Майкрософт

## <a name="overview"></a>Overview

Корпорация Майкрософт создает и поддерживает различные программные продукты для систем Linux и делает их доступными через стандартные репозитории пакетов APT и YUM. В этом документе описывается, как настроить репозиторий в системе Linux, чтобы можно было установить или обновить программное обеспечение Microsoft Linux с помощью стандартных средств управления пакетами для дистрибутива.

Репозиторий программного обеспечения Microsoft Linux состоит из нескольких дочерних репозиториев:

 - произ. рабочий репозиторий рабочей области предназначен для пакетов, предназначенных для использования в рабочей среде. Эти пакеты коммерчески поддерживаются корпорацией Майкрософт в соответствии с условиями действующего соглашения о поддержке или программы, имеющейся в корпорации Майкрософт.

 - MSSQL-Server — эти репозитории содержат пакеты для Microsoft SQL Server на Linux — см. также [SQL Server на Linux](https://www.microsoft.com/sql-server/sql-server-vnext-including-Linux).

> [!NOTE]
> Пакеты в репозиториях программного обеспечения Linux подчиняются условиям лицензии, расположенным в пакетах. Прежде чем использовать пакет, ознакомьтесь с условиями лицензии. Установка и использование пакета означают, что вы принимаете эти условия. Если вы не согласны с условиями лицензии, не используйте пакет.

## <a name="configuring-the-repositories"></a>Настройка репозиториев

Репозитории можно настроить автоматически, установив пакет Linux, который относится к дистрибутиву и версии Linux. Пакет установит конфигурацию репозитория вместе с открытым ключом GPG, который используется такими инструментами, как APT/Yum/zypper, для проверки подписанных пакетов и метаданных репозитория.

### <a name="enterprise-linux-rhel-and-variants"></a>Enterprise Linux (RHEL и варианты)

 - Enterprise Linux 6 (EL6)<p>`sudo rpm -Uvh https://packages.microsoft.com/config/rhel/6/packages-microsoft-prod.rpm`

 - Enterprise Linux 7 (EL7)<p>`sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm`

 - Enterprise Linux 8 (EL8)<p>`sudo rpm -Uvh https://packages.microsoft.com/config/rhel/8/packages-microsoft-prod.rpm`

### <a name="suse"></a>SUSE

 - SUSE Linux Enterprise Server 12<p>`sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm`

 - SUSE Linux Enterprise Server 15<p>`sudo rpm -Uvh https://packages.microsoft.com/config/sles/15/packages-microsoft-prod.rpm`

### <a name="ubuntu"></a>Ubuntu

 - Ubuntu 16,04 (Xenial)<p>`curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -`<p>`sudo apt-add-repository https://packages.microsoft.com/ubuntu/16.04/prod`<p>`sudo apt-get update`

 - Ubuntu 18,04 (Бионик)<p>`curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -`<p>`sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod`<p>`sudo apt-get update`

 - Ubuntu 20,04 (Disco)<p>`curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -`<p>`sudo apt-add-repository https://packages.microsoft.com/ubuntu/20.04/prod`<p>`sudo apt-get update`

## <a name="manual-configuration"></a>Настроить вручную

Файлы конфигурации репозитория доступны в [Packages.Microsoft.com/config](https://packages.microsoft.com/config/). Имя и расположение этих файлов можно найти с помощью следующего соглашения об именовании URI:

`https://packages.microsoft.com/config/<Distribution>/<Version>/prod.(repo|list)`

### <a name="package-and-repository-signing-key"></a>Ключ подписывания пакета и репозитория

- Открытый ключ Microsoft GPG можно скачать здесь: [https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc)
- Идентификатор открытого ключа: Майкрософт (подписывание выпуска) <gpgsecurity@microsoft.com>
- Отпечаток открытого ключа: `BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF`

### <a name="examples"></a>Примеры

 - RHEL или CentOS 7

```
# Install repository configuration
curl -sSL https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft-prod.repo

# Install Microsoft's GPG public key
curl -sSL https://packages.microsoft.com/keys/microsoft.asc > ./microsoft.asc
sudo rpm --import ./microsoft.asc
```

 - Ubuntu 20.04

```
# Install repository configuration
curl -sSL https://packages.microsoft.com/config/ubuntu/20.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft-prod.list

# Install Microsoft GPG public key
curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Update package index files
sudo apt-get update
```
