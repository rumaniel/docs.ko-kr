---
title: 구조체 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 08/21/2018
helpviewer_keywords:
- C# language, structs
- structs [C#]
ms.assetid: b7cf4ff2-0eb7-4e5c-93d5-b2196b4f5d89
ms.openlocfilehash: df2a235651a2242ffe18df377dce9995af31e99f
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392456"
---
# <a name="structs-c-programming-guide"></a>구조체(C# 프로그래밍 가이드)

구조체는 [struct](../../language-reference/keywords/struct.md) 키워드를 사용하여 정의합니다. 예를 들면 다음과 같습니다.  
  
 [!code-csharp[csProgGuideObjects#39](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#39)]  
  
구조체는 클래스와 대부분 동일한 구문을 공유합니다. 구조체의 이름은 유효한 C# [식별자 이름](../inside-a-program/identifier-names.md)이어야 합니다. 구조체는 다음과 같은 방법으로 클래스보다 더 제한적입니다.  
  
- 구조체 선언 내에서 필드가 const 또는 static으로 선언된 경우가 아니면 필드를 초기화할 수 없습니다.  
- 구조체는 매개 변수 없는 생성자(매개 변수가 없는 생성자) 또는 종료자를 선언할 수 없습니다.  
- 할당 시 구조체가 복사됩니다. 구조체를 새 변수에 할당하면 모든 데이터가 복사되고, 새 복사본을 수정해도 원래 복사본의 데이터는 변경되지 않습니다. `Dictionary<string, myStruct>`와 같은 값 형식의 컬렉션으로 작업할 때 이 점을 명심해야 합니다.  
- 구조체는 참조 형식인 클래스와 달리 값 형식입니다.  
- 클래스와 달리 구조체는 `new` 연산자를 사용하지 않고 인스턴스화할 수 있습니다.  
- 구조체는 매개 변수가 있는 생성자를 선언할 수 있습니다.
- 구조체는 다른 구조체 또는 클래스에서 상속될 수 없으며, 클래스의 기본 클래스가 될 수도 없습니다. 모든 구조체는 <xref:System.Object>에서 상속하는 <xref:System.ValueType>에서 직접 상속합니다.  
- 구조체는 인터페이스를 구현할 수 있습니다.
- 변수가 nullable 값 형식으로 선언되지 않으면 구조체는 `null`일 수 없으며 구조체 변수에 `null`을 지정할 수 없습니다.
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](index.md)
- [클래스](classes.md)
- [Nullable 값 형식](../nullable-types/index.md)
- [식별자 이름](../inside-a-program/identifier-names.md)
- [구조체 사용](using-structs.md)
- [방법: 메서드에 구조체를 전달하는 것과 클래스 참조를 전달하는 것의 차이점 이해](how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method.md)
