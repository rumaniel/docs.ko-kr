---
title: 약한 이벤트 패턴
ms.date: 03/30/2017
helpviewer_keywords:
- weak event pattern implementation [WPF]
- event handlers [WPF], weak event pattern
- IWeakEventListener interface [WPF]
ms.assetid: e7c62920-4812-4811-94d8-050a65c856f6
ms.openlocfilehash: f4cbb22a3cdd7b966c36f6c8246b13b5c58e056d
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991795"
---
# <a name="weak-event-patterns"></a>약한 이벤트 패턴
응용 프로그램에서 이벤트 소스에 연결 된 처리기가 소스에 처리기를 연결 하는 수신기 개체와 조정 되지 않을 수 있습니다. 이 경우 메모리 누수가 발생할 수 있습니다. [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]특정 이벤트에 대 한 전용 관리자 클래스를 제공 하 고 해당 이벤트에 대 한 수신기에 인터페이스를 구현 하 여이 문제를 해결 하는 데 사용할 수 있는 디자인 패턴을 소개 합니다. 이 디자인 패턴을 *약한 이벤트 패턴*이라고 합니다.  
  
## <a name="why-implement-the-weak-event-pattern"></a>약한 이벤트 패턴을 구현 하는 이유  
 이벤트를 수신 대기 하면 메모리 누수가 발생할 수 있습니다. 이벤트를 수신 하는 일반적인 방법은 소스에서 이벤트에 처리기를 연결 하는 언어 관련 구문을 사용 하는 것입니다. 예를 들어에서 C#해당 구문은 `source.SomeEvent += new SomeEventHandler(MyEventHandler)`입니다.  
  
 이 기술은 이벤트 소스에서 이벤트 수신기로의 강력한 참조를 만듭니다. 일반적으로 수신기에 대 한 이벤트 처리기를 연결 하면 이벤트 처리기가 명시적으로 제거 되지 않는 한 수신기에 소스의 개체 수명에 의해 영향을 받는 개체 수명이 있습니다. 그러나 특정 상황에서는 수신기의 개체 수명이 다른 요소 (예: 현재 응용 프로그램의 시각적 트리에 속해 있는지 여부, 소스 수명이 아닌 경우)에 의해 제어 되도록 할 수 있습니다. 소스 개체 수명이 수신기의 개체 수명 보다 크게 확장 될 때마다 일반적인 이벤트 패턴은 메모리 누수를 초래 합니다. 수신기는 의도 한 것 보다 오래 유지 됩니다.  
  
 약한 이벤트 패턴은이 메모리 누수 문제를 해결 하도록 설계 되었습니다. 약한 이벤트 패턴은 수신기가 이벤트에 등록 해야 할 때마다 사용할 수 있지만, 수신기가 등록 취소할 시기를 명시적으로 알 수 없습니다. 소스의 개체 수명이 수신기의 유용한 개체 수명을 초과할 때마다 weak 이벤트 패턴을 사용할 수 있습니다. (이 경우에는 *유용* 하 게 결정 됩니다.) Weak 이벤트 패턴을 사용 하면 수신기가 수신기의 개체 수명 특성에 영향을 주지 않고 이벤트를 등록 하 고 받을 수 있습니다. 실제로 소스에서 암시 된 참조는 수신기가 가비지 수집에 적합 한지 여부를 결정 하지 않습니다. 참조는 약한 참조 이므로 weak 이벤트 패턴 및 관련 Api의 이름을 지정 합니다. 수신기를 가비지 수집 하거나 소멸 시킬 수 있으며, 현재 소멸 된 개체에 대 한 수집 되지 않은 처리기 참조를 유지 하지 않고 소스를 계속할 수 있습니다.  
  
## <a name="who-should-implement-the-weak-event-pattern"></a>약한 이벤트 패턴을 구현 해야 하는 사람은 누구 인가요?  
 약한 이벤트 패턴을 구현 하는 것은 주로 컨트롤 작성자에 게 유용 합니다. 컨트롤 작성자는 컨트롤이 삽입 되는 응용 프로그램에 미치는 영향 및 컨트롤의 동작 및 포함을 주로 담당 합니다. 여기에는 제어 개체 수명 동작이 포함 됩니다. 특히 설명 된 메모리 누수 문제를 처리 하는 것입니다.  
  
 특정 시나리오는 기본적으로 약한 이벤트 패턴의 응용 프로그램에 적합 합니다. 이러한 시나리오 중 하나는 데이터 바인딩입니다. 데이터 바인딩에서 소스 개체는 일반적으로 바인딩의 대상인 수신기 개체와 완전히 독립적으로 진행 됩니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 데이터 바인딩의 많은 측면에는 이미 이벤트 구현 방식에 약한 이벤트 패턴이 적용 되어 있습니다.  
  
## <a name="how-to-implement-the-weak-event-pattern"></a>약한 이벤트 패턴을 구현 하는 방법  
 약한 이벤트 패턴을 구현 하는 방법에는 세 가지가 있습니다. 다음 표에서는 세 가지 방법을 나열 하 고 각각을 사용 해야 하는 경우에 대 한 몇 가지 지침을 제공 합니다.  
  
|접근 방식|구현 시기|  
|--------------|-----------------------|  
|기존 weak 이벤트 관리자 클래스 사용|구독 하려는 이벤트에 해당 <xref:System.Windows.WeakEventManager>하는 경우 기존 weak 이벤트 관리자를 사용 합니다. WPF에 포함 된 weak 이벤트 관리자 목록은 <xref:System.Windows.WeakEventManager> 클래스의 상속 계층 구조를 참조 하세요. 포함 된 weak 이벤트 관리자는 제한적 이므로 다른 방법 중 하나를 선택 해야 합니다.|  
|일반적인 약한 이벤트 관리자 클래스 사용|<xref:System.Windows.WeakEventManager%602> 기존<xref:System.Windows.WeakEventManager> 를 사용할 수 없는 경우 제네릭를 사용 합니다 .이 방법을 사용 하면 쉽게 구현 하 고 효율성을 걱정 하지 않을 수 있습니다. 제네릭 <xref:System.Windows.WeakEventManager%602> 는 기존 또는 사용자 지정 weak 이벤트 관리자 보다 효율성이 낮습니다. 예를 들어, 제네릭 클래스는 이벤트 이름이 지정 된 경우 이벤트를 검색 하기 위해 더 많은 리플렉션을 수행 합니다. 또한 제네릭 <xref:System.Windows.WeakEventManager%602> 를 사용 하 여 이벤트를 등록 하는 코드는 기존 또는 사용자 지정 <xref:System.Windows.WeakEventManager>을 사용 하는 것 보다 더 자세한 정보를 표시 합니다.|  
|사용자 지정 weak 이벤트 관리자 클래스 만들기|<xref:System.Windows.WeakEventManager> 기존<xref:System.Windows.WeakEventManager> 를 사용할 수 없는 경우 사용자 지정을 만들고 최상의 효율성을 원합니다. 사용자 지정 <xref:System.Windows.WeakEventManager> 을 사용 하 여 이벤트를 구독 하는 것이 더 효율적일 수 있지만 앞으로 더 많은 코드를 작성 하는 비용이 발생 합니다.|  
|타사 weak 이벤트 관리자 사용|NuGet에는 [몇 가지 weak 이벤트 관리자](https://www.nuget.org/packages?q=weak+event+manager&prerel=false) 가 있으며 많은 WPF 프레임 워크 에서도 패턴을 지원 합니다. 예를 들어 느슨하게 연결 된 [이벤트 구독에 대 한 프리즘 설명서](https://github.com/PrismLibrary/Prism-Documentation/blob/master/docs/wpf/Communication.md#subscribing-to-events)를 참조 하세요.|

 다음 섹션에서는 weak 이벤트 패턴을 구현 하는 방법을 설명 합니다.  이 논의의 목적을 위해 구독할 이벤트에는 다음과 같은 특징이 있습니다.  
  
- 이벤트 이름은 `SomeEvent`입니다.  
  
- 이벤트는 `EventSource` 클래스에 의해 발생 합니다.  
  
- 이벤트 처리기의 형식은 `SomeEventEventHandler` (또는 `EventHandler<SomeEventEventArgs>`)입니다.  
  
- 이벤트는 형식의 `SomeEventEventArgs` 매개 변수를 이벤트 처리기에 전달 합니다.  
  
### <a name="using-an-existing-weak-event-manager-class"></a>기존 Weak 이벤트 관리자 클래스 사용  
  
1. 기존 weak 이벤트 관리자를 찾습니다.  
  
     WPF에 포함 된 weak 이벤트 관리자 목록은 <xref:System.Windows.WeakEventManager> 클래스의 상속 계층 구조를 참조 하세요.  
  
2. 일반적인 이벤트 후크 대신 새로운 weak 이벤트 관리자를 사용 합니다.  
  
     예를 들어 코드에서 다음 패턴을 사용 하 여 이벤트를 구독할 수 있습니다.  
  
    ```csharp  
    source.SomeEvent += new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     패턴을 다음과 같이 변경 합니다.  
  
    ```csharp  
    SomeEventWeakEventManager.AddHandler(source, OnSomeEvent);  
    ```  
  
     마찬가지로 코드에서 다음 패턴을 사용 하 여 이벤트를 구독 취소 합니다.  
  
    ```csharp  
    source.SomeEvent -= new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     패턴을 다음과 같이 변경 합니다.  
  
    ```csharp  
    SomeEventWeakEventManager.RemoveHandler(source, OnSomeEvent);  
    ```  
  
### <a name="using-the-generic-weak-event-manager-class"></a>일반적인 약한 이벤트 관리자 클래스 사용  
  
1. 일반적인 이벤트 후크 <xref:System.Windows.WeakEventManager%602> 대신 제네릭 클래스를 사용 합니다.  
  
     를 사용 <xref:System.Windows.WeakEventManager%602> 하 여 이벤트 수신기를 등록할 때 이벤트 소스 및 <xref:System.EventArgs> 형식을 클래스에 대 한 형식 매개 변수로 제공 하 고 다음 <xref:System.Windows.WeakEventManager%602.AddHandler%2A> 코드와 같이를 호출 합니다.  
  
    ```csharp  
    WeakEventManager<EventSource, SomeEventEventArgs>.AddHandler(source, "SomeEvent", source_SomeEvent);  
    ```  
  
### <a name="creating-a-custom-weak-event-manager-class"></a>사용자 지정 Weak 이벤트 관리자 클래스 만들기  
  
1. 다음 클래스 템플릿을 프로젝트에 복사 합니다.  
  
     이 클래스에서 상속 된 <xref:System.Windows.WeakEventManager> 클래스입니다.  
  
     [!code-csharp[WeakEvents#WeakEventManagerTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/WeakEvents/CSharp/WeakEventManagerTemplate.cs#weakeventmanagertemplate)]  
  
2. `SomeEventWeakEventManager` 이름을 자신의 이름으로 바꿉니다.  
  
3. 앞에서 설명한 세 개의 이름을 이벤트의 해당 이름으로 바꿉니다. (`SomeEvent`, `EventSource`및 )`SomeEventEventArgs`  
  
4. 약한 이벤트 관리자 클래스의 표시 유형 (공개/내부/개인)을 관리 하는 이벤트와 동일한 표시 유형으로 설정 합니다.  
  
5. 일반적인 이벤트 후크 대신 새로운 weak 이벤트 관리자를 사용 합니다.  
  
     예를 들어 코드에서 다음 패턴을 사용 하 여 이벤트를 구독할 수 있습니다.  
  
    ```csharp  
    source.SomeEvent += new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     패턴을 다음과 같이 변경 합니다.  
  
    ```csharp  
    SomeEventWeakEventManager.AddHandler(source, OnSomeEvent);  
    ```  
  
     마찬가지로 코드에서 다음 패턴을 사용 하 여 이벤트를 구독 취소 합니다.  
  
    ```csharp  
    source.SomeEvent -= new SomeEventEventHandler(OnSome);  
    ```  
  
     패턴을 다음과 같이 변경 합니다.  
  
    ```csharp  
    SomeEventWeakEventManager.RemoveHandler(source, OnSomeEvent);  
    ```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.WeakEventManager>
- <xref:System.Windows.IWeakEventListener>
- [라우트된 이벤트 개요](routed-events-overview.md)
- [데이터 바인딩 개요](../data/data-binding-overview.md)
