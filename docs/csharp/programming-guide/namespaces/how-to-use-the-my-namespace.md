---
title: '방법: My 네임스페이스 사용 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, My namespace access
ms.assetid: e7152414-0ea5-4c8e-bf02-c8d5bbe45ff4
ms.openlocfilehash: ff00a60d92ec6abbeb257abec76ed2812867f651
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69588868"
---
# <a name="how-to-use-the-my-namespace-c-programming-guide"></a>방법: My 네임스페이스 사용(C# 프로그래밍 가이드)
<xref:Microsoft.VisualBasic.MyServices> 네임스페이스(Visual Basic의 `My`)는 .NET Framework 클래스에 대한 쉽고 직관적인 액세스를 제공하여 컴퓨터, 애플리케이션, 설정, 리소스 등을 조작하는 코드를 작성할 수 있게 해줍니다. 원래 Visual Basic에서 사용하도록 설계되었지만 `MyServices` 네임스페이스는 C# 애플리케이션에서 사용할 수 있습니다.  
  
 Visual Basic에서 `MyServices` 네임스페이스를 사용하는 방법에 대한 자세한 내용은 [My를 사용한 개발](../../../visual-basic/developing-apps/development-with-my/index.md)을 참조하세요.  
  
## <a name="adding-a-reference"></a>참조 추가  
 솔루션에서 `MyServices` 클래스를 사용하려면 먼저 Visual Basic 라이브러리에 대한 참조를 추가해야 합니다.  
  
#### <a name="to-add-a-reference-to-the-visual-basic-library"></a>Visual Basic 라이브러리에 대한 참조를 추가하려면  
  
1. **솔루션 탐색기**에서 **참조** 노드를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 선택합니다.  
  
2. **참조** 대화 상자가 나타나면 목록 아래로 스크롤한 다음 Microsoft.VisualBasic.dll을 선택합니다.  
  
     프로그램의 시작 부분에 있는 `using` 섹션에 다음 줄을 포함할 수도 있습니다.  
  
     [!code-csharp[csProgGuideNamespaces#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces3.cs#18)]  
  
## <a name="example"></a>예  
 이 예제에서는 `MyServices` 네임스페이스에 포함된 다양한 정적 메서드를 호출합니다. 이 코드를 컴파일하려면 Microsoft.VisualBasic.DLL에 대한 참조를 프로젝트에 추가해야 합니다.  
  
 [!code-csharp[csProgGuideNamespaces#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces3.cs#19)]  
  
 `MyServices` 네임스페이스의 모든 클래스를 C# 애플리케이션에서 호출할 수 있는 것은 아닙니다. 예를 들어 <xref:Microsoft.VisualBasic.MyServices.FileSystemProxy> 클래스는 호환되지 않습니다. 이 특정한 경우에는 <xref:Microsoft.VisualBasic.FileIO.FileSystem>의 일부이고 VisualBasic.dll에도 포함된 정적 메서드를 대신 사용할 수 있습니다. 예를 들어 이러한 메서드 중 하나를 사용하여 디렉터리를 복제하는 방법은 다음과 같습니다.  
  
 [!code-csharp[csProgGuideNamespaces#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces3.cs#20)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [네임스페이스](./index.md)
- [네임스페이스 사용](./using-namespaces.md)
