---
title: NativeActivity 기본 클래스
ms.date: 03/30/2017
ms.assetid: 254a4c50-425b-426d-a32f-0f7234925bac
ms.openlocfilehash: 604535e39937a75c6d268cf1abbc90dbcd506a16
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989558"
---
# <a name="nativeactivity-base-class"></a>NativeActivity 기본 클래스

<xref:System.Activities.NativeActivity>는 protected 생성자를 가진 추상 클래스입니다. <xref:System.Activities.CodeActivity>와 마찬가지로 <xref:System.Activities.NativeActivity>는 <xref:System.Activities.NativeActivity.Execute%2A> 메서드를 구현하여 필수 동작을 작성하는 데 사용됩니다. <xref:System.Activities.CodeActivity>와 달리 <xref:System.Activities.NativeActivity>는 <xref:System.Activities.NativeActivityContext> 메서드에 전달되는 <xref:System.Activities.NativeActivity.Execute%2A> 개체를 통해 워크플로 런타임의 모든 노출된 기능에 액세스할 수 있습니다.

## <a name="using-nativeactivitycontext"></a>NativeActivityContext 사용
 <xref:System.Activities.NativeActivity.Execute%2A> 형식의 `context` 매개 변수 멤버를 사용하여 <xref:System.Activities.NativeActivityContext> 메서드에서 워크플로 런타임 기능에 액세스할 수 있습니다. <xref:System.Activities.NativeActivityContext>를 통해 사용할 수 있는 기능은 다음과 같습니다.

- 인수 및 변수 가져오기 및 설정

- <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A>를 사용하여 자식 활동 예약

- <xref:System.Activities.NativeActivityContext.Abort%2A>를 사용하여 활동 실행 중단

- <xref:System.Activities.NativeActivityContext.CancelChild%2A> 및 <xref:System.Activities.NativeActivityContext.CancelChildren%2A>을 사용하여 자식 실행 취소

- <xref:System.Activities.NativeActivityContext.CreateBookmark%2A>, <xref:System.Activities.NativeActivityContext.RemoveBookmark%2A>, <xref:System.Activities.NativeActivityContext.ResumeBookmark%2A> 등과 같은 메서드를 사용하여 활동 책갈피 액세스

- <xref:System.Activities.CodeActivityContext.Track%2A>을 사용하는 사용자 지정 추적 기능

- <xref:System.Activities.CodeActivityContext.GetProperty%2A> 및 <xref:System.Activities.NativeActivityContext.GetValue%2A>를 사용하여 활동 실행 속성 및 값 속성 액세스

- <xref:System.Activities.NativeActivityContext.ScheduleAction%2A> 및 <xref:System.Activities.NativeActivityContext.ScheduleFunc%2A>을 사용하여 활동 동작 및 기능 예약

### <a name="to-create-a-custom-activity-that-inherits-from-nativeactivity"></a>NativeActivity에서 상속되는 사용자 지정 활동을 만들려면

1. OpenVisual Studio 2010.

2. **파일**, **새로 만들기**, **프로젝트**를 차례로 선택 합니다. **프로젝트 형식** 창에서 **Visual C#**  아래에 있는 **Workflow 4.0** 을 선택 하 고 **v2010** 노드를 선택 합니다. **템플릿** 창에서 **활동 라이브러리** 를 선택 합니다. 새 프로젝트의 이름을 HelloActivity로 지정합니다.

3. HelloActivity 프로젝트에서 Activity1를 마우스 오른쪽 단추로 클릭 하 고 **삭제**를 선택 합니다.

4. HelloActivity 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **클래스**를 선택 합니다. 새 프로젝트의 이름을 HelloActivity.cs로 지정합니다.

5. HelloActivity.cs 파일에서 다음 `using` 지시문을 추가합니다.

    ```csharp
    using System.Activities;
    using System.Activities.Statements;
    ```

6. 기본 클래스를 클래스 선언에 추가하여 새 클래스를 <xref:System.Activities.NativeActivity>에서 상속하도록 설정합니다.

    ```csharp
    class HelloActivity : NativeActivity
    ```

7. <xref:System.Activities.NativeActivity.Execute%2A> 메서드를 추가하여 클래스에 기능을 추가합니다.

    ```csharp
    protected override void Execute(NativeActivityContext context)
    {
        Console.WriteLine("Hello World!");
    }
    ```

8. <xref:System.Activities.NativeActivity.CacheMetadata%2A> 메서드를 재정의하고 적합한 Add 메서드를 호출하여 워크플로 런타임에서 사용자 지정 활동의 변수, 인수, 자식 및 대리자를 알 수 있도록 합니다. 자세한 내용은 <xref:System.Activities.NativeActivityMetadata> 클래스를 참조하세요.

9. <xref:System.Activities.NativeActivityContext> 개체를 사용하여 책갈피를 예약합니다. 책갈피를 만들고 예약하고 다시 시작하는 방법은 <xref:System.Activities.WorkflowApplicationIdleEventArgs.Bookmarks%2A>를 참조하세요.

    ```csharp
    protected override void Execute(NativeActivityContext context)
        {
            // Create a Bookmark and wait for it to be resumed.
            context.CreateBookmark(BookmarkName.Get(context),
                new BookmarkCallback(OnResumeBookmark));
        }
    ```
