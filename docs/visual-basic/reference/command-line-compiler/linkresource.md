---
title: -linkresource (Visual Basic)
ms.date: 03/10/2018
helpviewer_keywords:
- /linkresource compiler option [Visual Basic]
- -linkresource compiler option [Visual Basic]
- linkresource compiler option [Visual Basic]
- /linkres compiler option [Visual Basic]
- linkres compiler option [Visual Basic]
- -linkres compiler option [Visual Basic]
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
ms.openlocfilehash: dee5384696d543442f3280b9fdb535a7d9b6f863
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005494"
---
# <a name="-linkresource-visual-basic"></a>-linkresource (Visual Basic)
관리되는 리소스에 대한 링크를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-linkresource:filename[,identifier[,public|private]]  
```

로 구분하거나 여러  

```console
-linkres:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>인수  
 `filename`  
 필수. 어셈블리에 연결할 리소스 파일입니다. 파일 이름에 공백이 포함 된 경우 이름을 큰따옴표 ("")로 묶습니다.  
  
 `identifier`  
 (선택 사항) 리소스의 논리적 이름입니다. 리소스를 로드 하는 데 사용 되는 이름입니다. 기본값은 파일 이름입니다. 필요에 따라 어셈블리 매니페스트에서 파일이 공개 인지 아니면 개인 파일 인지를 지정할 수 있습니다 (예: `-linkres:filename.res,myname.res,public`). 기본적으로 `filename`은 어셈블리에서 public입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 옵션은 출력 파일에 리소스 파일을 포함 하지 않습니다. `-resource` 옵션을 사용 하 여이 작업을 수행 합니다.  
  
 @No__t-0 옵션을 사용 하려면 `-target:module` 이외의 `-target` 옵션 중 하나가 필요 합니다.  
  
 예를 들어 `filename`이 [resgen.exe (리소스 파일 생성기)](../../../framework/tools/resgen-exe-resource-file-generator.md) 를 사용 하 여 만든 .NET Framework 리소스 파일인 경우 <xref:System.Resources> 네임 스페이스의 멤버를 사용 하 여 액세스할 수 있습니다. 자세한 내용은 <xref:System.Resources.ResourceManager>을 참조하세요. 런타임에 다른 모든 리소스에 액세스 하려면 <xref:System.Reflection.Assembly> 클래스에서 `GetManifestResource`으로 시작 하는 메서드를 사용 합니다.  
  
 파일 이름은 임의의 파일 형식일 수 있습니다. 예를 들어 네이티브 DLL을 어셈블리의 일부로 설정하면 전역 어셈블리 캐시에 설치하고 어셈블리의 관리 코드에서 액세스할 수 있습니다.  
  
 `-linkresource`의 약식은 `-linkres`입니다.  
  
> [!NOTE]
> @No__t-0 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드는 `in.vb`을 컴파일하고 리소스 파일 `rf.resource`에 대 한 링크를 제공 합니다.  
  
```console  
vbc -linkresource:rf.resource in.vb  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
- [-리소스 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
