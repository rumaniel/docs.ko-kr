---
title: '#pragma checksum(C# 참조)'
ms.date: 07/20/2015
f1_keywords:
- '#pragma checksum'
helpviewer_keywords:
- '#pragma checksum [C#]'
ms.assetid: 3673e4ca-6098-4ec1-890f-8fceb2a794a2
ms.openlocfilehash: 28a9ccfb9d36e648304a177294904ab1b7f18892
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48024547"
---
# <a name="pragma-checksum-c-reference"></a>#pragma checksum(C# 참조)
[!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] 페이지의 디버그를 돕기 위해 소스 파일에 대한 체크섬을 생성합니다.  
  
## <a name="syntax"></a>구문  
  
```csharp
#pragma checksum "filename" "{guid}" "checksum bytes"  
```  
  
#### <a name="parameters"></a>매개 변수  
 `"filename"`  
 변경 내용이나 업데이트를 모니터링해야 하는 파일의 이름입니다.  
  
 `"{guid}"`  
 해시 알고리즘의 GUID(Globally Unique Identifier)입니다.  
  
 `"checksum_bytes"`  
 체크섬의 바이트를 나타내는 16진수 문자열입니다. 짝수의 16진수여야 합니다. 홀수를 사용하면 컴파일 시간 경고가 발생하고 지시문이 무시됩니다.  
  
## <a name="remarks"></a>설명  
 Visual Studio 디버거는 체크섬을 사용하여 항상 올바른 소스를 찾도록 합니다. 컴파일러는 소스 파일에 대한 체크섬을 계산한 다음 출력을 PDB(프로그램 데이터베이스) 파일로 내보냅니다. 그런 다음 디버거는 PDB를 사용하여 소스 파일에 대해 계산하는 체크섬과 비교합니다.  
  
 체크섬이 .aspx 파일이 아니라 생성된 소스 파일에 대해 계산되므로 이 솔루션은 [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] 프로젝트에서 작동하지 않습니다. 이 문제를 해결하기 위해 `#pragma checksum`은 [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] 페이지에 대한 체크섬 지원을 제공합니다.  
  
 Visual C#에서 [!INCLUDE[vstecasp](~/includes/vstecasp-md.md)] 프로젝트를 만드는 경우 생성된 소스 파일에 소스가 생성되는 .aspx 파일에 대한 체크섬이 포함됩니다. 그런 다음 컴파일러는 PDB 파일에 이 정보를 씁니다.  
  
 컴파일러가 파일에서 `#pragma checksum` 지시문을 발견하지 못하면 체크섬을 계산하고 PDB 파일에 값을 씁니다.  
  
## <a name="example"></a>예  
  
```csharp
class TestClass  
{  
    static int Main()  
    {  
        #pragma checksum "file.cs" "{406EA660-64CF-4C82-B6F0-42D48172A799}" "ab007f1d23d9" // New checksum  
    }  
}  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../../../csharp/language-reference/index.md)  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [C# 전처리기 지시문](../../../csharp/language-reference/preprocessor-directives/index.md)
