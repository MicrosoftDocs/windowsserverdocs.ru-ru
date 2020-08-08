---
title: Перенос служб ролей для служб федерации Active Directory в Windows Server 2012
description: Содержит инструкции по переносу службы AD FS в Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: abbd51daea374eb4684f5416bed45fb0aaf315d4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938214"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>Перенос служб ролей для служб федерации Active Directory в Windows Server 2012

Ниже приведены инструкции по миграции следующих служб ролей в службы федерации Active Directory (AD FS) (AD FS) в Windows Server 2012.

-   агент на базе токенов Windows AD FS 1.1 и агент с поддержкой утверждений AD FS 1.1, установленный с Windows Server 2008 или Windows Server 2008 R2;

-   сервера федерации AD FS 2.0 и прокси-сервера федерации AD FS 2.0, установленные в Windows Server 2008 или Windows Server 2008 R2,

## <a name="supported-migration-scenarios"></a>Поддерживаемые сценарии миграции
 Инструкции по миграции содержат следующие задачи.

- экспорт данных конфигурации AD FS 2.0 с сервера, работающего под управлением Windows Server 2008 или Windows Server 2008 R2;

- Выполнение обновления операционной системы этого сервера на месте с Windows Server 2008 или Windows Server 2008 R2 до Windows Server 2012.

- Повторное создание исходной конфигурации AD FS и восстановление оставшихся параметров службы AD FS на этом сервере, на котором теперь выполняется роль AD FS Server, установленная вместе с Windows Server 2012.

  Данное руководство не содержит инструкций по переносу сервера, на котором выполняются несколько ролей. Если сервер выполняет несколько ролей, рекомендуется разработать специальную процедуру миграции для данной серверной среды c использованием информации из других руководств по переносу ролей. Руководства по миграции для дополнительных ролей можно найти на [портале по миграции Windows Server](https://go.microsoft.com/fwlink/?LinkId=247608).

## <a name="supported-operating-systems"></a>Поддерживаемые операционные системы
 **Операционная система целевого сервера:**


- Windows Server 2012 или Windows Server 2008 R2 (параметры Server Core и полная установка)

  **Процессор целевого сервера:**


- 64-разрядный (x64)

|Процессор исходного сервера|Операционная система исходного сервера|
|-----|-----|
|32-разрядный (x86) или 64-разрядный (x64)|Windows Server 2003 с пакетом обновления 2 (SP2)|
|32-разрядный (x86) или 64-разрядный (x64)|Windows Server 2003 R2|
|32-разрядный (x86) или 64-разрядный (x64)|Windows Server 2008, оба варианта установки: Full и Server Core|
|64-разрядный (x64)|Windows Server 2008 R2|
|64-разрядный (x64)|Вариант установки основных серверных компонентов Windows Server 2008 R2|
|64-разрядный (x64)|Параметры Server Core и полная установка Windows Server 2012|

> [!NOTE]
> - Версии операционных систем, представленные в предыдущей таблице, являются самыми ранними поддерживаемыми сочетаниями ОС и пакетов обновления.
>   -   В качестве исходных или конечных серверов поддерживаются следующие выпуски ОС Windows Server: Foundation, Standard, Enterprise и Datacenter.
>   -   Также поддерживается миграция между физическими и виртуальными операционными системами.

### <a name="supported-ad-fs-role-services-and-features"></a>Поддерживаемые службы ролей и компоненты AD FS
 В следующей таблице представлены сценарии переноса служб ролей AD FS и их соответствующие параметры, описанные в данном руководстве.

|Исходный тип|Установка AD FS с Windows Server 2012|
|----------|-----|
|сервера федерации AD FS 1.0, установленного с Windows Server 2003 R2,|миграция не поддерживается|
|прокси-сервера федерации AD FS 1.0, установленного с Windows Server 2003 R2|миграция не поддерживается|
|агента на базе токенов Windows AD FS 1.0, установленного с Windows Server 2003 R2|миграция не поддерживается|
|агента с поддержкой утверждений AD FS 1.0, установленного с Windows Server 2003 R2|миграция не поддерживается|
|сервера федерации AD FS 1.1, установленного с Windows Server 2008 или Windows Server 2008 R2|миграция не поддерживается|
|прокси-сервера федерации AD FS 1.1, установленного с Windows Server 2008 или Windows Server 2008 R2|миграция не поддерживается|
|агента на базе токенов Windows AD FS 1.1, установленного с Windows Server 2008 или Windows Server 2008 R2|Миграция на одном и том же сервере поддерживается, однако перенесенный агент на базе токенов Windows AD FS Windows будет функционировать только в том случае, если служба федерации AD FS 1.1 установлена с Windows Server 2008 или Windows Server 2008 R2. Дополнительные сведения можно найти в разделе<p> [Перенос веб-агентов AD FS 1.1](migrate-the-ad-fs-web-agent.md)<p> [Взаимодействие с AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|
|агента с поддержкой утверждений AD FS 1.1, установленного с Windows Server 2008 или Windows Server 2008 R2|Поддерживается миграция на том же сервере. Перенесенный веб-агент с поддержкой утверждений AD FS 1.1 будет функционировать со следующими системами:<p> службой федерации AD FS 1.1, установленной с Windows Server 2008 или Windows Server 2008 R2<p> службой федерации AD FS 2.0, установленной с Windows Server 2008 или Windows Server 2008 R2<p> AD FS Служба федерации, установленная с Windows Server 2012<p> Дополнительные сведения можно найти в разделе<p> [Перенос веб-агентов AD FS 1.1](migrate-the-ad-fs-web-agent.md)<p> [Взаимодействие с AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|
|сервера федерации AD FS 2.0, установленного в Windows Server 2008 или Windows Server 2008 R2|Поддерживается миграция на том же сервере. Дополнительные сведения можно найти в разделе<p> [Подготовка к переносу сервера федерации AD FS 2.0](prepare-to-migrate-ad-fs-fed-server.md)<p> [Перенос сервера федерации AD FS 2.0](migrate-the-ad-fs-fed-server.md)|
|Прокси-сервера федерации AD FS 2.0, установленного с Windows Server 2008 или Windows Server 2008 R2|Поддерживается миграция на том же сервере.  Дополнительные сведения см. в разделах:<p> [Подготовка к переносу прокси-сервера федерации AD FS 2.0](prepare-to-migrate-ad-fs-fed-proxy.md)<p> [Перенос прокси-сервера федерации AD FS 2.0](migrate-the-ad-fs-2-fed-server-proxy.md)|

## <a name="see-also"></a>См. также:
 [Подготовка к переносу сервера федерации AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) [Подготовка к переносу AD FS 2,0 прокси-](prepare-to-migrate-ad-fs-fed-proxy.md) сервер федерации миграция [сервера AD FS 2,0 сервер федерации](migrate-the-ad-fs-fed-server.md) миграция [AD FS 2,0 прокси-сервер](migrate-the-ad-fs-2-fed-server-proxy.md) [AD FS 1,1](migrate-the-ad-fs-web-agent.md)