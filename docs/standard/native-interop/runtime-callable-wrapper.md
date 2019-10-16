---
title: RCW
ms.date: 03/30/2017
helpviewer_keywords:
- COM interop, COM wrappers
- RCW
- COM wrappers
- runtime callable wrappers
- interoperation with unmanaged code, COM wrappers
ms.assetid: 7e542583-1e31-4e10-b523-8cf2f29cb4a4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a460ac730db85dfa8d4a8ee6949a168bc228193d
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68631387"
---
# <a name="runtime-callable-wrapper"></a>RCW
공용 언어 런타임은 RCW(런타임 호출 가능 래퍼)라는 프록시를 통해 COM 개체를 노출합니다. RCW는 .NET 클라이언트에 일반적인 개체인 것처럼 나타나지만 주요 기능이 .NET 클라이언트와 COM 개체 간의 호출을 마샬링하는 것입니다.  
  
 런타임은 개체에 있는 참조 수에 관계없이 각 COM 개체에 대해 RCW를 정확한 한 개 만듭니다. 런타임은 각 개체에 대해 프로세스당 하나의 RCW를 유지 관리합니다.  특정 애플리케이션 도메인이나 아파트에서 RCW를 만든 다음 다른 애플리케이션 도메인이나 아파트에 참조를 전달하는 경우 첫 번째 개체에 대한 프록시가 사용됩니다.  다음 그림과 같이 INew 및 INewer 인터페이스를 노출하는 COM 개체에 대한 참조가 임의 개수의 관리되는 클라이언트에 포함될 수 있습니다.  

다음 이미지에서는 런타임 호출 가능 래퍼를 통해 COM 개체에 액세스하기 위한 프로세스를 보여줍니다.

 ![RCW를 통해 COM 개체에 액세스하는 프로세스.](./media/runtime-callable-wrapper/runtime-callable-wrapper.gif)  

 형식 라이브러리에서 파생된 메타데이터를 사용하여 런타임은 호출되는 COM 개체와 해당 개체에 대한 래퍼를 둘 다 만듭니다. 각 RCW는 래핑하는 COM 개체에서 인터페이스 포인터 캐시를 유지 관리하고, RCW가 더 이상 필요하지 않으면 COM 개체에서 해당 참조를 해제합니다. 런타임은 RCW에서 가비지 컬렉션을 수행합니다.  
  
 다른 활동 중에서도 RCW는 래핑된 개체를 대신하여 관리 코드와 비관리 코드 간에 데이터를 마샬링합니다. 특히, RCW는 클라이언트와 서버 간에 서로 다른 데이터 표현이 전달될 때마다 메서드 인수 및 메서드 반환 값에 대한 마샬링을 제공합니다.  
  
 표준 래퍼는 기본 제공 마샬링 규칙을 적용합니다. 예를 들어 .NET 클라이언트가 관리되지 않는 개체에 문자열 형식을 인수의 일부로 전달하는 경우 래퍼가 문자열을 BSTR 형식으로 변환합니다. COM 개체가 관리되는 호출자에게 BSTR을 반환하는 경우 호출자는 문자열을 수신합니다. 클라이언트와 서버 둘 다 익숙한 데이터를 보내고 받습니다. 다른 형식은 변환이 필요하지 않습니다. 예를 들어 표준 래퍼는 형식을 변환하지 않고 관리 코드와 비관리 코드 간에 항상 4바이트 정수를 전달합니다.  
  
## <a name="marshaling-selected-interfaces"></a>선택한 인터페이스 마샬링  
 RCW([런타임 호출 가능 래퍼](runtime-callable-wrapper.md))의 주요 목표는 관리되는 프로그래밍 모델과 관리되지 않는 프로그래밍 모델 간의 차이를 숨기는 것입니다. 매끄러운 전환을 만들기 위해 RCW는 다음 그림과 같이 .NET 클라이언트에 노출하지 않고 선택한 COM 인터페이스를 사용합니다. 

 다음 이미지에서는 COM 인터페이스 및 런타임 호출 가능 래퍼를 보여줍니다. 
  
 ![인터페이스를 사용하는 런타임 호출 가능 래퍼 스크린샷.](./media/runtime-callable-wrapper/runtime-callable-wrapper-interfaces.gif)  
  
 초기 바인딩된 개체로 만들어진 경우 RCW는 특정 형식입니다. COM 개체가 구현하는 인터페이스를 구현하고 개체의 인터페이스에서 메서드, 속성 및 이벤트를 노출합니다. 그림에서 RCW는 INew 인터페이스를 노출하지만 **IUnknown** 및 **IDispatch** 인터페이스를 사용합니다. 또한 RCW는 INew 인터페이스의 모든 멤버를 .NET 클라이언트에 노출합니다.  
  
 RCW는 래핑하는 개체에 의해 노출되는, 다음 표에 나열된 인터페이스를 사용합니다.  
  
|인터페이스|설명|  
|---------------|-----------------|  
|**IDispatch**|리플렉션을 통해 런타임에 COM 개체에 바인딩합니다.|  
|**IErrorInfo**|오류, 소스, 도움말 파일, 도움말 컨텍스트에 대한 설명과 오류를 정의한 인터페이스의 GUID를 제공합니다(.NET 클래스의 경우 항상 **GUID_NULL**).|  
|**IProvideClassInfo**|래핑되는 COM 개체가 **IProvideClassInfo**를 구현하는 경우 RCW는 이 인터페이스에서 형식 정보를 추출하여 더 나은 형식 ID를 제공합니다.|  
|**IUnknown**|개체 ID, 형식 강제 변환 및 수명 관리에 사용됩니다.<br /><br /> -   개체 ID<br />     런타임은 각 개체에 대한 **IUnknown** 인터페이스의 값을 비교하여 COM 개체를 구분합니다.<br />-   형식 강제 변환<br />     RCW는 **QueryInterface** 메서드에 의해 수행된 동적 형식 검색을 인식합니다.<br />-   수명 관리<br />     **QueryInterface** 메서드를 통해 RCW는 관리되지 않는 개체에 대한 참조를 가져오고, 런타임이 래퍼에 대해 가비지 수집을 수행하여 관리되지 않는 개체를 해제할 때까지 유지합니다.|  
  
 필요에 따라 RCW는 래핑하는 개체에 의해 노출되는, 다음 표에 나열된 인터페이스를 사용합니다.  
  
|인터페이스|설명|  
|---------------|-----------------|  
|**IConnectionPoint** 및 **IConnectionPointContainer**|RCW는 연결 지점 이벤트 스타일을 대리자 기반 이벤트에 노출하는 개체를 변환합니다.|  
|**IDispatchEx**(.NET Framework만 해당) |클래스가 **IDispatchEx**를 구현하는 경우 RCW는 **IExpando**를 구현합니다. **IDispatchEx** 인터페이스는 **IDispatch**와 달리 멤버의 대/소문자 구분 호출, 열거형, 추가, 삭제를 가능하게 하는 **IDispatch** 인터페이스의 확장입니다.|  
|**IEnumVARIANT**|열거형을 지원하는 COM 형식이 컬렉션으로 처리될 수 있게 합니다.|  
  
## <a name="see-also"></a>참고 항목

- [COM 래퍼](com-wrappers.md)
- [COM 호출 가능 래퍼](com-callable-wrapper.md)
- [형식 라이브러리를 어셈블리로 변환 요약](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))
- [형식 라이브러리를 어셈블리로 가져오기](../../framework/interop/importing-a-type-library-as-an-assembly.md)
