---
title: '예제: 동적 프로그래밍 문제 해결'
ms.date: 03/30/2017
ms.assetid: 42ed860a-a022-4682-8b7f-7c9870784671
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 866ec425fd66ee8b3b62263180ac7e6d776108f0
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049798"
---
# <a name="example-troubleshooting-dynamic-programming"></a>예제: 동적 프로그래밍 문제 해결
> [!NOTE]
> 이 항목은 시험판 소프트웨어인 .NET Native Developer Preview를 참조합니다. 이 Preview 버전은 [Microsoft Connect 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=394611)에서 다운로드할 수 있습니다(등록 필요).  
  
 .NET 네이티브 도구 체인을 사용 하 여 개발 된 앱에서 일부 메타 데이터 조회 실패가 발생 하면 예외가 발생 합니다.  앱에서 예기치 않은 방식으로 나타나는 오류도 있습니다.  다음 예제에서는 null 개체를 참조하여 발생하는 액세스 위반을 보여 줍니다.  
  
```output
Access violation - code c0000005 (first chance)  
App!$3_App::Core::Util::NavigationArgs.Setup  
App!$3_App::Core::Util::NavigationArgs..ctor  
App!$0_App::Gibbon::Util::DesktopNavigationArgs..ctor  
App!$0_App::ViewModels::DesktopAppVM.NavigateToPage  
App!$3_App::Core::ViewModels::AppViewModel.NavigateToFirstPage  
App!$3_App::Core::ViewModels::AppViewModel::<HandleLaunch>d__a.MoveNext  
App!$43_System::Runtime::CompilerServices::AsyncMethodBuilderCore.CallMoveNext  
App!System::Action.InvokeClosedStaticThunk  
App!System::Action.Invoke  
App!$43_System::Threading::Tasks::AwaitTaskContinuation.InvokeAction  
App!$43_System::Threading::SendOrPostCallback.InvokeOpenStaticThunk  
[snip]  
```  
  
 이제 [시작](getting-started-with-net-native.md)의 “수동으로 누락된 메타데이터 문제 해결” 섹션에서 설명하는 대로 3단계 방식을 통해 이 예외가 발생하는 문제를 해결해 보겠습니다.  
  
## <a name="what-was-the-app-doing"></a>앱이 수행 중이었던 작업  
 먼저 스택의 기반이 되는 `async` 키워드를 확인합니다.  스택에서 원래 호출 컨텍스트가 손실되었으며 다른 스레드에 대해 `async` 코드가 실행되었기 때문에 `async` 메서드에서 앱이 실제로 수행 중이었던 작업을 확인하기가 어려울 수도 있습니다. 그러나 앱이 첫 페이지를 로드하고 있었다는 것은 추론할 수 있습니다.  `NavigationArgs.Setup` 구현에서는 다음 코드로 인해 액세스 위반이 발생했습니다.  
  
`AppViewModel.Current.LayoutVM.PageMap`  
  
 여기서는 `AppViewModel.Current`의 `LayoutVM` 속성이 **null**이었습니다.  일부 메타데이터가 누락되어 동작이 약간 달라졌으며, 그로 인해 앱이 작동할 수 있도록 속성이 설정되는 대신 초기화되지 않았습니다.  코드에서 `LayoutVM`이 초기화되어야 하는 위치에 중단점을 설정하면 문제 해결에 도움이 될 수 있습니다.  그러나 `LayoutVM`의 형식은 `App.Core.ViewModels.Layout.LayoutApplicationVM`입니다.  그러므로 rd.xml 파일에 지금까지 포함된 메타데이터 지시문은 다음 항목뿐입니다.  
  
```xml  
<Namespace Name="App.ViewModels" Browse="Required Public" Dynamic="Required Public" />  
```  
  
 `App.Core.ViewModels.Layout.LayoutApplicationVM`이 다른 네임스페이스에 있어서 메타데이터가 누락되었기 때문에 오류가 발생했을 수도 있습니다.  
  
 이 경우 `App.Core.ViewModels`에 대해 런타임 지시문을 추가하면 문제가 해결됩니다. 근본 원인은 <xref:System.Type.GetType%28System.String%29?displayProperty=nameWithType> 메서드에 대한 API 호출에서 **null**이 반환된 것이며, 앱은 충돌이 해결될 때까지 문제를 자동으로 무시합니다.  
  
 동적 프로그래밍에서 .NET 네이티브에서 리플렉션 api를 사용할 때는 오류 발생 시 예외를 throw 하 <xref:System.Type.GetType%2A?displayProperty=nameWithType> 는 오버 로드를 사용 하는 것이 좋습니다.  
  
## <a name="is-this-an-isolated-case"></a>사례의 격리 여부 확인  
 `App.Core.ViewModels` 사용 시에는 다른 문제도 발생할 수 있습니다.  따라서 각 메타데이터 누락 예외를 파악하여 수정할지 아니면 시간 절약을 위해 대형 형식 클래스에 대한 지시문을 추가할지를 결정해야 합니다.  여기서는 생성되는 출력 바이너리의 크기가 증가해도 문제가 없다면 `dynamic`에 대해 `App.Core.ViewModels` 메타데이터를 추가하는 것이 가장 효율적인 방법입니다.  
  
## <a name="could-the-code-be-rewritten"></a>코드 다시 작성 가능 여부 확인  
 앱에서 `typeof(LayoutApplicationVM)` 대신 `Type.GetType("LayoutApplicationVM")`를 사용했다면 도구 체인이 `browse` 메타데이터를 보존했을 수 있습니다.  그러나 `invoke` 메타데이터는 작성되지 않았으므로 형식을 인스턴스화할 때 [MissingMetadataException](missingmetadataexception-class-net-native.md) 예외가 발생합니다. 이 예외를 방지하려면 `dynamic` 정책을 지정하는 형식 또는 네임스페이스에 대해 런타임 지시문을 추가해야 합니다. 런타임 지시문에 대한 자세한 내용은 [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [시작](getting-started-with-net-native.md)
- [예제: 데이터를 바인딩할 때 예외 처리](example-handling-exceptions-when-binding-data.md)
