---
title: -sdkpath
ms.date: 07/20/2015
f1_keywords:
- sdkpath
- -sdkpath
helpviewer_keywords:
- -sdkpath compiler option [Visual Basic]
- /sdkpath compiler option [Visual Basic]
- sdkpath compiler option [Visual Basic]
ms.assetid: fec8a3f1-b791-4a37-8af7-344859f8212d
ms.openlocfilehash: bf665082f079901ec45122ce7797090b7519fafe
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50200851"
---
# <a name="-sdkpath"></a>-sdkpath
Mscorlib.dll 및 Microsoft.VisualBasic.dll의 위치를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
-sdkpath:path  
```  
  
## <a name="arguments"></a>인수  
 `path`  
 Mscorlib.dll 및 Microsoft.VisualBasic.dll 컴파일에 사용할의 버전이 포함 된 디렉터리입니다. 이 경로 로드 될 때까지 확인 되지 않습니다. 디렉터리 이름을 따옴표로 묶습니다 ("")에 공백이 있는 경우.  
  
## <a name="remarks"></a>설명  
 이 옵션을 Visual Basic 컴파일러가 기본이 아닌 위치에서 mscorlib.dll 및 Microsoft.VisualBasic.dll 파일을 로드 합니다. 합니다 `-sdkpath` 옵션은 사용 하도록 설계 되었습니다 [-netcf](../../../visual-basic/reference/command-line-compiler/netcf.md)합니다. [!INCLUDE[Compact](~/includes/compact-md.md)] 이러한 서로 다른 버전을 사용 하 여 형식 및 장치에 없는 언어 기능을 사용 하지 않는 라이브러리를 지원 합니다.  
  
> [!NOTE]
>  `-sdkpath` 옵션은 Visual Studio 개발 환경 내에서 사용할 수 있는 명령줄에서 컴파일할 경우에 사용할 수 있는 것입니다. `-sdkpath` Visual Basic 장치 프로젝트를 로드 하면 옵션이 설정 됩니다.  
  
 컴파일러를 사용 하 여 Visual Basic 런타임 라이브러리에 대 한 참조 없이 컴파일하도록 할지 지정할 수 있습니다는 `-vbruntime` 컴파일러 옵션입니다. 자세한 내용은 [-vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md)합니다.  
  
## <a name="example"></a>예제  
 다음 코드에서는 `Myfile.vb` 사용 하 여 합니다 [!INCLUDE[Compact](~/includes/compact-md.md)]의 기본 설치 디렉터리에서 찾을 Mscorlib.dll 및 Microsoft.VisualBasic.dll의 버전을 사용 하는 [!INCLUDE[Compact](~/includes/compact-md.md)] C 드라이브에 합니다. 최신 버전의 사용은 일반적으로 [!INCLUDE[Compact](~/includes/compact-md.md)]합니다.  
  
```console
vbc -netcf -sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb  
```  
  
## <a name="see-also"></a>참고 항목  
 [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)  
 [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [-netcf](../../../visual-basic/reference/command-line-compiler/netcf.md)  
 [-vbruntime](../../../visual-basic/reference/command-line-compiler/vbruntime.md)
