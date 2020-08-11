---
title: Изменения сервера Nano Server в Semi-Annual Channel для Windows Server
description: В новой модели обслуживания Windows Server сервер Nano Server представляет собой операционную систему контейнера с определенными измененными функциями.
ms.mktglfcycl: manage
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 05/21/2019
ms.topic: get-started-article
ms.assetid: a270334d-42a7-46ff-8eed-d8656a276544
ms.openlocfilehash: c1b25402a209bf460c130f4fd76928f95dc7c0a7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87967921"
---
# <a name="changes-to-nano-server-in-windows-server-semi-annual-channel"></a>Изменения сервера Nano Server в Semi-Annual Channel для Windows Server

>Область применения. Windows Server, Semi-Annual Channel

Если вы уже используете сервер Nano Server, модель обслуживания [Semi-Annual Channel для Windows Server](../get-started-19/servicing-channels-19.md) вам должна быть знакома, так как ранее его обслуживание выполнялось в рамках модели Current Branch for Business (CBB). Semi-Annual Channel для Windows Server — это просто новое название все той же модели. В этой модели обновления компонентов сервера Nano Server выходят два-три раза в год.

Но, начиная с Windows Server версии 1803, сервер Nano Server будет доступен только в качестве **базового образа ОС для контейнера**. Его необходимо запускать как контейнер в узле контейнера, например, как установку Windows Server Core. Запуск контейнера на основе сервера Nano Server в этом выпуске отличается от его запуска в более ранних выпусках следующим образом:

- Сервер Nano Server был оптимизирован для приложений .NET Core.
- Сервер Nano Server имеет меньший размер, чем версия сервера Windows Server 2016.
- PowerShell Core, .NET Core и WMI больше не входят в состав сервера по умолчанию, но вы можете добавить в него пакеты контейнера [.NET Core](https://hub.docker.com/r/microsoft/dotnet/) и [PowerShell Core](https://hub.docker.com/r/microsoft/powershell/) при создании контейнера.
- Обслуживающий стек больше не входит в состав сервера Nano Server. Корпорация Майкрософт публикует обновленный контейнер Nano в Docker Hub, а вы выполняете его повторное развертывание.
- Устранение неполадок с новым контейнером Nano выполняется с помощью Docker.
- Контейнеры Nano теперь можно запускать в среде IoT Базовая.

## <a name="related-topics"></a>Связанные темы

- [Документация по контейнерам Windows](https://aka.ms/windowscontainers)
- [Обзор Semi-Annual Channel для Windows Server](../get-started-19/servicing-channels-19.md)
