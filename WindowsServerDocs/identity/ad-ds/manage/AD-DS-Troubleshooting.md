---
ms.assetid: fd3bc84a-48eb-4f00-9dc2-846bf2c2668b
title: Диагностика доменных служб Active Directory
description: Обзор раздела "Устранение неполадок" для AD DS
ms.author: daveba
author: iainfoulds
manager: dcscontentpm
ms.date: 11/22/2019
ms.topic: article
ms.openlocfilehash: 923b2442d68590821dfdfccee15f732c47829f3a
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93068116"
---
# <a name="ad-ds-troubleshooting"></a>Диагностика доменных служб Active Directory

>Область применения: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

В этом разделе содержатся рекомендации по устранению неполадок и процедуры диагностики и устранения проблем, которые могут возникнуть во время репликации Active Directory. Она посвящена тому, как реагировать на записи в журнале событий службы каталогов и как интерпретировать сообщения, которые такие средства, как Repadmin.exe и Dcdiag.exe, могут сообщать о них.

Repadmin.exe и Dcdiag.exe доступны на всех контроллерах домена под управлением Windows Server 2012 R2 или более поздних версий. Дополнительные сведения об использовании этих средств для устранения неполадок см. в следующих статьях.

- [Настройка компьютера для устранения неполадок Active Directory](../manage/troubleshoot/Configuring-a-Computer-for-Troubleshooting.md)
- [Устранение неполадок с репликацией Active Directory](../manage/troubleshoot/Troubleshooting-Active-Directory-Replication-Problems.md)

Еще одна полезная технология — трассировка событий Windows (ETW). ETW можно использовать для устранения неполадок подключений LDAP между контроллерами домена. Дополнительные сведения см. [в разделе Использование ETW для устранения неполадок подключений LDAP](../manage/troubleshoot/troubleshoot-ldap-using-etw.md).

Средства удаленного администрирования сервера (RSAT) можно также установить на рядовом сервере под Windows 10. Дополнительные сведения об установке RSAT см. в разделе [средства удаленного администрирования сервера](../../../remote/remote-server-administration-tools.md).
