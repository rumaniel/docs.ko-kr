---
title: 책갈피-WF
ms.date: 03/30/2017
ms.assetid: 9b51a346-09ae-455c-a70a-e2264ddeb9e2
ms.openlocfilehash: a15a28cc39a4227765c238a6f2b86c72197f1a39
ms.sourcegitcommit: 9ee6cd851b6e176a5811ea28ed0d5935c71950f9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68868926"
---
# <a name="bookmarks"></a>Bookmarks
책갈피는 활동이 워크플로 스레드에 그대로 유지되지 않고 입력을 수동적으로 기다릴 수 있도록 하는 메커니즘입니다. 활동에서 자극을 기다리고 있음을 알릴 때 책갈피를 만들 수 있습니다. 이는 현재 실행 중인 메서드(<xref:System.Activities.Bookmark>를 만든 메서드)에서 반환되더라도 활동 실행이 완료된 것으로 간주해서는 안 된다는 것을 런타임에 나타냅니다.  
  
## <a name="bookmark-basics"></a>책갈피 기본 사항  
 <xref:System.Activities.Bookmark>는 워크플로 인스턴스 내에서 실행을 다시 시작하고 입력을 전달할 수 있는 지점을 나타냅니다. 일반적으로 <xref:System.Activities.Bookmark>에는 이름이 지정되며 외부(호스트 또는 확장) 코드를 사용하여 관련 데이터로 책갈피를 다시 시작합니다. <xref:System.Activities.Bookmark>가 다시 시작되면 워크플로 런타임은 생성 시 해당 <xref:System.Activities.BookmarkCallback>와 연결된 <xref:System.Activities.Bookmark> 대리자를 예약합니다.  
  
## <a name="bookmark-options"></a>책갈피 옵션  
 <xref:System.Activities.BookmarkOptions> 클래스는 생성되는 <xref:System.Activities.Bookmark>의 유형을 지정합니다. 함께 사용할 수 있는 값은 <xref:System.Activities.BookmarkOptions.None>, <xref:System.Activities.BookmarkOptions.MultipleResume> 및 <xref:System.Activities.BookmarkOptions.NonBlocking>입니다. 정확히 한 번 다시 시작될 것으로 예상되는 <xref:System.Activities.BookmarkOptions.None>를 만들 경우 기본값인 <xref:System.Activities.Bookmark>을 사용합니다. 여러 번 다시 시작될 수 있는 <xref:System.Activities.BookmarkOptions.MultipleResume>를 만들 경우 <xref:System.Activities.Bookmark>을 사용합니다. 다시 시작되지 않을 <xref:System.Activities.BookmarkOptions.NonBlocking>를 만들 경우 <xref:System.Activities.Bookmark>을 사용합니다. 기본 <xref:System.Activities.BookmarkOptions>를 사용하여 만든 책갈피와는 달리, <xref:System.Activities.BookmarkOptions.NonBlocking> 책갈피는 활동 완료를 제한하지 않습니다.  
  
## <a name="bookmark-resumption"></a>책갈피 다시 시작  
 <xref:System.Activities.WorkflowApplication.ResumeBookmark%2A> 오버로드 중 하나를 사용하여 워크플로 외부에서 코드를 통해 책갈피를 다시 시작할 수 있습니다. 이 예제에서는 `ReadLine` 활동을 만듭니다. `ReadLine` 활동이 실행되면 <xref:System.Activities.Bookmark>를 만들고 콜백을 등록한 다음 <xref:System.Activities.Bookmark>가 다시 시작될 때까지 기다립니다. 책갈피가 다시 시작되면 `ReadLine` 활동은 <xref:System.Activities.Bookmark>와 함께 전달된 데이터를 해당 <xref:System.Activities.Activity%601.Result%2A> 인수에 할당합니다.  
  
```csharp  
public sealed class ReadLine : NativeActivity<string>  
{  
    [RequiredArgument]  
    public  InArgument<string> BookmarkName { get; set; }  
  
    protected override void Execute(NativeActivityContext context)  
    {  
        // Create a Bookmark and wait for it to be resumed.  
        context.CreateBookmark(BookmarkName.Get(context),   
            new BookmarkCallback(OnResumeBookmark));  
    }  
  
    // NativeActivity derived activities that do asynchronous operations by calling   
    // one of the CreateBookmark overloads defined on System.Activities.NativeActivityContext   
    // must override the CanInduceIdle property and return true.  
    protected override bool CanInduceIdle  
    {  
        get { return true; }  
    }  
  
    public void OnResumeBookmark(NativeActivityContext context, Bookmark bookmark, object obj)  
    {  
        // When the Bookmark is resumed, assign its value to  
        // the Result argument.  
        Result.Set(context, (string)obj);  
    }  
}  
```  
  
 이 예제에서는 `ReadLine` 활동을 사용하여 사용자 이름을 수집하고 콘솔 창에 표시하는 워크플로를 만듭니다. 호스트 애플리케이션에서는 실제로 입력을 수집하는 작업을 수행하고 <xref:System.Activities.Bookmark>를 다시 시작하여 이를 워크플로에 전달합니다.  
  
```csharp  
Variable<string> name = new Variable<string>  
{  
    Name = "name"  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        name  
    },  
    Activities =  
    {  
        new WriteLine()  
        {  
            Text = "What is your name?"  
        },  
        new ReadLine()  
        {  
            BookmarkName = "UserName",  
            Result = name  
        },  
        new WriteLine()  
        {  
            Text = new InArgument<string>((env) => "Hello, " + name.Get(env))  
        }  
    }  
};  
  
AutoResetEvent syncEvent = new AutoResetEvent(false);  
  
// Create the WorkflowApplication using the desired  
// workflow definition.  
WorkflowApplication wfApp = new WorkflowApplication(wf);  
  
// Handle the desired lifecycle events.  
wfApp.Completed = delegate(WorkflowApplicationCompletedEventArgs e)  
{  
    // Signal the host that the workflow is complete.  
    syncEvent.Set();  
};  
  
// Start the workflow.  
wfApp.Run();  
  
// Collect the user's name and resume the bookmark.  
// Bookmark resumption only occurs when the workflow  
// is idle. If a call to ResumeBookmark is made and the workflow  
// is not idle, ResumeBookmark blocks until the workflow becomes  
// idle before resuming the bookmark.  
wfApp.ResumeBookmark("UserName", Console.ReadLine());  
  
// Wait for Completed to arrive and signal that  
// the workflow is complete.  
syncEvent.WaitOne();  
```  
  
 `ReadLine` 활동이 실행되면 <xref:System.Activities.Bookmark>이라는 `UserName`를 만든 다음 책갈피가 다시 시작될 때까지 기다립니다. 호스트는 원하는 데이터를 수집한 다음 <xref:System.Activities.Bookmark>를 다시 시작합니다. 워크플로가 다시 시작되고 이름을 표시한 다음 완료됩니다. 책갈피를 다시 시작하는 데는 동기화 코드가 필요 없습니다. 워크플로가 유휴 상태일 때만 <xref:System.Activities.Bookmark>를 다시 시작할 수 있습니다. 워크플로가 유휴 상태가 아닌 경우 워크플로가 유휴 상태가 될 때까지 <xref:System.Activities.WorkflowApplication.ResumeBookmark%2A>에 대한 호출이 차단됩니다.  
  
## <a name="bookmark-resumption-result"></a>책갈피 다시 시작 결과  
 <xref:System.Activities.WorkflowApplication.ResumeBookmark%2A>에서 책갈피 다시 시작 요청의 결과를 나타내는 <xref:System.Activities.BookmarkResumptionResult> 열거형 값을 반환합니다. 가능한 반환 값은 <xref:System.Activities.BookmarkResumptionResult.Success>, <xref:System.Activities.BookmarkResumptionResult.NotReady> 및 <xref:System.Activities.BookmarkResumptionResult.NotFound>입니다. 호스트 및 확장 프로그램에서는 이 값을 사용하여 진행 방법을 결정합니다.
