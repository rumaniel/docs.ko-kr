---
title: Visual Studio에서 식 트리 디버깅 (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 492cc28f-b7a2-4c47-b582-b3c437b8a5d5
ms.openlocfilehash: 3334828475ef5d933ea660ea33ae264d4ccce172
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106875"
---
# <a name="debugging-expression-trees-in-visual-studio-visual-basic"></a>Visual Studio에서 식 트리 디버깅 (Visual Basic)
애플리케이션을 디버그할 때 식 트리의 구조 및 내용을 분석할 수 있습니다. 식 트리 구조에 대한 간략한 개요를 보려면 [특수 구문](debugview-syntax.md)을 사용하여 식 트리를 나타내는 `DebugView` 속성을 사용합니다. (`DebugView`는 디버그 모드에서만 사용할 수 있습니다.)  

![Visual Studio 디버거 내의 식 트리 DebugView](media/debugging-expression-trees-in-visual-studio/debugview_vb.png)

`DebugView`는 문자열이므로 `DebugView` 레이블 옆의 돋보기 아이콘에서 **텍스트 시각화 도우미**를 선택하여 [기본 제공 텍스트 시각화 도우미](https://docs.microsoft.com/visualstudio/debugger/view-strings-visualizer#open-a-string-visualizer)를 사용하여 여러 줄에서 볼 수 있습니다.

 !['DebugView'의 결과에 적용되는 텍스트 시각화 도우미](media/debugging-expression-trees-in-visual-studio/string_visualizer_vb.png)

또는 다음과 같은 식 트리에 [사용자 지정 시각화 도우미](https://docs.microsoft.com/visualstudio/debugger/create-custom-visualizers-of-data)를 설치하여 사용할 수 있습니다.

- [읽을 수 있는 식](https://github.com/agileobjects/ReadableExpressions)([MIT 라이선스](https://github.com/agileobjects/ReadableExpressions/blob/master/LICENSE.md), [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=vs-publisher-1232914.ReadableExpressionsVisualizers)에서 사용 가능)은 식 트리를 C# 코드로 렌더링합니다.

  ![읽을 수 있는 식 시각화 도우미](media/debugging-expression-trees-in-visual-studio/readable_expressions_visualizer.png)

- [식 트리 시각화 도우미](https://github.com/zspitz/ExpressionToString#visual-studio-debugger-visualizer-for-expression-trees) ([MIT 라이선스](https://github.com/zspitz/ExpressionToString/blob/master/LICENSE))은 식 트리, 해당 속성 및 관련 개체에 대 한 그래픽 뷰를 제공 합니다. 및는 Visual Basic 코드를 사용 하 여 식 트리를 렌더링할 수 있습니다.

  ![ExpressionToString 시각화 도우미](media/debugging-expression-trees-in-visual-studio/expression_to_string_visualizer_vb.png)

### <a name="to-open-a-visualizer-for-an-expression-tree"></a>식 트리에 대한 시각화 도우미를 열려면  
  
1. **DataTips**, **조사식** 창, **자동** 창 또는 **지역** 창의 식 트리 옆에 나타나는 돋보기 아이콘을 클릭합니다.  
  
     사용 가능한 시각화 도우미의 목록이 나타납니다. 

      ![Visual Studio에서 시각화 도우미 열기](media/debugging-expression-trees-in-visual-studio/expression_tree_visualizers_vb.png)

2. 사용할 시각화 도우미를 클릭합니다.  

## <a name="see-also"></a>참고자료

- [식 트리(Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)
- [Visual Studio의 디버깅](/visualstudio/debugger/debugging-in-visual-studio)
- [Create Custom Visualizers of Data](/visualstudio/debugger/create-custom-visualizers-of-data)(데이터의 사용자 지정 시각화 도우미 만들기)
- [`DebugView` 구문](debugview-syntax.md)
