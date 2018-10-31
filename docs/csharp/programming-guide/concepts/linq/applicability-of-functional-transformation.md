---
title: 함수 변환의 적용 가능 범위(C#)
ms.date: 07/20/2015
ms.assetid: c78107bd-b006-4574-a3d4-bbf808388ff3
ms.openlocfilehash: baa3866c8c2c148a3080522d7c02e28e9d0fd945
ms.sourcegitcommit: 2eb5ca4956231c1a0efd34b6a9cab6153a5438af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49086819"
---
# <a name="applicability-of-functional-transformation-c"></a>함수 변환의 적용 가능 범위(C#)
순수 함수 변환은 광범위한 상황에서 적용 가능합니다.  
  
 함수 변환 방법은 구조화된 데이터의 쿼리와 조작에 이상적으로 적합하므로 LINQ 기술과 함께 사용하기에 좋습니다. 그러나 함수 변환은 LINQ보다 적용 가능성이 훨씬 큽니다. 데이터를 변환하는 데 주로 집중하는 프로세스는 함수 변환의 대상으로 간주될 수 있습니다.  
  
 이 방법은 처음에는 적합한 대상으로 보이지 않을 수 있는 많은 문제에 적용 가능합니다. 함수 변환을 LINQ와 함께 사용하거나 별도로 사용하는 경우 다음 영역에 대한 함수 변환을 고려해야 합니다.  
  
-   XML 기반 문서. XML 언어의 제대로 구성된 데이터는 함수 변환을 통해 쉽게 조작할 수 있습니다. 자세한 내용은 [XML의 함수 변환(C#)](../../../../csharp/programming-guide/concepts/linq/functional-transformation-of-xml.md)을 참조하세요.  
  
-   다른 구조화된 파일 형식. Windows.ini 파일에서 일반 텍스트 문서에 이르는 대부분의 파일에는 분석과 변환에 적합한 구조가 있습니다.  
  
-   데이터 스트리밍 프로토콜. 데이터를 통신 프로토콜로 인코딩하고 통신 프로토콜에서 데이터를 디코딩하는 작업을 간단한 함수 변환으로 나타낼 수 있는 경우가 많습니다.  
  
-   RDBMS 및 OODBMS 데이터. XML과 같은 개체 지향 데이터베이스와 관계형 데이터베이스는 널리 사용되는 구조화된 데이터 소스입니다.  
  
-   수학, 통계 및 과학 솔루션. 이러한 분야에서는 중요한 문제를 시각화하거나, 예측하거나, 실제로 해결하는 데 도움을 주기 위해 큰 데이터 집합을 조작하는 일이 많습니다.  
  
 [순수 함수로 리팩터링(C#)](../../../../csharp/programming-guide/concepts/linq/refactoring-into-pure-functions.md)에서 설명하는 것처럼 순수 함수 사용은 함수형 프로그래밍의 예입니다. 순수 함수를 사용하면 즉각적인 혜택을 얻을 수 있을 뿐만 아니라 함수 변환 관점에서 문제에 대해 생각하는 귀중한 경험을 할 수 있습니다. 이 방법은 프로그램과 클래스 디자인에도 중요한 영향을 미칠 수 있습니다. 이는 문제가 위에서 설명한 데이터 변환 솔루션에 적합한 경우 특히 해당되는 사실입니다.  
  
 이 자습서의 범위를 벗어나긴 하지만, 함수 변환 관점의 영향을 받는 디자인은 행위자로 개체보다 프로세스에 중점을 두는 경향이 있으며, 생성되는 솔루션은 개별 개체 상태 변경 대신 일련의 대규모 변환으로 구현되기 쉽습니다.  
  
 C#에서는 명령형 방법과 함수형 방법을 모두 지원하므로 응용 프로그램에 최적인 디자인에는 두 언어의 요소가 모두 통합될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [순수 함수 변환 소개(C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)  
- [XML의 함수 변환(C#)](../../../../csharp/programming-guide/concepts/linq/functional-transformation-of-xml.md)  
- [순수 함수로 리팩터링(C#)](../../../../csharp/programming-guide/concepts/linq/refactoring-into-pure-functions.md)
