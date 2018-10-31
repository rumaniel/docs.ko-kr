---
title: Blittable 형식 및 비 Blittable 형식
ms.date: 03/30/2017
helpviewer_keywords:
- interop marshaling, blittable types
- blittable types, interop marshaling
ms.assetid: d03b050e-2916-49a0-99ba-f19316e5c1b3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8b4c1d213c2ed87126fc5eb9995050e14f9214bd
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199840"
---
# <a name="blittable-and-non-blittable-types"></a>Blittable 형식 및 비 Blittable 형식
대부분의 데이터 형식은 관리되는 메모리와 관리되지 않는 메모리 둘 다에서 공통된 표현을 사용하며 interop 마샬러의 특별한 처리가 필요하지 않습니다. 이러한 형식은 관리 코드와 비관리 코드 간에 전달될 때 변환이 필요하지 않기 때문에 *blittable 형식*이라고 합니다.  
  
 플랫폼 호출에서 반환되는 구조는 blittable 형식이어야 합니다. 플랫폼 호출은 비 blittable 구조를 반환 형식으로 지원하지 않습니다.  
  
 <xref:System> 네임스페이스의 다음 형식은 blittable 형식입니다.  
  
-   <xref:System.Byte?displayProperty=nameWithType>  
  
-   <xref:System.SByte?displayProperty=nameWithType>  
  
-   <xref:System.Int16?displayProperty=nameWithType>  
  
-   <xref:System.UInt16?displayProperty=nameWithType>  
  
-   <xref:System.Int32?displayProperty=nameWithType>  
  
-   <xref:System.UInt32?displayProperty=nameWithType>  
  
-   <xref:System.Int64?displayProperty=nameWithType>  
  
-   <xref:System.UInt64?displayProperty=nameWithType>  
  
-   <xref:System.IntPtr?displayProperty=nameWithType>  
  
-   <xref:System.UIntPtr?displayProperty=nameWithType>  
  
-   <xref:System.Single?displayProperty=nameWithType>  
  
-   <xref:System.Double?displayProperty=nameWithType>  
  
 다음 복합 형식도 blittable 형식입니다.  
  
-   정수 배열 등 blittable 형식의 1차원 배열. 그러나 blittable 형식의 변수 배열을 포함하는 형식 자체는 blittable이 아닙니다.  
  
-   blittable 형식(및 서식이 지정된 형식으로 마샬링된 경우 클래스)만 포함하는 서식이 지정된 값 형식. 서식이 지정된 값 형식에 대한 자세한 내용은 [값 형식에 대한 기본 마샬링](https://msdn.microsoft.com/library/4d9a876c-e05a-40ba-bd85-bd22877f984a(v=vs.100))을 참조하세요.  
  
 개체 참조는 blittable이 아닙니다. 여기에는 그 자체가 blittable인 개체에 대한 참조 배열이 포함됩니다. 예를 들어 blittable인 구조를 정의할 수 있지만 이러한 구조에 대한 참조 배열을 포함하는 blittable 형식을 정의할 수 없습니다.  
  
 최적화로, blittable 형식의 배열 및 blittable 멤버만 포함하는 클래스는 마샬링 중 복사되지 않고 [고정](../../../docs/framework/interop/copying-and-pinning.md)됩니다. 호출자와 호출 수신자가 동일한 아파트에 있을 경우 이러한 형식은 In/Out 매개 변수로 마샬링되는 것처럼 보일 수 있습니다. 그러나 이러한 형식은 실제로 In 매개 변수로 마샬링되며, 인수를 In/Out 매개 변수로 마샬링하려는 경우 <xref:System.Runtime.InteropServices.InAttribute> 및 <xref:System.Runtime.InteropServices.OutAttribute> 특성을 적용해야 합니다.  
  
 관리되는 일부 데이터 형식은 관리되지 않는 환경에서 다른 표현이 필요합니다. 이러한 비 blittable 데이터 형식을 마샬링할 수 있는 형식으로 변환해야 합니다. 예를 들어 관리되는 문자열은 문자열 개체로 변환해야 마샬링할 수 있기 때문에 비 blittable 형식입니다.  
  
 다음 표에는 <xref:System> 네임스페이스의 비 blittable 형식이 나와 있습니다. 정적 메서드 또는 클래스 인스턴스를 참조하는 데이터 구조인 [대리자](https://msdn.microsoft.com/library/d176ee76-f982-494b-b03d-92e4118896e2(v=vs.100))도 비 blittable입니다.  
  
|비 blittable 형식|설명|  
|-------------------------|-----------------|  
|[System.Array](../../../docs/framework/interop/default-marshaling-for-arrays.md)|C 스타일 배열 또는 `SAFEARRAY`로 변환합니다.|  
|[System.Boolean](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/t2t3725f(v=vs.100))|`true`가 1 또는 -1인 1, 2 또는 4바이트 값으로 변환합니다.|  
|[System.Char](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/6tyybbf2(v=vs.100))|유니코드 또는 ANSI 문자로 변환합니다.|  
|[System.Class](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/s0968xy8(v=vs.100))|클래스 인터페이스로 변환합니다.|  
|[System.Object](../../../docs/framework/interop/default-marshaling-for-objects.md)|Variant 또는 인터페이스로 변환합니다.|  
|[System.Mdarray](../../../docs/framework/interop/default-marshaling-for-arrays.md)|C 스타일 배열 또는 `SAFEARRAY`로 변환합니다.|  
|[System.String](../../../docs/framework/interop/default-marshaling-for-strings.md)|null 참조로 종료되는 문자열 또는 BSTR로 변환합니다.|  
|[System.Valuetype](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/0t2cwe11(v=vs.100))|고정된 메모리 레이아웃을 사용하는 구조로 변환합니다.|  
|[System.Szarray](../../../docs/framework/interop/default-marshaling-for-arrays.md)|C 스타일 배열 또는 `SAFEARRAY`로 변환합니다.|  
  
 클래스 및 개체 형식은 COM interop에서만 지원됩니다. [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)], C# 및 C++의 해당 형식은 [클래스 라이브러리 개요](../../../docs/standard/class-library-overview.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [기본 마샬링 동작](../../../docs/framework/interop/default-marshaling-behavior.md)
