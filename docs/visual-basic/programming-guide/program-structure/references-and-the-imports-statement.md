---
title: 참조 및 Imports 문(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- assemblies [Visual Basic], namespaces
- references [Visual Basic], assembly
- namespaces [Visual Basic], assemblies
- referencing assemblies
- Imports statement [Visual Basic], referencing assemblies
- assemblies [Visual Basic], references
ms.assetid: 38149bd4-0a6f-4b31-b5f8-94a8c33f1600
ms.openlocfilehash: 5b810af86f8659ffbe27d23d36aece408516a9bd
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972053"
---
# <a name="references-and-the-imports-statement-visual-basic"></a>참조 및 Imports 문(Visual Basic)
**프로젝트** 메뉴에서 **참조 추가** 명령을 선택 하 여 프로젝트에서 외부 개체를 사용할 수 있도록 설정할 수 있습니다. Visual Basic의 참조는 형식 라이브러리와 같지만 추가 정보를 포함 하는 어셈블리를 가리킬 수 있습니다.  
  
## <a name="the-imports-statement"></a>Imports 문  
 어셈블리는 하나 이상의 네임 스페이스를 포함 합니다. 어셈블리에 대 한 참조를 추가 하는 경우 모듈 내에서 해당 `Imports` 어셈블리의 네임 스페이스에 대 한 표시 여부를 제어 하는 문을 모듈에 추가할 수도 있습니다. `Imports` 문은 고유한 참조를 제공 하는 데 필요한 네임 스페이스의 일부만 사용할 수 있도록 하는 범위 지정 컨텍스트를 제공 합니다.  
  
 `Imports` 문에는 다음 구문이 있습니다.  
  
 `Imports [Aliasname =] Namespace`  
  
 `Aliasname`코드 내에서 가져온 네임 스페이스를 참조 하는 데 사용할 수 있는 짧은 이름을 참조 합니다. `Namespace`는 프로젝트 참조, 프로젝트 내의 정의 또는 이전 `Imports` 문을 통해 사용할 수 있는 네임 스페이스입니다.  
  
 모듈은 개수에 `Imports` 관계 없이 문을 포함할 수 있습니다. 이러한 `Option` 문은 문 (있는 경우)이 아니라 다른 코드 앞에 나와야 합니다.  
  
> [!NOTE]
> 프로젝트 참조 `Imports` 를 문이나 `Declare` 문과 혼동 하지 마십시오. 프로젝트 참조는 어셈블리의 개체와 같은 외부 개체를 Visual Basic 프로젝트에서 사용할 수 있도록 합니다. `Imports` 문은 프로젝트 참조에 대 한 액세스를 간소화 하는 데 사용 되지만 이러한 개체에 대 한 액세스는 제공 하지 않습니다. `Declare` 문은 DLL (동적 연결 라이브러리)에서 외부 프로시저에 대 한 참조를 선언 하는 데 사용 됩니다.  
  
## <a name="using-aliases-with-the-imports-statement"></a>Imports 문과 함께 별칭 사용  
 `Imports` 문을 사용 하면 참조의 정규화 된 이름을 명시적으로 입력할 필요가 없으므로 클래스의 메서드에 더 쉽게 액세스할 수 있습니다. 별칭을 사용 하면 네임 스페이스의 한 부분에만 친숙 한 이름을 할당할 수 있습니다. 예를 들어 단일 텍스트를 여러 줄에 표시 하는 캐리지 리턴/줄 바꿈 시퀀스는 <xref:Microsoft.VisualBasic.ControlChars> <xref:Microsoft.VisualBasic?displayProperty=nameWithType> 네임 스페이스에 있는 모듈의 일부입니다. 별칭 없이 프로그램에서이 상수를 사용 하려면 다음 코드를 입력 해야 합니다.  
  
 [!code-vb[VbVbalrApplication#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#3)]  
  
 `Imports`문은 항상 모듈의 `Option` 문 바로 다음에 오는 첫 번째 줄 이어야 합니다. 다음 코드 조각에서는 <xref:Microsoft.VisualBasic.ControlChars?displayProperty=nameWithType> 모듈에 별칭을 가져오고 할당 하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrApplication#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#4)]  
  
 이 네임 스페이스에 대 한 이후 참조는 훨씬 더 짧을 수 있습니다.  
  
 [!code-vb[VbVbalrApplication#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrApplication/VB/Class1.vb#5)]  
  
 `Imports` 문에 별칭 이름이 포함 되지 않은 경우에는 가져온 네임 스페이스 내에 정의 된 요소를 한정자 없이 모듈에서 사용할 수 있습니다. 별칭 이름을 지정 하는 경우 해당 네임 스페이스 내에 포함 된 이름에 대 한 한정자로 사용 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.ControlChars>
- <xref:Microsoft.VisualBasic>
- [Visual Basic 네임 스페이스](namespaces.md)
- [.NET 어셈블리](../../../standard/assembly/index.md)
- [Imports 문(.NET 네임스페이스 및 형식)](../../language-reference/statements/imports-statement-net-namespace-and-type.md)
