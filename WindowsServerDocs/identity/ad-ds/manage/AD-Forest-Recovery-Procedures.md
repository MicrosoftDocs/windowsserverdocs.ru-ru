---
title: Восстановление леса AD — процедуры
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 47a471fb-3b0b-4aa8-8525-1c92d0d51e93
ms.openlocfilehash: c59990486da26847884aec3052818bce1ebe450d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969861"
---
# <a name="ad-forest-recovery---procedures"></a>Восстановление леса AD — процедуры

>Область применения: Windows Server 2016, Windows Server 2012 и 2012 R2, Windows Server 2008 и 2008 R2

Этот раздел содержит процедуры, связанные с процессом восстановления леса. Процедуры применимы к Windows Server 2016, 2012 R2, 2012 и также применимы к Windows Server 2008 R2 и 2008 с некоторыми небольшими исключениями.

Процедуры, которые включают в себя различные действия для Windows Server 2003, находятся в статье [восстановление леса с контроллерами домена Windows Server 2003](AD-Forest-Recovery-Windows-Server-2003.md).

Ниже приведен список процедур, используемых при резервном копировании и восстановлении контроллеров домена и Active Directory.

- [Резервное копирование полного сервера](AD-Forest-Recovery-Backing-up-a-Full-Server.md)
- [Резервное копирование данных состояния системы](AD-Forest-Recovery-Backing-up-System-State.md)
- [Выполнение полного восстановления сервера](AD-Forest-Recovery-Perform-a-Full-Recovery.md)
- [Выполнение полномочной синхронизации SYSVOL, реплицированной с помощью DFSR](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)
- [Выполнение неполномочного восстановления служб домен Active Directory](AD-Forest-Recovery-Nonauthoritative-Restore.md)

В этих шагах объясняется, как выполнить полномочное восстановление SYSVOL в то же время.

- [Настройка службы DNS-сервера](AD-Forest-Recovery-Configure-DNS.md)
- [Удаление глобального каталога](AD-Forest-Recovery-Remove-GC.md)
- [Повышение значения доступных пулов RID](AD-Forest-Recovery-Raise-RID-Pool.md)
- [Идет недействительность текущего пула RID](AD-Forest-Recovery-Invaildate-RID-Pool.md)
- [Присвоение роли хозяина операций](AD-Forest-Recovery-Seizing-Operations-Master-Role.md)
- [Очистка после восстановления](AD-Forest-Recovery-Cleanup.md)
- [Очистка метаданных удаленных контроллеров домена с возможностью записи](AD-Forest-Recovery-Cleaning-Metadata.md)
- [Сброс пароля учетной записи компьютера контроллера домена](AD-Forest-Recovery-Reset-Computer-Account-DC.md)
- [Сброс пароля KRBTGT](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)
- [Сброс пароля доверия с одной стороны доверия](AD-Forest-Recovery-Reset-Trust.md)
- [Добавление глобального каталога](AD-Forest-Recovery-Add-GC.md)
- [Ресурсы для проверки работы репликации](AD-Forest-Recovery-Verify-Replication.md)

## <a name="next-steps"></a>Next Steps

- [Восстановление леса AD — необходимые условия](AD-Forest-Recovery-Prerequisties.md)
- [Восстановление леса AD — Девисинг план восстановления пользовательского леса](AD-Forest-Recovery-Devising-a-Plan.md)
- [Восстановление леса AD. обнаружение проблемы](AD-Forest-Recovery-Identify-the-Problem.md)
- [Восстановление леса AD. Определение способа восстановления](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [Восстановление леса AD — выполнение начального восстановления](AD-Forest-Recovery-Perform-initial-recovery.md)
- [Восстановление леса AD — процедуры](AD-Forest-Recovery-Procedures.md)
- [Восстановление леса AD — часто задаваемые вопросы](AD-Forest-Recovery-FAQ.md)
- [Восстановление леса Active Directory. Восстановление одного домена в лесу с несколькими доменами](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)
- [Восстановление леса Active Directory — восстановление леса с контроллерами домена Windows Server 2003](AD-Forest-Recovery-Windows-Server-2003.md)
