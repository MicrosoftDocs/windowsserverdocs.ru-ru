---
title: Устранение неполадок системы доменных имен (DNS)
description: В этой статье описывается, как выполнять получение данных при возникновении проблем с DNS.
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: f56c3b7004392f06e0e0728e6e82851ae015640d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954070"
---
# <a name="troubleshooting-domain-name-system-dns-issues"></a>Устранение неполадок системы доменных имен (DNS)

Проблемы разрешения доменных имен могут быть разбиты на клиентские и серверные проблемы. Как правило, следует начать с устранения неполадок на стороне клиента, если не определить на этапе определения того, что проблема определенно возникает на стороне сервера.

- [Устранение неполадок DNS-клиентов](troubleshoot-dns-client.md)

- [Устранение неполадок DNS-серверов](troubleshoot-dns-server.md)

## <a name="data-collection"></a>Сбор данных

При возникновении проблемы рекомендуется одновременно выполнять получение данных как на стороне клиента, так и на сервере. Однако в зависимости от фактической проблемы можно запустить коллекцию в одном наборе данных на DNS-клиенте или на DNS-сервере.

Чтобы выполнить сбор данных диагностики сети Windows с затронутого клиента и его настроенного DNS-сервера, выполните следующие действия.

1. Запуск сбора данных о сети на клиенте и сервере:

   ```cmd
   netsh trace start capture=yes tracefile=c:\%computername%_nettrace.etl
   ```

2. Очистите кэш DNS на DNS-клиенте, выполнив следующую команду:

   ```cmd
   ipconfig /flushdns
   ```

3. Воспроизведите проблему.

4. Останавливает и сохраняет трассировки:

   ```cmd
   netsh trace stop
   ```

5. Сохраните Nettrace.cab файлы с каждого компьютера. Эти сведения будут полезны при обращении служба поддержки Майкрософт.