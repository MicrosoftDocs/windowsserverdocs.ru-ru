---
title: Добавление имен доменов третьего уровня
description: Описание использования Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: e5b4a362-1881-4024-ae4e-cc3b05e50103
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: dd68308646eba5fba2f79593cba82de467c1888b
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626360"
---
# <a name="add-third-level-domain-names"></a>Добавление имен доменов третьего уровня

>Область применения: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

В мастере настройки доменных имен можно предоставить пользователям возможность запрашивать имена доменов третьего уровня. Для этого необходимо создать и установить сборку кода, которая используется диспетчером доменов операционной системы.

## <a name="create-a-provider-of-third-level-domain-names"></a>Создание поставщика имен доменов третьего уровня
 Чтобы сделать доступными имена доменов третьего уровня, можно создать и установить сборку кода, которая предоставляет мастеру имена доменов. Для этого необходимо выполнить следующие задачи.

-   [Добавление в сборку реализации интерфейса IDomainSignupProvider](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup)

-   [Добавление в сборку реализации интерфейса IDomainMaintenanceProvider](Add-Third-Level-Domain-Names.md#BKMK_DomainMaintenance)

-   [Поставьте на сборке подпись Authenticode](Add-Third-Level-Domain-Names.md#BKMK_SignAssembly)

-   [Установка сборки на эталонном компьютере](Add-Third-Level-Domain-Names.md#BKMK_InstallAssembly)

-   [Перезапуск службы управления доменными именами Windows Server](Add-Third-Level-Domain-Names.md#BKMK_RestartService)

###  <a name="add-an-implementation-of-the-idomainsignupprovider-interface-to-the-assembly"></a><a name="BKMK_DomainSignup"></a> Добавление в сборку реализации интерфейса Идомаинсигнуппровидер
 Интерфейс IDomainSignupProvider используется для обеспечения доступности доменов для мастера.

##### <a name="to-add-the-idomainsignupprovider-code-to-the-assembly"></a>Добавление в сборку кода интерфейса IDomainSignupProvider

1.  Откройте Visual Studio 2008 с правами администратора, щелкнув эту программу правой кнопкой мыши в меню **Пуск** и выбрав команду **Запуск от имени администратора**.

2.  В меню **Файл** выберите команду **Создать** и щелкните пункт **Проект**.

3.  В диалоговом окне **Новый проект** последовательно щелкните **Visual C#** и **Библиотека классов**, введите имя решения и нажмите кнопку **ОК**.

4.  Присвойте файлу Class1.cs другое имя, например MyDomainNameProvider.cs.

5.  Добавьте ссылки на файлы Wssg.Web.DomainManagerObjectModel.dll, CertManaged.dll, WssgCertMgmt.dll и WssgCommon.dll.

6.  Добавьте следующие инструкции using.

    ```c#

    using System.Collections.ObjectModel;
    using System.Net;
    using System.Net.Sockets;
    using Microsoft.WindowsServerSolutions.Certificates;
    using Microsoft.WindowsServerSolutions.CertificateManagement;
    using Microsoft.WindowsServerSolutions.Common;
    using Microsoft.Win32;
    ```

7.  Измените пространство имен и заголовок класса в соответствии с примером ниже.

    ```c#
    namespace Microsoft.WindowsServerSolutions.RemoteAccess.Domains
    {
        public class MyDomainNameProvider : IDomainSignupProvider
        {
        }
    }
    ```

8.  Добавьте в класс метод Initialize и необходимые переменные, которые определяют домены, предоставляемые мастеру.

    > [!NOTE]
    >  Метод Initialize определяет идентификатор поставщика доменов, который должен быть уникальным. В качестве уникального идентификатора, как правило, используют GUID. Дополнительные сведения о создании GUID см. в разделе [Создание Guid (guidgen.exe)](https://go.microsoft.com/fwlink/?LinkId=116098).

     В примере кода показан метод Initialize.

    ```c#

    static readonly Guid MyID = new Guid("8C999DF5-696A-47af-822D-94F1673D3397");
    public Guid ID { get { return MyID; } }
    public string Name { get { return "My Provider"; } }
    List<Offering> offerings = new List<Offering>();

    public void Initialize(DomainProviderSettings config)
    {
       var offer1 = new Offering()
       {
          Description = "My Domain Provider",
          Name = "Offering 1",
          ProviderID = ID,
          MoreInfoUrl = new Uri("http://www.contoso.com"),
          MembershipServiceName = "My Membership",
          EulaUrl = new Uri("http://www.contoso.com"),
       };

       this.offerings.Add(offer1);
       RegistryKey key =
          Registry.LocalMachine.CreateSubKey(@"Software\Microsoft\Windows Server\Domain Manager\Settings");
       key.Close();
    }
    ```

9. Добавьте метод GetOfferings, который возвращает список предлагаемых доменов, инициализированных на предыдущем шаге. В примере кода показан метод GetOfferings.

    ```c#

    public ReadOnlyCollection<Offering> GetOfferings()
    {
       return this.offerings.AsReadOnly();
    }
    ```

10. Добавьте метод FindOfferingForDomain, который возвращает предлагаемый домен из списка. В примере кода показан метод FindOfferingForDomain.

    ```

    public Offering FindOfferingForDomain(string domain)
    {
       // Return the offering that has the domain name.
       return offerings[0];
    }

    ```

11. Добавьте метод SetCredentials, который определяет учетные данные, необходимые для доступа к предлагаемым доменам. В примере кода показан метод SetCredentials.

    ```c#

    private string currentUser { get; set; }
    private string currentPassword { get; set; }

    public bool SetCredentials(DomainNameRequest request,
       DomainProviderCredentials credentials, bool validate)
    {
       currentUser = credentials.UserName;
       currentPassword = credentials.Password;
       if (validate)
       {
          return ValidateCredentials();
       }

       return true;
    }
    ```

12. Добавьте метод ValidateCredentials, который проверяет учетные данные, определенные методом SetCredentials. В примере кода показан метод ValidateCredentials.

    ```c#

    public static readonly string offerUser = "user1@contoso.com";
    public static readonly string offerPassword = "password1";

    public bool ValidateCredentials()
    {
       if (IsUser())
          return string.Equals(currentPassword, offerPassword);
       else
          return false;
    }

    private bool IsUser()
    {
       return string.Equals(currentUser, offerUser, StringComparison.OrdinalIgnoreCase);
    }
    ```

13. Добавьте метод GetAvailableDomainRoots, возвращающий список имен корневых доменов, которые поддерживаются предлагаемым доменом, указанным в запросе. Список имен корневых доменов не может быть пустым. В примере кода показан метод GetAvailableDomainRoots.

    ```c#

    public ReadOnlyCollection<string> GetAvailableDomainRoots(DomainNameRequest request)
    {
       List<string> list = new List<string>();
       list.Add("domain1.com");
       list.Add("domain1.org");

       return list.AsReadOnly();
    }
    ```

14. Добавьте метод GetUserDomainNames, возвращающий список имен доменов, которыми уже владеет текущий пользователь, связанный с запрашиваемым доменом. Этот список может быть пустым. В примере кода показан метод GetUserDomainNames.

    ```c#

    public static readonly string AvailableDomain1 = "available.domain1.com",
       AvailableDomain2 = "available.domain2.com";
    public static readonly string OccupiedDomain1 = "occupied.domain1.com",
       OccupiedDomain2 = "occupied.domain2.com";

    public ReadOnlyCollection<string> GetUserDomainNames(DomainNameRequest request)
    {
       var userDomains = new List<string>();
       userDomains.Add(OccupiedDomain1);
       userDomains.Add(AvailableDomain1);

       return userDomains.AsReadOnly();
    }
    ```

15. Добавьте метод GetUserDomainQuota, который возвращает максимальное число доменов, разрешенных для указанного предлагаемого домена. Если максимальное количество неприменимо, этот метод должен возвращать 0. В примере показан метод GetUserDomainQuota.

    ```c#

    public int GetUserDomainQuota(DomainNameRequest request)
    {
       return 0;
    }
    ```

16. Добавьте метод CheckDomainAvailability, который проверяет доступность запрашиваемого имени домена и может возвратить список предлагаемых имен. В примере кода показан метод CheckDomainAvailability.

    ```c#

    public bool CheckDomainAvailability(DomainNameRequest request,
       out ReadOnlyCollection<string> suggestions)
    {
       suggestions = null;

       return true;
    }
    ```

17. Добавьте метод CommitDomain, который фиксирует запрошенное имя домена. В случае успешного выполнения этого метода имя домена связывается с учетной записью пользователя, немедленно вызывается поставщик обслуживания для извлечения сертификата, если домен находится в полностью работоспособном состоянии, после чего поставщик и предлагаемый домен становятся активными. В примере кода показан метод CommitDomain.

    ```c#

    public DomainStatus CommitDomain(DomainNameRequest request)
    {
       ReadOnlyCollection<string> suggestions;
       if (!CheckDomainAvailability(request, out suggestions))
       {
          throw new DomainException(FailureReason.InvalidDomainName, null, null);
       }

       return DomainStatus.Ready;
    }
    ```

18. Добавьте метод ReleaseDomain, который информирует поставщика, что пользователь намерен освободить имя домена. В примере кода показан метод ReleaseDomain.

    ```c#

    public bool ReleaseDomain(DomainNameRequest request)
    {
       return true;
    }
    ```

19. Добавьте метод GetProviderLandingUrl, который возвращает URL-адрес целевой страницы в рабочем процессе регистрации домена. В примере кода показан метод GetProviderLandingUrl.

    ```c#

    public Url GetProviderLandingUrl(DomainNameRequest request)
    {
       return new Url("www.contoso.com");
    }
    ```

20. Добавьте метод GetDomainMaintenanceProvider, который возвращает экземпляр интерфейса IDomainMaintenanceProvider, используемого для задач обслуживания доменов. Этот метод вызывается после успешного выполнения метода CommitDomain при запуске диспетчера доменов. В примере кода показан метод GetDomainMaintenanceProvider.

    ```c#

    public IDomainMaintenanceProvider GetDomainMaintenanceProvider()
    {
       return new MyDomainMaintenanceProvider();
    }
    ```

21. Сохраните проект, но закрывайте его, поскольку в него будут добавляться объекты при выполнении следующей процедуры. До завершения этой процедуры построение проекта невозможно.

###  <a name="add-an-implementation-of-the-idomainmaintenanceprovider-interface-to-the-assembly"></a><a name="BKMK_DomainMaintenance"></a> Добавление в сборку реализации интерфейса Идомаинмаинтенанцепровидер
 Интерфейс IDomainMaintenanceProvider используется для обслуживания домена после его создания.

##### <a name="to-add-the-idomainmaintenanceprovider-code-to-the-assembly"></a>Добавление в сборку кода интерфейса IDomainMaintenanceProvider

1.  Добавьте заголовок класса для поставщика обслуживания домена. Убедитесь, что имя, определенное для поставщика, совпадает с именем, ранее определенном в методе GetDomainMaintenanceProvider.

    ```c#

    public class MyDomainMaintenanceProvider : IDomainMaintenanceProvider
    {
    }
    ```

2.  Добавьте метод Activate, который задает активный поставщик. В примере кода показан метод Activate.

    ```c#

    string DomainName { get; set; }
    protected DomainProviderSettings Settings { get; set; }

    public void Activate(DomainProviderSettings settings,
       DomainNameConfiguration config, DomainProviderCredentials credentials)
    {
       Settings = settings;
       SetCredentials(credentials);
       DomainName = config.AutoConfiguredAnywhereAccessFullName.Punycode;
    }
    ```

3.  Добавьте в метод Deactivate, который используется для отключения всех действий. В примере кода показан метод Deactivate.

    ```

    public void Deactivate()
    {
       //Deactivate all actions
    }

    ```

4.  Добавьте метод SetCredentials, который обновляет учетные данные пользователя. Этот метод можно вызвать, например, для обновления более недействительных учетных данных. В примере кода показан метод SetCredentials.

    ```c#

    protected DomainProviderCredentials Credentials { get; set; }

    public bool SetCredentials(DomainProviderCredentials credentials)
    {
       this.Credentials = credentials;

       return true;
    }
    ```

5.  Добавьте метод ValidateCredentials, который проверяет указанные учетные данные. В примере кода показан метод ValidateCredentials.

    ```c#

    public static readonly string offerUser = "user1@contoso.com";
    public static readonly string offerPassword = "password1";

    public bool ValidateCredentials()
    {
       if (string.Equals(this.Credentials.UserName,
          offerUser,
          StringComparison.OrdinalIgnoreCase) &&
             string.Equals(this.Credentials.Password, offerPassword))
          return true;

       return false;
    }
    ```

6.  Добавьте метод GetPublicAddress, который возвращает внешний IP-адрес сервера. В примере кода показан метод GetPublicAddress.

    ```c#

    public IPAddress GetPublicIPAddress()
    {
       string PublicIP = "0.0.0.0";
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))
       {
          PublicIP = (key == null) ? "0.0.0.0" : key.GetValue("PublicIP", "0.0.0.0").ToString();
       }
       IPAddress ip = IPAddress.Parse(PublicIP);

       if (PublicIP == "0.0.0.0")
       {
          string strHostName = Dns.GetHostName();
          IPHostEntry ipEntry = Dns.GetHostEntry(strHostName);

          IPAddress[] addr = ipEntry.AddressList;
          foreach (IPAddress add in addr)
          {
             if (add.AddressFamily == AddressFamily.InterNetwork)
             {
                return add;
             }
          }
       }
       else
       {
          return IPAddress.Parse(PublicIP);
       }

       return null;
    }
    ```

7.  Добавьте метод SubmitCertificateRequest, который запрос сертификата для настраиваемого имени домена.

    ```c#

    string cert=null;

    public void SubmitCertificateRequest(string certificateRequest)
    {
       cert = CertManaged.SubmitRequest(certificateRequest, CertCommon.CAServerFQDN + "\\" +
          CertCommon.CAName,
          Microsoft.WindowsServerSolutions.CertificateManagement.CRFlags.Base64Header,
          CertCommon.CATemplate,
          EncodingFlags.Base64);
    }
    ```

8.  Добавьте метод GetCertificateResponse, который возвращает запрашиваемый сертификат в случае полностью работоспособного состояния домена. Этот метод вызывается как для запросов на получение новых сертификатов, так и для запросов на обновление сертификатов. В примере кода показан метод GetCertificateResponse.

    ```c#

    public string GetCertificateResponse(bool renew)
    {
       return cert;
    }
    ```

9. Добавьте метод SubmitRenewCertificateRequest, который обрабатывает обновление сертификата. В примере кода показан метод SubmitRenewCertificateRequest.

    ```c#

    public void SubmitRenewCertificateRequest()
    {
       // Add certificate renewal code
    }
    ```

10. Добавьте метод UpdateDNSRecords, который обновляет записи DNS, сохраняемые поставщиком. В примере кода показан метод UpdateDNS.

    ```c#

    public bool UpdateDnsRecords(IList<DnsRecord> records)
    {
       string UpdateDNS = "true";
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))
       {
          UpdateDNS = (key == null) ? "true" : key.GetValue("UpdateDNS", "true").ToString();
       }

       return UpdateDNS == "true";
    }

    ```

11. Добавьте метод TestConnection, который пытается установить подключение к внутренней службе. Если для этого метода требуется проверка подлинности, должно создаваться соответствующее исключение. В примере кода показан метод TestConnection.

    ```c#

    public bool TestConnection()
    {
       // Add code to test connection

       return true;
    }
    ```

12. Добавьте метод GetDomainState, который возвращает текущее состояние домена. В примере кода показан метод GetDomainState.

    ```c#

    public DomainState GetDomainState()
    {
       string domainstatus = "FullyOperational";
       long expirationDate = 365;
       using (RegistryKey key = ProductInfo.RegKey.OpenSubKey("Domain Manager\\Settings", true))
       {
          domainstatus = (key == null) ? "Ready" : key.GetValue("DomainStatus", "Ready").ToString();
          expirationDate = Int64.Parse(key.GetValue("ExpirationDate", "365").ToString());
       }

       switch (domainstatus)
       {
          case "Failed":
             return new DomainState(DomainStatus.Failed,
                null,
                DateTime.Now.AddDays(expirationDate));
          case "Ready":
             return new DomainState(DomainStatus.Ready,
                null,
                DateTime.Now.AddDays(expirationDate));
          case "InRenewal":
             return new DomainState(DomainStatus.InRenewal,
                null,
                DateTime.Now.AddDays(expirationDate));
          case "InRenewalCustomerInterventionRequired":
             return new DomainState(DomainStatus.InRenewalCustomerInterventionRequired,
                null,
                DateTime.Now.AddDays(expirationDate));
          case "Pending":
             return new DomainState(DomainStatus.Pending,
                null,
                DateTime.Now.AddDays(expirationDate));
          case "PendingCustomerInterventionRequired":
             return new DomainState(DomainStatus.PendingCustomerInterventionRequired,
                null,
                DateTime.Now.AddDays(expirationDate));
          case "RenewalFailed":
             return new DomainState(DomainStatus.RenewalFailed,
                null,
                DateTime.Now.AddDays(expirationDate));
          default:
             return new DomainState(DomainStatus.Unknown,
                null,
                DateTime.Now.AddDays(expirationDate));
          }
    }
    ```

13. Добавьте метод GetCertificateState, который возвращает текущее состояние сертификата. В примере кода показан метод GetCertificateState.

    ```c#

    public CertificateState GetCertificateState(bool renew)
    {
       return new CertificateState(CertificateStatus.Ready, string.Empty);
    }
    ```

14. Сохраните решение и выполните его построение.

###  <a name="sign-the-assembly-with-an-authenticode-signature"></a><a name="BKMK_SignAssembly"></a> Подписать сборку с помощью подписи Authenticode
 Чтобы сборку можно было использовать в операционной системе, на ней должна быть подпись Authenticode. Дополнительные сведения о подписи сборки см. в разделе [Подпись и проверка кода с помощью Authenticode](https://msdn.microsoft.com/library/ms537364\(VS.85\).aspx#SignCode).

###  <a name="install-the-assembly-on-the-reference-computer"></a><a name="BKMK_InstallAssembly"></a> Установка сборки на эталонном компьютере
 Поместите сборку в папку на компьютере-образце. Запишите путь к этой папке, поскольку его необходимо добавить в реестр на следующем шаге.

### <a name="add-a-key-to-the-registry"></a>Добавление раздела реестра
 Запись добавляется в реестр для определения расположения сборки и ее характеристик.

##### <a name="to-add-a-key-to-the-registry"></a>Добавление раздела в реестр

1.  На компьютере-образце нажмите кнопку **Пуск**, введите команду **regedit** и нажмите клавишу **ВВОД**.

2.  В левой области последовательно разверните узлы **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server**, **Domain Managers** и **Providers**.

3.  Щелкните правой кнопкой мыши раздел **Providers**, выберите команду **Создать** и щелкните пункт **Раздел**.

4.  В качестве имени раздела введите идентификатор поставщика. Этот идентификатор представляет собой GUID, определенный для поставщика на шаге 8 процедуры [Добавление в сборку реализации интерфейса IDomainSignupProvider](Add-Third-Level-Domain-Names.md#BKMK_DomainSignup).

5.  Щелкните правой кнопкой мыши созданный раздел и выберите пункт **Строковый параметр**.

6.  Введите **Assembly** в качестве имени строки и нажмите клавишу **Ввод**.

7.  Щелкните правой кнопкой мыши строку **Assembly** в правой области и выберите команду **Изменить**.

8.  Введите полный путь к ранее созданному файлу сборки и нажмите кнопку **ОК**.

9. Снова щелкните раздел правой кнопкой мыши и выберите пункт **Строковый параметр**.

10. В качестве имени строки введите **Enabled** и нажмите клавишу **ВВОД**.

11. Щелкните правой кнопкой мыши строку **Enabled** в правой области и выберите команду **Изменить**.

12. Введите **True** и нажмите кнопку **ОК**.

13. Снова щелкните раздел правой кнопкой мыши и выберите пункт **Строковый параметр**.

14. В качестве имени строки введите **Type** и нажмите клавишу **ВВОД**.

15. Щелкните правой кнопкой мыши строку **Type** в правой панели и выберите команду **Изменить**.

16. Введите полное имя класса поставщика, определенного в сборке, и нажмите кнопку **ОК**.

###  <a name="restart-the-windows-server-domain-name-management-service"></a><a name="BKMK_RestartService"></a> Перезапуск службы управления доменными именами Windows Server
 Чтобы поставщик стал доступным для операционной системы, необходимо перезапустить службу управления доменными именами Windows Server.

##### <a name="restart-the-service"></a>Перезапустите службу.

1.  Нажмите кнопку **Пуск**, введите **mmc**, а затем нажмите клавишу **ВВОД**.

2.  Если консоль не отображается в оснастке "Службы", добавьте ее в список, выполнив следующие действия.

    1.  В меню **Файл** выберите команду **Добавить или удалить оснастку**.

    2.  В списке **Доступные оснастки** выберите пункт **Службы** и нажмите кнопку **Добавить**.

    3.  Убедитесь, что в диалоговом окне **Службы** выбран **локальный компьютер**, и нажмите кнопку **Готово**.

    4.  Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Добавить или удалить оснастку**.

3.  Дважды щелкните пункт **Службы**, прокрутите список вниз, выберите **Управление доменами Windows Server** и щелкните **Перезапуск службы**.

## <a name="see-also"></a>См. также:
 [Создание и Настройка образа](Creating-and-Customizing-the-Image.md) [Дополнительные настройки](Additional-Customizations.md) [Подготовка образа для развертывания](Preparing-the-Image-for-Deployment.md) [Тестирование взаимодействия с пользователем](Testing-the-Customer-Experience.md)