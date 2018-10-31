---
title: '방법: 시간 기반 캐시 정책을 사용자 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time-based cache policies
- customizing time-based cache policies
- cache [.NET Framework], time-based policies
ms.assetid: 8d84f936-2376-4356-9264-03162e0f9279
ms.openlocfilehash: 1a9e0d3197dcba63ef5497613e216a96868a03da
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50182452"
---
# <a name="how-to-customize-a-time-based-cache-policy"></a>방법: 시간 기반 캐시 정책을 사용자 지정
시간 기반 캐시 정책을 만들 경우 최대 기간, 최소 새로 고침, 최대 부실 또는 캐시 동기화 날짜에 대한 값을 지정하여 캐싱 동작을 사용자 지정할 수 있습니다. <xref:System.Net.Cache.HttpRequestCachePolicy> 개체는 이러한 값의 유효한 조합을 지정할 수 있는 여러 가지 생성자를 제공합니다.  
  
### <a name="to-create-a-time-based-cache-policy-that-uses-a-cache-synchronization-date"></a>캐시 동기화 날짜를 사용하는 시간 기반 캐시 정책을 만들려면  
  
-   <xref:System.DateTime> 개체를 <xref:System.Net.Cache.HttpRequestCachePolicy> 생성자에 전달하여 캐시 동기화 날짜를 사용하는 시간 기반 캐시 정책을 만듭니다.  
  
    ```csharp  
    public static HttpRequestCachePolicy CreateLastSyncPolicy(DateTime when)  
    {  
        HttpRequestCachePolicy policy =   
            new HttpRequestCachePolicy(when);  
        Console.WriteLine("When: {0}", when);  
        Console.WriteLine(policy.ToString());  
        return policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Function CreateLastSyncPolicy([when] As DateTime) As HttpRequestCachePolicy  
        Dim policy As New HttpRequestCachePolicy([when])  
        Console.WriteLine("When: {0}", [when])  
        Console.WriteLine(policy.ToString())  
        Return policy  
    End Function  
    ```  
  
 출력은 다음과 비슷합니다.  
  
```  
When: 1/14/2004 8:07:30 AM  
Level:Default CacheSyncDate:1/14/2004 8:07:30 AM  
```  
  
### <a name="to-create-a-time-based-cache-policy-that-is-based-on-minimum-freshness"></a>최소 새로 고침을 기반으로 하는 시간 기반 캐시 정책을 만들려면  
  
-   <xref:System.Net.Cache.HttpCacheAgeControl.MinFresh>를 `cacheAgeControl` 매개 변수 값으로 지정하고 <xref:System.TimeSpan> 개체를 <xref:System.Net.Cache.HttpRequestCachePolicy> 생성자에 전달하여 최소 새로 고침을 기반으로 하는 시간 기반 캐시 정책을 만듭니다.  
  
    ```csharp  
    public static HttpRequestCachePolicy CreateMinFreshPolicy(TimeSpan span)  
    {  
        HttpRequestCachePolicy policy =   
            new HttpRequestCachePolicy(HttpCacheAgeControl.MinFresh, span);  
        Console.WriteLine(policy.ToString());  
        return policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Function CreateMinFreshPolicy(span As TimeSpan) As HttpRequestCachePolicy  
        Dim policy As New HttpRequestCachePolicy(HttpCacheAgeControl.MinFresh, span)  
        Console.WriteLine(policy.ToString())  
        Return policy  
    End Function  
    ```  
  
 다음 호출의 경우:  
  
```  
CreateMinFreshPolicy(new TimeSpan(1,0,0));  
```  
  
```  
Level:Default MinFresh:3600  
```  
  
### <a name="to-create-a-time-based-cache-policy-that-is-based-on-minimum-freshness-and-maximum-age"></a>최소 새로 고침 및 최대 기간을 기반으로 하는 시간 기반 캐시 정책을 만들려면  
  
-   <xref:System.Net.Cache.HttpCacheAgeControl.MaxAgeAndMinFresh>를 `cacheAgeControl` 매개 변수 값으로 지정하고 두 개의 <xref:System.TimeSpan> 개체를 <xref:System.Net.Cache.HttpRequestCachePolicy> 생성자에 전달하여 최소 새로 고침 및 최대 기간을 기반으로 하는 시간 기반 캐시 정책을 만듭니다. 하나의 개체는 리소스의 최대 기간을 지정하고 두 번째 개체는 캐시에서 반환된 개체에 허용되는 최소 새로 고침을 지정합니다.  
  
    ```csharp  
    public static HttpRequestCachePolicy CreateFreshAndAgePolicy(TimeSpan freshMinimum, TimeSpan ageMaximum)  
    {  
        HttpRequestCachePolicy policy =   
        new HttpRequestCachePolicy(HttpCacheAgeControl.MaxAgeAndMinFresh, ageMaximum, freshMinimum);  
        Console.WriteLine(policy.ToString());  
        return policy;  
    }  
    ```  
  
    ```vb  
    Public Shared Function CreateFreshAndAgePolicy(freshMinimum As TimeSpan, ageMaximum As TimeSpan) As HttpRequestCachePolicy  
        Dim policy As New HttpRequestCachePolicy(HttpCacheAgeControl.MaxAgeAndMinFresh, ageMaximum, freshMinimum)  
        Console.WriteLine(policy.ToString())  
        Return policy  
    End Function  
    ```  
  
 다음 호출의 경우:  
  
```  
CreateFreshAndAgePolicy(new TimeSpan(5,0,0), new TimeSpan(10,0,0));  
```  
  
```  
Level:Default MaxAge:36000 MinFresh:18000  
```  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 응용 프로그램에 대한 캐시 관리](../../../docs/framework/network-programming/cache-management-for-network-applications.md)  
 [캐시 정책](../../../docs/framework/network-programming/cache-policy.md)  
 [위치 기반 캐시 정책](../../../docs/framework/network-programming/location-based-cache-policies.md)  
 [시간 기반 캐시 정책](../../../docs/framework/network-programming/time-based-cache-policies.md)  
 [\<requestCaching> 요소(네트워크 설정)](../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)
