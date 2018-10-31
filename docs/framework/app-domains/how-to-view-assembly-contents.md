---
title: '방법: 어셈블리 내용 보기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- assembly manifest, viewing information
- Ildasm.exe
- MSIL Disassembler
- assemblies [.NET Framework], viewing contents
- viewing assembly information
- MSIL
- viewing MSIL information
ms.assetid: fb7baaab-4c0d-47ad-8fd3-4591cf834709
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 10ba2930dcaee6c118562e685ad49dd73c980564
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50191105"
---
# <a name="how-to-view-assembly-contents"></a>방법: 어셈블리 내용 보기
[Ildasm.exe(IL 디스어셈블러)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)를 사용하여 파일의 MSIL(Microsoft Intermediate Language) 정보를 볼 수 있습니다. 검사되는 파일이 어셈블리이면 이 정보에 어셈블리의 특성뿐만 아니라 다른 모듈 및 어셈블리에 대한 참조가 포함될 수 있습니다. 이 정보는 파일이 어셈블리 또는 어셈블리의 일부인지 여부 및 파일이 다른 모듈 또는 어셈블리에 대한 참조를 포함하는지 여부를 확인하는 데 유용할 수 있습니다.  
  
### <a name="to-display-the-contents-of-an-assembly-using-ildasmexe"></a>Ildasm.exe를 사용하여 어셈블리의 내용을 표시하려면  
  
1.  명령 프롬프트에서 **ildasm** \<*assembly name*>을 입력합니다. 예를 들어 다음 명령은 `Hello.exe` 어셈블리를 디스어셈블합니다.  
  
    ```  
    ildasm Hello.exe  
    ```  
  
### <a name="to-view-assembly-manifest-information"></a>어셈블리 매니페스트 정보를 보려면  
  
1.  MSIL 디스어셈블러 창에서 매니페스트 아이콘을 두 번 클릭합니다.  
  
## <a name="example"></a>예  
 다음 예제는 기본 "Hello, World" 프로그램으로 시작합니다. 프로그램을 컴파일한 후 Ildasm.exe를 사용하여 Hello.exe 어셈블리를 디스어셈블하고 어셈블리 매니페스트를 봅니다.  
  
 [!code-cpp[Conceptual.Assembly.Contents#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.contents/cpp/source.cpp#1)]
 [!code-csharp[Conceptual.Assembly.Contents#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.contents/cs/source.cs#1)]
 [!code-vb[Conceptual.Assembly.Contents#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.contents/vb/source.vb#1)]  
  
 Hello.exe 어셈블리에서 ildasm.exe 명령을 실행하고 IL DASM 창에서 매니페스트 아이콘을 두 번 클릭하면 다음과 같은 출력이 생성됩니다.  
  
```  
// Metadata version: v4.0.30319  
.assembly extern mscorlib  
{  
  .publickeytoken = (B7 7A 5C 56 19 34 E0 89 )                         // .z\V.4..  
  .ver 4:0:0:0  
}  
.assembly Hello  
{  
  .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilationRelaxationsAttribute::.ctor(int32) = ( 01 00 08 00 00 00 00 00 )   
  .custom instance void [mscorlib]System.Runtime.CompilerServices.RuntimeCompatibilityAttribute::.ctor() = ( 01 00 01 00 54 02 16 57 72 61 70 4E 6F 6E 45 78   // ....T..WrapNonEx  
                                                                                                             63 65 70 74 69 6F 6E 54 68 72 6F 77 73 01 )       // ceptionThrows.  
  .hash algorithm 0x00008004  
  .ver 0:0:0:0  
}  
.module Hello.exe  
// MVID: {7C2770DB-1594-438D-BAE5-98764C39CCCA}  
.imagebase 0x00400000  
.file alignment 0x00000200  
.stackreserve 0x00100000  
.subsystem 0x0003       // WINDOWS_CUI  
.corflags 0x00000001    //  ILONLY  
// Image base: 0x00600000  
```  
  
 다음 표에서는 예제에 사용된 Hello.exe 어셈블리의 어셈블리 매니페스트에 있는 각 지시문에 대해 설명합니다.  
  
|지시문|설명|  
|---------------|-----------------|  
|**.assembly extern \<** *assembly name* **>**|현재 모듈에서 참조하는 항목이 포함된 다른 어셈블리를 지정합니다(이 예제에서는 `mscorlib`).|  
|**.publickeytoken \<** *token* **>**|참조된 어셈블리의 실제 키의 토큰을 지정합니다.|  
|**.ver \<** *version number* **>**|참조된 어셈블리의 버전 번호를 지정합니다.|  
|**.assembly \<** *assembly name* **>**|어셈블리 이름을 지정합니다.|  
|**.hash algorithm \<** *int32 value* **>**|사용되는 해시 알고리즘을 지정합니다.|  
|**.ver \<** *version number* **>**|어셈블리의 버전 번호를 지정합니다.|  
|**.module \<** *file name* **>**|어셈블리를 구성하는 모듈의 이름을 지정합니다. 이 예제에서는 어셈블리가 파일 하나로만 구성됩니다.|  
|**.subsystem \<** *value* **>**|프로그램에 필요한 응용 프로그램 환경을 지정합니다. 이 예제에서 값 3은 이 실행 파일이 콘솔에서 실행됨을 나타냅니다.|  
|**.corflags**|현재 메타데이터에서 예약된 필드입니다.|  
  
 어셈블리 매니페스트에는 어셈블리의 내용에 따라 여러 다른 지시문이 포함될 수 있습니다. 어셈블리 매니페스트에 있는 지시문의 광범위한 목록은 ECMA 설명서의 "파티션 II: 메타데이터 정의 및 의미 체계" 및 "파티션 III: CIL 명령 집합"을 참조하세요. 이 설명서는 온라인으로 제공됩니다. MSDN의 [ECMA C# 및 공용 언어 인프라 표준](https://go.microsoft.com/fwlink/?LinkID=99212) 및 Ecma International 웹 사이트의 [표준 ECMA-335 - CLI(공용 언어 인프라)](https://go.microsoft.com/fwlink/?LinkID=65552)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
- [응용 프로그램 도메인 및 어셈블리](https://msdn.microsoft.com/library/433b04ae-4ba8-4849-9dbd-79194f240346)  
- [응용 프로그램 도메인 및 어셈블리 방법 항목](../../../docs/framework/app-domains/application-domains-and-assemblies-how-to-topics.md)  
- [Ildasm.exe(IL 디스어셈블러)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)
