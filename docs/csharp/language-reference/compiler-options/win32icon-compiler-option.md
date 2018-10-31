---
title: -win32icon(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /win32icon
helpviewer_keywords:
- win32icon compiler option [C#]
- /win32icon compiler option [C#]
- -win32icon compiler option [C#]
ms.assetid: 756d9b6d-ab07-41b7-ba58-5bd88f711138
ms.openlocfilehash: 5014b1da714f8e29f869d4641da93796a607aa4d
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48027795"
---
# <a name="-win32icon-c-compiler-options"></a>-win32icon(C# 컴파일러 옵션)
**-win32icon** 옵션은 .ico 파일을 출력 파일에 삽입하여 파일 탐색기에서 출력 파일을 원하는 모양으로 표시합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-win32icon:filename  
```  
  
## <a name="arguments"></a>인수  
 `filename`  
 출력 파일에 추가하려는 .ico 파일입니다.  
  
## <a name="remarks"></a>설명  
 .ico 파일은 [리소스 컴파일러](/windows/desktop/menurc/resource-compiler)로 만들 수 있습니다. 리소스 컴파일러는 Visual C++ 프로그램을 컴파일할 때 실행되며 .rc 파일에서 .iso 파일이 만들어집니다.  
  
 .NET Framework 리소스 파일을 참조하려면 [-linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)를, 첨부하려면 [-resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md)를 참조하세요. .res 파일을 가져오려면 [-win32res](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md)를 참조하세요.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1.  프로젝트 **속성** 페이지를 엽니다.  
  
2.  **응용 프로그램** 속성 페이지를 클릭합니다.  
  
3.  **응용 프로그램 아이콘** 속성을 수정합니다.  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.ProjectProperties3.ApplicationIcon%2A>을 참조하세요.  
  
## <a name="example"></a>예  
 `in.cs`를 컴파일하고 .ico 파일 `rf.ico`를 첨부하여 `in.exe`를 생성합니다.  
  
```console  
csc -win32icon:rf.ico in.cs  
```  
  
## <a name="see-also"></a>참고 항목  

- [C# 컴파일러 옵션](../../../csharp/language-reference/compiler-options/index.md)  
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
