---
title: Сценарий делегирования удостоверений с AD FS
description: В этом сценарии описывается приложение, которому требуется доступ к внутренним ресурсам, для которых требуется выполнение проверок управления доступом в цепочке делегирования удостоверений.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/22/2018
ms.topic: article
ms.openlocfilehash: 9d0cc816ce27130867988f51a097456bb37faef0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964951"
---
# <a name="identity-delegation-scenario-with-ad-fs"></a>Сценарий делегирования удостоверений с AD FS


[Начиная с .NET Framework 4,5, Windows Identity Foundation (WIF) полностью интегрирована в .NET Framework. Версия WIF, описанная в этом разделе, WIF 3,5, является устаревшей и должна использоваться только при разработке на .NET Framework 3,5 с пакетом обновления 1 (SP1) или .NET Framework 4. Дополнительные сведения о WIF в .NET Framework 4,5, также известном как WIF 4,5, см. в документации по Windows Identity Foundation в руководстве по разработке .NET Framework 4,5.]

В этом сценарии описывается приложение, которому требуется доступ к внутренним ресурсам, для которых требуется выполнение проверок управления доступом в цепочке делегирования удостоверений. Простая цепочка делегирования удостоверений обычно состоит из информации об исходном вызывающем объекте и идентификации непосредственных вызывающих объектов.

Теперь, когда модель делегирования Kerberos на платформе Windows уже сегодня, серверные ресурсы имеют доступ только к идентификации непосредственного вызывающего объекта, а не от первоначального вызывающего. Эта модель обычно называется моделью доверенной подсистемы. WIF поддерживает идентификацию начального вызывающего объекта, а также непосредственный вызывающий объект в цепочке делегирования с помощью свойства субъекта.

На следующей схеме показан типичный сценарий делегирования удостоверений, в котором сотрудник Fabrikam получает доступ к ресурсам, предоставляемым приложением Contoso.com.

![Идентификация](media/ad-fs-identity-delegation/id1.png)

Вымышленные пользователи, участвующие в этом сценарии:

- Федор: сотрудник Fabrikam, желающий получить доступ к ресурсам Contoso.
- Даниэль: разработчик приложения Contoso, который реализует необходимые изменения в приложении.
- Адам — администратор Contoso.

Ниже перечислены компоненты, задействованные в этом сценарии.

- web1: веб-приложение со ссылками на серверные ресурсы, для которых требуется делегированное удостоверение начального вызывающего объекта. Это приложение создано с помощью ASP.NET.
- Веб-служба, обращающаяся к SQL Server, для которой требуется делегированное удостоверение начального вызывающего объекта, а также непосредственно вызывающий объект. Эта служба создается с помощью WCF.
- sts1: STS, который находится в роли поставщика утверждений, и выдает утверждения, ожидаемые приложением (web1). Он установил отношение доверия с Fabrikam.com, а также с приложением.
- sts2: STS, который входит в роль поставщика удостоверений для Fabrikam.com и предоставляет конечную точку, которую сотрудник Fabrikam использует для проверки подлинности. Он установил отношение доверия с Contoso.com, чтобы сотрудники Fabrikam могли получать доступ к ресурсам в Contoso.com.

>[!NOTE]
>Термин "ActAs token", который часто используется в этом сценарии, относится к маркеру, выданному STS и содержащему удостоверение пользователя. Свойство Actor содержит удостоверение STS.

Как показано на предыдущей схеме, последовательность в этом сценарии:


1. Приложение Contoso настроено для получения токена ActAs, который содержит удостоверение сотрудника Fabrikam и идентификатор непосредственных вызывающих объектов в свойстве субъекта. Даниэль реализовала эти изменения в приложении.
2. Приложение Contoso настроено на передачу токена ActAs в серверную службу. Даниэль реализовала эти изменения в приложении.
3. Веб-служба Contoso настроена для проверки токена ActAs путем вызова sts1. Адам включил sts1 для обработки запросов на делегирование.
4. Пользователь Fabrikam имеет доступ к приложению Contoso и получает доступ к ресурсам серверной части.

## <a name="set-up-the-identity-provider-ip"></a>Настройка поставщика удостоверений (IP)

Для администратора Fabrikam.com доступны три варианта, Федор:


1. Приобретите и установите продукт STS, например &reg; службы Active Directory Federation Services (AD FS).
2. Подпишитесь на облачный продукт STS, например LiveID STS.
3. Создайте настраиваемую STS с помощью WIF.

В этом образце сценария предполагается, что Федор выбирает параметр1 и устанавливает AD FS как IP-STS. Он также настраивает конечную точку с именем \виндовсаус для проверки подлинности пользователей. Ссылаясь на AD FSную документацию по продукту и обращаясь к Адаму, ИТ администратора Contoso, Федор устанавливает доверие с доменом Contoso.com.

## <a name="set-up-the-claims-provider"></a>Настройка поставщика утверждений

Параметры, доступные для Contoso.com Administrator, ADAM, как описано ранее для поставщика удостоверений. В этом образце сценария предполагается, что Алексей выбирает вариант 1 и устанавливает AD FS 2,0 в качестве RP-STS.

## <a name="set-up-trust-with-the-ip-and-application"></a>Настройка отношений доверия с IP-адресом и приложением

При обращении к документации по AD FS ADAM устанавливает доверие между Fabrikam.com и приложением.

## <a name="set-up-delegation"></a>Настройка делегирования

AD FS обеспечивает обработку делегирования. При ссылке на документацию по AD FS Адам включает обработку маркеров ActAs.

## <a name="application-specific-changes"></a>Изменения, относящиеся к приложению

Чтобы добавить поддержку делегирования удостоверений в существующее приложение, необходимо внести следующие изменения. Даниэль использует WIF для внесения этих изменений.


- Кэшировать маркер начальной загрузки, полученный от sts1, Web1.
- Используйте Креатечаннелактингас с выданным токеном для создания канала к внутренней веб-службе.
- Вызовите метод серверной службы.

## <a name="cache-the-bootstrap-token"></a>Кэширование токена начальной загрузки

Маркер начальной загрузки — это начальный маркер, выданный службой STS, и приложение извлекает из него утверждения. В этом примере сценария этот маркер выдается sts1 для пользователя Федор, а приложение кэширует его. В следующем примере кода показано, как получить маркер начальной загрузки в приложении ASP.NET:

```
// Get the Bootstrap Token
SecurityToken bootstrapToken = null;

IClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as IClaimsPrincipal;
if ( claimsPrincipal != null )
{
    IClaimsIdentity claimsIdentity = (IClaimsIdentity)claimsPrincipal.Identity;
    bootstrapToken = claimsIdentity.BootstrapToken;
}
```
WIF предоставляет метод [креатечаннелактингас](/previous-versions/windows-identity-foundation/ee733863(v=msdn.10)), который создает канал указанного типа, который дополняет запросы на выдачу маркера с указанным маркером безопасности в качестве элемента ActAs. Вы можете передать маркер начальной загрузки этому методу, а затем вызвать необходимый метод службы для возвращенного канала. В этом образце сценария удостоверение Федор имеет свойство [Actor](/previous-versions/windows-identity-foundation/ee766706(v=msdn.10)) со значением web1's Identity.

В следующем фрагменте кода показано, как вызвать веб-службу с помощью [креатечаннелактингас](/previous-versions/windows-identity-foundation/ee733863(v=msdn.10)) , а затем вызвать один из методов службы компутереспонсе на возвращенном канале:

```
// Get the channel factory to the backend service from the application state
ChannelFactory<IService2Channel> factory = (ChannelFactory<IService2Channel>)Application[Global.CachedChannelFactory];

// Create and setup channel to talk to the backend service
IService2Channel channel;
lock (factory)
{
// Setup the ActAs to point to the caller's token so that we perform a
// delegated call to the backend service
// on behalf of the original caller.
    channel = factory.CreateChannelActingAs<IService2Channel>(callerToken);
}

string retval = null;

// Call the backend service and handle the possible exceptions
try
{
    retval = channel.ComputeResponse(value);
    channel.Close();
} catch (Exception exception)
{
    StringBuilder sb = new StringBuilder();
    sb.AppendLine("An unexpected exception occurred.");
    sb.AppendLine(exception.StackTrace);
    channel.Abort();
    retval = sb.ToString();
}

```
## <a name="web-service-specific-changes"></a>Изменения, относящиеся к веб-службе

Так как веб-служба построена с помощью WCF и включена для WIF, после настройки привязки с помощью Иссуедсекурититокенпараметерс с правильным адресом издателя проверка ActAs автоматически обрабатывается WIF.

Веб-служба предоставляет конкретные методы, необходимые для приложения. Для службы не требуются конкретные изменения кода. В следующем примере кода показана конфигурация веб-службы с помощью Иссуедсекурититокенпараметерс:

```
// Configure the issued token parameters with the correct settings
IssuedSecurityTokenParameters itp = new IssuedSecurityTokenParameters( "http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" );
itp.IssuerMetadataAddress = new EndpointAddress( "http://localhost:6000/STS/mex" );
itp.IssuerAddress = new EndpointAddress( "http://localhost:6000/STS" );

// Create the security binding element
SecurityBindingElement sbe = SecurityBindingElement.CreateIssuedTokenForCertificateBindingElement( itp );
sbe.MessageSecurityVersion = MessageSecurityVersion.WSSecurity11WSTrust13WSSecureConversation13WSSecurityPolicy12BasicSecurityProfile10;

// Create the HTTP transport binding element
HttpTransportBindingElement httpBE = new HttpTransportBindingElement();

// Create the custom binding using the prepared binding elements
CustomBinding binding = new CustomBinding( sbe, httpBE );

using ( ServiceHost host = new ServiceHost( typeof( Service2 ), new Uri( "http://localhost:6002/Service2" ) ) )
{
    host.AddServiceEndpoint( typeof( IService2 ), binding, "" );
    host.Credentials.ServiceCertificate.SetCertificate( "CN=localhost", StoreLocation.LocalMachine, StoreName.My );

// Enable metadata generation via HTTP GET
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
    smb.HttpGetEnabled = true;
    host.Description.Behaviors.Add( smb );
    host.AddServiceEndpoint( typeof( IMetadataExchange ), MetadataExchangeBindings.CreateMexHttpBinding(), "mex" );

// Configure the service host to use WIF
    ServiceConfiguration configuration = new ServiceConfiguration();
    configuration.IssuerNameRegistry = new TrustedIssuerNameRegistry();

    FederatedServiceCredentials.ConfigureServiceHost( host, configuration );

    host.Open();

    Console.WriteLine( "Service2 started, press ENTER to stop ..." );
    Console.ReadLine();

    host.Close();
}
```

## <a name="next-steps"></a>Next Steps
[Разработка AD FS](../../ad-fs/AD-FS-Development.md)
