---
title: '방법: 응용 프로그램에 대해 위치 기반 캐시 정책 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- expliciting defining cache behavior
- location-based cache policies
- local cache
- request cache policies
- cache [.NET Framework], location-based policies
ms.assetid: 683bb88e-3411-4f46-9686-3411b6ba511c
ms.openlocfilehash: e47b7de00941a8da24052c21f28e91391cff390d
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50193684"
---
# <a name="how-to-set-a-location-based-cache-policy-for-an-application"></a>방법: 응용 프로그램에 대해 위치 기반 캐시 정책 설정
위치 기반 캐시 정책을 사용하면 응용 프로그램이 요청된 리소스의 위치를 기반으로 캐싱 동작을 명시적으로 정의할 수 있습니다. 이 항목에서는 캐시 정책을 프로그래밍 방식으로 설정하는 방법을 보여 줍니다. 구성 파일을 사용하여 응용 프로그램에 대한 정책을 설정하는 방법에 대한 자세한 내용은 [\<requestCaching> 요소(네트워크 설정)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)를 참조하세요.  
  
### <a name="to-set-a-location-based-cache-policy-for-an-application"></a>응용 프로그램에 대해 위치 기반 캐시 정책을 설정하려면  
  
1.  <xref:System.Net.Cache.RequestCachePolicy> 또는 <xref:System.Net.Cache.HttpRequestCachePolicy> 개체를 만듭니다.  
  
2.  정책 개체를 응용 프로그램 도메인의 기본값으로 설정합니다.  
  
### <a name="to-set-a-policy-that-takes-requested-resources-from-a-cache"></a>캐시에서 요청된 리소스를 가져오는 정책을 설정하려면  
  
-   캐시를 사용할 수 있으면 캐시에서 요청된 리소스를 가져오는 정책을 만듭니다. 사용할 수 없으면 캐시 수준을 <xref:System.Net.Cache.HttpRequestCacheLevel.CacheIfAvailable>로 설정하여 요청을 서버에 보냅니다. 원격 캐시를 포함하여 클라이언트와 서버 간에 캐시를 통해 요청을 수행할 수 있습니다.  
  
    ```csharp  
    public static void UseCacheIfAvailable()  
    {  
        HttpRequestCachePolicy policy = new HttpRequestCachePolicy  
            (HttpRequestCacheLevel.CacheIfAvailable);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub UseCacheIfAvailable()  
        Dim policy As New HttpRequestCachePolicy _  
             (HttpRequestCacheLevel.CacheIfAvailable)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### <a name="to-set-a-policy-that-prevents-any-cache-from-supplying-resources"></a>캐시가 리소스를 제공하지 못하도록 제한하는 정책을 설정하려면  
  
-   캐시 수준을 <xref:System.Net.Cache.HttpRequestCacheLevel.NoCacheNoStore>로 설정하여 캐시가 요청된 리소스를 제공하지 못하도록 제한하는 정책을 만듭니다. 이 정책 수준은 캐시가 있는 경우 로컬 캐시에서 리소스를 제거하고 원격 캐시에서도 리소스를 제거해야 함을 나타냅니다.  
  
    ```csharp  
    public static void DoNotUseCache()  
    {  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy   
            (HttpRequestCacheLevel.NoCacheNoStore);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub DoNotUseCache()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.NoCacheNoStore)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### <a name="to-set-a-policy-that-returns-requested-resources-only-if-they-are-in-the-local-cache"></a>리소스가 로컬 캐시에 있는 경우에만 요청된 리소스를 반환하는 정책을 설정하려면  
  
-   캐시 수준을 <xref:System.Net.Cache.HttpRequestCacheLevel.CacheOnly>로 설정하여 리소스가 로컬 캐시에 있는 경우에만 요청된 리소스를 반환하는 정책을 만듭니다. 요청된 리소스가 캐시에 없으면 <xref:System.Net.WebException> 예외가 throw됩니다.  
  
    ```csharp  
    public static void OnlyUseCache()  
    {  
        HttpRequestCachePolicy policy = new HttpRequestCachePolicy   
            (HttpRequestCacheLevel.CacheOnly);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub OnlyUseCache()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.CacheOnly)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### <a name="to-set-a-policy-that-prevents-the-local-cache-from-supplying-resources"></a>로컬 캐시가 리소스를 제공하지 못하도록 제한하는 정책을 설정하려면  
  
-   캐시 수준을 <xref:System.Net.Cache.HttpRequestCacheLevel.Refresh>로 설정하여 로컬 캐시가 요청된 리소스를 제공하지 못하도록 제한하는 정책을 만듭니다. 요청된 리소스가 중간 캐시에 있고 성공적으로 유효성이 다시 검증된 경우 중간 캐시는 요청된 리소스를 제공할 수 있습니다.  
  
    ```csharp  
    public static void DoNotUseLocalCache()  
    {  
     HttpRequestCachePolicy policy = new HttpRequestCachePolicy   
            (HttpRequestCacheLevel.Refresh);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub DoNotUseLocalCache()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.Refresh)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### <a name="to-set-a-policy-that-prevents-any-cache-from-supplying-requested-resources"></a>캐시가 요청된 리소스를 제공하지 못하도록 제한하는 정책을 설정하려면  
  
-   캐시 수준을 <xref:System.Net.Cache.HttpRequestCacheLevel.Reload>로 설정하여 캐시가 요청된 리소스를 제공하지 못하도록 제한하는 정책을 만듭니다. 서버에서 반환된 리소스를 캐시에 저장할 수 있습니다.  
  
    ```csharp  
    public static void SendToServer()  
    {  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy   
            (HttpRequestCacheLevel.Reload);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub SendToServer()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.Reload)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
### <a name="to-set-a-policy-that-allows-any-cache-to-supply-requested-resources-if-the-resource-on-the-server-is-not-newer-than-the-cached-copy"></a>서버의 리소스가 캐시된 복사본보다 최신 버전이 아닐 경우 캐시가 요청된 리소스를 제공하도록 허용하는 정책을 설정하려면  
  
-   캐시 수준을 <xref:System.Net.Cache.HttpRequestCacheLevel.Revalidate>로 설정하여 서버의 리소스가 캐시된 복사본보다 최신 버전이 아닐 경우 캐시가 요청된 리소스를 제공하도록 허용하는 정책을 만듭니다.  
  
    ```csharp  
    public static void CheckServer()  
    {  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy  
             (HttpRequestCacheLevel.Revalidate);  
        HttpWebRequest.DefaultCachePolicy = policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Sub CheckServer()  
        Dim policy As New HttpRequestCachePolicy _  
            (HttpRequestCacheLevel.Revalidate)  
        HttpWebRequest.DefaultCachePolicy = policy  
    End Sub  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 응용 프로그램에 대한 캐시 관리](../../../docs/framework/network-programming/cache-management-for-network-applications.md)  
 [캐시 정책](../../../docs/framework/network-programming/cache-policy.md)  
 [위치 기반 캐시 정책](../../../docs/framework/network-programming/location-based-cache-policies.md)  
 [시간 기반 캐시 정책](../../../docs/framework/network-programming/time-based-cache-policies.md)  
 [\<requestCaching> 요소(네트워크 설정)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)
