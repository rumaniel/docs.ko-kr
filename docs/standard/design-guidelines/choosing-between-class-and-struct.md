---
title: 클래스와 구조체 간의 선택
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], structures
- class library design guidelines [.NET Framework], classes
- structures [.NET Framework], vs. classes
- classes [.NET Framework], design guidelines
- type design guidelines, structures
- structures [.NET Framework], design guidelines
- classes [.NET Framework], vs. structures
- type design guidelines, classes
ms.assetid: f8b8ec9b-0ba7-4dea-aadf-a93395cd804f
author: KrzysztofCwalina
ms.openlocfilehash: 5041368ca1a440698c399c935ac72aba2002c3ba
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615275"
---
# <a name="choosing-between-class-and-struct"></a>클래스와 구조체 간의 선택
모든 프레임 워크 디자이너 얼굴 기본 디자인 결정 사항 중 하나 (참조 형식) 클래스 또는 구조체 (값 형식) 형식이 디자인 여부입니다. 값 형식과 참조 동작의 차이점 이해 하는 것은이 선택 하는 중요 합니다.  
  
 첫 번째 스택의 반면 스택에 하거나 값 형식 할당 된 또는 포함 하는 인라인 형식 및 할당 취소 될 때 참조 형식 힙에 할당 되 고 가비지가 수집은 생각 값 형식과 참조 형식 간의 차이점 해제 또는 포함 하는 형식 가져옵니다 할당 취소 된 경우. 따라서 할당 및 할당 취소 값 형식의 일반 할당 및 할당 취소 참조 형식의 보다 저렴 한에 있습니다.  
  
 다음으로, 형식은 참조의 배열 힙에 있는 참조 형식의 인스턴스에 대 한만 참조 아웃 아웃오브 라인, 배열 요소를 의미를 할당 합니다. 값 형식 배열의 배열 요소 값 형식의 실제 인스턴스 즉 인라인으로 할당 됩니다. 따라서, 할당 및 할당 취소 값 형식 배열의 할당 및 할당 취소는 참조 형식 배열 보다 훨씬 저렴 합니다. 또한은 대부분의 경우 값 형식 배열 참조의 효율이 훨씬을 나타냅니다.  
  
 다음 차이점 메모리 사용량 관련이 있습니다. 값 형식은 참조 형식 또는 구현 하는 인터페이스 중 하나를 변환할 때는 boxed 가져옵니다. Unboxed 받게 경우 값 형식으로 다시 캐스팅 합니다. 상자 개체 힙에 할당 되는 가비지 수집, 너무 boxing 및 unboxing 되는 힙, 가비지 수집기 및 궁극적으로 응용 프로그램의 성능에 부정적인 영향을 줄을 수도 있습니다.  반면, 참조 형식 캐스팅 하는 이러한 boxing 되지 않습니다 발생 합니다. (자세한 내용은 [Boxing 및 Unboxing](../../csharp/programming-guide/types/boxing-and-unboxing.md)).
  
 다음으로, 참조 형식 할당 값 형식 할당 전체 값을 복사 하는 반면 참조를 복사 합니다. 따라서 큰 참조 형식의 할당은 큰 값 형식 할당 보다 저렴 합니다.  
  
 마지막으로, 참조 형식은 값 형식이 값으로 전달 되는 반면 참조로 전달 됩니다. 참조 형식의 인스턴스에 대 한 변경 내용을 인스턴스를 가리키는 모든 참조를 영향을 줍니다. 값 형식 인스턴스 값으로 전달 될 때 복사 됩니다. 값 형식 인스턴스의 변경 되 면 물론 바뀌지 않습니다 복사본 중 하나입니다. 복사본을 사용자에 의해 명시적으로 생성 하지는 인수는 전달 또는 반환 값이 반환 됩니다 때 암시적으로 만들어지는 하지만 때문에 값 형식을 변경할 수 있는 많은 사용자에 게 혼동을 줄 수 있습니다. 따라서 값 형식을 변경할 수 없어야 합니다.  
  
 일반적으로 대부분의 프레임 워크에서 형식 클래스 여야 합니다. 그러나 경우도, 있는 값 형식의 특성 있도록 구조체를 사용 하는 것이 적합 합니다.  
  
 **✓ CONSIDER** 형식 인스턴스의 작고 일반적으로 수명이 또는 일반적으로 다른 개체에 포함 된 경우 클래스 대신 구조체를 정의 합니다.  
  
 **X AVOID** 형식에는 다음과 같은 특성을 모두 하지 않으면 구조체를 정의 합니다.  
  
- 단일 값을 기본 형식과 비슷한를 논리적으로 나타내는 (`int`, `double`등.).  
  
- 인스턴스 크기를 16 바이트를 있습니다.  
  
- 변경할 수는 없습니다.  
  
- 자주 넣을 않아도 됩니다.  
  
 다른 모든 경우에 클래스 형식을 정의 해야 합니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [형식 디자인 지침](../../../docs/standard/design-guidelines/type.md)
- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
