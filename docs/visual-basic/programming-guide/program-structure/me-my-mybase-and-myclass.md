---
title: Visual Basic의 Me, My, MyBase 및 MyClass
ms.date: 07/20/2015
f1_keywords:
- MyClass
- vb.Me
- MyBase
- vb.MyBase
- Me
- vb.MyClass
- vb.This
- vb.My
helpviewer_keywords:
- My object
- self-reference [Visual Basic], Me keyword
- MyClass keyword [Visual Basic], relationship to similar programming elements
- Me keyword [Visual Basic], relationship to similar programming elements
- Me keyword [Visual Basic], referring to the current instance of an object
- Me keyword [Visual Basic]
- self-reference
- current instance [Visual Basic], Me keyword
- MyBase keyword [Visual Basic], relationship to similar programming elements
ms.assetid: f8e241ae-b1ed-4886-9aa0-08c632154029
ms.openlocfilehash: 7df146e09a1d7cd730f4cf539d6823f7ced44bd1
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002537"
---
# <a name="me-my-mybase-and-myclass-in-visual-basic"></a>Visual Basic의 Me, My, MyBase 및 MyClass
`Me`, `My`, `MyBase`, Visual Basic의 `MyClass`은 이름이 비슷하지만 용도가 다릅니다. 이 항목에서는 이러한 각 엔터티를 구별 하기 위해 설명 합니다.  
  
## <a name="me"></a>Me  
 @No__t-0 키워드는 코드가 현재 실행 되 고 있는 클래스 또는 구조체의 특정 인스턴스를 참조 하는 방법을 제공 합니다. `Me`은 개체 변수 또는 현재 인스턴스를 참조 하는 구조체 변수와 같은 동작을 수행 합니다. @No__t-0은 현재 실행 중인 클래스 또는 구조체의 인스턴스에 대 한 정보를 다른 클래스, 구조체 또는 모듈의 프로시저에 전달 하는 데 특히 유용 합니다.  
  
 예를 들어 모듈에 다음 절차가 있는 경우를 가정 합니다.  
  
```vb  
Sub ChangeFormColor(FormName As Form)  
   Randomize()  
   FormName.BackColor = Color.FromArgb(Rnd() * 256, Rnd() * 256, Rnd() * 256)  
End Sub  
```  
  
 다음 문을 사용 하 여이 프로시저를 호출 하 고 <xref:System.Windows.Forms.Form> 클래스의 현재 인스턴스를 인수로 전달할 수 있습니다.  
  
```vb  
ChangeFormColor(Me)  
```  
  
## <a name="my"></a>My  
 @No__t-0 기능을 사용 하면 다양 한 .NET Framework 클래스에 쉽고 직관적으로 액세스할 수 있으므로 Visual Basic 사용자가 컴퓨터, 응용 프로그램, 설정, 리소스 등을 조작할 수 있습니다.  
  
## <a name="mybase"></a>Mybase.new  
 @No__t-0 키워드는 클래스의 현재 인스턴스에 대 한 기본 클래스를 참조 하는 개체 변수 처럼 동작 합니다. `MyBase`은 파생 클래스에서 재정의 되거나 숨겨진 기본 클래스 멤버에 액세스 하는 데 주로 사용 됩니다. `MyBase.New`은 파생 된 클래스 생성자에서 기본 클래스 생성자를 명시적으로 호출 하는 데 사용 됩니다.  
  
## <a name="myclass"></a>MyClass  
 @No__t-0 키워드는 원래 구현 된 클래스의 현재 인스턴스를 참조 하는 개체 변수 처럼 동작 합니다. `MyClass`은 `Me`과 유사 하지만 메서드가-2 @no__t 된 것 처럼이에 대 한 모든 메서드 호출을 처리 합니다.  
  
## <a name="see-also"></a>참조

- [상속 기본 사항](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
