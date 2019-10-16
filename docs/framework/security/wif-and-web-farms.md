---
title: WIF 및 웹 팜
ms.date: 03/30/2017
ms.assetid: fc3cd7fa-2b45-4614-a44f-8fa9b9d15284
author: BrucePerlerMS
ms.openlocfilehash: 32d2875ebe0a46b9f9b1856ed70a30114793e492
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045246"
---
# <a name="wif-and-web-farms"></a>WIF 및 웹 팜
WIF(Windows Identity Foundation)를 사용하여 웹 팜에 배포된 RP(신뢰 당사자) 애플리케이션의 리소스를 보호하는 경우 특정 단계를 수행하여 WIF가 팜의 여러 컴퓨터에서 실행되는 RP 애플리케이션 인스턴스의 토큰을 처리할 수 있도록 해야 합니다. 이 처리에는 세션 토큰 시그니처의 유효성 검사, 세션 토큰 암호화 및 암호 해독, 세션 토큰 캐싱 및 재생된 보안 토큰 검색이 포함됩니다.  
  
 일반적인 경우 WIF가 RP 애플리케이션의 리소스를 보호하는 데 사용되는 경우 RP가 단일 컴퓨터 또는 웹 팜에서 실행되는지에 관계없이 STS(보안 토큰 서비스)에서 가져온 보안 토큰에 따라 클라이언트와 세션이 설정됩니다. 이렇게 하면 클라이언트가 WIF를 사용하여 보호되는 모든 애플리케이션 리소스에 대해 STS에서 인증하지 않아도 됩니다. WIF의 세션 처리 방법에 대한 자세한 내용은 [WIF 세션 관리](wif-session-management.md)를 참조하세요.  
  
 기본 설정이 사용되는 경우 WIF는 다음을 수행합니다.  
  
- <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> 클래스 인스턴스를 사용하여 인증에 사용된 보안 토큰에 대한 클레임 및 기타 정보와 세션 자체에 대한 정보를 전달하는 세션 토큰(<xref:System.IdentityModel.Tokens.SessionSecurityToken> 클래스 인스턴스)을 읽고 씁니다. 세션 토큰은 세션 쿠키에 패키징되어 저장됩니다. <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>에서는 기본적으로 DPAPI(데이터 보호 API)를 사용하는 <xref:System.IdentityModel.ProtectedDataCookieTransform> 클래스를 통해 세션 토큰을 보호합니다. DPAPI는 사용자 또는 컴퓨터 자격 증명을 사용하여 보호를 제공하고 사용자 프로필에 키 데이터를 저장합니다.  
  
- <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> 클래스의 메모리 내 기본 구현을 사용하여 세션 토큰을 저장하고 처리합니다.  
  
 RP 애플리케이션이 단일 컴퓨터에 배포되는 시나리오에서는 이러한 기본 설정이 작동하지만 웹 팜에 배포된 경우 각 HTTP 요청이 컴퓨터마다 실행되는 다른 RP 애플리케이션 인스턴스에 전송되고 처리될 수 있습니다. 이 시나리오에서 위에 설명한 기본 WIF 설정은 토큰 보호 및 토큰 캐싱이 둘 다 특정 컴퓨터에 종속되어 있으므로 작동하지 않습니다.  
  
 웹 팜에 RP 애플리케이션을 배포하려면 세션 토큰(및 재생된 토큰)의 처리가 특정 컴퓨터에서 실행되는 애플리케이션에 종속되지 않도록 해야 합니다. 이 작업을 수행하는 한 가지 방법은 ASP.NET `<machineKey>` 구성 요소에서 제공하는 기능을 사용하고 세션 토큰 및 재생된 토큰 처리를 위한 분산 캐싱을 제공하도록 RP 애플리케이션을 구현하는 것입니다. `<machineKey>` 요소를 사용하면 구성 파일에 토큰의 유효성 검사, 암호화, 암호 해독에 필요한 키를 지정할 수 있습니다. 웹 팜에 있는 여러 다른 컴퓨터에 동일한 키를 지정할 수 있습니다. WIF는 `<machineKey>` 요소에 지정된 키를 사용하여 토큰을 보호하는 특수 세션 토큰 처리기 <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>를 제공합니다. 이 전략을 구현하려면 다음 지침을 따르세요.  
  
- ASP.NET `<machineKey>` 요소를 구성에 사용하여 팜의 전체 컴퓨터에서 사용할 수 있는 서명 및 암호화 키를 명시적으로 지정합니다. 다음 XML은 구성 파일의 `<system.web>` 요소 아래에 있는 `<machineKey>` 요소의 사양을 보여 줍니다.  
  
    ```xml  
    <machineKey compatibilityMode="Framework45" decryptionKey="CC510D … 8925E6" validationKey="BEAC8 … 6A4B1DE" />  
    ```  
  
- 토큰 처리기 컬렉션에 추가하여 <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>를 사용하도록 애플리케이션을 구성합니다. <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>(또는 <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler> 클래스에서 파생된 임의 처리기)가 있는 경우 먼저 토큰 처리기 컬렉션에서 제거해야 합니다. <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>는 `<machineKey>` 요소에 지정된 암호화 자료를 사용하여 세션 쿠키 데이터를 보호하는 <xref:System.IdentityModel.Services.MachineKeyTransform> 클래스를 사용합니다. 다음 XML에서는 <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>를 토큰 처리기 컬렉션에 추가하는 방법을 보여 줍니다.  
  
    ```xml  
    <securityTokenHandlers>  
      <remove type="System.IdentityModel.Tokens.SessionSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
      <add type="System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    </securityTokenHandlers>  
    ```  
  
- <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache>에서 파생하고 분산 캐싱, 즉 RP를 실행할 수 있는 팜의 모든 컴퓨터에서 액세스할 수 있는 캐시를 구현합니다. 구성 파일에 [\<sessionSecurityTokenCache>](../configure-apps/file-schema/windows-identity-foundation/sessionsecuritytokencache.md) 요소를 지정하여 분산 캐시를 사용하도록 RP를 구성합니다. 파생 클래스의 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache.LoadCustomConfiguration%2A?displayProperty=nameWithType> 메서드를 재정의하여 필요한 경우 `<sessionSecurityTokenCache>` 요소의 자식 요소를 구현할 수 있습니다.  
  
    ```xml  
    <caches>  
      <sessionSecurityTokenCache type="MyCacheLibrary.MySharedSessionSecurityTokenCache, MyCacheLibrary">  
        <!--optional child configuration elements, if implemented by the derived class -->  
      </sessionSecurityTokenCache>  
    </caches>  
    ```  
  
     분산 캐싱을 구현하는 한 가지 방법은 사용자 지정 캐시에 대한 WCF 프런트 엔드를 제공하는 것입니다. WCF 캐싱 서비스를 구현하는 방법에 대한 자세한 내용은 [WCF 캐싱 서비스](#BKMK_TheWCFCachingService)를 참조하세요. RP 애플리케이션이 캐싱 서비스 호출에 사용할 수 있는 WCF 클라이언트를 구현하는 방법에 대한 자세한 내용은 [WCF 캐싱 클라이언트](#BKMK_TheWCFClient)를 참조하세요.  
  
- 응용 프로그램이 재생된 토큰을 검색하는 경우 <xref:System.IdentityModel.Tokens.TokenReplayCache>에서 파생하고 [\<tokenReplayCache>](../configure-apps/file-schema/windows-identity-foundation/tokenreplaycache.md) 구성 요소의 토큰 재생 캐싱 서비스를 가리켜 토큰 재생 캐시에 대한 유사한 분산 캐싱 전략을 따라야 합니다.  
  
> [!IMPORTANT]
> 이 항목의 모든 예제 XML 및 코드는 [ClaimsAwareWebFarm](https://go.microsoft.com/fwlink/?LinkID=248408) 샘플에서 가져온 것입니다.  
  
> [!IMPORTANT]
> 이 항목의 예제는 현재 상태대로 제공되며 수정 없이 프로덕션 코드에서 사용할 수 없습니다.  
  
<a name="BKMK_TheWCFCachingService"></a>   
## <a name="the-wcf-caching-service"></a>WCF 캐싱 서비스  
 다음 인터페이스는 WCF 캐싱 서비스와 신뢰 당사자 애플리케이션이 통신에 사용하는 WCF 클라이언트 간의 계약을 정의합니다. 기본적으로 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> 클래스의 메서드를 서비스 작업으로 노출합니다.  
  
```csharp
[ServiceContract()]  
public interface ISessionSecurityTokenCacheService  
{  
    [OperationContract]  
    void AddOrUpdate(string endpointId, string contextId, string keyGeneration, SessionSecurityToken value, DateTime expiryTime);  
  
    [OperationContract]  
    IEnumerable<SessionSecurityToken> GetAll(string endpointId, string contextId);  
  
    [OperationContract]  
    SessionSecurityToken Get(string endpointId, string contextId, string keyGeneration);  
  
    [OperationContract(Name = "RemoveAll")]  
    void RemoveAll(string endpointId, string contextId);  
  
    [OperationContract(Name = "RemoveAllByEndpointId")]  
    void RemoveAll(string endpointId);  
  
    [OperationContract]  
    void Remove(string endpointId, string contextId, string keyGeneration);  
}  
```  
  
 다음 코드에서는 WCF 캐싱 서비스의 구현을 보여 줍니다. 이 예제에서는 WIF에 의해 구현되는 메모리 내 기본 세션 토큰 캐시가 사용됩니다. 또는 데이터베이스에서 지원하는 영구 캐시를 구현할 수 있습니다. `ISessionSecurityTokenCacheService`에서는 위에 표시된 인터페이스를 정의합니다. 이 예제에서 인터페이스를 구현하는 데 필요한 일부 메서드는 간단한 설명을 위해 표시되지 않습니다.  
  
```csharp
using System;  
using System.Collections.Generic;  
using System.IdentityModel.Configuration;  
using System.IdentityModel.Tokens;  
using System.ServiceModel;  
using System.Xml;  
  
namespace WcfSessionSecurityTokenCacheService  
{  
    [ServiceBehavior(InstanceContextMode = InstanceContextMode.Single)]  
    public class SessionSecurityTokenCacheService : ISessionSecurityTokenCacheService  
    {  
        SessionSecurityTokenCache internalCache;  
  
        // sets the internal cache used by the service to the default WIF in-memory cache.  
        public SessionSecurityTokenCacheService()  
        {  
            internalCache = new IdentityModelCaches().SessionSecurityTokenCache;  
        }  
  
        ...  
  
        public SessionSecurityToken Get(string endpointId, string contextId, string keyGeneration)  
        {  
            // Delegates to the default, in-memory MruSessionSecurityTokenCache used by WIF  
            SessionSecurityToken token = internalCache.Get(new SessionSecurityTokenCacheKey(endpointId, GetContextId(contextId), GetKeyGeneration(keyGeneration)));  
            return token;  
        }  
  
        ...  
  
        private static UniqueId GetContextId(string contextIdString)  
        {  
            return contextIdString == null ? null : new UniqueId(contextIdString);  
        }  
  
        private static UniqueId GetKeyGeneration(string keyGenerationString)  
        {  
            return keyGenerationString == null ? null : new UniqueId(keyGenerationString);  
        }  
    }  
}  
```  
  
<a name="BKMK_TheWCFClient"></a>   
## <a name="the-wcf-caching-client"></a>WCF 캐싱 클라이언트  
 이 섹션에서는 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache>에서 파생되는 클래스의 구현과 캐싱 서비스에 대한 대리자 호출을 보여 줍니다. 다음 XML과 같이 [\<sessionSecurityTokenCache&gt;](../configure-apps/file-schema/windows-identity-foundation/sessionsecuritytokencache.md) 요소를 통해 이 클래스를 사용하도록 RP 애플리케이션을 구성합니다.  
  
```xml  
<caches>  
  <sessionSecurityTokenCache type="CacheLibrary.SharedSessionSecurityTokenCache, CacheLibrary">  
    <!--cacheServiceAddress points to the centralized session security token cache service running in the web farm.-->  
    <cacheServiceAddress url="http://localhost:4161/SessionSecurityTokenCacheService.svc" />  
  </sessionSecurityTokenCache>  
</caches>  
```  
  
 이 클래스는 `<sessionSecurityTokenCache>` 요소의 사용자 지정 `<cacheServiceAddress>` 자식 요소에서 서비스 엔드포인트를 가져오도록 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache.LoadCustomConfiguration%2A> 메서드를 재정의합니다. 이 엔드포인트를 사용하여 서비스와 통신할 수 있는 `ISessionSecurityTokenCacheService` 채널을 초기화합니다.  이 예제에서 <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache> 클래스를 구현하는 데 필요한 일부 메서드는 간단한 설명을 위해 표시되지 않습니다.  
  
```csharp
using System;  
using System.Configuration;  
using System.IdentityModel.Configuration;  
using System.IdentityModel.Tokens;  
using System.ServiceModel;  
using System.Xml;  
  
namespace CacheLibrary  
{  
    /// <summary>  
    /// This class acts as a proxy to the WcfSessionSecurityTokenCacheService.  
    /// </summary>  
    public class SharedSessionSecurityTokenCache : SessionSecurityTokenCache, ICustomIdentityConfiguration  
    {  
        private ISessionSecurityTokenCacheService WcfSessionSecurityTokenCacheServiceClient;  
  
        internal SharedSessionSecurityTokenCache()  
        {  
        }  
  
        /// <summary>  
        /// Creates a client channel to call the service host.  
        /// </summary>  
        protected void Initialize(string cacheServiceAddress)  
        {  
            if (this.WcfSessionSecurityTokenCacheServiceClient != null)  
            {  
                return;  
            }  
  
            ChannelFactory<ISessionSecurityTokenCacheService> cf = new ChannelFactory<ISessionSecurityTokenCacheService>(  
                new WS2007HttpBinding(SecurityMode.None),  
                new EndpointAddress(cacheServiceAddress));  
            this.WcfSessionSecurityTokenCacheServiceClient = cf.CreateChannel();  
        }  
  
        #region SessionSecurityTokenCache Members  
        // Delegates the following operations to the centralized session security token cache service in the web farm.  
  
        ...  
  
        public override SessionSecurityToken Get(SessionSecurityTokenCacheKey key)  
        {  
            return this.WcfSessionSecurityTokenCacheServiceClient.Get(key.EndpointId, GetContextIdString(key), GetKeyGenerationString(key));  
        }  
  
        ...  
  
        #endregion  
  
        #region ICustomIdentityConfiguration Members  
        // Called from configuration infrastructure to load custom elements  
        public void LoadCustomConfiguration(XmlNodeList nodeList)  
        {  
            // Retrieve the endpoint address of the centralized session security token cache service running in the web farm  
            if (nodeList.Count == 0)  
            {  
                throw new ConfigurationException("No child config element found under <sessionSecurityTokenCache>.");  
            }  
  
            XmlElement cacheServiceAddressElement = nodeList.Item(0) as XmlElement;  
            if (cacheServiceAddressElement.LocalName != "cacheServiceAddress")  
            {  
                throw new ConfigurationException("First child config element under <sessionSecurityTokenCache> is expected to be <cacheServiceAddress>.");  
            }  
  
            string cacheServiceAddress = null;  
            if (cacheServiceAddressElement.Attributes["url"] != null)  
            {  
                cacheServiceAddress = cacheServiceAddressElement.Attributes["url"].Value;  
            }  
            else  
            {  
                throw new ConfigurationException("<cacheServiceAddress> is expected to contain a 'url' attribute.");  
            }  
  
            // Initialize the proxy to the WebFarmSessionSecurityTokenCacheService  
            this.Initialize(cacheServiceAddress);  
        }  
        #endregion  
  
        private static string GetKeyGenerationString(SessionSecurityTokenCacheKey key)  
        {  
            return key.KeyGeneration == null ? null : key.KeyGeneration.ToString();  
        }  
  
        private static string GetContextIdString(SessionSecurityTokenCacheKey key)  
        {  
            return GetContextIdString(key.ContextId);  
        }  
  
        private static string GetContextIdString(UniqueId contextId)  
        {  
            return contextId == null ? null : contextId.ToString();  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Tokens.SessionSecurityTokenCache>
- <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>
- <xref:System.IdentityModel.Services.Tokens.MachineKeySessionSecurityTokenHandler>
- [WIF 세션 관리](wif-session-management.md)
