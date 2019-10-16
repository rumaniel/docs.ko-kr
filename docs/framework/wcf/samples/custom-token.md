---
title: Custom Token
ms.date: 03/30/2017
ms.assetid: e7fd8b38-c370-454f-ba3e-19759019f03d
ms.openlocfilehash: b073375325d2989a23624303f2c40b8f61a29d02
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928659"
---
# <a name="custom-token"></a>Custom Token

이 샘플에서는 WCF (Windows Communication Foundation) 응용 프로그램에 사용자 지정 토큰 구현을 추가 하는 방법을 보여 줍니다. 이 예제에서는 클라이언트 신용 카드에 대한 정보를 서비스에 안전하게 전달하기 위해 `CreditCardToken`을 사용합니다. 이 토큰은 WS-Security 메시지 헤더로 전달되고 메시지 본문 및 다른 메시지 헤더와 함께 대칭 보안 바인딩 요소를 사용하여 서명 및 암호화됩니다. 이 방법은 기본 제공 토큰이 충분하지 않은 경우 유용합니다. 이 샘플에서는 기본 제공 토큰 중 하나를 사용하는 대신 사용자 지정 보안 토큰을 서비스에 제공하는 방법을 보여 줍니다. 이 서비스는 요청-회신 통신 패턴을 정의하는 계약을 구현합니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

 즉, 이 샘플에서는 다음 방법을 보여 줍니다.

- 클라이언트가 사용자 지정 보안 토큰을 서비스에 전달하는 방법

- 서비스가 사용자 지정 보안 토큰을 사용하고 유효성을 검사하는 방법

- WCF 서비스 코드에서 사용자 지정 보안 토큰을 비롯 하 여 수신 된 보안 토큰에 대 한 정보를 얻을 수 있는 방법입니다.

- 서버의 X.509 인증서를 사용하여 메시지 암호화 및 서명에 사용되는 대칭 키를 보호하는 방법

## <a name="client-authentication-using-a-custom-security-token"></a>사용자 지정 보안 토큰을 사용한 클라이언트 인증

 서비스는 `BindingHelper` 및 `EchoServiceHost` 클래스를 사용하여 프로그래밍 방식으로 만들어진 단일 엔드포인트를 노출합니다. 끝점은 하나의 주소, 바인딩 및 계약으로 구성됩니다. 바인딩은 `SymmetricSecurityBindingElement` 및 `HttpTransportBindingElement`를 사용하여 사용자 지정 바인딩으로 구성됩니다. 이 샘플에서는 서비스의 X.509 인증서를 사용하여 전송 도중 대칭 키를 보호하고 WS-Security 메시지 헤더에서 사용자 지정 `SymmetricSecurityBindingElement`을 서명 및 암호화된 보안 토큰으로 전달하도록 `CreditCardToken`를 설정합니다. 동작은 클라이언트 인증에 사용되는 서비스 자격 증명과 서비스 X.509 인증서에 대한 정보를 지정합니다.

```csharp
public static class BindingHelper
{
    public static Binding CreateCreditCardBinding()
    {
        var httpTransport = new HttpTransportBindingElement();

        // The message security binding element will be configured to require a credit card.
        // The token that is encrypted with the service's certificate.
        var messageSecurity = new SymmetricSecurityBindingElement();
        messageSecurity.EndpointSupportingTokenParameters.SignedEncrypted.Add(new CreditCardTokenParameters());
        X509SecurityTokenParameters x509ProtectionParameters = new X509SecurityTokenParameters();
        x509ProtectionParameters.InclusionMode = SecurityTokenInclusionMode.Never;
        messageSecurity.ProtectionTokenParameters = x509ProtectionParameters;
        return new CustomBinding(messageSecurity, httpTransport);
    }
}
```

 메시지에서 신용 카드 토큰을 사용하기 위해 샘플에서는 이 기능을 제공하는 사용자 지정 서비스 자격 증명을 사용합니다. 서비스 자격 증명 클래스는 `CreditCardServiceCredentials` 클래스에 있으며 `EchoServiceHost.InitializeRuntime` 메서드에서 서비스 호스트의 동작 컬렉션에 추가됩니다.

```csharp
class EchoServiceHost : ServiceHost
{
    string creditCardFile;

    public EchoServiceHost(parameters Uri[] addresses)
        : base(typeof(EchoService), addresses)
    {
        creditCardFile = ConfigurationManager.AppSettings["creditCardFile"];
        if (string.IsNullOrEmpty(creditCardFile))
        {
            throw new ConfigurationErrorsException("creditCardFile not specified in service config");
        }

        creditCardFile = String.Format("{0}\\{1}", System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath, creditCardFile);
    }

    override protected void InitializeRuntime()
    {
        // Create a credit card service credentials and add it to the behaviors.
        CreditCardServiceCredentials serviceCredentials = new CreditCardServiceCredentials(this.creditCardFile);
        serviceCredentials.ServiceCertificate.SetCertificate("CN=localhost", StoreLocation.LocalMachine, StoreName.My);
        this.Description.Behaviors.Remove((typeof(ServiceCredentials)));
        this.Description.Behaviors.Add(serviceCredentials);

        // Register a credit card binding for the endpoint.
        Binding creditCardBinding = BindingHelper.CreateCreditCardBinding();
        this.AddServiceEndpoint(typeof(IEchoService), creditCardBinding, string.Empty);

        base.InitializeRuntime();
    }
}
```

 클라이언트 엔드포인트는 서비스 엔드포인트와 동일한 방식으로 구성됩니다. 클라이언트는 동일한 `BindingHelper` 클래스를 사용하여 바인딩을 만듭니다. 설정의 나머지 부분은 `Client` 클래스에 있습니다. 또한 클라이언트는 적절한 데이터와 함께 `CreditCardToken` 인스턴스를 클라이언트 끝점 동작 컬렉션에 추가하여 `CreditCardClientCredentials`에 포함될 정보와 설정 코드의 서비스 X.509 인증서에 대한 정보를 설정합니다. 이 샘플에서는 `CN=localhost`로 설정된 주체 이름을 가진 X.509 인증서를 서비스 인증서로 사용합니다.

```csharp
Binding creditCardBinding = BindingHelper.CreateCreditCardBinding();
var serviceAddress = new EndpointAddress("http://localhost/servicemodelsamples/service.svc");

// Create a client with given client endpoint configuration.
channelFactory = new ChannelFactory<IEchoService>(creditCardBinding, serviceAddress);

// Configure the credit card credentials on the channel factory.
var credentials =
      new CreditCardClientCredentials(
      new CreditCardInfo(creditCardNumber, issuer, expirationTime));
// Configure the service certificate on the credentials.
credentials.ServiceCertificate.SetDefaultCertificate(
      "CN=localhost", StoreLocation.LocalMachine, StoreName.My);

// Replace ClientCredentials with CreditCardClientCredentials.
channelFactory.Endpoint.Behaviors.Remove(typeof(ClientCredentials));
channelFactory.Endpoint.Behaviors.Add(credentials);

client = channelFactory.CreateChannel();

Console.WriteLine($"Echo service returned: {client.Echo()}");

((IChannel)client).Close();
channelFactory.Close();
```

## <a name="custom-security-token-implementation"></a>사용자 지정 보안 토큰 구현

 WCF에서 사용자 지정 보안 토큰을 사용 하도록 설정 하려면 사용자 지정 보안 토큰의 개체 표현을 만듭니다. 이 샘플에서는 `CreditCardToken` 클래스에 이 표현이 있습니다. 개체 표현은 모든 관련 보안 토큰 정보를 보유하고 보안 토큰에 포함된 보안 키의 목록을 제공합니다. 이 경우에는 신용 카드 보안 토큰에 보안 키가 포함되지 않습니다.

 다음 섹션에서는 사용자 지정 토큰을 유선을 통해 전송 하 고 WCF 끝점에서 사용할 수 있도록 하기 위해 수행 해야 하는 작업에 대해 설명 합니다.

```csharp
class CreditCardToken : SecurityToken
{
    CreditCardInfo cardInfo;
    DateTime effectiveTime = DateTime.UtcNow;
    string id;
    ReadOnlyCollection<SecurityKey> securityKeys;

    public CreditCardToken(CreditCardInfo cardInfo) : this(cardInfo, Guid.NewGuid().ToString()) { }

    public CreditCardToken(CreditCardInfo cardInfo, string id)
    {
        if (cardInfo == null)
            throw new ArgumentNullException(nameof(cardInfo));

        if (id == null)
            throw new ArgumentNullException(nameof(id));

        this.cardInfo = cardInfo;
        this.id = id;

        // The credit card token is not capable of any cryptography.
        this.securityKeys = new ReadOnlyCollection<SecurityKey>(new List<SecurityKey>());
    }

    public CreditCardInfo CardInfo { get { return this.cardInfo; } }

    public override ReadOnlyCollection<SecurityKey> SecurityKeys { get { return this.securityKeys; } }

    public override DateTime ValidFrom { get { return this.effectiveTime; } }
    public override DateTime ValidTo { get { return this.cardInfo.ExpirationDate; } }
    public override string Id { get { return this.id; } }
}
```

## <a name="getting-the-custom-credit-card-token-to-and-from-the-message"></a>사용자 지정 신용 카드 토큰을 메시지로 가져가거나 메시지에서 가져오기

 WCF의 보안 토큰 serializer는 메시지의 XML에서 보안 토큰의 개체 표현을 만들고 보안 토큰의 XML 양식을 만드는 역할을 담당 합니다. 또한 이러한 serializer는 보안 토큰을 가리키는 읽기 및 쓰기 키 식별자와 같은 다른 기능을 수행하지만 이 예제에서는 보안 토큰 관련 기능만 사용합니다. 사용자 지정 토큰을 사용하도록 설정하려면 고유한 보안 토큰 serializer를 구현해야 합니다. 이 샘플에서는 이를 위해 `CreditCardSecurityTokenSerializer` 클래스를 사용합니다.

 서비스에서 사용자 지정 serializer는 사용자 지정 토큰의 XML 양식을 읽고 이로부터 사용자 지정 토큰 개체 표현을 만듭니다.

 클라이언트에서 `CreditCardSecurityTokenSerializer` 클래스는 보안 토큰 개체 표현에 포함된 정보를 XML 작성기에 씁니다.

```csharp
public class CreditCardSecurityTokenSerializer : WSSecurityTokenSerializer
{
    public CreditCardSecurityTokenSerializer(SecurityTokenVersion version) : base() { }

    protected override bool CanReadTokenCore(XmlReader reader)
    {
        XmlDictionaryReader localReader = XmlDictionaryReader.CreateDictionaryReader(reader);

        if (reader == null)
            throw new ArgumentNullException(nameof(reader));

        if (reader.IsStartElement(Constants.CreditCardTokenName, Constants.CreditCardTokenNamespace))
            return true;

        return base.CanReadTokenCore(reader);
    }

    protected override SecurityToken ReadTokenCore(XmlReader reader, SecurityTokenResolver tokenResolver)
    {
        if (reader == null)
            throw new ArgumentNullException(nameof(reader));

        if (reader.IsStartElement(Constants.CreditCardTokenName, Constants.CreditCardTokenNamespace))
        {
            string id = reader.GetAttribute(Constants.Id, Constants.WsUtilityNamespace);

            reader.ReadStartElement();

            // Read the credit card number.
            string creditCardNumber = reader.ReadElementString(Constants.CreditCardNumberElementName, Constants.CreditCardTokenNamespace);

            // Read the expiration date.
            string expirationTimeString = reader.ReadElementString(Constants.CreditCardExpirationElementName, Constants.CreditCardTokenNamespace);
            DateTime expirationTime = XmlConvert.ToDateTime(expirationTimeString, XmlDateTimeSerializationMode.Utc);

            // Read the issuer of the credit card.
            string creditCardIssuer = reader.ReadElementString(Constants.CreditCardIssuerElementName, Constants.CreditCardTokenNamespace);
            reader.ReadEndElement();

            var cardInfo = new CreditCardInfo(creditCardNumber, creditCardIssuer, expirationTime);

            return new CreditCardToken(cardInfo, id);
        }
        else
        {
            return WSSecurityTokenSerializer.DefaultInstance.ReadToken(reader, tokenResolver);
        }
    }

    protected override bool CanWriteTokenCore(SecurityToken token)
    {
        if (token is CreditCardToken)
            return true;
        return base.CanWriteTokenCore(token);
    }

    protected override void WriteTokenCore(XmlWriter writer, SecurityToken token)
    {
        if (writer == null)
            throw new ArgumentNullException(nameof(writer));
        if (token == null)
            throw new ArgumentNullException(nameof(token));

        CreditCardToken c = token as CreditCardToken;
        if (c != null)
        {
            writer.WriteStartElement(Constants.CreditCardTokenPrefix, Constants.CreditCardTokenName, Constants.CreditCardTokenNamespace);
            writer.WriteAttributeString(Constants.WsUtilityPrefix, Constants.Id, Constants.WsUtilityNamespace, token.Id);
            writer.WriteElementString(Constants.CreditCardNumberElementName, Constants.CreditCardTokenNamespace, c.CardInfo.CardNumber);
            writer.WriteElementString(Constants.CreditCardExpirationElementName, Constants.CreditCardTokenNamespace, XmlConvert.ToString(c.CardInfo.ExpirationDate, XmlDateTimeSerializationMode.Utc));
            writer.WriteElementString(Constants.CreditCardIssuerElementName, Constants.CreditCardTokenNamespace, c.CardInfo.CardIssuer);
            writer.WriteEndElement();
            writer.Flush();
        }
        else
        {
            base.WriteTokenCore(writer, token);
        }
    }
}
```

## <a name="how-token-provider-and-token-authenticator-classes-are-created"></a>토큰 공급자 및 토큰 인증자 클래스가 만들어지는 방법

 클라이언트 및 서비스 자격 증명은 보안 토큰 관리자 인스턴스를 제공합니다. 보안 토큰 관리자 인스턴스는 토큰 공급자, 토큰 인증자 및 토큰 serializer를 가져오는 데 사용됩니다.

 토큰 공급자는 클라이언트 또는 서비스 자격 증명에 포함된 정보를 기반으로 토큰의 개체 표현을 만듭니다. 그런 다음 토큰 개체 표현은 앞 단원에 설명된 토큰 serializer를 사용하여 메시지에 기록됩니다.

 토큰 인증자는 메시지에 도착하는 토큰의 유효성을 검사합니다. 들어오는 토큰 개체 표현은 토큰 serializer에 의해 만들어집니다. 그런 다음 이 개체 표현은 유효성 검사를 위해 토큰 인증자에 전달됩니다. 토큰의 유효성이 검사되고 나면 토큰 인증자는 토큰에 포함된 정보를 나타내는 `IAuthorizationPolicy` 개체의 컬렉션을 반환합니다. 이 정보는 권한 부여 결정을 수행하고 응용 프로그램에 대한 클레임을 제공하기 위해 나중에 메시지 처리 도중 사용됩니다. 이 예제에서 신용 카드 토큰 인증자는 이러한 목적을 위해 `CreditCardTokenAuthorizationPolicy`를 사용합니다.

 토큰 serializer는 연결을 통해 토큰의 개체 표현을 가져오거나 가져갑니다. 이에 대해서는 위의 단원에서 설명했습니다.

 이 샘플에서는 클라이언트에서 서비스 방향으로만 신용 카드 토큰을 전송하므로 토큰 공급자는 클라이언트에서만 사용하고 토큰 인증자는 서비스에서만 사용합니다.

 클라이언트의 기능은 `CreditCardClientCredentials`, `CreditCardClientCredentialsSecurityTokenManager` 및 `CreditCardTokenProvider` 클래스에 있습니다.

 서비스에서 기능은 `CreditCardServiceCredentials`, `CreditCardServiceCredentialsSecurityTokenManager`, `CreditCardTokenAuthenticator` 및 `CreditCardTokenAuthorizationPolicy` 클래스에 있습니다.

```csharp
    public class CreditCardClientCredentials : ClientCredentials
    {
        CreditCardInfo creditCardInfo;

        public CreditCardClientCredentials(CreditCardInfo creditCardInfo)
            : base()
        {
            if (creditCardInfo == null)
                throw new ArgumentNullException(nameof(creditCardInfo));

            this.creditCardInfo = creditCardInfo;
        }

        public CreditCardInfo CreditCardInfo
        {
            get { return this.creditCardInfo; }
        }

        protected override ClientCredentials CloneCore()
        {
            return new CreditCardClientCredentials(this.creditCardInfo);
        }

        public override SecurityTokenManager CreateSecurityTokenManager()
        {
            return new CreditCardClientCredentialsSecurityTokenManager(this);
        }
    }

    public class CreditCardClientCredentialsSecurityTokenManager : ClientCredentialsSecurityTokenManager
    {
        CreditCardClientCredentials creditCardClientCredentials;

        public CreditCardClientCredentialsSecurityTokenManager(CreditCardClientCredentials creditCardClientCredentials)
            : base (creditCardClientCredentials)
        {
            this.creditCardClientCredentials = creditCardClientCredentials;
        }

        public override SecurityTokenProvider CreateSecurityTokenProvider(SecurityTokenRequirement tokenRequirement)
        {
            // Handle this token for Custom.
            if (tokenRequirement.TokenType == Constants.CreditCardTokenType)
                return new CreditCardTokenProvider(this.creditCardClientCredentials.CreditCardInfo);
            // Return server cert.
            else if (tokenRequirement is InitiatorServiceModelSecurityTokenRequirement)
            {
                if (tokenRequirement.TokenType == SecurityTokenTypes.X509Certificate)
                {
                    return new X509SecurityTokenProvider(creditCardClientCredentials.ServiceCertificate.DefaultCertificate);
                }
            }

            return base.CreateSecurityTokenProvider(tokenRequirement);
        }

        public override SecurityTokenSerializer CreateSecurityTokenSerializer(SecurityTokenVersion version)
        {

            return new CreditCardSecurityTokenSerializer(version);
        }

    }

    class CreditCardTokenProvider : SecurityTokenProvider
    {
        CreditCardInfo creditCardInfo;

        public CreditCardTokenProvider(CreditCardInfo creditCardInfo) : base()
        {
            if (creditCardInfo == null)
                throw new ArgumentNullException(nameof(creditCardInfo));

            this.creditCardInfo = creditCardInfo;
        }

        protected override SecurityToken GetTokenCore(TimeSpan timeout)
        {
            SecurityToken result = new CreditCardToken(this.creditCardInfo);
            return result;
        }
    }

    public class CreditCardServiceCredentials : ServiceCredentials
    {
        string creditCardFile;

        public CreditCardServiceCredentials(string creditCardFile)
            : base()
        {
            if (creditCardFile == null)
                throw new ArgumentNullException(nameof(creditCardFile));

            this.creditCardFile = creditCardFile;
        }

        public string CreditCardDataFile
        {
            get { return this.creditCardFile; }
        }

        protected override ServiceCredentials CloneCore()
        {
            return new CreditCardServiceCredentials(this.creditCardFile);
        }

        public override SecurityTokenManager CreateSecurityTokenManager()
        {
            return new CreditCardServiceCredentialsSecurityTokenManager(this);
        }
    }

    public class CreditCardServiceCredentialsSecurityTokenManager : ServiceCredentialsSecurityTokenManager
    {
        CreditCardServiceCredentials creditCardServiceCredentials;

        public CreditCardServiceCredentialsSecurityTokenManager(CreditCardServiceCredentials creditCardServiceCredentials)
            : base(creditCardServiceCredentials)
        {
            this.creditCardServiceCredentials = creditCardServiceCredentials;
        }

        public override SecurityTokenAuthenticator CreateSecurityTokenAuthenticator(SecurityTokenRequirement tokenRequirement, out SecurityTokenResolver outOfBandTokenResolver)
        {
            if (tokenRequirement.TokenType == Constants.CreditCardTokenType)
            {
                outOfBandTokenResolver = null;
                return new CreditCardTokenAuthenticator(creditCardServiceCredentials.CreditCardDataFile);
            }

            return base.CreateSecurityTokenAuthenticator(tokenRequirement, out outOfBandTokenResolver);
        }

        public override SecurityTokenSerializer CreateSecurityTokenSerializer(SecurityTokenVersion version)
        {
            return new CreditCardSecurityTokenSerializer(version);
        }
    }

    class CreditCardTokenAuthenticator : SecurityTokenAuthenticator
    {
        string creditCardsFile;
        public CreditCardTokenAuthenticator(string creditCardsFile)
        {
            this.creditCardsFile = creditCardsFile;
        }

        protected override bool CanValidateTokenCore(SecurityToken token)
        {
            return (token is CreditCardToken);
        }

        protected override ReadOnlyCollection<IAuthorizationPolicy> ValidateTokenCore(SecurityToken token)
        {
            CreditCardToken creditCardToken = token as CreditCardToken;

            if (creditCardToken.CardInfo.ExpirationDate < DateTime.UtcNow)
                throw new SecurityTokenValidationException("The credit card has expired.");
            if (!IsCardNumberAndExpirationValid(creditCardToken.CardInfo))
                throw new SecurityTokenValidationException("Unknown or invalid credit card.");

            // the credit card token has only 1 claim - the card number. The issuer for the claim is the
            // credit card issuer

            var cardIssuerClaimSet = new DefaultClaimSet(new Claim(ClaimTypes.Name, creditCardToken.CardInfo.CardIssuer, Rights.PossessProperty));
            var cardClaimSet = new DefaultClaimSet(cardIssuerClaimSet, new Claim(Constants.CreditCardNumberClaim, creditCardToken.CardInfo.CardNumber, Rights.PossessProperty));
            var policies = new List<IAuthorizationPolicy>(1);
            policies.Add(new CreditCardTokenAuthorizationPolicy(cardClaimSet));
            return policies.AsReadOnly();
        }

        /// <summary>
        /// Helper method to check if a given credit card entry is present in the User DB
        /// </summary>
        private bool IsCardNumberAndExpirationValid(CreditCardInfo cardInfo)
        {
            try
            {
                using (var myStreamReader = new StreamReader(this.creditCardsFile))
                {
                    string line = "";
                    while ((line = myStreamReader.ReadLine()) != null)
                    {
                        string[] splitEntry = line.Split('#');
                        if (splitEntry[0] == cardInfo.CardNumber)
                        {
                            string expirationDateString = splitEntry[1].Trim();
                            DateTime expirationDateOnFile = DateTime.Parse(expirationDateString, System.Globalization.DateTimeFormatInfo.InvariantInfo, System.Globalization.DateTimeStyles.AdjustToUniversal);
                            if (cardInfo.ExpirationDate == expirationDateOnFile)
                            {
                                string issuer = splitEntry[2];
                                return issuer.Equals(cardInfo.CardIssuer, StringComparison.InvariantCultureIgnoreCase);
                            }
                            else
                            {
                                return false;
                            }
                        }
                    }
                    return false;
                }
            }
            catch (Exception e)
            {
                throw new Exception("BookStoreService: Error while retrieving credit card information from User DB " + e.ToString());
            }
        }
    }

    public class CreditCardTokenAuthorizationPolicy : IAuthorizationPolicy
    {
        string id;
        ClaimSet issuer;
        IEnumerable<ClaimSet> issuedClaimSets;

        public CreditCardTokenAuthorizationPolicy(ClaimSet issuedClaims)
        {
            if (issuedClaims == null)
                throw new ArgumentNullException(nameof(issuedClaims));
            this.issuer = issuedClaims.Issuer;
            this.issuedClaimSets = new ClaimSet[] { issuedClaims };
            this.id = Guid.NewGuid().ToString();
        }

        public ClaimSet Issuer { get { return this.issuer; } }

        public string Id { get { return this.id; } }

        public bool Evaluate(EvaluationContext context, ref object state)
        {
            foreach (ClaimSet issuance in this.issuedClaimSets)
            {
                context.AddClaimSet(this, issuance);
            }

            return true;
        }
    }
```

## <a name="displaying-the-callers-information"></a>호출자의 정보 표시

 호출자의 정보를 표시하려면 다음 샘플 코드에서와 같이 `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets`를 사용합니다. `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets`는 현재 호출자와 연관된 권한 부여 클레임을 포함합니다. 이러한 클레임은 해당 `CreditCardToken` 컬렉션의 `AuthorizationPolicies` 클래스에 의해 제공됩니다.

```csharp
bool TryGetStringClaimValue(ClaimSet claimSet, string claimType, out string claimValue)
{
    claimValue = null;
    IEnumerable<Claim> matchingClaims = claimSet.FindClaims(claimType, Rights.PossessProperty);
    if (matchingClaims == null)
        return false;
    IEnumerator<Claim> enumerator = matchingClaims.GetEnumerator();
    enumerator.MoveNext();
    claimValue = (enumerator.Current.Resource == null) ? null :
        enumerator.Current.Resource.ToString();
    return true;
}

string GetCallerCreditCardNumber()
{
     foreach (ClaimSet claimSet in
         ServiceSecurityContext.Current.AuthorizationContext.ClaimSets)
     {
         string creditCardNumber = null;
         if (TryGetStringClaimValue(claimSet,
             Constants.CreditCardNumberClaim, out creditCardNumber))
             {
                 string issuer;
                 if (!TryGetStringClaimValue(claimSet.Issuer,
                        ClaimTypes.Name, out issuer))
                 {
                     issuer = "Unknown";
                 }
                 return $"Credit card '{creditCardNumber}' issued by '{issuer}'";
        }
    }
    return "Credit card is not known";
}
```

 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.

## <a name="setup-batch-file"></a>설치 배치 파일

 이 샘플에 포함된 Setup.bat 배치 파일을 사용하면 서버 인증서 기반 보안이 필요한 IIS에서 호스트되는 응용 프로그램을 실행하도록 관련 인증서가 있는 서버를 구성할 수 있습니다. 다중 컴퓨터 구성이나 호스트되지 않는 환경에서 이 배치 파일을 사용하려면 배치 파일을 수정해야 합니다.

 아래에는 적절한 구성에서 실행할 수 있도록 배치 파일을 수정하는 데 도움이 되는 여러 관련 단원의 간략한 개요가 소개되어 있습니다.

- 서버 인증서 만들기

     `Setup.bat` 배치 파일에서 다음 행은 사용할 서버 인증서를 만듭니다. `%SERVER_NAME%`변수는 서버 이름을 지정합니다. 이 변수를 변경하여 고유의 서버 이름을 지정합니다. 이 배치 파일에서의 기본값은 localhost입니다. `%SERVER_NAME%` 변수를 변경할 경우 Client.cs 및 Service.cs 파일을 확인하여 localhost의 모든 인스턴스를 Setup.bat 스크립트에서 사용하는 서버 이름으로 대체해야 합니다.

     인증서는 `LocalMachine` 저장 위치에 있는 My(개인) 저장소에 저장됩니다. IIS에서 호스트되는 서비스의 경우 인증서는 LocalMachine 저장소에 저장됩니다. 자체 호스팅 서비스의 경우 LocalMachine 문자열을 CurrentUser로 대체하여 CurrentUser 저장소 위치에 클라이언트 인증서를 저장하도록 배치 파일을 수정해야 합니다.

    ```bat
    echo ************
    echo Server cert setup starting
    echo %SERVER_NAME%
    echo ************
    echo making server cert
    echo ************
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
    ```

- 클라이언트의 신뢰할 수 있는 인증서 저장소에 서버 인증서 설치:

     Setup.bat 배치 파일에서 다음 행은 클라이언트의 신뢰할 수 있는 사용자 저장소로 서버 인증서를 복사합니다. 이 단계는 Makecert.exe에서 생성한 인증서를 클라이언트 컴퓨터에서 절대적으로 신뢰하지는 않기 때문에 필요합니다. Microsoft에서 발급한 인증서와 같이 클라이언트가 신뢰할 수 있는 루트 인증서를 기반으로 하는 인증서가 이미 있는 경우 클라이언트 인증서 저장소를 서버 인증서로 채우는 이 단계를 수행할 필요가 없습니다.

    ```bat
    echo ************
    echo copying server cert to client's TrustedPeople store
    echo ************
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
    ```

- IIS에서 호스트되는 서비스에서 인증서 개인 키에 액세스할 수 있게 하려면 IIS에서 호스트되는 프로세스가 실행 중인 사용자 계정에 개인 키에 대한 적절한 사용 권한을 부여해야 합니다. Setup.bat 스크립트에서 마지막 단계를 통해 이 작업을 수행합니다.

    ```bat
    echo ************
    echo setting privileges on server certificates
    echo ************
    for /F "delims=" %%i in ('"%ProgramFiles%\ServiceModelSampleTools\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i
    set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE
    (ver | findstr /C:"5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R
    iisreset
    ```

> [!NOTE]
> 설치 .bat 배치 파일은 Visual Studio 2012 명령 프롬프트에서 실행 되도록 디자인 되었습니다. Visual Studio 2012 명령 프롬프트 내에서 설정 된 PATH 환경 변수는 Setup. .bat 스크립트에 필요한 실행 파일을 포함 하는 디렉터리를 가리킵니다.

#### <a name="to-set-up-and-build-the-sample"></a>샘플을 설치하고 빌드하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. 솔루션을 빌드하려면 [Windows Communication Foundation 샘플 빌드](building-the-samples.md)의 지침을 따르세요.

#### <a name="to-run-the-sample-on-the-same-computer"></a>단일 컴퓨터 구성에서 샘플을 실행하려면

1. 관리자 권한으로 Visual Studio 2012 명령 프롬프트 창을 열고 샘플 설치 폴더에서 Setup.exe를 실행 합니다. 이 작업은 샘플 실행에 필요한 모든 인증서를 설치합니다. Makecert.exe가 있는 폴더가 경로에 포함되는지 확인합니다.

> [!NOTE]
> 샘플 사용을 마쳤으면 Cleanup.bat를 실행하여 인증서를 제거해야 합니다. 다른 보안 샘플에도 동일한 인증서가 사용됩니다.  
  
1. client\bin 디렉터리에서 Client.exe를 실행합니다. 클라이언트 콘솔 애플리케이션에 클라이언트 동작이 표시됩니다.  
  
2. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
#### <a name="to-run-the-sample-across-computer"></a>다중 컴퓨터 구성에서 샘플을 실행하려면  
  
1. 서비스 컴퓨터에 서비스 이진 파일용 디렉터리를 만듭니다.  
  
2. 서비스 프로그램 파일을 서비스 컴퓨터의 서비스 디렉터리에 복사합니다. CreditCardFile.txt를 복사해야 합니다. 그렇지 않으면 클라이언트에서 보내진 신용 카드 정보의 유효성을 신용 카드 인증자에서 검사할 수 없습니다. Setup.bat 및 Cleanup.bat 파일도 서비스 컴퓨터로 복사합니다.  
  
3. 컴퓨터의 정규화된 도메인 이름을 포함하는 주체 이름을 가진 서버 인증서가 있어야 합니다. `%SERVER_NAME%` 변수를 서비스가 호스트되는 컴퓨터의 정규화된 이름으로 변경할 경우 Setup.bat를 사용하여 이러한 서버 인증서를 만들 수 있습니다. Setup.exe 파일은 관리자 권한으로 연 Visual Studio 용 개발자 명령 프롬프트에서 실행 해야 합니다.  
  
4. 서버 인증서를 클라이언트의 CurrentUser-TrustedPeople 저장소에 복사합니다. 신뢰할 수 있는 발급자에 의해 서버 인증서가 발급되지 않은 경우에만 이 작업을 수행해야 합니다.  
  
5. EchoServiceHost.cs 파일에서 인증서 주체 이름의 값을 변경하여 localhost 대신 정규화된 컴퓨터 이름을 지정합니다.  
  
6. 언어별 폴더의 \client\bin\ 폴더에서 클라이언트 프로그램 파일을 클라이언트 컴퓨터로 복사합니다.  
  
7. Client.cs 파일에서 엔드포인트의 주소 값을 서비스의 새 주소와 일치하도록 변경합니다.  
  
8. Client.cs 파일에서 서비스 X.509 인증서의 주체 이름을 localhost 대신 원격 호스트의 정규화된 컴퓨터 이름과 일치하도록 변경합니다.  
  
9. 클라이언트 컴퓨터의 명령 프롬프트 창에서 Client.exe를 실행합니다.  
  
10. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.  
  
#### <a name="to-clean-up-after-the-sample"></a>샘플 실행 후 정리를 수행하려면  
  
1. 샘플 실행을 완료했으면 샘플 폴더에서 Cleanup.bat를 실행합니다.  
