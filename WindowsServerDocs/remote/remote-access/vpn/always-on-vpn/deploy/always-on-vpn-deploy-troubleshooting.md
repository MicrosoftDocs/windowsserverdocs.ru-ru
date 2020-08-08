---
title: Устранение неполадок Always On VPN
description: В этом разделе приведены инструкции по проверке и устранению неполадок Always On развертывании VPN в Windows Server 2016.
ms.topic: article
ms.assetid: 4d08164e-3cc8-44e5-a319-9671e1ac294a
ms.localizationpriority: medium
ms.date: 06/11/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.openlocfilehash: 3a1b85504fcae1aabc155d9cf415bc49d4722494
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993634"
---
# <a name="troubleshoot-always-on-vpn"></a>Устранение неполадок Always On VPN

>Область применения: Windows Server (половина ежегодного канала), Windows Server 2016, Windows Server 2012 R2, Windows 10

Если Always On установки VPN не удается подключить клиентов к внутренней сети, причиной является недопустимый сертификат VPN, неправильные политики NPS или проблемы с сценариями развертывания клиента или маршрутизацией и удаленным доступом. Первым шагом в устранении неполадок и тестировании VPN-подключения является понимание основных компонентов инфраструктуры VPN Always On.

Устранить проблемы с подключением можно несколькими способами. Для проблем на стороне клиента и общего устранения неполадок приложение регистрируется на клиентских компьютерах. Для проблем, связанных с проверкой подлинности, журнал NPS на сервере NPS может помочь определить источник проблемы.

## <a name="error-codes"></a>Коды ошибок

### <a name="error-code-800"></a>Код ошибки: 800

- **Описание ошибки.** "Удаленное подключение не удалось установить из-за сбоя использованных VPN-туннелей. VPN-сервер может быть недоступен. Если это подключение пытается использовать туннель L2TP/IPsec, параметры безопасности, необходимые для согласования IPsec, могут быть настроены неправильно.

- **Возможная причина.** Эта ошибка возникает, если VPN-туннель имеет тип **Авто** и попытка подключения завершается неудачно для всех VPN-туннелей.

- **Возможные решения**

    - Если вы понимаете, какой туннель использовать для развертывания, задайте тип VPN на стороне VPN-клиента для этого типа туннеля.

    - При установлении VPN-подключения с определенным типом туннеля подключение по-прежнему будет завершаться сбоем, но это приведет к появлению дополнительной ошибки, относящейся к туннелю (например, "GRE заблокирован для PPTP").

    - Эта ошибка также возникает, когда не удается подключиться к VPN-серверу или не удается установить туннельное подключение.

- **Проверьте следующее.**

    - Порты IKE (UDP-порты 500 и 4500) не блокируются.

    - Правильные сертификаты для IKE существуют как на клиенте, так и на сервере.

### <a name="error-code-809"></a>Код ошибки: 809

- **Описание ошибки.**  Не удалось установить сетевое подключение между компьютером и VPN-сервером, так как удаленный сервер не отвечает. Это может быть вызвано тем, что одно из сетевых устройств (например, брандмауэры, NAT, маршрутизаторы) между компьютером и удаленным сервером не настроено для разрешения VPN-подключений. Обратитесь к администратору или поставщику услуг, чтобы определить, какое устройство может быть причиной проблемы.

- **Возможная причина.** Эта ошибка вызвана блокированием портов UDP 500 или 4500 на VPN-сервере или брандмауэре.

- **Возможное решение.** Убедитесь, что UDP-порты 500 и 4500 разрешены через все брандмауэры между клиентом и сервером RRAS.

### <a name="error-code-812"></a>Код ошибки: 812

- **Описание ошибки.** Не удается подключиться к Always On VPN. Подключение не выполнено из-за политики, заданной на вашем RAS/VPN сервере. В частности, метод проверки подлинности, используемый сервером для проверки имени пользователя и пароля, может не соответствовать методу проверки подлинности, настроенному в профиле подключения. Обратитесь к администратору сервера RAS и сообщите ему об этой ошибке.

- **Возможные причины:**

    - Типичная причина этой ошибки заключается в том, что NPS указал условие проверки подлинности, которое клиент не может удовлетворить. Например, NPS может указать использование сертификата для защиты подключения PEAP, но клиент пытается использовать EAP-MSCHAPv2.

    - Журнал событий 20276 регистрируется в средстве просмотра событий, если параметр протокола проверки подлинности VPN-сервера на основе RRAS не соответствует компьютеру VPN-клиента.

- **Возможное решение.** Убедитесь, что конфигурация клиента соответствует условиям, указанным на сервере NPS.

### <a name="error-code-13806"></a>Код ошибки: 13806

- **Описание ошибки.** IKE не удалось найти действительный сертификат компьютера. Обратитесь к администратору безопасности сети, чтобы установить действительный сертификат в соответствующем хранилище сертификатов.

- **Возможная причина.** Эта ошибка обычно возникает, когда на VPN-сервере отсутствует сертификат компьютера или сертификат корневого компьютера.

- **Возможное решение.** Убедитесь, что сертификаты, указанные в этом развертывании, установлены как на клиентском компьютере, так и на VPN-сервере.

### <a name="error-code-13801"></a>Код ошибки: 13801

- **Описание ошибки.** Учетные данные проверки подлинности IKE недопустимы.

- **Возможные причины.** Эта ошибка обычно возникает в одном из следующих случаев.

    - Сертификат компьютера, используемый для проверки IKEv2 на сервере RAS, не имеет **проверки подлинности сервера** в разделе " **Расширенное использование ключа**".

    - Срок действия сертификата компьютера на сервере удаленного доступа истек.

    - Корневой сертификат для проверки сертификата сервера удаленного доступа отсутствует на клиентском компьютере.

    - Имя VPN-сервера, используемое на клиентском компьютере, не соответствует **SubjectName** сертификата сервера.

- **Возможное решение.** Убедитесь, что сертификат сервера включает **проверку подлинности сервера** в разделе **Расширенное использование ключа**. Убедитесь, что сертификат сервера все еще действителен. Убедитесь, что используемый центр сертификации указан в списке **Доверенные корневые центры сертификации** на сервере RRAS. Убедитесь, что VPN-клиент подключается с помощью полного доменного имени VPN-сервера, представленного в сертификате VPN-сервера.

### <a name="error-code-0x80070040"></a>Код ошибки: 0x80070040

- **Описание ошибки.** В сертификате сервера не используется **Проверка подлинности сервера** в качестве одной из записей использования сертификатов.

- **Возможная причина.** Эта ошибка может возникать, если на сервере удаленного доступа не установлен сертификат проверки подлинности сервера.

- **Возможное решение.** Убедитесь, что сертификат компьютера, используемый сервером RAS для **IKEv2** , использует **проверку подлинности сервера** в качестве одной из записей использования сертификатов.

### <a name="error-code-0x800b0109"></a>Код ошибки: 0x800B0109

Как правило, компьютер VPN-клиента присоединяется к домену на основе Active Directory. Если для входа на VPN-сервер используются учетные данные домена, сертификат автоматически устанавливается в хранилище Доверенные корневые центры сертификации. Однако если компьютер не присоединен к домену или используется другая цепочка сертификатов, может возникнуть эта проблема.

- **Описание ошибки.** Цепочка сертификатов обработана, но была прервана в корневом сертификате, которому не доверяет поставщик доверия.

- **Возможная причина.** Эта ошибка может возникать, если соответствующий доверенный корневой сертификат ЦС не установлен в хранилище доверенных корневых центров сертификации на клиентском компьютере.

- **Возможное решение.** Убедитесь, что корневой сертификат установлен на клиентском компьютере в хранилище доверенных корневых центров сертификации.

## <a name="logs"></a>Журналы

### <a name="application-logs"></a>Журналы приложений

Приложение регистрируется на клиентских компьютерах в большинстве сведений о событиях VPN-подключений более высокого уровня.

Найдите события из источника Расклиент. Все сообщения об ошибках возвращают код ошибки в конце сообщения. Ниже описаны некоторые из наиболее распространенных кодов ошибок, но полный список доступен в [кодах ошибок маршрутизации и удаленного доступа](/previous-versions/mt728163(v=technet.10)).

## <a name="nps-logs"></a>Журналы NPS

NPS создает и сохраняет журналы учета NPS. По умолчанию они хранятся в файлах% SYSTEMROOT% \\ system32 \\ \\ в файле с именем*XXXX*. txt, где *XXXX* — это Дата создания файла.

По умолчанию эти журналы находятся в формате значений с разделителями-запятыми, но не содержат строки заголовка. Строка заголовка:

```
ComputerName,ServiceName,Record-Date,Record-Time,Packet-Type,User-Name,Fully-Qualified-Distinguished-Name,Called-Station-ID,Calling-Station-ID,Callback-Number,Framed-IP-Address,NAS-Identifier,NAS-IP-Address,NAS-Port,Client-Vendor,Client-IP-Address,Client-Friendly-Name,Event-Timestamp,Port-Limit,NAS-Port-Type,Connect-Info,Framed-Protocol,Service-Type,Authentication-Type,Policy-Name,Reason-Code,Class,Session-Timeout,Idle-Timeout,Termination-Action,EAP-Friendly-Name,Acct-Status-Type,Acct-Delay-Time,Acct-Input-Octets,Acct-Output-Octets,Acct-Session-Id,Acct-Authentic,Acct-Session-Time,Acct-Input-Packets,Acct-Output-Packets,Acct-Terminate-Cause,Acct-Multi-Ssn-ID,Acct-Link-Count,Acct-Interim-Interval,Tunnel-Type,Tunnel-Medium-Type,Tunnel-Client-Endpt,Tunnel-Server-Endpt,Acct-Tunnel-Conn,Tunnel-Pvt-Group-ID,Tunnel-Assignment-ID,Tunnel-Preference,MS-Acct-Auth-Type,MS-Acct-EAP-Type,MS-RAS-Version,MS-RAS-Vendor,MS-CHAP-Error,MS-CHAP-Domain,MS-MPPE-Encryption-Types,MS-MPPE-Encryption-Policy,Proxy-Policy-Name,Provider-Type,Provider-Name,Remote-Server-Address,MS-RAS-Client-Name,MS-RAS-Client-Version
```

Если вставить эту строку заголовка в качестве первой строки файла журнала, а затем импортировать файл в Microsoft Excel, столбцы будут помечены правильно.

Журналы NPS могут быть полезны при диагностике проблем, связанных с политиками. Дополнительные сведения о журналах NPS см. в разделе [Интерпретация файлов журнала в формате базы данных NPS](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771748(v=ws.10)).

## <a name="vpn_profileps1-script-issues"></a>Проблемы в работе скрипта VPN_Profile.ps1

Наиболее распространенные проблемы, возникающие при ручном запуске Profile.ps1 сценария VPN_ включают:

- Используется ли средство удаленного подключения?  Не следует использовать RDP или другой метод удаленного подключения, так как он перепутать с обнаружением входа пользователя.

- Является ли пользователь администратором этого локального компьютера?  Убедитесь, что при выполнении сценария VPN_Profile.ps1, у которого у пользователя есть права администратора.

- Включены ли дополнительные функции безопасности PowerShell? Убедитесь, что политика выполнения PowerShell не блокирует скрипт. Перед выполнением скрипта можно отключить ограниченный языковой режим, если он включен. Вы можете активировать ограниченный языковой режим после успешного завершения сценария.

## <a name="always-on-vpn-client-connection-issues"></a>Проблемы с подключением клиента Always On VPN

Небольшая неудачная настройка может привести к сбою клиентского подключения, что может быть трудно обнаружить причину.  Перед установкой соединения Always On VPN-клиент проходит несколько шагов. При устранении неполадок с подключением клиентов пройдите процесс исключения следующим образом:

1. Подключен ли шаблон к внешнему компьютеру? При сканировании **вхатисмип** должен отображаться общедоступный IP-адрес, который не принадлежит вам.

2. Можно ли разрешить имя сервера удаленного доступа или VPN-адреса в адрес? В окне "Сетевые подключения" **панели управления**  >  **Network** **Internet**  >  **Network Connections**откройте свойства профиля VPN. Значение на вкладке **Общие** должно быть открыто разрешимым с помощью DNS.

3. Можно ли получить доступ к VPN-серверу из внешней сети? Попробуйте открыть внешний интерфейс с помощью протокола ICMP и проверить связь с именем удаленного клиента. После успешной проверки связи можно удалить правило Allow ICMP.

4. Правильно ли настроены внутренние и внешние сетевые адаптеры на VPN-сервере? Они находятся в разных подсетях? Подключение внешнего сетевого адаптера к правильному интерфейсу в брандмауэре?

5. Открыты ли порты UDP 500 и 4500 от клиента к внешнему интерфейсу VPN-сервера? Проверьте брандмауэр клиента, брандмауэр сервера и все аппаратные брандмауэры. IPSEC использует UDP-порт 500, поэтому убедитесь, что ИПЕК отключены или не заблокированы в любом месте.

6. Происходит сбой проверки сертификата? Убедитесь, что NPS-сервер имеет сертификат проверки подлинности сервера, который может обслуживать запросы IKE. Убедитесь, что в качестве клиента NPS указан правильный IP-адрес VPN-сервера. Убедитесь, что проверяется подлинность с помощью протокола PEAP, а защищенные свойства EAP должны разрешать проверку подлинности только с помощью сертификата. Журналы событий NPS можно проверить на наличие ошибок проверки подлинности. Дополнительные сведения см. [в разделе Установка и настройка сервера NPS](vpn-deploy-nps.md) .

7. Вы подключаетесь, но у вас нет доступа к Интернету или локальной сети? Проверьте пулы IP-адресов серверов DHCP и VPN на наличие проблем с конфигурацией.

8. Вы подключаетесь и имеете действительный внутренний IP-адрес, но не имеете доступа к локальным ресурсам?  Убедитесь, что клиенты узнают, как получить эти ресурсы. Для маршрутизации запросов можно использовать VPN-сервер.

## <a name="azure-ad-conditional-access-connection-issues"></a>Проблемы подключения при использовании условного доступа Azure AD

### <a name="oops---you-cant-get-to-this-yet"></a>Ой! вы еще не можете получить доступ к этому

- **Описание ошибки.** Если политика условного доступа не удовлетворена, блокирует VPN-подключение, но подключается после того, как пользователь выберет **X** , чтобы закрыть сообщение.  Нажатие кнопки **ОК** вызывает другую проверку подлинности, которая завершается другим сообщением "ой". Эти события записываются в журнал рабочих событий AAD клиента.

- **Возможные причины**

  - У пользователя есть допустимый сертификат проверки подлинности клиента в хранилище личных сертификатов, который не был выдан Azure AD.

  - Раздел профиля VPN \<TLSExtensions\> отсутствует или не содержит ** \<EKUName\> условия условного доступа AAD \</EKUName\> \<EKUOID\> 1.3.6.1.4.1.311.87</екуоид \> \<EKUName> AAD</екунаме \> \<EKUOID\> 1.3.6.1.4.1.311.87</екуоид \> ** . \<EKUName>Записи и \<EKUOID> указывают VPN-клиенту, какой сертификат следует получить из хранилища сертификатов пользователя при передаче сертификата на VPN-сервер. Без этого VPN-клиент использует любой допустимый сертификат проверки подлинности клиента, находящегося в хранилище сертификатов пользователя, и проверка подлинности будет выполнена.

  - Сервер RADIUS (NPS) не настроен на прием только сертификатов клиентов, содержащих OID **условного доступа AAD** .

- **Возможное решение.** Для экранирования этого цикла выполните следующие действия.

  1. В Windows PowerShell выполните командлет **Get-WmiObject** , чтобы создать дамп конфигурации профиля VPN.
  2. Убедитесь, что **\<TLSExtensions>** **\<EKUName>** разделы, и содержат **\<EKUOID>** правильное имя и идентификатор объекта.

      ```powershell
      PS C:\> Get-WmiObject -Class MDM_VPNv2_01 -Namespace root\cimv2\mdm\dmmap

      __GENUS                 : 2
      __CLASS                 : MDM_VPNv2_01
      __SUPERCLASS            :
      __DYNASTY               : MDM_VPNv2_01
      __RELPATH               : MDM_VPNv2_01.InstanceID="AlwaysOnVPN",ParentID="./Vendor/MSFT/VPNv2"
      __PROPERTY_COUNT        : 10
      __DERIVATION            : {}
      __SERVER                : DERS2
      __NAMESPACE             : root\cimv2\mdm\dmmap
      __PATH                  : \\DERS2\root\cimv2\mdm\dmmap:MDM_VPNv2_01.InstanceID="AlwaysOnVPN",ParentID="./Vendor/MSFT/VP
                                  Nv2"
      AlwaysOn                :
      ByPassForLocal          :
      DnsSuffix               :
      EdpModeId               :
      InstanceID              : AlwaysOnVPN
      LockDown                :
      ParentID                : ./Vendor/MSFT/VPNv2
      ProfileXML              : <VPNProfile><RememberCredentials>false</RememberCredentials><DeviceCompliance><Enabled>true</
                                  Enabled><Sso><Enabled>true</Enabled></Sso></DeviceCompliance><NativeProfile><Servers>derras2.
                                  corp.deverett.info;derras2.corp.deverett.info</Servers><RoutingPolicyType>ForceTunnel</Routin
                                  gPolicyType><NativeProtocolType>Ikev2</NativeProtocolType><Authentication><UserMethod>Eap</Us
                                  erMethod><MachineMethod>Eap</MachineMethod><Eap><Configuration><EapHostConfig
                                  xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><EapMethod><Type
                                  xmlns="https://www.microsoft.com/provisioning/EapCommon">25</Type><VendorId
                                  xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorId><VendorType
                                  xmlns="https://www.microsoft.com/provisioning/EapCommon">0</VendorType><AuthorId
                                  xmlns="https://www.microsoft.com/provisioning/EapCommon">0</AuthorId></EapMethod><Config
                                  xmlns="https://www.microsoft.com/provisioning/EapHostConfig"><Eap xmlns="https://www.microsoft.
                                  com/provisioning/BaseEapConnectionPropertiesV1"><Type>25</Type><EapType xmlns="https://www.mic
                                  rosoft.com/provisioning/MsPeapConnectionPropertiesV1"><ServerValidation><DisableUserPromptFor
                                  ServerValidation>true</DisableUserPromptForServerValidation><ServerNames></ServerNames></Serv
                                  erValidation><FastReconnect>true</FastReconnect><InnerEapOptional>false</InnerEapOptional><Ea
                                  p xmlns="https://www.microsoft.com/provisioning/BaseEapConnectionPropertiesV1"><Type>13</Type>
                                  <EapType xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV1"><Credenti
                                  alsSource><CertificateStore><SimpleCertSelection>true</SimpleCertSelection></CertificateStore
                                  ></CredentialsSource><ServerValidation><DisableUserPromptForServerValidation>true</DisableUse
                                  rPromptForServerValidation><ServerNames></ServerNames><TrustedRootCA>5a 89 fe cb 5b 49 a7 0b
                                  1a 52 63 b7 35 ee d7 1c c2 68 be 4b </TrustedRootCA></ServerValidation><DifferentUsername>fal
                                  se</DifferentUsername><PerformServerValidation xmlns="https://www.microsoft.com/provisioning/E
                                  apTlsConnectionPropertiesV2">true</PerformServerValidation><AcceptServerName xmlns="https://ww
                                  w.microsoft.com/provisioning/EapTlsConnectionPropertiesV2">false</AcceptServerName><TLSExtens
                                  ions
                                  xmlns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xml
                                  ns="https://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><
                                  EKUName>AAD Conditional
                                  Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList
                                  Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></Client
                                  AuthEKUList></FilteringInfo></TLSExtensions></EapType></Eap><EnableQuarantineChecks>false</En
                                  ableQuarantineChecks><RequireCryptoBinding>false</RequireCryptoBinding><PeapExtensions><Perfo
                                  rmServerValidation xmlns="https://www.microsoft.com/provisioning/MsPeapConnectionPropertiesV2"
                                  >false</PerformServerValidation><AcceptServerName xmlns="https://www.microsoft.com/provisionin
                                  g/MsPeapConnectionPropertiesV2">false</AcceptServerName></PeapExtensions></EapType></Eap></Co
                                  nfig></EapHostConfig></Configuration></Eap></Authentication></NativeProfile></VPNProfile>
      RememberCredentials     : False
      TrustedNetworkDetection :
      PSComputerName          : DERS2
      ```

  3. Чтобы определить наличие допустимых сертификатов в хранилище сертификатов пользователя, выполните команду **certutil** :

     ```powershell
     C:\>certutil -store -user My

      My "Personal"
      ================ Certificate 0 ================
      Serial Number: 32000000265259d0069fa6f205000000000026
      Issuer: CN=corp-DEDC0-CA, DC=corp, DC=deverett, DC=info
       NotBefore: 12/8/2017 8:07 PM
       NotAfter: 12/8/2018 8:07 PM
      Subject: E=winfed@deverett.info, CN=WinFed, OU=Users, OU=Corp, DC=corp, DC=deverett, DC=info
      Certificate Template Name (Certificate Type): User
      Non-root Certificate
      Template: User
      Cert Hash(sha1): a50337ab015d5612b7dc4c1e759d201e74cc2a93
        Key Container = a890fd7fbbfc072f8fe045e680c501cf_5834bfa9-1c4a-44a8-a128-c2267f712336
        Simple container name: te-User-c7bcc4bd-0498-4411-af44-da2257f54387
        Provider = Microsoft Enhanced Cryptographic Provider v1.0
      Encryption test passed

      ================ Certificate 1 ================
      Serial Number: 367fbdd7e6e4103dec9b91f93959ac56
      Issuer: CN=Microsoft VPN root CA gen 1
       NotBefore: 12/8/2017 6:24 PM
       NotAfter: 12/8/2017 7:29 PM
      Subject: CN=WinFed@deverett.info
      Non-root Certificate
      Cert Hash(sha1): 37378a1b06dcef1b4d4753f7d21e4f20b18fbfec
        Key Container = 31685cae-af6f-48fb-ac37-845c69b4c097
        Unique container name: bf4097e20d4480b8d6ebc139c9360f02_5834bfa9-1c4a-44a8-a128-c2267f712336
        Provider = Microsoft Software Key Storage Provider
      Private key is NOT exportable
      Encryption test passed
     ```
     >[!NOTE]
     >Если сертификат от издателя **CN = корневой ЦС Microsoft VPN Gen 1** имеется в личном хранилище пользователя, но пользователь получил доступ, выбрав **X** , чтобы закрыть сообщение о сообщении, СОбирайте журналы событий CAPI2, чтобы убедиться, что сертификат, используемый для проверки подлинности, был допустимым сертификатом проверки подлинности клиента, который не был выдан корневым ЦС Microsoft VPN.

  4. Если в личном хранилище пользователя существует допустимый сертификат проверки подлинности клиента, соединение не будет выполнено (как должно) после выбора пользователем **X** и **\<TLSExtensions>** **\<EKUName>** **\<EKUOID>** существования разделов, и и содержащих правильные данные.

     Появляется сообщение об ошибке "не удалось найти сертификат, который может использоваться с протоколом расширяемого протокола проверки подлинности".

### <a name="unable-to-delete-the-certificate-from-the-vpn-connectivity-blade"></a>Не удалось удалить сертификат из колонки VPN-подключения

- **Описание ошибки.** Не удается удалить сертификаты в колонке VPN-подключения.

- **Возможная причина.** Для сертификата задан **первичный**сертификат.

- **Возможное решение.**

    1. В колонке VPN-подключение выберите сертификат.
    2. В разделе **Основная**выберите **нет**, а затем нажмите кнопку **сохранить**.
    3. В колонке VPN-подключение снова выберите сертификат.
    4. Нажмите кнопку **Удалить**.
