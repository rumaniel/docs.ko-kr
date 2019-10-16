---
title: Tlbexp.exe(형식 라이브러리 내보내기)
ms.date: 03/30/2017
helpviewer_keywords:
- exporting type library [.NET Framework]
- exporter tool [.NET Framework]
- Tlbexp.exe
- Type Library Exporter
- type libraries [.NET Framework], exporting
ms.assetid: a487d61b-d166-467b-a7ca-d8b52fbff42d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 84ae47b984d6a1a207e6678e30991073ba02a438
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044003"
---
# <a name="tlbexpexe-type-library-exporter"></a>Tlbexp.exe(형식 라이브러리 내보내기)
형식 라이브러리 내보내기를 사용하면 공용 언어 런타임 어셈블리에 정의된 형식을 설명하는 형식 라이브러리를 생성할 수 있습니다.  
  
 이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
tlbexp assemblyName [options]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|인수|설명|  
|--------------|-----------------|  
|*assemblyName*|형식 라이브러리를 내보내려는 대상 어셈블리를 나타냅니다.|  
  
|옵션|설명|  
|------------|-----------------|  
|**/asmpath:** *directory*|어셈블리를 검색할 위치를 지정합니다. 이 옵션을 사용하는 경우 현재 디렉터리를 포함하여 참조되는 어셈블리를 검색할 위치를 명시적으로 지정해야 합니다.<br /><br /> **asmpath** 옵션을 사용하는 경우 형식 라이브러리 내보내기가 GAC(전역 어셈블리 캐시)에서 어셈블리를 찾지 않습니다.|  
|**/help**|이 도구의 명령 구문 및 옵션을 표시합니다.|  
|**/names:** *filename*|형식 라이브러리에 있는 이름을 대문자로 지정합니다. *filename* 인수는 텍스트 파일입니다. 파일의 각 줄에서 형식 라이브러리에 있는 이름을 하나씩 대문자로 지정합니다.|  
|**/nologo**|Microsoft 시작 배너를 표시하지 않습니다.|  
|**/oldnames**|형식 이름이 충돌할 경우 Tlbexp.exe에서 데코레이팅된 형식 이름을 내보내도록 합니다. .NET Framework 2.0 이전 버전에서는 이 옵션이 기본 동작이었습니다.|  
|**/out:** *file*|생성할 형식 라이브러리 파일의 이름을 지정합니다. 이 옵션을 지정하지 않으면 해당 어셈블리와 동일한 이름(실제 어셈블리 이름으로서 해당 어셈블리가 들어 있는 파일 이름과 동일하지 않을 수도 있음) 및 .tlb 확장명을 가지는 형식 라이브러리가 생성됩니다.|  
|**/silence:** `warningnumber`|지정한 경고를 표시하지 않습니다. 이 옵션은 **/silent**와 함께 사용할 수 없습니다.|  
|**/silent**|성공 메시지를 표시하지 않습니다. 이 옵션은 **/silence**와 함께 사용할 수 없습니다.|  
|**/tlbreference:** *typelibraryname*|Tlbexp.exe에서 레지스트리를 조회하지 않고 형식 라이브러리 참조를 명시적으로 확인하도록 합니다. 예를 들어, 어셈블리 B가 어셈블리 A를 참조하는 경우, 레지스트리에 지정된 형식 라이브러리에 의존하지 않고 이 옵션을 사용하여 명시적 형식 라이브러리 참조를 제공할 수 있습니다. Tlbexp.exe에서는 버전을 검사하여 형식 라이브러리 버전이 어셈블리 버전과 일치하는지 확인합니다. 일치하지 않으면 오류가 발생합니다.<br /><br /> **tlbreference** 옵션은 다른 형식으로 구현되는 인터페이스에 <xref:System.Runtime.InteropServices.ComImportAttribute> 특성이 적용되는 경우에도 레지스트리를 참조합니다.|  
|**/tlbrefpath:** *path*|참조되는 형식 라이브러리에 대한 정규화된 경로입니다.|  
|**/win32**|이 옵션은 64비트 컴퓨터에서 컴파일할 때 Tlbexp.exe가 32비트 형식 라이브러리를 생성하도록 지정합니다.|  
|**/win64**|이 옵션은 32비트 컴퓨터에서 컴파일할 때 Tlbexp.exe가 64비트 형식 라이브러리를 생성하도록 지정합니다.|  
|**/verbose**|세부 정보 표시 모드를 지정합니다. 즉, 형식 라이브러리가 생성되어야 하는 참조되는 어셈블리의 목록을 표시합니다.|  
|**/?**|이 도구의 명령 구문 및 옵션을 표시합니다.|  
  
> [!NOTE]
> Tlbexp.exe의 명령줄 옵션은 대/소문자를 구분하지 않으며 순서에 관계없이 지정할 수 있습니다. 또한, 고유하게 식별할 수 있을 정도로만 옵션을 지정하면 됩니다. 예를 들어, **/n**은 **/nologo**와 같고, **/o:** *outfile.tlb*는 **/out:** *outfile.tlb*와 같습니다.  
  
## <a name="remarks"></a>설명  
 Tlbexp.exe를 사용하여 어셈블리에 정의된 형식에 대한 정의가 들어 있는 형식 라이브러리를 생성할 수 있으며, Visual Basic 6.0과 같은 애플리케이션에서는 이렇게 생성된 형식 라이브러리를 사용하여 어셈블리에 정의된 .NET 형식에 바인딩할 수 있습니다.  
  
> [!IMPORTANT]
> Tlbexp.exe를 사용하여 Windows 메타데이터(.winmd) 파일을 내보낼 수 없습니다. Windows 런타임 어셈블리 내보내기는 지원되지 않습니다.  
  
 어셈블리는 전체가 한 번에 변환됩니다. Tlbexp.exe를 사용하여 어셈블리에 정의된 형식의 하위 집합에 대한 형식 정보를 생성할 수는 없습니다.  
  
 또한 [형식 라이브러리 가져오기(Tlbimp.exe)](tlbimp-exe-type-library-importer.md)를 사용하여 가져온 어셈블리에서 형식 라이브러리를 생성할 수도 없습니다. 대신 Tlbimp.exe를 사용하여 가져온 원본 형식 라이브러리를 참조해야 합니다. Tlbimp.exe를 사용하여 가져온 어셈블리를 참조하는 어셈블리에서 형식 라이브러리를 내보낼 수 있습니다. 아래의 예제 단원을 참조하십시오.  
  
 Tlbexp.exe를 사용하면 생성된 형식 라이브러리는 현재 작업 디렉터리 또는 출력 파일에 대해 지정된 디렉터리에 놓이며, 하나의 어셈블리에서 여러 개의 형식 라이브러리가 생성될 수도 있습니다.  
  
 Tlbexp.exe를 사용하면 형식 라이브러리는 생성되지만 등록되지는 않습니다. 즉, 형식 라이브러리의 생성 및 등록을 모두 수행하는 [어셈블리 등록 도구(Regasm.exe)](regasm-exe-assembly-registration-tool.md)와는 정반대입니다. 따라서 COM을 사용하여 형식 라이브러리를 생성 및 등록하려면 Regasm.exe를 사용하십시오.  
  
 `/win32` 또는 `/win64` 옵션을 지정하지 않으면 Tlbexp.exe는 컴파일을 수행할 컴퓨터(32비트 또는 64비트 컴퓨터)의 형식에 해당하는 32비트 또는 64비트 형식 라이브러리를 생성합니다. 크로스 컴파일의 경우 32비트 컴퓨터에서 `/win64` 옵션을 사용하여 64비트 형식 라이브러리를 생성하거나 64비트 컴퓨터에서 `/win32` 옵션을 사용하여 32비트 형식 라이브러리를 생성할 수 있습니다. 32비트 형식 라이브러리에서 <xref:System.Runtime.InteropServices.ComTypes.SYSKIND> 값은 <xref:System.Runtime.InteropServices.ComTypes.SYSKIND.SYS_WIN32>로 설정되고 64비트 형식 라이브러리에서 <xref:System.Runtime.InteropServices.ComTypes.SYSKIND> 값은 <xref:System.Runtime.InteropServices.ComTypes.SYSKIND.SYS_WIN64>로 설정됩니다. 모든 데이터 형식 변환(예: `IntPtr` 및 `UIntPtr` 같은 포인터 크기의 데이터 형식)이 적절하게 변환됩니다.  
  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성을 사용하여 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType> 또는 `VT_UNKOWN`의 `VT_DISPATCH` 값을 지정하면 Tlbexp.exe에서는 이후에 사용하는 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType> 필드를 모두 무시합니다. 예를 들어, 다음과 같은 서명을 지정할 경우  
  
```csharp
[return:MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VarEnum.VT_UNKNOWN, SafeArrayUserDefinedSubType=typeof(ConsoleKeyInfo))] public Array StructUnkSafe(){return null;}  
[return:MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VarEnum.VT_DISPATCH, SafeArrayUserDefinedSubType=typeof(ConsoleKeyInfo))] public Array StructDispSafe(){return null;}  
```  
  
 다음 형식 라이브러리가 생성됩니다.  
  
```cpp 
[id(0x60020004)]  
HRESULT StructUnkSafe([out, retval] SAFEARRAY(IUnknown*)* pRetVal);  
[id(0x60020005)]  
HRESULT StructDispSafe([out, retval] SAFEARRAY(IDispatch*)* pRetVal);  
```  
  
 Tlbexp.exe에서는 <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType> 필드를 무시합니다.  
  
 형식 라이브러리가 어셈블리의 모든 정보를 포함할 수 없으므로 변환 프로세스를 통해 내보내는 동안 일부 데이터가 삭제될 수도 있습니다. 변형 프로세스 설명 및 형식 라이브러리에 내보낸 정보에 대한 소스 식별에 대한 자세한 내용은 [어셈블리와 형식 라이브러리 간 변환 요약](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/xk1120c3(v=vs.100))을 참조하세요.  
  
 형식 라이브러리 내보내기는 <xref:System.TypedReference> 개체가 비관리 코드에서 의미가 없더라도 `VARIANT` 매개 변수가 <xref:System.TypedReference>인 메서드를 내보냅니다. <xref:System.TypedReference> 매개 변수가 있는 메서드를 내보내면 형식 라이브러리 내보내기가 경고나 오류를 생성하지 않으며 결과 형식 라이브러리를 사용하는 비관리 코드가 제대로 실행되지 않습니다.  
  
 형식 라이브러리 내보내기는 Microsoft Windows 2000 이상에서 지원됩니다.  
  
## <a name="examples"></a>예  
 다음 명령을 사용하여 `myTest.dll`에 있는 어셈블리와 동일한 이름의 형식 라이브러리를 생성합니다.  
  
```console  
tlbexp myTest.dll  
```  
  
 다음 명령을 사용하여 `clipper.tlb`라는 이름의 형식 라이브러리를 생성합니다.  
  
```console  
tlbexp myTest.dll /out:clipper.tlb  
```  
  
 다음 예제에서는 Tlbimp.exe를 사용하여 가져온 어셈블리를 참조하는 어셈블리에서 Tlbexp.exe를 사용하여 형식 라이브러리를 내보내는 방법을 보여 줍니다.  
  
 먼저, Tlbimp.exe를 사용하여 형식 라이브러리 `myLib.tlb`를 가져온 다음 이를 `myLib.dll`로 저장합니다.  
  
```console  
tlbimp myLib.tlb /out:myLib.dll  
```  
  
 다음 명령을 사용하여 앞의 예제에서 생성된 `Sample.dll,`을 참조하는 `myLib.dll`을 C# 컴파일러로 컴파일합니다.  
  
```console  
CSC Sample.cs /reference:myLib.dll /out:Sample.dll  
```  
  
 다음 명령을 사용하여 `Sample.dll`을 참조하는 `myLib.dll`에 대한 형식 라이브러리를 생성합니다.  
  
```console  
tlbexp Sample.dll  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Runtime.InteropServices.TypeLibExporterFlags>
- [도구](index.md)
- [Regasm.exe(어셈블리 등록 도구)](regasm-exe-assembly-registration-tool.md)
- [어셈블리와 형식 라이브러리 간 변환 요약](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/xk1120c3(v=vs.100))
- [Tlbimp.exe(형식 라이브러리 가져오기)](tlbimp-exe-type-library-importer.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
