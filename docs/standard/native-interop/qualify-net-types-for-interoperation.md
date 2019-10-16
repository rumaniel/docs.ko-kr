---
title: COM 상호 운용성을 위한 .NET 형식의 정규화
ms.date: 03/30/2017
helpviewer_keywords:
- exposing .NET Framework components to COM
- COM interop, qualifying .NET types
- qualifying .NET types for interoperation
- interoperation with unmanaged code, qualifying .NET types
- interoperation with unmanaged code, exposing .NET Framework components
- COM interop, exposing COM components
ms.assetid: 4b8afb52-fb8d-4e65-b47c-fd82956a3cdd
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 04ebdf5d3e5caf2c34823528703f75cf972f302f
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68631397"
---
# <a name="qualifying-net-types-for-com-interoperation"></a>COM 상호 운용성을 위한 .NET 형식의 정규화
어셈블리에서 형식을 COM 애플리케이션으로 노출하려는 경우 디자인 타임에 COM interop의 요구 사항을 고려하세요. 다음 지침을 준수하면 관리되는 형식(클래스, 인터페이스, 구조체 및 열거형)이 COM 형식과 원활하게 통합됩니다.  
  
- 클래스에서 인터페이스를 명시적으로 구현해야 합니다.  
  
     COM interop에서 클래스의 모든 멤버와 기본 클래스의 멤버를 포함하는 인터페이스를 자동으로 생성하는 메커니즘을 제공하지만 명시적 인터페이스를 제공하는 것이 훨씬 좋습니다. 자동으로 생성된 인터페이스는 클래스 인터페이스라고 합니다. 지침은 [클래스 인터페이스 소개](com-callable-wrapper.md#introducing-the-class-interface)를 참조하세요.  
  
     IDL(Interface Definition Language) 또는 이와 동등한 사항을 사용할 필요 없이 Visual Basic, C# 및 C++를 사용하여 코드에 인터페이스 정의를 통합할 수 있습니다. 구문에 대한 세부 정보는 언어 문서를 참조하세요.  
  
- 관리되는 형식은 public이어야 합니다.  
  
     어셈블리의 public 형식만 등록하고 형식 라이브러리로 내보냅니다. 결과적으로 public 형식만 COM에 표시됩니다.  
  
     관리되는 형식은 COM에 노출되지 않을 수 있는 기타 관리 코드에 기능을 공개합니다. 예를 들어 매개 변수화된 생성자, 정적 메서드 및 상수 필드는 COM 클라이언트에 노출되지 않습니다. 또한 런타임 시 데이터를 형식에 대해 마샬링할 때 데이터가 복사되거나 변환될 수 있습니다.  
  
- 메서드, 속성, 필드 및 이벤트는 public이어야 합니다.  
  
     public 형식의 멤버를 COM에 표시하려는 경우 해당 멤버도 public이어야 합니다. <xref:System.Runtime.InteropServices.ComVisibleAttribute>를 적용하여 어셈블리의 가시성, public 형식 또는 public 형식의 공용 멤버를 제한할 수 있습니다. 기본적으로 모든 public 형식 및 멤버만 표시됩니다.  
  
- 형식에는 COM에서 활성화될 public 매개 변수가 없는 생성자가 있어야 합니다.  
  
     관리되는 public 형식만 COM에 표시됩니다. 그러나 public 매개 변수가 없는 생성자(인수 없는 생성자)가 없으면 COM 클라이언트에서 형식을 만들 수 없습니다. 다른 방법으로 활성화된 경우에도 COM 클라이언트에서 여전히 형식을 사용할 수 있습니다.  
  
- 형식은 추상일 수 없습니다.  
  
     COM 클라이언트와 .NET 클라이언트 모두 추상 형식을 만들 수 없습니다.  
  
 COM으로 내보낼 때 관리되는 형식의 상속 계층 구조가 평면화됩니다. 관리되는 환경과 관리되지 않는 환경에서는 버전 관리도 다릅니다. COM에 노출된 형식에는 관리되는 다른 형식과 동일한 버전 관리 특성이 없습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Runtime.InteropServices.ComVisibleAttribute>
- [.NET Framework 구성 요소를 COM에 노출](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)
- [클래스 인터페이스 소개](com-callable-wrapper.md#introducing-the-class-interface)
- [Interop 특성 적용](../../../docs/standard/native-interop/apply-interop-attributes.md)
- [COM용 .NET Framework 어셈블리 패키징](../../../docs/framework/interop/packaging-an-assembly-for-com.md)
