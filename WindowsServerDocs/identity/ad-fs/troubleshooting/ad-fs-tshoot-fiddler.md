---
title: Устранение неполадок AD FS — Fiddler
description: В этом документе описывается, что такое Fiddler и как установить и настроить Fiddler для устранения неполадок, связанных с утверждениями AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/02/2018
ms.topic: article
ms.openlocfilehash: e631d9b1dd93b9f3eb3d224fa5e2007e3661e21c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972031"
---
# <a name="ad-fs-troubleshooting---fiddler"></a>Устранение неполадок AD FS — Fiddler
Fiddler — это средство, которое можно использовать для записи веб-трафика HTTP/HTTPS.  Это средство можно использовать для устранения неполадок в процессе выдачи заявки.  Просматривая трафик, можно получить более полное представление о том, где происходит прерывание взаимодействия.  В этом документе описано, как установить и настроить Fiddler для сбора трафика AD FS.  Пример трассировки Fiddler с помощью WS-Federation см. в [статье AD FS устранение неполадок — Fiddler-WS-Federation](ad-fs-tshoot-fiddler-ws-fed.md) .

## <a name="download-and-install-fiddler"></a>Скачивание и установка Fiddler
Вы можете скачать Fiddler [здесь](https://www.telerik.com/download/fiddler).  После загрузки выполните его установку.

## <a name="configure-fiddler-to-capture-ad-fs-traffic"></a>Настройка Fiddler для записи трафика AD FS
Чтобы захватить AD FS трафик, необходимо настроить Fiddler для расшифровки трафика SSL.

### <a name="configure-the-fiddler-ssl-certificate"></a>Настройка SSL-сертификата Fiddler
 Используйте следующую процедуру, чтобы настроить Fiddler для расшифровки трафика SSL.

1.  Открыть Fiddler
2.  В верхней части окна " **Сервис**" выберите **Параметры Fiddler**.
3.  Перейдите на вкладку HTTPS.
4.  Установите флажок **расшифровать HTTPS-трафик** и выберите в раскрывающемся списке **только браузеры** .
5.  Установите флажок **игнорировать ошибки сертификата сервера**.
6.  Нажмите кнопку **ОК**.

![Fiddler](media/ad-fs-tshoot-fiddler/fiddler1.png)

## <a name="next-steps"></a>Next Steps

- [Устранение неполадок в AD FS](ad-fs-tshoot-overview.md)