---
title: Visual Basic의 개체 및 클래스
ms.date: 07/20/2015
helpviewer_keywords:
- classes [Visual Basic]
- objects [Visual Basic]
ms.assetid: c68c5752-1006-46e1-975a-6717b62a42fc
ms.openlocfilehash: dd2968f7ab528fa07ef0c5af85f2a7f07147a76e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67755159"
---
# <a name="objects-and-classes-in-visual-basic"></a>Visual Basic의 개체 및 클래스

*개체*는 하나의 단위로 취급될 수 있는 코드 및 데이터의 조합입니다. 개체는 컨트롤 또는 폼과 같은 애플리케이션의 부분일 수 있습니다. 전체 애플리케이션이 하나의 개체가 될 수도 있습니다.

Visual Basic에서 응용 프로그램을 만들 때 지속적으로 개체를 사용 하 여 작동 합니다. 컨트롤, 폼 및 데이터 액세스 개체와 같은 Visual Basic에서 제공 하는 개체를 사용할 수 있습니다. 또한 Visual Basic 응용 프로그램 내에서 다른 응용 프로그램에서 개체를 사용할 수 있습니다. 개체를 직접 만들고 해당 개체에 대해 추가 속성 및 메서드를 정의할 수 있습니다. 개체는 프로그램에 대한 조립식 빌딩 블록처럼 작동합니다. 즉, 코드 조각을 한 번 작성한 후 반복해서 다시 사용할 수 있습니다.

이 항목에서는 개체에 대해 좀 더 자세히 설명합니다.

## <a name="objects-and-classes"></a>개체 및 클래스

Visual Basic에서는 각 개체는 정의 되는 *클래스*합니다. 클래스는 개체의 변수, 속성, 프로시저 및 이벤트를 설명합니다. 개체는 클래스의 인스턴스입니다. 클래스를 정의한 후에는 필요한 수만큼 개체를 만들 수 있습니다.

개체와 해당 클래스 간의 관계를 이해하기 위해 쿠키 커터와 쿠키를 생각해 보세요. 쿠키 커터는 클래스입니다. 각 쿠키에 대해 크기와 모양 같은 특징을 정의합니다. 클래스는 개체를 만드는 데 사용됩니다. 개체는 쿠키입니다.

해당 멤버에 액세스하려면 먼저 개체를 만들어야 합니다.

### <a name="to-create-an-object-from-a-class"></a>클래스에서 개체를 만들려면

1. 개체를 만들려는 클래스를 결정합니다.

2. 클래스 인스턴스를 할당할 수 있는 변수를 만드는 [Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md)을 작성합니다. 변수는 원하는 클래스의 형식이어야 합니다.

   ```vb
   Dim nextCustomer As customer
   ```

3. [New 연산자](../../../../visual-basic/language-reference/operators/new-operator.md) 키워드를 추가하여 변수를 클래스의 새 인스턴스로 초기화합니다.

   ```vb
   Dim nextCustomer As New customer
   ```

4. 이제 개체 변수를 통해 클래스의 멤버에 액세스할 수 있습니다.

   ```vb
   nextCustomer.accountNumber = lastAccountNumber + 1
   ```

> [!NOTE]
> 가능하면 항상 할당하려는 클래스 형식으로 변수를 선언해야 합니다. 이것을 *초기 바인딩*이라고 합니다. 컴파일 시간의 클래스 형식을 모르는 경우 변수를 [개체 데이터 형식](../../../../visual-basic/language-reference/data-types/object-data-type.md)으로 선언하여 *런타임에 바인딩*을 호출할 수 있습니다. 그러나 런타임에 바인딩을 사용하면 성능이 저하되고 런타임 개체 멤버에 대한 액세스가 제한됩니다. 자세한 내용은 [개체 변수 선언](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)을 참조하세요.

### <a name="multiple-instances"></a>여러 인스턴스

클래스에서 새로 만든 개체들이 서로 동일한 경우가 많습니다. 그렇지만 개별 개체로 존재할 경우 다른 인스턴스와 독립적으로 해당 변수 및 속성을 변경할 수 있습니다. 예를 들어 양식에 세 개의 확인란을 추가하는 경우 각 확인란 개체는 <xref:System.Windows.Forms.CheckBox> 클래스의 인스턴스입니다. 개별 <xref:System.Windows.Forms.CheckBox> 개체는 클래스가 정의하는 공통된 특징 및 기능(속성, 변수, 프로시저 및 이벤트) 집합을 공유합니다. 그러나 각각은 고유한 이름을 가지며, 개별적으로 사용하거나 사용하지 않도록 설정하고, 폼의 다른 위치에 배치할 수 있습니다.

## <a name="object-members"></a>개체 멤버

개체는 애플리케이션의 요소로, 클래스의 *인스턴스*를 나타냅니다. 필드, 속성, 메서드 및 이벤트는 개체의 구성 요소이며 해당 *멤버*로 구성됩니다.

### <a name="member-access"></a>멤버 액세스

개체 변수의 이름, 마침표 (`.`) 및 멤버 이름을 순서대로 지정하여 개체 멤버에 액세스합니다. 다음 예제에서는 <xref:System.Windows.Forms.Control.Text%2A> 개체의 <xref:System.Windows.Forms.Label> 속성을 설정합니다.

```vb
warningLabel.Text = "Data not saved"
```

#### <a name="intellisense-listing-of-members"></a>IntelliSense 멤버 목록

IntelliSense는 멤버 나열 옵션을 호출할 때(예를 들어 멤버 액세스 연산자로 마침표(`.`)를 입력할 때) 클래스의 멤버를 나열합니다. 해당 클래스의 인스턴스로 선언된 변수 이름 뒤에 마침표를 입력하는 경우 IntelliSense는 공유 멤버가 아닌 모든 인스턴스 멤버를 나열합니다. 클래스 이름 뒤에 마침표를 입력하는 경우 IntelliSense는 인스턴스 멤버가 아닌 모든 공유 멤버를 나열합니다. 자세한 내용은 [IntelliSense 사용](/visualstudio/ide/using-intellisense)을 참조하세요.

### <a name="fields-and-properties"></a>필드 및 속성

*필드* 및 *속성*은 개체에 저장된 정보를 나타냅니다. 프로시저에서 지역 변수를 검색하고 설정하는 것과 동일한 방식으로 대입문을 사용하여 해당 값을 검색하고 설정합니다. 다음 예제에서는 <xref:System.Windows.Forms.Control.Width%2A> 속성을 검색하고 <xref:System.Windows.Forms.Label> 개체의 <xref:System.Windows.Forms.Control.ForeColor%2A> 속성을 설정합니다.

```vb
Dim warningWidth As Integer = warningLabel.Width
warningLabel.ForeColor = System.Drawing.Color.Red
```

필드를 *멤버 변수*라고도 합니다.

다음 경우에 Property 프로시저를 사용합니다.

- 값을 설정하거나 검색할 시기와 방법을 제어해야 합니다.

- 속성에는 유효성을 검사해야 하는 잘 정의된 값 집합이 있습니다.

- 값을 설정하면 `IsVisible` 속성과 같은 개체의 상태가 획기적으로 변경될 수 있습니다.

- 속성을 설정하면 다른 내부 변수 또는 다른 속성의 값이 변경됩니다.

- 속성을 설정하거나 검색하려면 먼저 일련의 단계를 수행해야 합니다.

다음 경우에 필드를 사용합니다.

- 값이 자체적으로 유효성을 검사하는 형식입니다. 예를 들어 `True` 또는 `False` 이외의 값이 `Boolean` 변수에 할당되면 오류 또는 자동 데이터 변환이 발생합니다.

- 데이터 형식이 지원하는 범위의 모든 값이 유효합니다. `Single` 또는 `Double` 형식의 많은 속성이 여기에 해당합니다.

- 속성이 `String` 데이터 형식이고 문자열 크기 또는 값에 제약이 없습니다.

- 자세한 내용은 [Property 프로시저](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)를 참조하세요.

### <a name="methods"></a>메서드

*메서드*는 개체에서 수행할 수 있는 작업입니다. 예를 들어 <xref:System.Windows.Forms.ComboBox.ObjectCollection.Add%2A>는 콤보 상자에 새 항목을 추가하는 <xref:System.Windows.Forms.ComboBox> 개체의 메서드입니다.

다음 예제에서는 <xref:System.Windows.Forms.Timer> 개체의 <xref:System.Windows.Forms.Timer.Start%2A> 메서드를 설명합니다.

```vb
Dim safetyTimer As New System.Windows.Forms.Timer
safetyTimer.Start()
```

메서드는 개체에 의해 노출되는 *프로시저*일 뿐입니다.

자세한 내용은 [프로시저](../../../../visual-basic/programming-guide/language-features/procedures/index.md)를 참조하세요.

### <a name="events"></a>이벤트

이벤트는 마우스 클릭이나 키 누르기와 같이 개체가 인식하는 동작이며 응답하기 위해 코드를 작성할 수 있습니다. 이벤트는 사용자 동작 또는 프로그램 코드의 결과로 발생하거나 시스템에 의해 발생할 수 있습니다. 이벤트에 신호를 보내는 코드를 이벤트 *발생*이라고 하고, 신호에 응답하는 코드를 *처리*라고 합니다.

개체에 의해 발생하고 다른 개체에서 처리되는 사용자 지정 이벤트를 개발할 수도 있습니다. 자세한 내용은 [이벤트](../../../../visual-basic/programming-guide/language-features/events/index.md)를 참조하세요.

### <a name="instance-members-and-shared-members"></a>인스턴스 멤버 및 공유 멤버

클래스에서 개체를 만들 때 결과는 해당 클래스의 인스턴스가 됩니다. [Shared](../../../../visual-basic/language-reference/modifiers/shared.md) 키워드로 선언되지 않은 멤버는 해당 특정 인스턴스에 반드시 속하는 *인스턴스 멤버*입니다. 한 인스턴스의 인스턴스 멤버는 동일한 클래스의 다른 인스턴스에 있는 동일한 멤버와 무관합니다. 예를 들어 인스턴스 멤버 변수는 서로 다른 인스턴스에서 다른 값을 가질 수 있습니다.

`Shared` 키워드로 선언된 멤버는 특정 인스턴스가 아니라 전체 클래스에 속하는 *공유 멤버*입니다. 공유 멤버는 사용자가 만드는 클래스의 인스턴스 수에 관계 없이, 사용자가 인스턴스를 만들지 않더라도 한 번만 존재합니다. 예를 들어 공유 멤버 변수는 클래스에 액세스할 수 있는 모든 코드에서 사용할 수 있는 하나의 값만 갖습니다.

#### <a name="accessing-nonshared-members"></a>비공유 멤버 액세스

##### <a name="to-access-a-nonshared-member-of-an-object"></a>개체의 비공유 멤버에 액세스하려면

1. 개체가 해당 클래스에서 생성되고 개체 변수에 할당되어 있는지 확인합니다.

   ```vb
   Dim secondForm As New System.Windows.Forms.Form
   ```

2. 멤버에 액세스하는 문에서 개체 변수 이름 다음에 *멤버-액세스 연산자*(`.`)를 지정한 후 멤버 이름을 지정합니다.

   ```vb
   secondForm.Show()
   ```

#### <a name="accessing-shared-members"></a>공유 멤버 액세스

##### <a name="to-access-a-shared-member-of-an-object"></a>개체의 공유 멤버에 액세스하려면

- 클래스 이름 뒤에 *멤버-액세스 연산자*(`.`)를 지정한 다음 멤버 이름을 지정합니다. 항상 클래스 이름을 통해 직접적으로 개체의 `Shared` 멤버에 액세스해야 합니다.

   ```vb
   MsgBox("This computer is called " & Environment.MachineName)
   ```

- 클래스에서 개체를 이미 만들었으면 개체의 변수를 통해 `Shared` 멤버에 액세스할 수도 있습니다.

### <a name="differences-between-classes-and-modules"></a>클래스와 모듈 간의 차이점

클래스와 모듈 간의 주요 차이점은 클래스는 개체로 인스턴스화할 수 있지만 표준 모듈은 그럴 수 없다는 것입니다. 표준 모듈의 데이터 복사본은 하나만 있으므로 프로그램의 한 부분이 표준 모듈의 공용 변수를 변경하면 프로그램의 다른 부분은 해당 변수를 읽을 때 동일한 값을 얻습니다. 반면 개체 데이터는 인스턴스화된 각 개체에 대해 개별적으로 존재합니다. 또 다른 차이점은 표준 모듈과 달리 클래스는 인터페이스를 구현할 수 있다는 것입니다.

> [!NOTE]
> `Shared` 한정자가 클래스 멤버에 적용되면 클래스의 특정 인스턴스가 아닌 클래스 자체에 연결됩니다. 모듈 멤버에 액세스하는 것과 같은 방식으로 멤버에도 클래스 이름을 사용하여 직접 액세스합니다.

클래스와 모듈은 또한 해당 멤버의 범위가 각기 다를 수도 있습니다. 클래스 내에 정의된 멤버는 클래스의 특정 인스턴스 범위를 벗어나지 않으며 개체의 수명 동안만 존재합니다. 클래스 외부에서 클래스 멤버에 액세스하려면 *개체*.*멤버* 형식의 정규화된 이름을 사용해야 합니다.

반면에 모듈 내에서 선언된 멤버는 기본적으로 공개적으로 액세스할 수 있으며 모듈에 액세스할 수 있는 모든 코드에서 액세스할 수 있습니다. 즉, 표준 모듈의 변수는 프로젝트의 모든 위치에서 볼 수 있으며 프로그램의 수명 동안 존재하기 때문에 결과적으로 전역 변수에 해당합니다.

## <a name="reusing-classes-and-objects"></a>클래스 및 개체 다시 사용

개체를 사용하면 변수 및 프로시저를 한 번 선언한 후 필요할 때마다 다시 사용할 수 있습니다. 예를 들어 애플리케이션에 맞춤법 검사기를 추가하려는 경우 모든 변수 및 지원 함수를 정의하여 맞춤법 검사 기능을 제공할 수 있습니다. 맞춤법 검사기를 클래스로 만드는 경우 컴파일된 어셈블리에 대한 참조를 추가하여 다른 애플리케이션에서 다시 사용할 수 있습니다. 다른 사람이 이미 개발한 맞춤법 검사기 클래스를 사용하여 일부 작업을 줄일 수도 있습니다.

.NET Framework는 여러 가지 용도로 사용할 수 있는 구성 요소를 제공 합니다. 다음 예제에서는 <xref:System> 네임스페이스의 <xref:System.TimeZone> 클래스를 사용합니다. <xref:System.TimeZone>에서는 현재 컴퓨터 시스템의 표준 시간대에 대한 정보를 검색할 수 있도록 하는 멤버를 제공합니다.

```vb
Public Sub examineTimeZone()
    Dim tz As System.TimeZone = System.TimeZone.CurrentTimeZone
    Dim s As String = "Current time zone is "
    s &= CStr(tz.GetUtcOffset(Now).Hours) & " hours and "
    s &= CStr(tz.GetUtcOffset(Now).Minutes) & " minutes "
    s &= "different from UTC (coordinated universal time)"
    s &= vbCrLf & "and is currently "
    If tz.IsDaylightSavingTime(Now) = False Then s &= "not "
    s &= "on ""summer time""."
    MsgBox(s)
End Sub
```

앞의 예제에서 첫 번째 [Dim 문](../../../../visual-basic/language-reference/statements/dim-statement.md)은 <xref:System.TimeZone> 형식의 개체 변수를 선언하고 이를 <xref:System.TimeZone.CurrentTimeZone%2A> 속성에 의해 반환된 <xref:System.TimeZone> 개체에 할당합니다.

## <a name="relationships-among-objects"></a>개체 간 관계

개체는 여러 가지 방법으로 서로 관련될 수 있습니다. 관계의 주요 종류로는 *계층적* 및 *포함*이 있습니다.

### <a name="hierarchical-relationship"></a>계층적 관계

클래스가 보다 기본적인 클래스에서 파생되면 *계층적 관계*에 있다고 할 수 있습니다. 클래스 계층 구조는 보다 일반적인 클래스의 하위 항목을 설명하는 경우에 유용합니다.

다음 예제에서는 일반적인 <xref:System.Windows.Forms.Button>처럼 작동하지만 전경색 및 배경색을 거꾸로 뒤집는 메서드도 제공하는 특수한 종류의 <xref:System.Windows.Forms.Button>을 정의하려 한다고 가정합니다.

#### <a name="to-define-a-class-is-derived-from-an-already-existing-class"></a>클래스가 기존 클래스에서 파생된다고 정의하려면

1. [Class 문](../../../../visual-basic/language-reference/statements/class-statement.md)을 사용하여 필요한 개체를 만들 클래스를 정의합니다.

   ```vb
   Public Class reversibleButton
   ```

   `End Class` 문은 클래스의 마지막 코드 줄 다음에 나옵니다. 기본적으로 IDE(통합 개발 환경)는 사용자가 `Class` 문을 입력하면 `End Class`를 자동으로 생성합니다.

2. `Class` 문 바로 다음에 [Inherits 문](../../../../visual-basic/language-reference/statements/inherits-statement.md)을 입력합니다. 새 클래스가 파생되는 클래스를 지정합니다.

   ```vb
   Inherits System.Windows.Forms.Button
   ```

   새 클래스는 기본 클래스에서 정의하는 모든 멤버를 상속합니다.

3. 파생 클래스가 노출하는 추가 멤버에 대한 코드를 추가합니다. 예를 들어 `reverseColors` 메서드를 추가할 수 있으며 이 경우 파생 클래스는 다음과 같이 표시될 수 있습니다.

   ```vb
   Public Class reversibleButton
       Inherits System.Windows.Forms.Button
           Public Sub reverseColors()
               Dim saveColor As System.Drawing.Color = Me.BackColor
               Me.BackColor = Me.ForeColor
               Me.ForeColor = saveColor
          End Sub
   End Class
   ```

   `reversibleButton` 클래스에서 개체를 만드는 경우 <xref:System.Windows.Forms.Button> 클래스의 모든 멤버뿐 아니라 `reverseColors` 메서드와 `reversibleButton`에 정의한 다른 모든 새 멤버에도 액세스할 수 있습니다.

파생 클래스는 해당 클래스의 기준이 되는 클래스에서 멤버를 상속하므로 클래스 계층 구조가 점점 복잡해질 수 있습니다. 자세한 내용은 [상속 기본 사항](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)을 참조하세요.

### <a name="compiling-the-code"></a>코드 컴파일

컴파일러에서 새 클래스를 파생하려는 원본 클래스에 액세스할 수 있어야 합니다. 이것은 이름을 완전히 한정하거나 앞의 예제에서와 같이 [Imports 문(.NET 네임스페이스 및 형식)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)에서 해당 네임스페이스를 식별하는 것을 의미할 수 있습니다. 클래스가 다른 프로젝트에 있으면 해당 프로젝트에 대한 참조를 추가해야 할 수 있습니다. 자세한 내용은 [프로젝트의 참조 관리](/visualstudio/ide/managing-references-in-a-project)를 참조하세요.

### <a name="containment-relationship"></a>포함 관계

개체를 연관지을 수 있는 또 다른 방법은 *포함 관계*입니다. 컨테이너 개체는 논리적으로 다른 개체를 캡슐화합니다. 예를 들어 <xref:System.OperatingSystem> 개체에 논리적으로 <xref:System.Version> 개체를 포함하며, 이는 해당 <xref:System.OperatingSystem.Version%2A> 속성을 통해 반환됩니다. 컨테이너 개체가 다른 개체를 물리적으로 포함하는 것은 아닙니다.

#### <a name="collections"></a>컬렉션

특정 형식의 개체 포함을 *컬렉션*으로 나타냅니다. 컬렉션은 열거할 수 있는 유사한 개체의 그룹입니다. Visual Basic에서 특정 구문을 지원 합니다 [각각에 대 한 중... 다음 문을](../../../../visual-basic/language-reference/statements/for-each-next-statement.md) 컬렉션의 항목을 반복할 수 있도록 합니다. 또한 컬렉션을 사용하면<xref:Microsoft.VisualBasic.Collection.Item%2A>을 사용하여 인덱스별로 또는 고유 문자열에 연결하여 요소를 검색할 수 있습니다. 컬렉션은 인덱스를 사용하지 않고도 항목을 추가 또는 제거할 수 있도록 하므로 배열보다 더 쉽게 사용할 수 있습니다. 사용 편의성 때문에 컬렉션을 폼 및 컨트롤을 저장하는 데 종종 사용합니다.

## <a name="related-topics"></a>관련 항목

[연습: 클래스 정의](../../../../visual-basic/programming-guide/language-features/objects-and-classes/walkthrough-defining-classes.md)\
클래스를 만드는 방법에 대한 단계별 설명을 제공합니다.

[오버 로드 된 속성 및 메서드](../../../../visual-basic/programming-guide/language-features/objects-and-classes/overloaded-properties-and-methods.md)\
오버로드된 속성 및 메서드

[상속 기본 사항](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)\
상속 한정자, 메서드 및 속성 재정의, MyClass 및 MyBase에 대해 설명합니다.

[개체 수명: 개체가 만들어지고 제거 하는 방법](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)\
클래스 인스턴스의 생성 및 삭제에 대해 설명합니다.

[무명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)\
익명 형식을 만들고 사용하여 데이터 형식에 대한 클래스 정의를 작성하지 않고 개체를 만들 수 있는 방법을 설명합니다.

[개체 이니셜라이저: 명명 된 형식과 익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)\
단일 식을 사용하여 명명된 형식 및 무명 형식의 인스턴스를 만드는 데 사용되는 개체 이니셜라이저에 대해 설명합니다.

[방법: 무명 형식 선언에서 속성 이름 및 형식 유추](../../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)\
무명 형식 선언에서 속성 이름 및 형식을 유추하는 방법을 설명합니다. 성공 및 실패한 유추의 예제를 제공합니다.
