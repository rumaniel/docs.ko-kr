---
title: '방법: 수동으로 래퍼 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- wrappers, creating manually
ms.assetid: cc2a70d8-6a58-4071-a8cf-ce28c018c09b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5db0ec9050c74b27d3ee25a99dcf8e2319835ffb
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894223"
---
# <a name="how-to-create-wrappers-manually"></a>방법: 수동으로 래퍼 만들기
관리 소스 코드에서 COM 형식을 수동으로 선언하도록 결정할 경우 기존 IDL(Interface Definition Language) 파일 또는 형식 라이브러리에서 시작하는 것이 좋습니다. IDL 파일이 없거나 형식 라이브러리 파일을 생성할 수 없으면 관리되는 선언을 만들고 결과 어셈블리를 형식 라이브러리에 내보내는 방식으로 COM 형식을 시뮬레이트할 수 있습니다.  
  
### <a name="to-simulate-com-types-from-managed-source"></a>관리되는 소스에서 COM 형식을 시뮬레이트하려면  
  
1. CLS(공용 언어 사양)를 준수하는 언어로 형식을 선언하고 파일을 컴파일합니다.  
  
2. [형식 라이브러리 내보내기(Tlbexp.exe)](../tools/tlbexp-exe-type-library-exporter.md)를 사용하여 형식이 포함된 어셈블리를 내보냅니다.  
  
3. 내보낸 COM 형식 라이브러리를 기반으로 COM 지향 관리되는 형식을 선언합니다.  
  
### <a name="to-create-a-runtime-callable-wrapper-rcw"></a>RCW(런타임 호출 가능 래퍼)를 만들려면  
  
1. IDL 파일 또는 형식 라이브러리 파일이 있다고 가정하고 사용자 지정 RCW에 포함할 클래스와 인터페이스를 결정합니다. 애플리케이션에서 직접적으로나 간접적으로 사용하지 않을 형식을 제외할 수 있습니다.  
  
2. 소스 파일을 CLS 규격 언어로 만들고 형식을 선언합니다. 가져오기 변환 프로세스에 대한 자세한 내용은 [형식 라이브러리와 어셈블리 간 변환 요약](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))을 참조하세요. 사실상 사용자 지정 RCW를 만들면 [형식 라이브러리 가져오기(Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md)에서 제공된 형식 변환 활동을 수동으로 수행하는 것입니다. 이 섹션 뒤에 나오는 예제에서는 IDL 또는 형식 라이브러리 파일에 있는 형식과 C# 코드에서 이 형식에 해당하는 형식을 보여 줍니다.  
  
3. 선언이 완료되면 다른 관리 소스 코드를 컴파일할 때 파일을 컴파일합니다.  
  
4. Tlbimp.exe로 가져온 형식처럼 일부 형식에는 코드에 직접 추가할 수 있는 추가적인 정보가 필요합니다. 자세한 내용은 [방법: interop 어셈블리 편집](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8zbc969t(v=vs.100))을 참조하세요.  
  
## <a name="example"></a>예  
 다음 코드에서는 IDL의 `ISATest` 인터페이스와 `SATest` 클래스 및 C# 소스 코드에서 이들 항목에 해당하는 형식의 예를 보여 줍니다.  
  
 **IDL 또는 형식 라이브러리 파일**  
  
```cpp
 [  
object,  
uuid(40A8C65D-2448-447A-B786-64682CBEF133),  
dual,  
helpstring("ISATest Interface"),  
pointer_default(unique)  
 ]  
interface ISATest : IDispatch  
 {  
[id(1), helpstring("method InSArray")]   
HRESULT InSArray([in] SAFEARRAY(int) *ppsa, [out,retval] int *pSum);  
 };  
 [  
uuid(116CCA1E-7E39-4515-9849-90790DA6431E),  
helpstring("SATest Class")  
 ]  
coclass SATest  
 {  
  [default] interface ISATest;  
 };  
```  
  
 **관리 소스 코드의 래퍼**  
  
```csharp  
using System;  
using System.Runtime.InteropServices;  
using System.Runtime.CompilerServices;  
  
[assembly:Guid("E4A992B8-6F5C-442C-96E7-C4778924C753")]  
[assembly:ImportedFromTypeLib("SAServerLib")]  
namespace SAServer  
{  
 [ComImport]  
 [Guid("40A8C65D-2448-447A-B786-64682CBEF133")]  
 [TypeLibType(TypeLibTypeFlags.FLicensed)]  
 public interface ISATest  
 {  
  [DispId(1)]  
  //[MethodImpl(MethodImplOptions.InternalCall,  
  // MethodCodeType=MethodCodeType.Runtime)]  
  int InSArray( [MarshalAs(UnmanagedType.SafeArray,  
      SafeArraySubType=VarEnum.VT_I4)] ref int[] param );  
 }   
 [ComImport]  
 [Guid("116CCA1E-7E39-4515-9849-90790DA6431E")]  
 [ClassInterface(ClassInterfaceType.None)]  
 [TypeLibType(TypeLibTypeFlags.FCanCreate)]  
 public class SATest : ISATest  
 {  
  [DispId(1)]  
  [MethodImpl(MethodImplOptions.InternalCall,   
  MethodCodeType=MethodCodeType.Runtime)]  
  extern int ISATest.InSArray( [MarshalAs(UnmanagedType.SafeArray,   
  SafeArraySubType=VarEnum.VT_I4)] ref int[] param );  
 }  
}  
```  
  
## <a name="see-also"></a>참고 항목

- [런타임 호출 가능 래퍼 사용자 지정](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100))
- [COM 데이터 형식](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sak564ww(v=vs.100))
- [방법: interop 어셈블리 편집](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8zbc969t(v=vs.100))
- [형식 라이브러리를 어셈블리로 변환 요약](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))
- [Tlbimp.exe(형식 라이브러리 가져오기)](../tools/tlbimp-exe-type-library-importer.md)
- [Tlbexp.exe(형식 라이브러리 내보내기)](../tools/tlbexp-exe-type-library-exporter.md)
