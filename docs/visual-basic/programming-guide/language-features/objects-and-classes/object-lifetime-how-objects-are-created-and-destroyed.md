---
title: '개체 수명: 개체를 만들고 제거 하는 방법 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.Constructor
helpviewer_keywords:
- destructors, object lifetime
- Sub Finalize destructor
- objects [Visual Basic], destroying
- lifetime [Visual Basic], objects
- Sub New constructor, object lifetime
- Finalize method [Visual Basic], object lifetime
- objects [Visual Basic], creating
- Class_Terminate
- Dispose method [Visual Basic], object lifetime
- Class_Initialize
- object creation [Visual Basic], object lifetime
- parameterized constructors
- objects [Visual Basic], lifetime
- objects [Visual Basic], garbage collection
- constructors [Visual Basic], object lifetime
- Sub Dispose destructor
- garbage collection [Visual Basic], Visual Basic
ms.assetid: f1ee8458-b156-44e0-9a8a-5dd171648cd8
ms.openlocfilehash: 932f56a9a277360b11c551aaa1faf819f8e07fe6
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796682"
---
# <a name="object-lifetime-how-objects-are-created-and-destroyed-visual-basic"></a>개체 수명: 개체를 만들고 제거 하는 방법 (Visual Basic)

`New` 키워드를 사용하여 클래스의 인스턴스인 개체를 만듭니다. 새 개체를 사용하기 전에 초기화 작업을 수행해야 하는 경우가 많습니다. 일반적인 초기화 작업으로는 파일 열기, 데이터베이스에 연결, 레지스트리 키의 값 읽기 등이 포함됩니다. Visual Basic는 *생성자* (초기화에 대 한 제어를 허용 하는 특수 메서드) 라는 프로시저를 사용 하 여 새 개체의 초기화를 제어 합니다.

범위를 벗어나는 개체는 CLR(공용 언어 런타임)에 의해 해제됩니다. Visual Basic은 *소멸자*라는 프로시저를 사용 하 여 시스템 리소스의 릴리스를 제어 합니다. 생성자와 소멸자를 통해 예측 가능하며 효율적인 클래스 라이브러리 만들기를 지원할 수 있습니다.

## <a name="using-constructors-and-destructors"></a>생성자 및 소멸자 사용

생성자와 소멸자는 개체 만들기 및 소멸을 제어합니다. 의 `Sub New` 및 `Sub Finalize` 프로시저 `Class_Terminate` 는`Class_Initialize` 개체를 초기화 및 제거 Visual Basic Visual Basic 6.0 이전 버전에서 사용 되는 및 메서드를 대체 합니다.

### <a name="sub-new"></a>Sub New

`Sub New` 생성자는 클래스를 만들 때 한 번만 실행할 수 있으며, 같은 클래스나 파생 클래스에서 다른 생성자의 첫 번째 코드 줄이 아닌 위치에서 명시적으로 호출할 수는 없습니다. 또한 `Sub New` 메서드의 코드는 항상 클래스의 다른 코드보다 먼저 실행됩니다. 클래스에 대 한 `Sub New` 프로시저를 `Sub New` 명시적으로 정의 하지 않은 경우 런타임에는 런타임에 생성자를 암시적으로 만듭니다. Visual Basic

클래스의 생성자를 만들려면 클래스 정의 내 임의의 위치에 `Sub New` 프로시저를 만듭니다. 매개 변수화된 생성자를 만들려면 다음 코드에 나와 있는 것처럼 다른 프로시저에 인수를 지정할 때와 마찬가지로 `Sub New`에 인수의 이름과 데이터 형식을 지정합니다.

[!code-vb[VbVbalrOOP#42](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/WhidbeyStuff.vb#42)]

다음 코드에서와 같이 생성자는 오버로드되는 경우가 많습니다.

[!code-vb[VbVbalrOOP#116](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/WhidbeyStuff.vb#116)]

다른 클래스에서 파생되는 클래스를 정의할 때 생성자의 첫 줄은 기본 클래스의 생성자에 대한 호출이어야 합니다. 단, 기본 클래스에 매개 변수가 없는 액세스 가능 생성자가 있는 경우는 예외입니다. 예를 들어 위의 생성자를 포함하는 기본 클래스에 대한 호출은 `MyBase.New(s)`가 됩니다. 그렇지 않으면 `MyBase.New` 는 선택 사항이 며 Visual Basic 런타임에서는이를 암시적으로 호출 합니다.

부모 개체의 생성자를 호출하는 코드를 작성한 후에는 `Sub New` 프로시저에 초기화 코드를 더 추가할 수 있습니다. `Sub New`는 매개 변수화된 생성자로 호출할 때 인수를 허용할 수 있습니다. 이러한 매개 변수는 생성자를 호출하는 프로시저에서 전달됩니다(예: `Dim AnObject As New ThisClass(X)`).

### <a name="sub-finalize"></a>Sub Finalize

CLR은 개체를 해제하기 전에 `Finalize` 프로시저를 정의하는 개체에 대해 `Sub Finalize` 메서드를 자동으로 호출합니다. `Finalize` 메서드는 파일을 닫고 상태 정보를 저장하는 코드와 같이 개체가 소멸되기 직전에 실행해야 하는 코드를 포함할 수 있습니다. `Sub Finalize`를 실행할 때는 성능이 약간 저하되므로 개체를 명시적으로 해제해야 하는 경우에만 `Sub Finalize` 메서드를 정의해야 합니다.

> [!NOTE]
> CLR의 가비지 수집기는 관리 되지 않는 *개체*, 즉 운영 체제가 clr 환경 외부에서 직접 실행 하는 개체를 삭제할 수 없습니다. 관리되지 않는 개체는 각각 다른 방식으로 삭제해야 하기 때문입니다. 해당 정보는 관리되지 않는 개체와 직접 연결되어 있지 않으며 개체 설명서에서 확인해야 합니다. 관리되지 않는 개체를 사용하는 클래스는 해당 `Finalize` 메서드에서 개체를 삭제해야 합니다.

`Finalize` 소멸자는 소멸자가 속한 클래스나 파생 클래스에서만 호출할 수 있는 보호된 메서드입니다. 시스템은 개체 소멸 시 `Finalize`를 자동으로 호출하므로 파생 클래스의 `Finalize` 구현 외부에서 `Finalize`를 명시적으로 호출해서는 안 됩니다.

개체가 nothing으로 설정되는 즉시 실행되는 `Class_Terminate`와는 달리, 개체 범위가 손실되는 시점과 Visual Basic에서 `Finalize` 소멸자를 호출하는 시점 사이에는 대개 지연 시간이 생깁니다. Visual Basic .net은 리소스를 즉시 해제 하기 위해 언제 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>든 지 명시적으로 호출할 수 있는 두 번째 종류의 소멸자를 허용 합니다.

> [!NOTE]
> `Finalize` 소멸자는 예외를 throw해서는 안 됩니다. 이러한 예외는 애플리케이션에서 처리할 수 없으며 throw되는 경우 애플리케이션이 종료되기 때문입니다.

### <a name="how-new-and-finalize-methods-work-in-a-class-hierarchy"></a>클래스 계층 구조에서 New 및 Finalize 메서드가 작동하는 방식

클래스의 인스턴스를 만들 때마다 CLR(공용 언어 런타임)은 `New` 프로시저가 개체에 있으면 해당 프로시저의 실행을 시도합니다. `New`는 개체의 다른 코드가 실행되기 전에 새 개체를 초기화하는 데 사용되는 `constructor`라는 프로시저 형식입니다. `New` 생성자를 사용하여 파일을 열고, 데이터베이스에 연결하고, 변수를 초기화하고, 개체를 사용하려면 수행해야 하는 기타 작업을 처리할 수 있습니다.

파생 클래스의 인스턴스를 만들 때는 기본 클래스의 `Sub New` 생성자가 먼저 실행되고 파생 클래스의 생성자가 실행됩니다. `Sub New` 생성자의 첫 번째 코드 줄은 `MyBase.New()` 구문을 사용하여 클래스 계층 구조에서 바로 위에 있는 클래스의 생성자를 호출하기 때문입니다. 그 다음에는 기본 클래스의 생성자에 도달할 때까지 클래스 계층 구조의 각 클래스에 대해 `Sub New` 생성자가 호출됩니다. 기본 클래스의 생성자에 도달하면 기본 클래스 생성자의 코드가 실행되며, 모든 파생 클래스 내 각 생성자의 코드와 대부분의 파생 클래스 내 코드가 마지막으로 실행됩니다.

![클래스 계층 구조 생성자 및 상속을 보여 주는 스크린샷](./media/object-lifetime-how-objects-are-created-and-destroyed/subnew-constructor-inheritance.gif)

CLR은 개체가 더 이상 필요하지 않으면 메모리를 해제하기 전에 해당 개체에 대해 <xref:System.Object.Finalize%2A> 메서드를 호출합니다. <xref:System.Object.Finalize%2A> 메서드는 상태 정보 저장, 데이터베이스에 대한 연결과 파일 닫기 그리고 개체를 해제하기 전에 수행해야 하는 기타 작업 등의 정리 작업을 수행하므로 `destructor`라고 합니다.

![Finalize 메서드 소멸자를 보여 주는 스크린샷](./media/object-lifetime-how-objects-are-created-and-destroyed/finalize-method-destructor.gif)

## <a name="idisposable-interface"></a>IDisposable 인터페이스

클래스 인스턴스는 Windows 핸들 및 데이터베이스 연결과 같이 CLR에서 관리하지 않는 리소스를 제어하는 경우가 많습니다. 이러한 리소스는 클래스의 `Finalize` 메서드에서 삭제되어야 하므로 가비지 수집기가 개체를 소멸시킬 때 해제됩니다. 그러나 가비지 컬렉션기는 CLR에 사용 가능한 메모리가 더 필요할 때만 개체를 제거합니다. 즉, 개체가 범위를 벗어난 후 오랜 시간이 지날 때까지 리소스가 해제되지 않을 수도 있습니다.

가비지 수집을 보완하기 위해 클래스는 <xref:System.IDisposable> 인터페이스를 구현하는 경우 시스템 리소스를 실제로 관리하는 메커니즘을 제공할 수 있습니다. <xref:System.IDisposable>에는 클라이언트가 개체 사용을 완료할 때 호출해야 하는 <xref:System.IDisposable.Dispose%2A>라는 메서드가 있습니다. <xref:System.IDisposable.Dispose%2A> 메서드를 사용하면 리소스를 즉시 해제하고 데이터베이스 연결 및 파일 닫기와 같은 작업을 수행할 수 있습니다. `Finalize` 소멸자와 달리 <xref:System.IDisposable.Dispose%2A> 메서드는 자동으로 호출되지 않기 때문에 리소스를 즉시 해제하려는 경우 클래스의 클라이언트가 <xref:System.IDisposable.Dispose%2A>를 명시적으로 호출해야 합니다.

### <a name="implementing-idisposable"></a>IDisposable 구현

<xref:System.IDisposable> 인터페이스를 구현하는 클래스는 다음 코드 섹션을 포함해야 합니다.

- 개체가 삭제되었는지 여부를 추적하는 필드

  ```vb
  Protected disposed As Boolean = False
  ```

- 클래스 리소스를 해제하는 <xref:System.IDisposable.Dispose%2A>의 오버로드. 기본 클래스의 <xref:System.IDisposable.Dispose%2A> 및 `Finalize` 메서드가 이 메서드를 호출해야 합니다.

  ```vb
  Protected Overridable Sub Dispose(ByVal disposing As Boolean)
      If Not Me.disposed Then
          If disposing Then
              ' Insert code to free managed resources.
          End If
          ' Insert code to free unmanaged resources.
      End If
      Me.disposed = True
  End Sub
  ```

- 다음 코드만 포함하는 <xref:System.IDisposable.Dispose%2A>의 구현

  ```vb
  Public Sub Dispose() Implements IDisposable.Dispose
      Dispose(True)
      GC.SuppressFinalize(Me)
  End Sub
  ```

- 다음 코드만 포함하는 `Finalize` 메서드의 재정의

  ```vb
  Protected Overrides Sub Finalize()
      Dispose(False)
      MyBase.Finalize()
  End Sub
  ```

### <a name="deriving-from-a-class-that-implements-idisposable"></a>IDisposable을 구현하는 클래스에서 파생

<xref:System.IDisposable> 인터페이스를 구현하는 기본 클래스에서 파생되는 클래스는 삭제해야 하는 추가 리소스를 사용하는 경우가 아니면 기본 메서드를 재정의할 필요가 없습니다. 이 경우 파생 클래스는 기본 클래스의 `Dispose(disposing)` 메서드를 재정의하여 파생 클래스의 리소스를 삭제해야 합니다. 이 재정의는 기본 클래스의 `Dispose(disposing)` 메서드를 호출해야 합니다.

```vb
Protected Overrides Sub Dispose(ByVal disposing As Boolean)
    If Not Me.disposed Then
        If disposing Then
            ' Insert code to free managed resources.
        End If
        ' Insert code to free unmanaged resources.
    End If
    MyBase.Dispose(disposing)
End Sub
```

파생 클래스는 기본 클래스의 <xref:System.IDisposable.Dispose%2A> 및 `Finalize` 메서드를 재정의해서는 안 됩니다. 파생 클래스의 인스턴스에서 이러한 메서드를 호출하면 해당 메서드의 기본 클래스 구현이 파생 클래스의 `Dispose(disposing)` 메서드 재정의를 호출합니다.

## <a name="garbage-collection-and-the-finalize-destructor"></a>가비지 컬렉션 및 Finalize 소멸자

.NET Framework는 *참조 추적 가비지 수집* 시스템을 사용 하 여 사용 하지 않는 리소스를 정기적으로 해제 합니다. Visual Basic 6.0 이전 버전에서는 *참조 계산* 이라는 다른 시스템을 사용 하 여 리소스를 관리 합니다. 두 시스템은 동일한 기능을 자동으로 수행하지만 몇 가지 중요한 차이점이 있습니다.

CLR은 시스템에서 더 이상 필요하지 않다고 결정하는 개체를 주기적으로 제거합니다. 개체는 시스템 리소스가 부족하면 더 빨리 해제되고 그렇지 않으면 더 천천히 해제됩니다. 개체의 범위가 손실되는 시점과 CLR이 해당 개체를 해제하는 시점 사이에는 지연 시간이 있습니다. 즉, Visual Basic 6.0 이하 버전의 개체와는 달리 개체 소멸 시기를 정확하게 확인할 수는 없습니다. 이러한 상황에서 개체는 *비결 정적 수명*이라고 합니다. `Finalize` 소멸자가 즉시 실행되지 않을 수도 있다는 점만 기억한다면 대부분의 경우 수명이 명확하지 않더라도 개체의 범위 손실 시 애플리케이션 작성 방법을 변경할 필요가 없습니다.

가비지 컬렉션 시스템 간의 또 다른 차이점은 `Nothing` 사용법입니다. Visual Basic 6.0 이하 버전에서는 프로그래머가 참조 횟수 기능을 활용하기 위해 개체 변수에 `Nothing`을 할당하여 해당 변수에 저장된 참조를 해제하는 경우가 있었습니다. 이때 개체에 대한 마지막 참조가 변수에 저장되어 있었다면 해당 개체의 리소스가 즉시 해제됩니다. 최신 Visual Basic 버전에서는 이 프로시저가 계속 유용한 경우도 있지만, 해당 프로시저를 수행해도 참조되는 개체가 리소스를 즉시 해제하지는 않습니다. 리소스를 즉시 해제하려면 개체의 <xref:System.IDisposable.Dispose%2A> 메서드를 사용합니다(사용 가능한 경우). 가비지 수집기가 분리된 개체를 검색하는 데 걸리는 시간에 비해 변수의 수명이 더 긴 경우에만 해당 변수를 `Nothing`로 설정해야 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.IDisposable.Dispose%2A>
- [구성 요소 초기화 및 종료](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/ws9dc6t6(v=vs.120))
- [New 연산자](../../../../visual-basic/language-reference/operators/new-operator.md)
- [관리되지 않는 리소스 정리](../../../../standard/garbage-collection/unmanaged.md)
- [Nothing](../../../../visual-basic/language-reference/nothing.md)
