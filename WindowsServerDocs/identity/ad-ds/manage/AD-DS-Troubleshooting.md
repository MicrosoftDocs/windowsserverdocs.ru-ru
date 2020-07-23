---
ms.assetid: fd3bc84a-48eb-4f00-9dc2-846bf2c2668b
title: Диагностика доменных служб Active Directory
description: Обзор раздела "Устранение неполадок" для AD DS
ms.author: joflore
author: MicrosoftGuyJFlo
manager: dcscontentpm
ms.date: 11/22/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 0cd49e4eee2d68209fa016547cdd2d0626128204
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961296"
---
# <a name="ad-ds-troubleshooting"></a>Диагностика доменных служб Active Directory

>Область применения: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

В этом разделе содержатся рекомендации по устранению неполадок и процедуры диагностики и устранения проблем, которые могут возникнуть во время репликации Active Directory. Она посвящена тому, как реагировать на записи в журнале событий службы каталогов и как интерпретировать сообщения, которые такие средства, как Repadmin.exe и Dcdiag.exe, могут сообщать о них.

Repadmin.exe и Dcdiag.exe доступны на всех контроллерах домена под управлением Windows Server 2012 R2 или более поздних версий. Дополнительные сведения об использовании этих средств для устранения неполадок см. в следующих статьях.

- [Настройка компьютера для устранения неполадок Active Directory](../manage/troubleshoot/Configuring-a-Computer-for-Troubleshooting.md)
- [Устранение неполадок с репликацией Active Directory](../manage/troubleshoot/Troubleshooting-Active-Directory-Replication-Problems.md)

Еще одна полезная технология — трассировка событий Windows (ETW). ETW можно использовать для устранения неполадок подключений LDAP между контроллерами домена. Дополнительные сведения см. [в разделе Использование ETW для устранения неполадок подключений LDAP](../manage/troubleshoot/troubleshoot-ldap-using-etw.md).

Средства удаленного администрирования сервера (RSAT) можно также установить на рядовом сервере под Windows 10. Дополнительные сведения об установке RSAT см. в разделе [средства удаленного администрирования сервера](../../../remote/remote-server-administration-tools.md).
