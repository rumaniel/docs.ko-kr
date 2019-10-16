---
title: '방법: 인터페이스 멤버를 명시적으로 구현 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- interfaces [C#], explicitly implementing
ms.assetid: 514cde76-f981-474e-8b40-9493619f899c
ms.openlocfilehash: 5ef8b42fe5ca07548d52b88720ea4845d2408bb1
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589213"
---
# <a name="how-to-explicitly-implement-interface-members-c-programming-guide"></a>방법: 인터페이스 멤버를 명시적으로 구현(C# 프로그래밍 가이드)
이 예제에서는 [interface](../../language-reference/keywords/interface.md) `IDimensions` 및 `Box` 클래스를 선언합니다. 이 클래스는 인터페이스 멤버 `getLength` 및 `getWidth`를 명시적으로 구현합니다. 멤버는 인터페이스 인스턴스 `dimensions`를 통해 액세스합니다.  
  
## <a name="example"></a>예  
 [!code-csharp[csProgGuideInheritance#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#8)]  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
  
- `Main` 메서드의 다음 줄은 컴파일 오류를 생성하므로 주석으로 처리되었습니다. 명시적으로 구현된 인터페이스 멤버는 [class](../../language-reference/keywords/class.md) 인스턴스에서 액세스할 수 없습니다.  
  
     [!code-csharp[csProgGuideInheritance#45](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#45)]  
  
- 또한 `Main` 메서드의 다음 줄은 메서드가 인터페이스 인스턴스에서 호출되기 때문에 상자 크기를 성공적으로 출력합니다.  
  
     [!code-csharp[csProgGuideInheritance#46](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#46)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](../classes-and-structs/index.md)
- [인터페이스](./index.md)
- [방법: 두 인터페이스의 멤버를 명시적으로 구현](./how-to-explicitly-implement-members-of-two-interfaces.md)
