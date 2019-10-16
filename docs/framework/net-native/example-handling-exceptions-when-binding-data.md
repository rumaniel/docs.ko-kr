---
title: '예제: 데이터를 바인딩하는 경우 예외 처리'
ms.date: 03/30/2017
ms.assetid: bd63ed96-9853-46dc-ade5-7bd1b0f39110
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8f7c40d1a179c29c3b92ca37848db6d1383e5d2d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049898"
---
# <a name="example-handling-exceptions-when-binding-data"></a>예제: 데이터를 바인딩하는 경우 예외 처리
> [!NOTE]
> 이 항목은 시험판 소프트웨어인 .NET Native Developer Preview를 참조합니다. 이 Preview 버전은 [Microsoft Connect 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=394611)에서 다운로드할 수 있습니다(등록 필요).  
  
 다음 예제에서는 .NET 네이티브 도구 체인을 사용 하 여 컴파일한 앱이 데이터 바인딩을 시도 하는 경우 throw 되는 [MissingMetadataException](missingmetadataexception-class-net-native.md) 예외를 해결 하는 방법을 보여 줍니다. 예외 정보는 다음과 같습니다.  
  
```output
This operation cannot be carried out as metadata for the following type was removed for performance reasons:   
App.ViewModels.MainPageVM  
```  
  
 관련 호출 스택은 다음과 같습니다.  
  
```output
Reflection::Execution::ReflectionDomainSetupImplementation.CreateNonInvokabilityException+0x238  
Reflection::Core::ReflectionDomain.CreateNonInvokabilityException+0x2e  
Reflection::Core::Execution::ExecutionEnvironment.+0x316  
System::Reflection::Runtime::PropertyInfos::RuntimePropertyInfo.GetValue+0x1cb  
System::Reflection::PropertyInfo.GetValue+0x22  
System::Runtime::InteropServices::WindowsRuntime::CustomPropertyImpl.GetValue+0x42  
App!$66_Interop::McgNative.Func_IInspectable_IInspectable+0x158  
App!$66_Interop::McgNative::__vtable_Windows_UI_Xaml_Data__ICustomProperty.GetValue__STUB+0x46  
Windows_UI_Xaml!DirectUI::PropertyProviderPropertyAccess::GetValue+0x3f   
Windows_UI_Xaml!DirectUI::PropertyAccessPathStep::GetValue+0x31   
Windows_UI_Xaml!DirectUI::PropertyPathListener::ConnectPathStep+0x113  
```  
  
## <a name="what-was-the-app-doing"></a>앱이 수행 중이었던 작업  
 스택의 기본에서 <xref:Windows.UI.Xaml?displayProperty=nameWithType> 네임 스페이스의 프레임은 XAML 렌더링 엔진이 실행 되 고 있음을 표시 합니다.   또한 <xref:System.Reflection.PropertyInfo.GetValue%2A?displayProperty=nameWithType> 메서드가 사용되었으므로 해당 메타데이터가 제거된 형식에 대해 속성 값의 리플렉션 기반 조회를 수행했음을 알 수 있습니다.  
  
 메타데이터 지시문을 제공하는 첫 단계에서는 모든 속성에 액세스할 수 있도록 형식에 대해 `serialize` 메타데이터를 추가합니다.  
  
```xml  
<Type Name="App.ViewModels.MainPageVM" Serialize="Required Public" />  
```  
  
## <a name="is-this-an-isolated-case"></a>사례의 격리 여부 확인  
 이 시나리오에서는 데이터 바인딩에서 `ViewModel` 하나의 메타데이터가 불완전하면 나머지 항목의 메타데이터도 불완전할 수 있습니다.  앱의 뷰 모델이 모두 `App.ViewModels` 네임스페이스에 포함되는 방식으로 코드를 작성한 경우에는 보다 일반적인 런타임 지시문을 사용할 수 있습니다.  
  
```xml  
<Namespace Name="App.ViewModels " Serialize="Required Public" />  
```  
  
## <a name="could-the-code-be-rewritten-to-not-use-reflection"></a>리플렉션을 사용하지 않도록 코드 다시 작성 가능 여부 확인  
 데이터 바인딩에서는 리플렉션을 많이 사용하므로 리플렉션을 사용하지 않도록 코드를 변경하기는 어렵습니다.  
  
 그러나 `ViewModel`을 XAML 페이지로 지정하여 도구 체인이 컴파일 타임에 속성 바인딩을 올바른 형식과 연결하고, 런타임 지시문을 사용하지 않고 메타데이터를 유지하도록 할 수는 있습니다.  예를 들어 속성에 <xref:Windows.UI.Xaml.Data.BindableAttribute?displayProperty=nameWithType> 특성을 적용할 수 있습니다. 이렇게 하면 XAML 컴파일러가 필요한 조회 정보를 생성하고 Default.rd.xml 파일에서 런타임 지시문이 필요하도록 설정하지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [시작](getting-started-with-net-native.md)
- [예제: 동적 프로그래밍 문제 해결](example-troubleshooting-dynamic-programming.md)
