---
title: '방법: 이벤트 구독 및 구독 취소 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- event handlers [C#], creating
- Code Editor, event handlers
- events [C#], creating using the IDE
ms.assetid: 6319f39f-282c-4173-8a62-6c4657cf51cd
ms.openlocfilehash: 523045e990532f1475e1c4816c98d1af76daa92b
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69590403"
---
# <a name="how-to-subscribe-to-and-unsubscribe-from-events-c-programming-guide"></a>방법: 이벤트 구독 및 구독 취소(C# 프로그래밍 가이드)
해당 이벤트가 발생할 때 호출되는 사용자 지정 코드를 작성하려는 경우 다른 클래스에 의해 게시되는 이벤트를 구독합니다. 예를 들어 사용자가 단추를 클릭할 때 애플리케이션에서 유용한 작업을 수행하도록 하려면 단추의 `click` 이벤트를 구독할 수 있습니다.  
  
### <a name="to-subscribe-to-events-by-using-the-visual-studio-ide"></a>Visual Studio IDE를 사용하여 이벤트를 구독하려면  
  
1. **속성** 창이 표시되지 않는 경우 **디자인** 보기에서 이벤트 처리기를 만들려는 양식 또는 컨트롤을 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2. **속성** 창의 맨 위에서 **이벤트** 아이콘을 클릭합니다.  
  
3. 만들려는 이벤트(예: `Load` 이벤트)를 두 번 클릭합니다.  
  
     Visual C#에서 빈 이벤트 처리기 메서드를 만들고 코드에 추가합니다. 또는 **코드** 보기에서 수동으로 코드를 추가할 수 있습니다. 예를 들어 다음 코드 줄은 `Form` 클래스에서 `Load` 이벤트가 발생할 때 호출되는 이벤트 처리기 메서드를 선언합니다.  
  
     [!code-csharp[csProgGuideEvents#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideEvents/CS/Events.cs#11)]  
  
     이벤트를 구독하는 데 필요한 코드 줄도 프로젝트의 Form1.Designer.cs 파일에 있는 `InitializeComponent` 메서드에 자동으로 생성됩니다. 해당 코드는 다음과 같습니다.  
  
    ```csharp
    this.Load += new System.EventHandler(this.Form1_Load);  
    ```  
  
### <a name="to-subscribe-to-events-programmatically"></a>프로그래밍 방식으로 이벤트를 구독하려면  
  
1. 이벤트의 대리자 시그니처와 일치하는 시그니처를 가진 이벤트 처리기 메서드를 정의합니다. 예를 들어 이벤트가 <xref:System.EventHandler> 대리자 형식을 기반으로 하는 경우 다음 코드는 메서드 스텁을 나타냅니다.  
  
    ```csharp
    void HandleCustomEvent(object sender, CustomEventArgs a)  
    {  
       // Do something useful here.  
    }  
    ```  
  
2. 더하기 대입 연산자(`+=`)를 사용하여 이벤트에 이벤트 처리기를 연결합니다. 다음 예제에서는 `publisher` 개체에 `RaiseCustomEvent`라는 이벤트가 있다고 가정합니다. 구독자 클래스가 해당 이벤트를 구독하려면 게시자 클래스에 대한 참조가 필요합니다.  
  
    ```csharp
    publisher.RaiseCustomEvent += HandleCustomEvent;  
    ```  
  
     앞의 구문은 C# 2.0의 새로운 기능입니다. `new` 키워드를 사용하여 명시적으로 캡슐화 대리자를 만들어야 한다는 점에서 C# 1.0 구문과 정확히 동일합니다.  
  
    ```csharp
    publisher.RaiseCustomEvent += new CustomEventHandler(HandleCustomEvent);  
    ```  
  
     [람다 식](../statements-expressions-operators/lambda-expressions.md)을 사용하여 이벤트 처리기를 지정할 수도 있습니다.
  
    ```csharp
    public Form1()  
    {  
        InitializeComponent();  
        this.Click += (s,e) =>
            {
                MessageBox.Show(((MouseEventArgs)e).Location.ToString());
            };
    }  
    ```  
  
### <a name="to-subscribe-to-events-by-using-an-anonymous-method"></a>무명 메서드를 사용하여 이벤트를 구독하려면  
  
- 나중에 이벤트 구독을 취소할 필요가 없는 경우 더하기 대입 연산자(`+=`)를 사용하여 이벤트에 무명 메서드를 연결할 수 있습니다. 다음 예제에서는 `publisher` 개체에 `RaiseCustomEvent`라는 이벤트가 있고 일종의 특수 이벤트 정보를 전달하도록 `CustomEventArgs` 클래스도 정의되었다고 가정합니다. 구독자 클래스가 해당 이벤트를 구독하려면 `publisher`에 대한 참조가 필요합니다.  
  
    ```csharp
    publisher.RaiseCustomEvent += delegate(object o, CustomEventArgs e)  
    {  
      string s = o.ToString() + " " + e.ToString();  
      Console.WriteLine(s);  
    };  
    ```  
  
     익명 함수를 사용하여 이벤트를 구독한 경우 쉽게 이벤트 구독을 취소할 수 없습니다. 이 시나리오에서 구독을 취소하려면 이벤트를 구독하고, 대리자 변수에 무명 메서드를 저장한 다음 이벤트에 대리자를 추가하는 코드로 돌아가야 합니다. 일반적으로 코드의 뒷부분에서 이벤트 구독을 취소해야 하는 경우 익명 함수를 사용하여 이벤트를 구독하지 않는 것이 좋습니다. 익명 함수에 대한 자세한 내용은 [익명 함수](../statements-expressions-operators/anonymous-functions.md)를 참조하세요.  
  
## <a name="unsubscribing"></a>구독 해제  
 이벤트가 발생할 때 이벤트 처리기가 호출되지 않도록 하려면 이벤트 구독을 취소합니다. 리소스 누수를 방지하려면 구독자 개체를 삭제하기 전에 이벤트 구독을 취소해야 합니다. 이벤트 구독을 취소할 때까지 게시 개체에서 이벤트의 기반이 되는 멀티캐스트 대리자에 구독자의 이벤트 처리기를 캡슐화하는 대리자에 대한 참조가 있습니다. 게시 개체에 해당 참조가 있기만 하면 가비지 수집 시 구독자 개체가 삭제되지 않습니다.  
  
#### <a name="to-unsubscribe-from-an-event"></a>이벤트 구독을 취소하려면  
  
- 빼기 대입 연산자(`-=`)를 사용하여 이벤트 구독을 취소합니다.  
  
    ```csharp
    publisher.RaiseCustomEvent -= HandleCustomEvent;  
    ```  
  
     모든 구독자가 이벤트 구독을 취소하면 게시자 클래스의 이벤트 인스턴스가 `null`로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목

- [이벤트](./index.md)
- [event](../../language-reference/keywords/event.md)
- [방법: .NET Framework 지침을 따르는 이벤트 게시](./how-to-publish-events-that-conform-to-net-framework-guidelines.md)
- [- 및 -= 연산자](../../language-reference/operators/subtraction-operator.md)
- [+ 및 += 연산자](../../language-reference/operators/addition-operator.md)
