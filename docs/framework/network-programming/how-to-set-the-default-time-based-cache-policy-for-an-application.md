---
title: '방법: 애플리케이션의 기본 시간 기반 캐시 정책 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time-based cache policies
- cache [.NET Framework], time-based policies
- default time-based cache policy
ms.assetid: 6bfce066-a2e7-4add-a05e-85c12ec9f07f
ms.openlocfilehash: 0aaa26f67ef1ef191060e682690fa14de328b812
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71048095"
---
# <a name="how-to-set-the-default-time-based-cache-policy-for-an-application"></a>방법: 애플리케이션의 기본 시간 기반 캐시 정책 설정
기본 시간 기반 캐시 정책을 사용하면 [IETF(Internet Engineering Task Force)](https://www.ietf.org/) 웹 사이트에서 제공되는 RFC 2616의 섹션 13 및 14에 정의된 캐시 동작 및 캐시된 리소스와 함께 전송된 헤더를 통해 정의된 캐시 동작이 애플리케이션에 나타날 수 있습니다. 이것은 대부분의 애플리케이션에서 적절한 캐시 동작입니다.  
  
### <a name="to-set-the-default-automatic-policy-for-an-application"></a>애플리케이션에 대한 기본 자동 정책을 설정하려면  
  
1. 기본 시간 기반 정책 개체를 만듭니다.  
  
2. 정책 개체를 애플리케이션 도메인의 기본값으로 설정합니다.  
  
## <a name="example"></a>예  
 이 섹션의 두 가지 예제는 동일한 정책을 생성합니다.  
  
 다음 예제에서는 기본 시간 기반 정책을 만들고 이 정책을 애플리케이션 도메인의 기본값으로 설정합니다.  
  
```csharp  
public static void SetDefaultTimeBasedPolicy ()  
{  
    HttpRequestCachePolicy policy = new HttpRequestCachePolicy ();  
    HttpWebRequest.DefaultCachePolicy = policy ;  
}  
```  
  
```vb  
Public Shared Sub SetDefaultTimeBasedPolicy ()  
    Dim policy = New HttpRequestCachePolicy ()  
    HttpWebRequest.DefaultCachePolicy = policy  
End Sub  
```  
  
 다음 예제와 같이 <xref:System.Net.Cache.RequestCachePolicy> 클래스를 사용하여 기본 시간 기반 캐시 정책을 만들 수도 있습니다.  
  
```csharp  
public static void SetDefaultTimeBasedPolicy2()  
{  
    RequestCachePolicy policy = new RequestCachePolicy ();  
    HttpWebRequest.DefaultCachePolicy = policy ;  
}  
```  
  
```vb  
Public Shared Sub SetDefaultTimeBasedPolicy2()  
    Dim policy As New RequestCachePolicy()  
    HttpWebRequest.DefaultCachePolicy = policy  
End Sub  
```  
  
## <a name="see-also"></a>참고 항목

- [네트워크 애플리케이션에 대한 캐시 관리](cache-management-for-network-applications.md)
- [캐시 정책](cache-policy.md)
- [위치 기반 캐시 정책](location-based-cache-policies.md)
- [시간 기반 캐시 정책](time-based-cache-policies.md)
- [\<requestCaching> 요소(네트워크 설정)](../configure-apps/file-schema/network/requestcaching-element-network-settings.md)
