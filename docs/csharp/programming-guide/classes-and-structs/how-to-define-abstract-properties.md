---
title: '방법: 추상 속성 정의 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- properties [C#], abstract
- abstract properties [C#]
ms.assetid: 672a90eb-47b9-4ae0-9914-af53852fddcb
ms.openlocfilehash: 57fd2ed3a26bf5986f9c8a1a6cae6b041811e84c
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70970894"
---
# <a name="how-to-define-abstract-properties-c-programming-guide"></a>방법: 추상 속성 정의(C# 프로그래밍 가이드)
다음 예제에서는 [abstract](../../language-reference/keywords/abstract.md) 속성을 정의하는 방법을 보여 줍니다. 추상 속성 선언은 속성 접근자의 구현을 제공하지 않습니다. 클래스가 속성을 지원하도록 선언하지만 접근자 구현은 파생 클래스에서 처리되도록 합니다. 다음 예제에서는 기본 클래스에서 상속된 추상 속성을 구현하는 방법을 보여 줍니다.  
  
 이 샘플은 개별적으로 컴파일된 파일 3개로 구성되었으며, 결과로 생성된 어셈블리는 다음 컴파일 시 참조됩니다.  
  
- abstractshape.cs: 추상 `Area` 속성이 포함된 `Shape` 클래스입니다.  
  
- shapes.cs: `Shape` 클래스의 서브클래스입니다.  
  
- shapetest.cs: 일부 `Shape` 파생 개체의 영역을 표시할 테스트 프로그램입니다.  
  
 예제를 컴파일하려면 다음 명령을 사용합니다.  
  
 `csc abstractshape.cs shapes.cs shapetest.cs`  
  
 그러면 shapetest.exe 실행 파일이 생성됩니다.  
  
## <a name="example"></a>예  
 이 파일에서는 `double` 형식의 `Area` 속성을 포함하는 `Shape` 클래스를 선언합니다.  
  
 [!code-csharp[csProgGuideInheritance#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#1)]  
  
- 속성의 한정자는 속성 선언 자체에 배치됩니다. 예:  
  
    ```csharp  
    public abstract double Area  
    ```  
  
- 추상 속성(이 예제의 `Area`)을 선언할 때는 단순히 사용할 수 있는 속성 접근자를 나타내고 구현하지 않습니다. 이 예제에서는 [get](../../language-reference/keywords/get.md) 접근자만 사용할 수 있으므로 속성은 읽기 전용입니다.  
  
## <a name="example"></a>예  
 다음 코드에서는 `Shape`의 세 가지 서브클래스와 이러한 서브클래스에서 `Area` 속성을 재정의하여 고유한 구현을 제공하는 방법을 보여 줍니다.  
  
 [!code-csharp[csProgGuideInheritance#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#2)]  
  
## <a name="example"></a>예  
 다음 코드에서는 많은 `Shape` 파생 개체를 만들고 해당 영역을 출력하는 테스트 프로그램을 보여 줍니다.  
  
 [!code-csharp[csProgGuideInheritance#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#3)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](./index.md)
- [추상/봉인된 클래스 및 클래스 멤버](./abstract-and-sealed-classes-and-class-members.md)
- [속성](./properties.md)
