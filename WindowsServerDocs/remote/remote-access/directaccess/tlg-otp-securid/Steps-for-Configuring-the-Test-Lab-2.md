---
title: Действия по настройке лаборатории тестирования с проверкой подлинности OTP и RSA SecurID
description: 'Эта статья является частью руководства по тестовой лаборатории: демонстрация DirectAccess с проверкой подлинности OTP и RSA SecurID для Windows Server 2016.'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 0a40183c-afd1-43ca-b306-05745640a37d
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 21a4fe4de5029c009594a0e8dc01dc4570e9e557
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769682"
---
# <a name="steps-for-configuring-the-test-lab-with-otp-authentication-and-rsa-securid"></a>Действия по настройке лаборатории тестирования с проверкой подлинности OTP и RSA SecurID

>Область применения. Windows Server (Semi-Annual Channel), Windows Server 2016

Следующие шаги описывают настройку инфраструктуры удаленного доступа, настройку сервера удаленного доступа и клиента, а также проверку подключения DirectAccess из подсетей Хоменет и Интернета.

В этом руководстве по тестированию вы создадите удаленный доступ с помощью среды OTP, выполнив следующие действия:

-   [Шаг 1. Завершение настройки DirectAccess](assetId:///4dbf877f-02fb-439b-907a-f5b3f1d8afa6). Выполните все действия, описанные в [руководстве по тестовой лаборатории: демонстрация настройки отдельного сервера DirectAccess с использованием смешанных IPv4 и IPv6](https://go.microsoft.com/fwlink/p/?LinkId=237004).

-   [Шаг 2. Настройка APP1](assetId:///c1bb590f-91d4-4ed5-bceb-b0e36eabd4ff). Настройте APP1 с помощью шаблонов сертификатов OTP для использования в EDGE1.

-   [Шаг 3. Настройка DC1](assetId:///904a6edc-a771-45ed-9630-a34a680bb522). Проверьте имя участника-пользователя, определенное на компьютере DC1.

-   [Шаг 7. Установка и настройка RSA](assetId:///baa4c28c-add7-42e2-8afd-ccc7a559406a). Установите и настройте RSA, сервер RADIUS и OTP и настройте EDGE1 для OTP.

-   [Шаг 11. Проверка работоспособности OTP в EDGE1](assetId:///3b397a4a-8478-47f2-a932-9e8e048c14ba). Убедитесь, что на сервере удаленного доступа установлено состояние OTP.

-   [Шаг 8. Проверка подключения DirectAccess из подсети Хоменет](assetId:///ba1652a6-0692-4add-91ca-34a84956ba14). Протестируйте функции OTP DirectAccess из устройства NAT.

-   [Шаг 10. Проверка подключения DirectAccess из Интернета](assetId:///321149eb-5f23-4a0b-b8fb-1244540126e9). Проверьте возможность подключения клиента DirectAccess из Интернета.

-   [Шаг 12. Создание моментального снимка конфигурации](assetId:///8a51ed3c-9c32-402f-85d1-617ce46845b4). После завершения лаборатории тестирования сделайте снимок рабочего DirectAccess с конфигурацией OTP, чтобы можно было вернуться к нему позже для тестирования дополнительных сценариев.



