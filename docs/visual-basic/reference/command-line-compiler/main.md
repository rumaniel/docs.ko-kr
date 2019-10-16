---
title: -main
ms.date: 03/13/2018
helpviewer_keywords:
- main compiler option [Visual Basic]
- /main compiler option [Visual Basic]
- -main compiler option [Visual Basic]
ms.assetid: 83fc339d-6652-415d-b205-b5133319b5b0
ms.openlocfilehash: 91f2a27ed9b6fb296dbb9e50fc488fd012311890
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005499"
---
# <a name="-main"></a>-main
`Sub Main` 프로시저가 포함된 클래스 또는 모듈을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-main:location  
```  
  
## <a name="arguments"></a>인수  
 `location`  
 필수. 프로그램이 시작 될 때 호출 되는 `Sub Main` 프로시저를 포함 하는 클래스 또는 모듈의 이름입니다. **-Main: module** 또는 **-main: namespace. module**형식으로 지정할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 실행 파일 또는 Windows 실행 프로그램을 만들 때이 옵션을 사용 합니다. **-Main** 옵션을 생략 하면 컴파일러가 모든 public 클래스 및 모듈에서 유효한 공유 @no__t 1을 검색 합니다.  
  
 @No__t-1 절차의 다양 한 형태에 대 한 설명은 [Visual Basic의 주 절차](../../../visual-basic/programming-guide/program-structure/main-procedure.md) 를 참조 하세요.  
  
 @No__t-0이 <xref:System.Windows.Forms.Form>에서 상속 하는 클래스인 경우 컴파일러는 클래스에 `Main` 프로시저가 없는 경우 응용 프로그램을 시작 하는 기본 `Main` 프로시저를 제공 합니다. 이를 통해 개발 환경에서 만든 명령줄에서 코드를 컴파일할 수 있습니다.  
  
 [!code-vb[VbVbalrCompiler#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/Class1.vb#16)]  
  
### <a name="to-set--main-in-the-visual-studio-integrated-development-environment"></a>Visual Studio 통합 개발 환경에서을 설정 하려면  
  
1. **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.  
  
2. **응용 프로그램** 탭을 클릭합니다.  
  
3. **응용 프로그램 프레임 워크 사용** 확인란이 선택 되어 있지 않은지 확인 합니다.  
  
4. **시작 개체** 상자에서 값을 수정 합니다.  
  
## <a name="example"></a>예제  
 다음 코드는 `T2.vb` 및 `T3.vb`을 컴파일하여 `Sub Main` 프로시저를 `Test2` 클래스에서 찾을 수 있도록 지정 합니다.  
  
```console
vbc t2.vb t3.vb -main:Test2  
```  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Visual Basic의 주 절차](../../../visual-basic/programming-guide/program-structure/main-procedure.md)
