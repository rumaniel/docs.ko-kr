---
title: LINQ to DataSet 쿼리 디버깅
ms.date: 03/30/2017
ms.assetid: f4c54015-8ce2-4c5c-8d18-7038144cc66d
ms.openlocfilehash: a82fd3e99a556daf40e5c65a16cf20278f38ea26
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785217"
---
# <a name="debugging-linq-to-dataset-queries"></a>LINQ to DataSet 쿼리 디버깅

Visual Studio는 LINQ to DataSet 코드의 디버깅을 지원 합니다. 그러나 디버깅 LINQ to DataSet 코드와 LINQ to DataSet 되지 않은 관리 코드 간에는 몇 가지 차이점이 있습니다. 단계별 실행, 중단점 설정 및 디버거 창에 표시 된 결과 보기와 같은 대부분의 디버깅 기능이 LINQ to DataSet 문에 사용 됩니다. 그러나의 지연 된 쿼리 실행에는 LINQ to DataSet 코드를 디버깅 하는 동안 고려해 야 할 부작용이 있으며 편집 하며 계속 하기를 사용 하는 데 몇 가지 제한 사항이 있습니다. 이 항목에서는 LINQ to DataSet 되지 않은 관리 코드와 비교 하 여 LINQ to DataSet에 고유한 디버깅 측면을 설명 합니다.  
  
## <a name="viewing-results"></a>결과 보기  
 DataTips, 조사식 창 및 간략 한 조사식 대화 상자를 사용 하 여 LINQ to DataSet 문의 결과를 볼 수 있습니다. 소스 창을 사용할 때 소스 창의 쿼리 위에 포인터를 올려 놓으면 DataTips가 나타납니다. LINQ to DataSet 변수를 복사 하 여 조사식 창 또는 간략 한 조사식 대화 상자에 붙여 넣을 수 있습니다. LINQ to DataSet 쿼리는 생성 되거나 선언 될 때 계산 되지 않고 쿼리가 실행 될 때에만 계산 됩니다. 이를 *지연 된 실행*이라고 합니다. 따라서 쿼리가 계산되기 전까지는 쿼리 변수에 값이 없습니다. 자세한 내용은 [LINQ to DataSet의 쿼리](queries-in-linq-to-dataset.md)를 참조 하세요.  
  
 쿼리 결과를 표시하려면 디버거에서 쿼리를 계산해야 합니다. 이 암시적 계산은 디버거에서 LINQ to DataSet 쿼리 결과를 볼 때 발생 하며 고려해 야 할 몇 가지 영향이 있습니다. 쿼리를 계산할 때마다 일정 시간이 소요됩니다. 결과 노드를 확장할 때 일정 시간이 소요됩니다. 일부 쿼리의 경우 계산을 반복하면 성능이 상당히 저하될 수 있습니다. 쿼리를 계산할 때 데이터의 값이나 프로그램의 상태가 변경되는 의도하지 않은 결과가 나타날 수 있습니다. 모든 쿼리에서 예기치 않은 결과가 나타나는 것은 아닙니다. 의도 하지 않은 결과 없이 쿼리를 안전 하 게 평가할 수 있는지 확인 하려면 쿼리를 구현 하는 코드를 이해 해야 합니다. 자세한 내용은 [부작용 및 식](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/a7a250bs(v=vs.120))을 참조 하세요.  
  
## <a name="edit-and-continue"></a>편집하며 계속하기  
 편집 하며 계속 하기는 LINQ to DataSet 쿼리의 변경을 지원 하지 않습니다. 디버깅 세션 중에 LINQ to DataSet 문을 추가, 제거 또는 변경 하면 변경 내용이 편집 하며 계속 하기에서 지원 되지 않는다는 대화 상자가 나타납니다. 이때 변경 내용을 취소할 수도 있고, 디버깅 세션을 중지하고 편집된 코드로 새 세션을 다시 시작할 수도 있습니다.  
  
 또한 편집 하며 계속 하기에서는 LINQ to DataSet 문에 사용 된 변수의 형식 또는 값을 변경할 수 없습니다. 이 경우에도 변경 내용을 취소할 수도 있고, 디버깅 세션을 중지하고 다시 시작할 수도 있습니다.  
  
 Visual Studio C# 의 visual Studio에서는 LINQ to DataSet 쿼리를 포함 하는 메서드의 코드에서 편집 하며 계속 하기를 사용할 수 없습니다.  
  
 Visual Studio의 Visual Basic에서는 LINQ to DataSet 쿼리를 포함 하는 메서드에서 LINQ to DataSet 되지 않은 코드에 대해 편집 하며 계속 하기를 사용할 수 있습니다. 변경 내용이 LINQ to DataSet 쿼리의 줄 번호에 영향을 주는 경우에도 LINQ to DataSet 문 앞에 코드를 추가 하거나 제거할 수 있습니다. LINQ to DataSet 되지 않은 코드에 대 한 Visual Basic 디버깅 환경은 LINQ to DataSet 도입 되기 전과 동일 하 게 유지 됩니다. 그러나 디버깅을 중지 하 고 변경 내용을 적용 하는 경우가 아니면 LINQ to DataSet 쿼리를 변경, 추가 또는 제거할 수 없습니다.  
  
## <a name="see-also"></a>참고자료

- [관리 코드 디버그](/visualstudio/debugger/debugging-managed-code)
- [프로그래밍 가이드](programming-guide-linq-to-dataset.md)
