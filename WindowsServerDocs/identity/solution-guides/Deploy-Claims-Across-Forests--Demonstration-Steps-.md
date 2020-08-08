---
ms.assetid: 846c3680-b321-47da-8302-18472be42421
title: Развертывание утверждений между лесами (обучающий пример)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 828b7256854f9d2fd6d58567c773d4abc288cd0a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952876"
---
# <a name="deploy-claims-across-forests-demonstration-steps"></a>Развертывание утверждений между лесами (обучающий пример)

>Область применения. Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

В этом разделе рассматривается базовый сценарий, посвященный настройке преобразований утверждений между доверенными и доверенными лесами. Вы узнаете, как можно создать объекты политики преобразования утверждений и связать их с отношением доверия в доверяющем лесу и доверенном лесу. Затем вы проверите сценарий.

## <a name="scenario-overview"></a>Общие сведения о сценарии
Корпорация adatum предоставляет финансовые услуги компании Contoso, Ltd. Каждый квартал adatum бухгалтеры копируют свои электронные таблицы своей учетной записи в папку на файловом сервере, расположенном в Contoso, Ltd. Существует двустороннее доверие, настроенное с Contoso на adatum. Компания Contoso, Ltd. хочет защитить общую папку, чтобы только adatum сотрудники могли получить доступ к удаленной общей папке.

В этом сценарии:

1.  [Настройка предварительных требований и тестовой среды](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_1.1)

2.  [Настройка преобразования утверждений в доверенном лесу (adatum)](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_3)

3.  [Настройка преобразования утверждений в доверяющем лесу (Contoso)](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_4)

4.  [Проверка сценария](Deploy-Claims-Across-Forests--Demonstration-Steps-.md#BKMK_5)

## <a name="set-up-the-prerequisites-and-the-test-environment"></a><a name="BKMK_1.1"></a>Настройка предварительных требований и тестовой среды
Конфигурация теста включает в себя настройку двух лесов: Adatum Corporation и Contoso, Ltd, а также двустороннее доверие между Contoso и adatum. "adatum.com" — это доверенный лес, а "contoso.com" — доверяющий лес.

В сценарии преобразования утверждений показано преобразование утверждения в доверенном лесу в утверждение в доверяющем лесу. Для этого необходимо настроить новый лес с именем adatum.com и заполнить его тестовым пользователем со значением компании "adatum". Затем необходимо настроить двустороннее доверие между contoso.com и adatum.com.

> [!IMPORTANT]
> При настройке лесов Contoso и adatum необходимо убедиться, что корневые домены находятся на функциональном уровне домена Windows Server 2012 для работы преобразования "утверждения".

Для лаборатории необходимо настроить следующие значения. Эти процедуры подробно описаны в [приложении б: Настройка тестовой среды.](Appendix-B--Setting-Up-the-Test-Environment.md)

Чтобы настроить лабораторию для этого сценария, необходимо реализовать следующие процедуры:

1.  [Задание adatum в качестве доверенного леса для contoso](Appendix-B--Setting-Up-the-Test-Environment.md)

2.  [Создание типа утверждения "компания" в Contoso](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.8)

3.  [Включение свойства ресурса "компания" в Contoso](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.55)

4.  [Создание правила централизованного доступа](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.9)

5.  [Создание централизованной политики доступа](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.10)

6.  [Публикация новой политики с помощью групповой политики](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.11)

7.  [Создание папки Earnings на файловом сервере](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.12)

8.  [Настройка классификации и применение централизованной политики доступа к новой папке](Appendix-B--Setting-Up-the-Test-Environment.md#BKMK_2.13)

Для выполнения этого сценария используйте следующую информацию:

|Объекты|Сведения|
|-----------|-----------|
|Пользователи|Иван Low, contoso|
|Утверждения пользователей в adatum и contoso|Идентификатор: ad://ext/Company:ContosoAdatum,<p>Исходный атрибут: Company<p>Предлагаемые значения: contoso, adatum **важно** ! для типа утверждения "Company" в Contoso и adatum необходимо задать одинаковый идентификатор для работы преобразования "утверждения".|
|Централизованное правило доступа в Contoso|адатумемплойиакцессруле|
|Централизованная политика доступа в Contoso|Политика доступа только для adatum|
|Политики преобразования утверждений в adatum и contoso|Компания Деняллексцепт|
|Папка с файлами в Contoso|д:\еарнингс|

## <a name="set-up-claims-transformation-on-trusted-forest-adatum"></a><a name="BKMK_3"></a>Настройка преобразования утверждений в доверенном лесу (adatum)
На этом шаге вы создадите политику преобразования в adatum, чтобы запретить всем утверждениям, кроме компании, передавать в Contoso.

Модуль Active Directory для Windows PowerShell предоставляет аргумент **деняллексцепт** , который удаляет все, кроме указанных утверждений в политике преобразования.

Чтобы настроить преобразование утверждений, необходимо создать политику преобразования утверждений и связать ее между доверенным и доверяющим лесами.

### <a name="create-a-claims-transformation-policy-in-adatum"></a><a name="BKMK_2.2"></a>Создание политики преобразования утверждений в adatum

##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-claims-except-company"></a>Создание политики преобразования adatum для запрета всех утверждений, кроме "Company"

1. Войдите на контроллер домена, adatum.com от имени администратора с паролем <strong>pass@word1</strong> .

2. Откройте командную строку с повышенными привилегиями в Windows PowerShell и введите следующую команду:

   ```
   New-ADClaimTransformPolicy `
   -Description:"Claims transformation policy to deny all claims except Company"`
   -Name:"DenyAllClaimsExceptCompanyPolicy" `
   -DenyAllExcept:company `
   -Server:"adatum.com" `

   ```

### <a name="set-a-claims-transformation-link-on-adatums-trust-domain-object"></a><a name="BKMK_2.3"></a>Задание ссылки преобразования утверждений для объекта домена доверия adatum
На этом шаге вы примените созданную политику преобразования утверждений в объекте домена доверия adatum для contoso.

##### <a name="to-apply-the-claims-transformation-policy"></a>Применение политики преобразования утверждений

1. Войдите на контроллер домена, adatum.com от имени администратора с паролем <strong>pass@word1</strong> .

2. Откройте командную строку с повышенными привилегиями в Windows PowerShell и введите следующую команду:

   ```

     Set-ADClaimTransformLink `
   -Identity:"contoso.com" `
   -Policy:"DenyAllClaimsExceptCompanyPolicy" `
   '"TrustRole:Trusted `

   ```

## <a name="set-up-claims-transformation-in-the-trusting-forest-contoso"></a><a name="BKMK_4"></a>Настройка преобразования утверждений в доверяющем лесу (Contoso)
На этом шаге вы создадите политику преобразования утверждений в Contoso (доверяющем лесу), чтобы запретить все утверждения, кроме Company. Необходимо создать политику преобразования утверждений и связать ее с доверием леса.

### <a name="create-a-claims-transformation-policy-in-contoso"></a><a name="BKMK_4.1"></a>Создание политики преобразования утверждений в Contoso

##### <a name="to-create-a-transformation-policy-adatum-to-deny-all-except-company"></a>Создание политики преобразования adatum для запрета всех, кроме "Company"

1. Войдите на контроллер домена, contoso.com от имени администратора с паролем <strong>pass@word1</strong> .

2. Откройте командную строку с повышенными привилегиями в Windows PowerShell и введите следующую команду:

   ```
   New-ADClaimTransformPolicy `
   -Description:"Claims transformation policy to deny all claims except company" `
   -Name:"DenyAllClaimsExceptCompanyPolicy" `
   -DenyAllExcept:company `
   -Server:"contoso.com" `

   ```

### <a name="set-a-claims-transformation-link-on-contosos-trust-domain-object"></a><a name="BKMK_4.2"></a>Задание ссылки преобразования утверждений для объекта домена доверия Contoso
На этом шаге вы примените вновь созданную политику преобразования утверждений в объекте домена доверия contoso.com для adatum, чтобы разрешить передачу "компании" через contoso.com. Объект домена доверия называется adatum.com.

##### <a name="to-set-the-claims-transformation-policy"></a>Настройка политики преобразования утверждений

1. Войдите на контроллер домена, contoso.com от имени администратора с паролем <strong>pass@word1</strong> .

2. Откройте командную строку с повышенными привилегиями в Windows PowerShell и введите следующую команду:

   ```

     Set-ADClaimTransformLink
   -Identity:"adatum.com" `
   -Policy:"DenyAllClaimsExceptCompanyPolicy" `
   -TrustRole:Trusting `

   ```

## <a name="validate-the-scenario"></a><a name="BKMK_5"></a>Проверка сценария
На этом шаге вы пытаетесь получить доступ к папке Д:\ЕАРНИНГС, настроенной на файловом файле FILE1, чтобы убедиться, что у пользователя есть доступ к общей папке.

#### <a name="to-ensure-that-the-adatum-user-can-access-the-shared-folder"></a>Проверка того, что пользователь adatum может получить доступ к общей папке

1. Войдите на клиентский компьютер, CLIENT1 как Джефф с низкими правами с паролем <strong>pass@word1</strong> .

2. Перейдите к папке \\ \FILE1.contoso.com\Earnings.

3. Джефф должен иметь доступ к папке.

## <a name="additional-scenarios-for-claims-transformation-policies"></a>Дополнительные сценарии для политик преобразования утверждений
Ниже приведен список дополнительных типичных случаев преобразования утверждений.


|                                                 Сценарий                                                 |                                                                                                                                                                                                                                           Политика                                                                                                                                                                                                                                            |
|----------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                  Разрешить всем утверждениям, поступившим от adatum, проходить до Contoso adatum                  |                                                          Приведен <br />New-Адклаимтрансформполици\`<br /> -Description: "политика преобразования утверждений для разрешения всех утверждений"\`<br />-Name: "Алловаллклаимсполици"\`<br />-Алловалл\`<br />-Server:"Контосо. com"\`<br />Set-Адклаимтрансформлинк\`<br />-Identity:"адатум. com"\`<br />-Policy: "Алловаллклаимсполици"\`<br />-Трустроле: доверие\`<br />-Server:"Контосо. com"\`                                                          |
|                  Отказ от всех утверждений, поступающих от adatum, к Contoso adatum                   |                                                            Приведен <br />New-Адклаимтрансформполици\`<br />-Description: "политика преобразования утверждений для запрета всех утверждений"\`<br />-Name: "Деняллклаимсполици"\`<br /> -Денялл\`<br />-Server:"Контосо. com"\`<br />Set-Адклаимтрансформлинк\`<br />-Identity:"адатум. com"\`<br />-Policy: "Деняллклаимсполици"\`<br />-Трустроле: доверие\`<br />-Server:"Контосо. com"\`                                                             |
| Разрешите всем заявкам, поступающим от adatum, за исключением "компания" и "Отдел", чтобы пройти до Contoso adatum | Код <br />-New-Адклаимтрансформатионполици\`<br />-Description: "политика преобразования утверждений для разрешения всех утверждений, кроме Организации и отдела"\`<br /> -Name: "Алловаллклаимсексцепткомпанянддепартментполици"\`<br />-Алловаллексцепт: организация, отдел\`<br />-Server:"Контосо. com"\`<br />Set-Адклаимтрансформлинк\`<br /> -Identity:"адатум. com"\`<br />-Policy: "Алловаллклаимсексцепткомпанянддепартментполици"\`<br /> -Трустроле: доверие\`<br />-Server:"Контосо. com"\` |

## <a name="see-also"></a><a name="BKMK_Links"></a> См. также

-   Список всех командлетов Windows PowerShell, доступных для преобразования утверждений, см. в разделе [Справочник по командлетам powershell Active Directory](https://go.microsoft.com/fwlink/?LinkId=243150).

-   Дополнительные задачи, в том числе экспорт и импорт сведений о конфигурации DAC между двумя лесами, см. в [справочнике по PowerShell для динамического управления доступом](https://go.microsoft.com/fwlink/?LinkId=243150) .

-   [Развертывание утверждений в лесах](Deploy-Claims-Across-Forests.md)

-   [Язык правил преобразования утверждений](Claims-Transformation-Rules-Language.md)

-   [Динамический контроль доступа. Обзор сценария](Dynamic-Access-Control--Scenario-Overview.md)


