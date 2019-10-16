---
title: -리소스 (Visual Basic)
ms.date: 03/13/2018
helpviewer_keywords:
- /resource compiler option [Visual Basic]
- -resource compiler option [Visual Basic]
- /res compiler option [Visual Basic]
- res compiler option [Visual Basic]
- -res compiler option [Visual Basic]
- resource compiler option [Visual Basic]
ms.assetid: eee2f227-91f2-4f2b-a9d6-1c51c5320858
ms.openlocfilehash: 5bedc346381f6de293933dce14a8c5c3044b246f
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005198"
---
# <a name="-resource-visual-basic"></a>-리소스 (Visual Basic)
관리되는 리소스를 어셈블리에 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-resource:filename[,identifier[,public|private]]  
```

로 구분하거나 여러  

```console
-res:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>인수  
  
|용어|정의|  
|---|---|  
|`filename`|필수. 출력 파일에 포함할 리소스 파일의 이름입니다. 기본적으로 `filename`은 어셈블리에서 public입니다. 공백을 포함 하는 경우 파일 이름을 따옴표 ("")로 묶습니다.|  
|`identifier`|(선택 사항) 리소스의 논리적 이름입니다. 로드 하는 데 사용 되는 이름입니다. 기본값은 파일 이름입니다. 필요에 따라 다음을 비롯 하 여 리소스가 어셈블리 매니페스트에서 공용 인지 아니면 개인 인지를 지정할 수 있습니다. `-res:filename.res, myname.res, public`|  
  
## <a name="remarks"></a>설명  
 리소스 파일을 출력 파일에 배치 하지 않고 어셈블리에 리소스를 연결 하려면 `-linkresource`을 사용 합니다.  
  
 예를 들어 `filename`이 [resgen.exe (리소스 파일 생성기)](../../../framework/tools/resgen-exe-resource-file-generator.md) 나 개발 환경에서 만든 .NET Framework 리소스 파일인 경우 <xref:System.Resources> 네임 스페이스의 멤버를 사용 하 여 액세스할 수 있습니다 (자세한 내용은 <xref:System.Resources.ResourceManager> 참조). 런타임에 다른 모든 리소스에 액세스 하려면 <xref:System.Reflection.Assembly.GetManifestResourceInfo%2A>, <xref:System.Reflection.Assembly.GetManifestResourceNames%2A> 또는 <xref:System.Reflection.Assembly.GetManifestResourceStream%2A> 메서드 중 하나를 사용 합니다.  
  
 `-resource`의 약식은 `-res`입니다.  
  
 Visual Studio IDE에서 `-resource`을 설정 하는 방법에 대 한 자세한 내용은 [응용 프로그램 리소스 관리 (.net)](/visualstudio/ide/managing-application-resources-dotnet)를 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 코드는-0 @no__t 컴파일하고-1 @no__t 리소스 파일을 연결 합니다.  
  
```console
vbc -res:rf.resource in.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md)
- [-linkresource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/linkresource.md)
- [-target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
