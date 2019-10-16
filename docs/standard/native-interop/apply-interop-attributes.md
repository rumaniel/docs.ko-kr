---
title: Interop 특성 적용
ms.date: 03/30/2017
helpviewer_keywords:
- design-time attributes
- .NET Framework, exposing components to COM
- attributes [.NET Framework], design-time functionality
- conversion-tool attributes
- attributes [.NET Framework], interop-specific
- attributes [.NET Framework], conversion-tool
- interoperation with unmanaged code, applying attributes
- interoperation with unmanaged code, exposing .NET Framework components
- COM interop, exposing COM components
- COM interop, applying attributes
ms.assetid: b6014613-641c-4912-9e2f-83a99210a037
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 27d1a8cc80db9e17000880c006ac1d7c1bd12fec
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68631497"
---
# <a name="applying-interop-attributes"></a>Interop 특성 적용
<xref:System.Runtime.InteropServices> 네임스페이스는 디자인 타임에 사용자가 적용한 특성, 변환 과정에서 COM interop 도구 및 API가 적용한 특성, 사용자 또는 COM interop가 적용한 특성 등 세 가지 범주의 interop 관련 특성을 제공합니다.  
  
 관리 코드에 특성을 적용하는 작업을 잘 모르겠으면 [특성을 사용하여 메타데이터 확장](../../../docs/standard/attributes/index.md)을 참조하세요. 다른 사용자 지정 특성과 마찬가지로, 형식, 메서드, 속성, 매개 변수, 필드 및 다른 멤버에 interop 관련 특성을 적용할 수 있습니다.  
  
## <a name="design-time-attributes"></a>디자인 타임 특성  
 디자인 타임 특성을 사용하여 COM interop 도구와 API가 수행하는 변환 프로세스의 결과를 조정할 수 있습니다. 다음 표에서는 관리되는 소스 코드에 적용할 수 있는 특성을 설명합니다. 경우에 따라 COM interop 도구가 이 표에 설명된 특성을 적용할 수도 있습니다.  
  
|특성|설명|  
|---------------|-----------------|  
|<xref:System.Runtime.InteropServices.AutomationProxyAttribute>|자동화 마샬러 또는 사용자 지정 프록시 및 스텁을 사용하여 형식의 마샬링 여부를 지정합니다.|  
|<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>|클래스에 대해 생성되는 인터페이스 형식을 제어합니다.|  
|<xref:System.Runtime.InteropServices.CoClassAttribute>|형식 라이브러리에서 가져온 원래 coclass의 CLSID를 식별합니다.<br /><br /> COM interop 도구는 일반적으로 이 특성을 적용합니다.|  
|<xref:System.Runtime.InteropServices.ComImportAttribute>|COM 형식 라이브러리에서 coclass 또는 인터페이스 정의를 가져왔음을 나타냅니다. 런타임은 이 플래그를 사용하여 형식을 활성화하고 마샬링하는 방법을 확인합니다. 이 특성은 형식을 형식 라이브러리로 다시 내보내지 않도록 차단합니다.<br /><br /> COM interop 도구는 일반적으로 이 특성을 적용합니다.|  
|<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>|등록 프로세스 중 사용자가 작성한 코드를 실행할 수 있도록, COM에서 사용하기 위해 어셈블리를 등록할 때 메서드를 호출해야 함을 나타냅니다.|  
|<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>|클래스에 대한 이벤트의 소스인 인터페이스를 식별합니다.<br /><br /> COM interop 도구는 이 특성을 적용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>|프로세스 중 사용자가 작성한 코드를 실행할 수 있도록, COM에서 어셈블리 등록을 취소할 때 메서드를 호출해야 함을 나타냅니다.|  
|<xref:System.Runtime.InteropServices.ComVisibleAttribute>|특성 값이 **false**와 같을 때 COM에 보이지 않는 형식을 렌더링합니다. 이 특성을 개별 형식 또는 전체 어셈블리에 적용하여 COM 표시 유형을 제어할 수 있습니다. 기본적으로 관리되는 모든 공용 형식이 표시됩니다. 표시하려는 경우에는 특성이 필요하지 않습니다.|  
|<xref:System.Runtime.InteropServices.DispIdAttribute>|메서드 또는 필드의 COM DISPID(디스패치 식별자)를 지정합니다. 이 특성에는 설명하는 메서드, 필드 또는 속성에 대한 DISPID가 포함됩니다.<br /><br /> COM interop 도구는 이 특성을 적용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.FieldOffsetAttribute>|**StructLayoutAttribute**와 함께 사용하고 **LayoutKind**가 명시적으로 설정된 경우 클래스 내 각 필드의 실제 위치를 나타냅니다.|  
|<xref:System.Runtime.InteropServices.GuidAttribute>|클래스, 인터페이스 또는 전체 형식 라이브러리의 GUID(Globally Unique Identifier)를 지정합니다. 특성에 전달된 문자열은 **System.Guid** 형식에 허용되는 생성자 인수인 형식이어야 합니다.<br /><br /> COM interop 도구는 이 특성을 적용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.IDispatchImplAttribute>|이중 인터페이스와 dispinterface를 COM에 노출할 때 공용 언어 런타임에서 사용하는 **IDispatch** 인터페이스 구현을 나타냅니다.|  
|<xref:System.Runtime.InteropServices.InAttribute>|데이터를 호출자로 마샬링되어야 함을 나타냅니다. 특성 매개 변수에 사용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>|관리되는 인터페이스가 COM 클라이언트(이중, IUnknown 파생 또는 IDispatch 전용)에 노출되는 방식을 제어합니다.<br /><br /> COM interop 도구는 이 특성을 적용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.LCIDConversionAttribute>|관리되지 않는 메서드 시그니처에 LCID 매개 변수가 필요함을 나타냅니다.<br /><br /> COM interop 도구는 이 특성을 적용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.MarshalAsAttribute>|필드 또는 매개 변수의 데이터가 관리 코드와 비관리 코드 간에 마샬링되어야 하는 방법을 나타냅니다. 각 데이터 형식에 기본 마샬링 동작이 있기 때문에 특성은 항상 선택 사항입니다.<br /><br /> COM interop 도구는 이 특성을 적용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.OptionalAttribute>|매개 변수가 옵션임을 나타냅니다.<br /><br /> COM interop 도구는 이 특성을 적용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.OutAttribute>|필드 또는 매개 변수의 데이터가 호출된 개체에서 호출자로 다시 마샬링되어야 함을 나타냅니다.|  
|<xref:System.Runtime.InteropServices.PreserveSigAttribute>|일반적으로 상호 운용 호출 중에 발생하는 HRESULT 또는 retval 시그니처 변환이 표시되지 않습니다. 이 특성은 마샬링 및 형식 라이브러리 내보내기에 영향을 줍니다.<br /><br /> COM interop 도구는 이 특성을 적용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.ProgIdAttribute>|.NET Framework 클래스의 ProgID를 지정합니다. 특성 클래스에 사용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.StructLayoutAttribute>|클래스 필드의 실제 레이아웃을 제어합니다.<br /><br /> COM interop 도구는 이 특성을 적용할 수 있습니다.|  
  
## <a name="conversion-tool-attributes"></a>변환 도구 특성  
 다음 표에서는 변환 프로세스 중 COM interop 도구가 적용하는 특성을 설명합니다. 디자인 타임에는 이러한 특성을 적용하지 않습니다.  
  
|특성|설명|  
|---------------|-----------------|  
|<xref:System.Runtime.InteropServices.ComAliasNameAttribute>|매개 변수 또는 필드 형식의 COM 별칭을 나타냅니다. 특성 매개 변수, 필드 또는 반환 값에 사용할 수 있습니다.|  
|<xref:System.Runtime.InteropServices.ComConversionLossAttribute>|형식 라이브러리에서 어셈블리로 가져올 때 클래스 또는 인터페이스에 대한 정보가 손실되었음을 나타냅니다.|  
|<xref:System.Runtime.InteropServices.ComEventInterfaceAttribute>|소스 인터페이스 및 이벤트 인터페이스의 메서드를 구현하는 클래스를 식별합니다.|  
|<xref:System.Runtime.InteropServices.ImportedFromTypeLibAttribute>|원래 COM 형식 라이브러리에서 어셈블리를 가져왔음을 나타냅니다. 이 특성에는 원래 형식 라이브러리의 형식 라이브러리 정의가 포함되어 있습니다.|  
|<xref:System.Runtime.InteropServices.TypeLibFuncAttribute>|원래 COM 형식 라이브러리에서 이 함수에 대해 가져온 **FUNCFLAGS**를 포함합니다.|  
|<xref:System.Runtime.InteropServices.TypeLibTypeAttribute>|원래 COM 형식 라이브러리에서 이 형식에 대해 가져온 **TYPEFLAGS**를 포함합니다.|  
|<xref:System.Runtime.InteropServices.TypeLibVarAttribute>|원래 COM 형식 라이브러리에서 이 변수에 대해 가져온 **VARFLAGS**를 포함합니다.|  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Runtime.InteropServices>
- [.NET Framework 구성 요소를 COM에 노출](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)
- [특성](../../../docs/standard/attributes/index.md)
- [상호 운용할 .NET 형식의 정규화](../../../docs/standard/native-interop/qualify-net-types-for-interoperation.md)
- [COM용 .NET Framework 어셈블리 패키징](../../../docs/framework/interop/packaging-an-assembly-for-com.md)
