---
title: XAML 구문 정보
ms.date: 03/30/2017
helpviewer_keywords:
- XML [WPF], namespaces
- XAML [WPF], parsing of attributes
- parsing of attributes [WPF]
- XAML [WPF], markup extensions
- attached properties [WPF]
- tag syntax [XAML]
- markup extensions [WPF]
- XAML [WPF], object element syntax
- XAML [WPF], syntax terminology
- attached events [WPF]
- lookup semantics [WPF]
- XAML [WPF], attached events
- XAML [WPF], content syntax
- XAML [WPF], lookup semantics
- content syntax [WPF]
- object element syntax [WPF]
- syntax terminology [XAML]
- XAML [WPF], attached properties
- attributes [XAML], parsing
- XAML [WPF], tag syntax
- XAML [WPF], attribute syntax
- property element syntax [WPF]
- terminology [XAML]
- namespaces [WPF], XML
- attribute syntax [XAML]
- XAML [WPF], property element syntax
ms.assetid: 67cce290-ca26-4c41-a797-b68aabc45479
ms.openlocfilehash: d48398f31c1452821292a6feb2867dbd2971e739
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991412"
---
# <a name="xaml-syntax-in-detail"></a>XAML 구문 정보
이 항목에서는 XAML 구문의 요소를 설명 하는 데 사용 되는 용어를 정의 합니다. 이러한 용어는이 설명서의 나머지 부분 전체에서 자주 사용 됩니다. WPF 설명서와 XAML을 사용 하는 다른 프레임 워크 또는 system.xaml 수준에서 XAML 언어 지원에 의해 설정 된 기본 XAML 개념에 대해 자주 사용 됩니다. 이 항목에서는 [XAML 개요 (WPF)](xaml-overview-wpf.md)항목에서 소개 하는 기본 용어를 확장 합니다.  

<a name="the_xaml_language_specification"></a>   
## <a name="the-xaml-language-specification"></a>XAML 언어 사양  
 여기에 정의 된 XAML 구문 용어는 XAML 언어 사양 내 에서도 정의 되거나 참조 됩니다. XAML은 XML을 기반으로 하는 언어 이며 XML 구조 규칙에 따라 다음을 수행 하거나 확장 합니다. 일부 용어는에서 공유 되거나 XML 언어 또는 XML 문서 개체 모델을 설명할 때 일반적으로 사용 되는 용어를 기반으로 합니다.  
  
 Xaml 언어 사양에 대 한 자세한 내용은 Microsoft 다운로드 센터에서 [ \[MS\] -xaml](https://go.microsoft.com/fwlink/?LinkId=114525) 을 다운로드 하세요.  
  
<a name="xaml_and_clr"></a>   
## <a name="xaml-and-clr"></a>XAML 및 CLR  
 XAML은 태그 언어입니다. 이름으로 암시 된 CLR (공용 언어 런타임)은 런타임 실행을 가능 하 게 합니다. XAML은 CLR 런타임에서 직접 사용 하는 공용 언어 중 하나가 아닙니다. 대신 XAML을 자체 형식 시스템을 지 원하는 것으로 간주할 수 있습니다. WPF에서 사용 되는 특정 XAML 구문 분석 시스템은 CLR 및 CLR 형식 시스템을 기반으로 합니다. WPF에 대 한 XAML이 구문 분석 될 때 런타임 표현을 인스턴스화하기 위해 XAML 형식이 CLR 형식에 매핑됩니다. 이러한 이유로이 문서의 구문에 대 한 나머지 부분에는 XAML 언어 사양의 동일한 구문 토론이 아닌 경우에도 CLR 형식 시스템에 대 한 참조가 포함 됩니다. Xaml 언어 사양 수준에 따라 XAML 형식은 다른 형식 시스템에 매핑될 수 있습니다. CLR 일 필요는 없지만 다른 XAML 파서의 생성 및 사용이 필요 합니다.  
  
#### <a name="members-of-types-and-class-inheritance"></a>형식 및 클래스 상속의 멤버  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 형식의 XAML 멤버로 표시 되는 속성 및 이벤트는 기본 형식에서 상속 되는 경우가 많습니다. 예를 들어 다음 `<Button Background="Blue" .../>`예제를 참조 하세요. 클래스 정의, 리플렉션 결과 또는 설명서를 확인 하려는 <xref:System.Windows.Controls.Button> 경우 속성은클래스의바로선언된속성이아닙니다.<xref:System.Windows.Controls.Control.Background%2A> 대신는 기본 <xref:System.Windows.Controls.Control> 클래스에서 상속 됩니다. <xref:System.Windows.Controls.Control.Background%2A>  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] XAML 요소의 클래스 상속 동작은 XML 태그의 스키마 적용 해석에서 상당한 출발입니다. 클래스 상속은 특히 중간 기본 클래스가 추상 이거나 인터페이스가 포함 된 경우 복잡할 수 있습니다. 이는 DTD 또는 XSD 형식과 같이 일반적으로 프로그래밍에 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 사용 되는 스키마 유형을 사용 하 여 XAML 요소 집합 및 해당 특성의 허용 되는 특성을 정확 하 게 표현 하기 어려운 한 가지 이유입니다. 또 다른 이유는 XAML 언어 자체의 확장성 및 형식 매핑 기능에서 허용 되는 형식 및 멤버의 고정 표현의 완전성을 배제 한다는 것입니다.  
  
<a name="object_element_syntax"></a>   
## <a name="object-element-syntax"></a>개체 요소 구문  
 *개체 요소 구문은* XML 요소를 선언 하 여 CLR 클래스 또는 구조체를 인스턴스화하는 XAML 태그 구문입니다. 이 구문은 HTML과 같은 다른 태그 언어의 요소 구문과 유사 합니다. 개체 요소 구문은 왼쪽 꺾쇠 괄호 (\<)로 시작 하 고 인스턴스화된 클래스 또는 구조체의 형식 이름 바로 뒤에 나옵니다. 0 개 이상의 공백이 형식 이름 뒤에 올 수 있으며, 개체 요소에서 0 개 이상의 특성을 선언할 수 있으며 각 특성 이름 = "value" 쌍을 구분 하는 하나 이상의 공백이 있습니다. 마지막으로 다음 중 하나를 충족 해야 합니다.  
  
- 요소와 태그는 슬래시 (/) 뒤에 오른쪽 꺾쇠 괄호 (>)로 즉시 닫혀야 합니다.  
  
- 여는 태그는 오른쪽 꺾쇠 괄호 (>)로 완료 되어야 합니다. 다른 개체 요소, 속성 요소 또는 내부 텍스트는 여는 태그 뒤에 올 수 있습니다. 여기에 포함 될 수 있는 콘텐츠는 일반적으로 요소의 개체 모델에 의해 제한 됩니다. 개체 요소에 해당 하는 닫는 태그도 있어야 하며, 적절 한 중첩 및 다른 여는 태그 쌍과의 균형을 유지 해야 합니다.  
  
 .NET에 의해 구현 되는 XAML에는 개체 요소를 형식, 특성에 속성 또는 이벤트에 매핑하는 규칙 집합, CLR 네임 스페이스와 어셈블리에 XAML 네임 스페이스가 있습니다. WPF 및 .NET의 경우 XAML 개체 요소가 참조 된 어셈블리에 정의 된 .NET 형식에 매핑되고 특성은 해당 형식의 멤버에 매핑됩니다. XAML에서 CLR 형식을 참조 하는 경우 해당 형식의 상속 된 멤버에도 액세스할 수 있습니다.  
  
 예를 들어 다음 예제는 <xref:System.Windows.Controls.Button> 클래스의 새 인스턴스를 인스턴스화하는 개체 요소 구문이 며 특성 및 해당 특성에 대 한 값도 <xref:System.Windows.FrameworkElement.Name%2A> 지정 합니다.  
  
 [!code-xaml[XAMLOvwSupport#SyntaxOE](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#syntaxoe)]  
  
 다음 예제는 XAML 콘텐츠 속성 구문도 포함 하는 개체 요소 구문입니다. 내에 포함 된 내부 텍스트는 <xref:System.Windows.Controls.TextBox> XAML 콘텐츠 속성인를 <xref:System.Windows.Controls.TextBox.Text%2A>설정 하는 데 사용 됩니다.  
  
 [!code-xaml[XAMLOvwSupport#ThisIsATextBox](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#thisisatextbox)]  
  
### <a name="content-models"></a>콘텐츠 모델  
 클래스는 구문을 사용 하 여 XAML 개체 요소로 사용을 지원할 수 있지만이 요소는 전체 콘텐츠 모델 또는 요소 트리의 예상 위치에 배치 된 경우에만 응용 프로그램 또는 페이지에서 제대로 작동 합니다. 예를 들어, <xref:System.Windows.Controls.MenuItem> 은 일반적으로와 <xref:System.Windows.Controls.Menu>같은 <xref:System.Windows.Controls.Primitives.MenuBase> 파생 클래스의 자식 으로만 배치 되어야 합니다. 특정 요소에 대 한 콘텐츠 모델은 XAML 요소로 사용할 수 있는 컨트롤 및 기타 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 클래스에 대 한 클래스 페이지에 대 한 설명의 일부로 설명 됩니다.  
  
<a name="properties_of_object_elements"></a>   
## <a name="properties-of-object-elements"></a>개체 요소의 속성  
 XAML의 속성은 가능한 여러 구문으로 설정 됩니다. 특정 속성에 사용할 수 있는 구문은 설정 중인 속성의 기본 형식 시스템 특성에 따라 달라 집니다.  
  
 속성 값을 설정 하 여 런타임 개체 그래프에 있는 개체에 기능 또는 특징을 추가 합니다. 개체 요소에서 만든 개체의 초기 상태는 매개 변수가 없는 생성자 동작을 기반으로 합니다. 일반적으로 응용 프로그램은 지정 된 개체의 완전히 기본 인스턴스 이외의 다른 항목을 사용 합니다.  
  
<a name="attribute_syntax_properties"></a>   
## <a name="attribute-syntax-properties"></a>특성 구문(속성)  
 특성 구문은 기존 개체 요소에 특성을 선언 하 여 속성에 대 한 값을 설정 하는 XAML 태그 구문입니다. 특성 이름은 관련 개체 요소를 지 원하는 클래스의 속성에 대 한 CLR 멤버 이름과 일치 해야 합니다. 특성 이름 다음에는 할당 연산자 (=)가 나옵니다. 특성 값은 따옴표로 묶인 문자열 이어야 합니다.  
  
> [!NOTE]
> 교대로 반복 되는 따옴표를 사용 하 여 특성 안에 리터럴 따옴표를 추가할 수 있습니다. 예를 들어 큰따옴표를 사용 하 여 큰따옴표 문자를 포함 하는 문자열을 선언할 수 있습니다. 작은따옴표 또는 큰따옴표를 사용 하는 경우에는 일치 하는 쌍을 사용 하 여 특성 값 문자열을 열고 닫아야 합니다. 특정 XAML 구문에 적용 되는 문자 제한을 해결 하는 데 사용할 수 있는 이스케이프 시퀀스 또는 기타 기술도 있습니다. [XML 문자 엔터티 및 XAML을](../../xaml-services/xml-character-entities-and-xaml.md)참조 하세요.  
  
 특성 구문을 통해 설정 하려면 속성이 public 이어야 하며 쓰기 가능 해야 합니다. 지원 형식 시스템의 속성 값은 값 형식 이어야 하며, 관련 된 지원 형식에 액세스할 때 XAML 프로세서가 인스턴스화하거나 참조할 수 있는 참조 형식 이어야 합니다.  
  
 WPF XAML 이벤트의 경우 특성 이름으로 참조 되는 이벤트는 public 이어야 하며 public 대리자가 있어야 합니다.  
  
 속성이 나 이벤트는 포함 하는 개체 요소에 의해 인스턴스화된 클래스 또는 구조체의 멤버 여야 합니다.  
  
### <a name="processing-of-attribute-values"></a>특성 값 처리  
 여는 따옴표와 닫는 따옴표 안에 포함 된 문자열 값은 XAML 프로세서에 의해 처리 됩니다. 속성의 경우 기본 처리 동작은 기본 CLR 속성의 형식에 따라 결정 됩니다.  
  
 이 처리 순서를 사용 하 여 특성 값은 다음 중 하나로 채워집니다.  
  
1. XAML 프로세서가 중괄호 또는에서 <xref:System.Windows.Markup.MarkupExtension>파생 되는 개체 요소를 발견할 경우 값을 문자열로 처리 하는 대신 참조 된 태그 확장이 먼저 평가 되 고 태그 확장에서 반환 된 개체가로 사용 됩니다. 기본값. 대부분의 경우 태그 확장에서 반환 되는 개체는 기존 개체에 대 한 참조 또는 런타임까지 계산을 지연 하는 식이 며 새로 인스턴스화된 개체가 아닙니다.  
  
2. 속성이 특성 <xref:System.ComponentModel.TypeConverter>을 사용 하 여 선언 되거나 해당 속성의 값 형식이 특성 <xref:System.ComponentModel.TypeConverter>을 사용 하 여 선언 된 경우 특성의 문자열 값이 변환 입력으로 형식 변환기에 전송 되 고 변환기에서 반환 됩니다. 새 개체 인스턴스입니다.  
  
3. 가 <xref:System.ComponentModel.TypeConverter>없으면 속성 형식으로 직접 변환 하려고 시도 합니다. 이 최종 수준은 XAML 언어 기본 형식 사이의 파서 네이티브 값에서 직접 변환 하거나, 열거형의 명명 된 상수 이름을 확인 하는 것입니다. 파서는 일치 하는 값에 액세스 합니다.  
  
#### <a name="enumeration-attribute-values"></a>열거 특성 값  
 XAML의 열거는 XAML 파서에서 내부적으로 처리 되며 열거형의 멤버는 열거형의 명명 된 상수 중 하나의 문자열 이름을 지정 하 여 지정 해야 합니다.  
  
 플래그가 지정 되지 않은 열거형 값의 경우 기본 동작은 특성 값의 문자열을 처리 하 고 열거형 값 중 하나로 확인 하는 것입니다. 형식 *열거*에서 열거형을 지정 하지 않습니다. *값*입니다. 대신 *값*만 지정 하면 설정 하는 속성의 형식에 따라 *열거가* 유추 됩니다. *열거형*의 특성을 지정 하는 경우 *값* 형식이 면 제대로 확인 되지 않습니다.  
  
 플래그 열거형의 경우 동작은 <xref:System.Enum.Parse%2A?displayProperty=nameWithType> 메서드를 기반으로 합니다. 각 값을 쉼표로 구분 하 여 플래그 열거에 대 한 값을 여러 개 지정할 수 있습니다. 그러나 플래그가 아닌 열거형 값은 결합할 수 없습니다. 예를 들어, 쉼표 구문을 사용 하 여 nonflag 열거형의 여러 <xref:System.Windows.Trigger> 조건에 대해 작동 하는을 만들 수 없습니다.  
  
```xaml  
<!--This will not compile, because Visibility is not a flagwise enumeration.-->  
...  
<Trigger Property="Visibility" Value="Collapsed,Hidden">  
  <Setter ... />  
</Trigger>  
...  
```  
  
 XAML로 설정할 수 있는 특성을 지 원하는 플래그 열거형은 WPF에서 드물게 발생 합니다. 그러나 이러한 열거형 중 하나는 <xref:System.Windows.Media.StyleSimulations>입니다. 예를 들어 쉼표로 구분 된 플래그 특성 구문을 사용 하 여 <xref:System.Windows.Documents.Glyphs> 클래스에 대 한 설명에 제공 된 예제를 수정할 수 있습니다. `StyleSimulations = "BoldSimulation"` 가 될`StyleSimulations = "BoldSimulation,ItalicSimulation"`수 있습니다. <xref:System.Windows.Input.KeyBinding.Modifiers%2A?displayProperty=nameWithType>둘 이상의 열거형 값을 지정할 수 있는 또 다른 속성입니다. 그러나 열거형에서 <xref:System.Windows.Input.ModifierKeys> 자체 형식 변환기를 지원 하기 때문에이 속성은 특별 한 경우에만 발생 합니다. 한정자에 대 한 형식 변환기는 쉼표 (,)가 아닌 더하기 기호 (+)를 구분 기호로 사용 합니다. 이 변환은 "Ctrl + Alt"와 같이 Microsoft Windows 프로그래밍의 키 조합을 나타내는 보다 일반적인 구문을 지원 합니다.  
  
### <a name="properties-and-event-member-name-references"></a>속성 및 이벤트 멤버 이름 참조  
 특성을 지정 하는 경우 포함 하는 개체 요소에 대해 인스턴스화한 CLR 형식의 멤버로 존재 하는 속성 또는 이벤트를 참조할 수 있습니다.  
  
 또는 포함 하는 개체 요소와 관계 없이 연결 된 속성 또는 연결 된 이벤트를 참조할 수 있습니다. (연결 된 속성은 이후의 섹션에서 설명 합니다.)  
  
 또한 *typeName*을 사용 하 여 기본 네임 스페이스를 통해 액세스할 수 있는 모든 개체에서 이벤트의 이름을 지정할 수 있습니다. 부분적으로 정규화 된 *이벤트* 이름; 이 구문은 자식 요소에서 라우트된 이벤트를 처리 하기 위해 처리기를 사용 하는 라우트된 이벤트에 대 한 처리기를 연결 하는 것을 지원 하지만, 부모 요소의 members 테이블에도 해당 이벤트가 없습니다. 이 구문은 연결 된 이벤트 구문과 유사 하지만 여기에 있는 이벤트는 진정한 연결 된 이벤트가 아닙니다. 대신 정규화 된 이름을 가진 이벤트를 참조 합니다. 자세한 내용은 [라우트된 이벤트 개요](routed-events-overview.md)합니다.  
  
 일부 시나리오에서는 속성 이름이 특성 이름이 아니라 특성의 값으로 제공 되는 경우도 있습니다. 해당 속성 이름에는 *ownerType*형식으로 지정 된 속성과 같은 한정자도 포함 될 수 있습니다. *dependencyPropertyName*. 이 시나리오는 XAML에서 스타일이 나 템플릿을 작성할 때 일반적입니다. 특성 값으로 제공 되는 속성 이름에 대 한 처리 규칙은 서로 다르며, 설정 되는 속성의 형식이 나 특정 WPF 하위 시스템의 동작에 의해 제어 됩니다. 자세한 내용은 스타일 지정 [및 템플릿](../controls/styling-and-templating.md)을 참조 하세요.  
  
 속성 이름에 대 한 다른 용도는 특성 값이 속성 속성 관계를 설명 하는 경우입니다. 이 기능은 데이터 바인딩과 스토리 보드 대상에 사용 되며 <xref:System.Windows.PropertyPath> 클래스와 해당 형식 변환기로 설정 됩니다. 조회 의미 체계에 대 한 자세한 설명은 [PROPERTYPATH XAML 구문](propertypath-xaml-syntax.md)을 참조 하세요.  
  
<a name="property_element_syntax"></a>   
## <a name="property-element-syntax"></a>속성 요소 구문  
 *Property 요소 구문은* 요소에 대 한 기본 XML 구문 규칙에서 달라 지므로 하는 구문입니다. XML에서 특성의 값은 사실상 문자열이 며 문자열 인코딩 형식만 사용 되는 경우에만 가능한 변형입니다. XAML에서 다른 개체 요소를 속성의 값으로 할당할 수 있습니다. 이 기능은 속성 요소 구문에 의해 활성화 됩니다. 요소 태그 내에서 특성으로 지정 되는 속성 대신 *Elementtypename*의 여는 요소 태그를 사용 하 여 속성을 지정 합니다. *propertyName* 폼, 속성 값이 내에서 지정 된 다음 property 요소가 닫혀 있습니다.  
  
 특히 구문은 왼쪽 꺾쇠 괄호 (\<)로 시작 하 고 그 뒤에는 속성 요소 구문이 포함 된 클래스 또는 구조체의 형식 이름이 바로 앞에 옵니다. 이 바로 뒤에는 단일 점 (.), 속성 이름, 오른쪽 꺾쇠 괄호 (>) 순으로 차례로 옵니다. 특성 구문과 마찬가지로 해당 속성은 지정 된 형식의 선언 된 public 멤버 내에 있어야 합니다. 속성에 할당할 값은 property 요소에 포함 됩니다. 일반적으로이 값은 하나 이상의 개체 요소로 지정 됩니다. 개체를 값으로 지정 하는 시나리오는 속성 요소 구문이 처리할 시나리오 이기 때문입니다. 마지막으로 동일한 *Elementtypename*을 지정 하는 상응 하는 닫는 태그입니다. *propertyName* 조합을 제공 해야 하며, 적절 한 중첩 및 다른 요소 태그와 균형을 맞추어야 합니다.  
  
 예를 들어 다음은 <xref:System.Windows.FrameworkElement.ContextMenu%2A> <xref:System.Windows.Controls.Button>의 속성에 대 한 속성 요소 구문입니다.  
  
 [!code-xaml[XAMLOvwSupport#ContextMenu](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#contextmenu)]  
  
 속성 요소 내의 값은 지정 되는 속성 형식이와 <xref:System.String>같은 기본 값 형식 이거나 이름이 지정 된 열거형 인 경우에도 내부 텍스트로 제공 될 수 있습니다. 이러한 두 가지 사용은 일반적이 지 않습니다. 이러한 각 경우에는 보다 간단한 특성 구문을 사용할 수도 있기 때문입니다. 속성 요소를 문자열로 채우는 한 가지 시나리오는 XAML 콘텐츠 속성이 아니지만 UI 텍스트 표현에 사용 되는 속성에 대 한 것 이며, 줄 바꿈과 같은 특정 공백 요소가 해당 UI 텍스트에 표시 되어야 합니다. 특성 구문은 줄 바꿈을 유지할 수 없지만, 유효 공백 유지가 활성화 되어 있으면 속성 요소 구문이 가능 합니다. 자세한 내용은 [XAML의 공백 처리](../../xaml-services/whitespace-processing-in-xaml.md)를 참조 하세요. 또 다른 시나리오는 [X:Uid 지시문](../../xaml-services/x-uid-directive.md) 을 property 요소에 적용 하 여의 값을 WPF 출력 BAML 또는 다른 기술에서 지역화 해야 하는 값으로 표시 하는 것입니다.  
  
 속성 요소는 WPF 논리 트리에 표시 되지 않습니다. 속성 요소는 속성을 설정 하기 위한 특정 구문 이지만 인스턴스 또는 개체를 지 원하는 요소는 아닙니다. 논리적 트리 개념에 대 한 자세한 내용은 [WPF의 트리](trees-in-wpf.md)를 참조 하세요.  
  
 특성과 속성 요소 구문이 모두 지원 되는 속성의 경우 두 구문은 일반적으로 동일한 결과를 가집니다. 단, 공백 처리와 같은 세부 사항은 구문 사이에서 약간 다를 수 있습니다.  
  
<a name="collection_syntax"></a>   
## <a name="collection-syntax"></a>컬렉션 구문  
 XAML 사양에서는 값 형식이 컬렉션인 속성을 식별 하기 위해 XAML 프로세서 구현이 필요 합니다. .NET의 일반적인 XAML 프로세서 구현은 관리 코드 및 CLR을 기반으로 하며 다음 중 하나를 통해 컬렉션 형식을 식별 합니다.  
  
- 형식을 구현 <xref:System.Collections.IList>합니다.  
  
- 형식을 구현 <xref:System.Collections.IDictionary>합니다.  
  
- 형식이에서 <xref:System.Array> 파생 됩니다. XAML의 배열에 대 한 자세한 내용은 [x:Array 태그 확장](../../xaml-services/x-array-markup-extension.md)을 참조 하세요.  
  
 속성 형식이 컬렉션인 경우에는 유추 된 컬렉션 형식을 개체 요소로 태그에 지정할 필요가 없습니다. 대신 컬렉션의 항목으로 사용 되는 요소는 property 요소의 자식 요소로 하나 이상의 자식 요소로 지정 됩니다. 이러한 각 항목은 로드 하는 동안 개체로 계산 된 후 암시적 컬렉션의 `Add` 메서드를 호출 하 여 컬렉션에 추가 됩니다. 예를 들어의 <xref:System.Windows.Style.Triggers%2A> <xref:System.Windows.Style> 속성은을 구현 <xref:System.Collections.IList>하는 특수화 <xref:System.Windows.TriggerCollection>된 컬렉션 형식을 사용 합니다. 태그의 개체 요소를 <xref:System.Windows.TriggerCollection> 인스턴스화할 필요는 없습니다. 대신 `Style.Triggers` 속성 요소 내에서 하나 이상의 <xref:System.Windows.Trigger> 항목을 요소로 지정 합니다. 여기서 <xref:System.Windows.Trigger> (또는 파생 클래스)은 강력한 형식 및 암시적 <xref:System.Windows.TriggerCollection>의 항목 형식으로 예상 되는 형식입니다.  
  
 [!code-xaml[XAMLOvwSupport#SyntaxPECollection](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#syntaxpecollection)]  
  
 속성은이 항목의 다음 섹션에서 설명 하는 해당 형식 및 파생 형식에 대 한 컬렉션 형식 및 XAML 콘텐츠 속성 일 수 있습니다.  
  
 암시적 컬렉션 요소는 태그에 요소로 나타나지 않는 경우에도 논리적 트리 표현에서 멤버를 만듭니다. 일반적으로 부모 형식의 생성자는 해당 속성 중 하나인 컬렉션에 대해 인스턴스화를 수행 하 고 처음에는 빈 컬렉션이 개체 트리의 일부가 됩니다.  
  
> [!NOTE]
> 제네릭 목록 및 사전 인터페이스 (<xref:System.Collections.Generic.IList%601> 및 <xref:System.Collections.Generic.IDictionary%602>)는 컬렉션 검색에 대해 지원 되지 않습니다. 그러나 클래스는 <xref:System.Collections.Generic.List%601> 직접 <xref:System.Collections.Generic.Dictionary%602> 을 <xref:System.Collections.IList> 구현<xref:System.Collections.IDictionary> 하기 때문에 클래스를 기본 클래스로 사용할 수 있습니다.  
  
 컬렉션 형식에 대 한 .NET 참조 페이지에서 컬렉션에 대 한 개체 요소를 의도적으로 생략 하는이 구문은 XAML 구문 섹션에서 암시적 컬렉션 구문으로 표시 되기도 합니다.  
  
 루트 요소를 제외 하 고, 다른 요소의 자식 요소로 중첩 된 XAML 파일의 모든 개체 요소는 사실 부모 요소의 암시적 컬렉션 속성의 멤버 중 하나 또는 둘 다의 요소입니다. 또는 부모 요소에 대 한 XAML 콘텐츠 속성의 값을 지정 하는 요소입니다 (XAML 콘텐츠 속성은 이후의 섹션에서 설명). 즉, 태그 페이지의 부모 요소와 자식 요소의 관계는 실질적으로 루트의 단일 개체 이며, 루트 아래의 모든 개체 요소는 부모의 속성 값을 제공 하는 단일 인스턴스이거나 col 내 항목 중 하나입니다. 부모의 컬렉션 형식 속성 값 이기도 한 lection입니다. 이 단일 루트 개념은 XML에 공통적 이며와 같이 <xref:System.Windows.Markup.XamlReader.Load%2A>XAML을 로드 하는 api의 동작에서 자주 강화 됩니다.  
  
 다음 예제는 명시적으로 지정 된 컬렉션<xref:System.Windows.Media.GradientStopCollection>에 대 한 개체 요소를 포함 하는 구문입니다.  
  
```xaml  
<LinearGradientBrush>  
  <LinearGradientBrush.GradientStops>  
    <GradientStopCollection>  
      <GradientStop Offset="0.0" Color="Red" />  
      <GradientStop Offset="1.0" Color="Blue" />  
    </GradientStopCollection>  
  </LinearGradientBrush.GradientStops>  
</LinearGradientBrush>  
```  
  
 컬렉션을 명시적으로 선언 하는 것은 항상 가능 하지는 않습니다. 예를 들어, 이전에 <xref:System.Windows.TriggerCollection> 표시 <xref:System.Windows.Style.Triggers%2A> 된 예제에서를 명시적으로 선언 하려고 하면 실패 합니다. 컬렉션을 명시적으로 선언 하려면 컬렉션 클래스에서 매개 변수가 없는 생성자를 지원 해야 <xref:System.Windows.TriggerCollection> 하 고 매개 변수가 없는 생성자가 없어야 합니다.  
  
<a name="xaml_content_properties"></a>   
## <a name="xaml-content-properties"></a>XAML 콘텐츠 속성  
 XAML 콘텐츠 구문은를 <xref:System.Windows.Markup.ContentPropertyAttribute> 해당 클래스 선언의 일부로 지정 하는 클래스 에서만 사용할 수 있는 구문입니다. 는 <xref:System.Windows.Markup.ContentPropertyAttribute> 파생 클래스를 포함 하 여 해당 요소 형식에 대 한 콘텐츠 속성인 속성 이름을 참조 합니다. XAML 프로세서에서 처리 하는 경우 개체 요소의 여는 태그와 닫는 태그 사이에 있는 모든 자식 요소나 내부 텍스트는 해당 개체에 대 한 XAML 콘텐츠 속성의 값으로 할당 됩니다. Content 속성에 대 한 명시적 속성 요소를 지정할 수 있지만이 사용은 일반적으로 .NET 참조의 XAML 구문 섹션에 표시 되지 않습니다. 명시적/자세한 기술 기술은 태그 명확성을 위해 또는 태그 스타일의 중요 한 값을 가지 지만, 일반적으로 콘텐츠 속성의 목적은 부모-자식과 직관적으로 관련 된 요소를 직접 중첩할 수 있도록 태그를 간소화 하는 것입니다. 요소의 다른 속성에 대 한 속성 요소 태그는 엄격한 XAML 언어 정의에 따라 "내용"으로 할당 되지 않습니다. 이러한 작업은 이전에 XAML 파서의 처리 순서에서 처리 되며 "내용"으로 간주 되지 않습니다.  
  
### <a name="xaml-content-property-values-must-be-contiguous"></a>XAML 콘텐츠 속성 값은 연속적 이어야 합니다.  
 XAML 콘텐츠 속성의 값은 해당 개체 요소에 대 한 다른 속성 요소 보다 먼저 또는 완전히 뒤에 지정 해야 합니다. 이는 XAML 콘텐츠 속성의 값이 문자열 또는 하나 이상의 개체로 지정 되는지 여부에 해당 합니다. 예를 들어 다음 태그는 구문 분석 하지 않습니다.  
  
```xaml  
<Button>I am a   
  <Button.Background>Blue</Button.Background>  
  blue button</Button>  
```  
  
 콘텐츠 속성의 속성 요소 구문을 사용 하 여이 구문을 명시적으로 만든 경우 content 속성을 두 번 설정 했기 때문에이는 기본적으로 유효 하지 않습니다.  
  
```xaml  
<Button>  
  <Button.Content>I am a </Button.Content>  
  <Button.Background>Blue</Button.Background>  
  <Button.Content> blue button</Button.Content>  
</Button>  
```  
  
 이와 유사한 잘못 된 예제는 content 속성이 컬렉션인 경우와 자식 요소가 속성 요소와 함께 사용 되는 경우입니다.  
  
```xaml  
<StackPanel>  
  <Button>This example</Button>  
  <StackPanel.Resources>  
    <SolidColorBrush x:Key="BlueBrush" Color="Blue"/>  
  </StackPanel.Resources>  
  <Button>... is illegal XAML</Button>  
</StackPanel>  
```  
  
<a name="content_properties_and_collection_syntax_combined"></a>   
## <a name="content-properties-and-collection-syntax-combined"></a>콘텐츠 속성 및 컬렉션 구문 조합  
 단일 개체 요소를 콘텐츠로 허용 하려면 콘텐츠 속성의 형식이 특히 컬렉션 형식 이어야 합니다. 컬렉션 형식에 대 한 속성 요소 구문과 마찬가지로 XAML 프로세서는 컬렉션 형식인 형식을 식별 해야 합니다. 요소에 XAML 콘텐츠 속성이 있고 XAML 콘텐츠 속성의 형식이 컬렉션인 경우에는 암시적 컬렉션 형식을 개체 요소로 태그에 지정할 필요가 없으며 XAML 콘텐츠 속성을 속성으로 지정할 필요가 없습니다. el 차서. 따라서 태그의 명백한 콘텐츠 모델에는 이제 내용으로 둘 이상의 자식 요소가 할당 될 수 있습니다. 다음은 <xref:System.Windows.Controls.Panel> 파생 된 클래스에 대 한 내용 구문입니다. 모든 <xref:System.Windows.Controls.Panel> 파생 클래스는 XAML 콘텐츠 속성을 <xref:System.Windows.Controls.Panel.Children%2A>로 설정 합니다 .이 속성에는 형식의 <xref:System.Windows.Controls.UIElementCollection>값이 필요 합니다.  
  
 [!code-xaml[XAMLOvwSupport#SyntaxContent](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page5.xaml#syntaxcontent)]  
  
 의 property 요소 <xref:System.Windows.Controls.Panel.Children%2A> 와의 요소 <xref:System.Windows.Controls.UIElementCollection> 는 태그에 필요 하지 않습니다. 이는 XAML의 디자인 기능으로,을 정의 하는 재귀적으로 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 포함 된 요소가 중간 속성 요소 태그 없이 직계 부모-자식 요소 관계를 가진 중첩 된 요소의 트리로 보다 직관적으로 표현 됩니다. 컬렉션 개체입니다. 실제로는 <xref:System.Windows.Controls.UIElementCollection> 의도적으로 태그에서 개체 요소로 명시적으로 지정할 수 없습니다. 유일 하 게 사용 되는 것은 암시적 컬렉션 <xref:System.Windows.Controls.UIElementCollection> 이므로는 매개 변수가 없는 public 생성자를 노출 하지 않으므로 개체 요소로 인스턴스화할 수 없습니다.  
  
### <a name="mixing-property-elements-and-object-elements-in-an-object-with-a-content-property"></a>콘텐츠 속성을 사용 하 여 개체에서 속성 요소 및 개체 요소 혼합  
 Xaml 사양에서는 XAML 프로세서가 개체 요소 내에서 XAML 콘텐츠 속성을 채우는 데 사용 되는 개체 요소를 연속 해야 하며 혼합할 수 없도록 선언 합니다. 속성 요소와 콘텐츠를 혼합 하는 이러한 제한은 XAML 프로세서 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 에 의해 적용 됩니다.  
  
 자식 개체 요소를 개체 요소 내의 첫 번째 직접 태그로 사용할 수 있습니다. 그런 다음 속성 요소를 도입할 수 있습니다. 또는 하나 이상의 속성 요소, 콘텐츠, 추가 속성 요소를 지정할 수 있습니다. 그러나 속성 요소가 콘텐츠 뒤에 오면 추가 콘텐츠를 도입할 수 없으며 속성 요소만 추가할 수 있습니다.  
  
 이 내용/속성 요소 순서 요구 사항은 콘텐츠로 사용 되는 내부 텍스트에 적용 되지 않습니다. 그러나 속성 요소가 내부 텍스트와 함께 사용 되는 경우 유효 공백은 태그에서 시각적으로 검색 하기가 어렵기 때문에 내부 텍스트를 연속 하 여 유지 하는 것은 여전히 좋은 태그 스타일입니다.  
  
<a name="xaml_namespaces"></a>   
## <a name="xaml-namespaces"></a>XAML 네임스페이스  
 이전 구문 예제에서 기본 XAML 네임 스페이스 이외의 XAML 네임 스페이스를 지정 하지 않았습니다. 일반적인 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램에서 기본 XAML 네임 스페이스는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 네임 스페이스로 지정 됩니다. 기본 XAML 네임 스페이스 외에도 여전히 유사한 구문을 사용 하는 XAML 네임 스페이스를 지정할 수 있습니다. 그러나 기본 XAML 네임 스페이스 내에서 액세스할 수 없는 클래스 이름이 지정 된 위치에 있는 경우 해당 클래스 이름 앞에는 해당 CLR 네임 스페이스에 매핑된 XAML 네임 스페이스의 접두사가와 야 합니다. 예를 들어 `<custom:Example/>` ,는 `Example` 클래스의 인스턴스를 인스턴스화하는 개체 요소 구문입니다 .이 클래스는 해당 클래스를 포함 하는 CLR 네임 스페이스 (및 지원 형식을 포함 하는 외부 어셈블리 정보)가 이전에에 매핑 되었습니다. `custom` 접두사.  
  
 XAML 네임 스페이스에 대 한 자세한 내용은 [WPF xaml을 위한 Xaml 네임 스페이스 및 네임 스페이스 매핑](xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)을 참조 하세요.  
  
<a name="markup_extensions"></a>   
## <a name="markup-extensions"></a>태그 확장  
 XAML은 문자열 특성 값 또는 개체 요소의 일반적인 XAML 프로세서 처리에서 이스케이프할 수 있도록 하 고 지원 클래스에 대 한 처리를 지연 하는 태그 확장 프로그래밍 엔터티를 정의 합니다. 특성 구문을 사용 하는 경우 XAML 프로세서에 대 한 태그 확장을 식별 하는 문자는 여는 중괄호 ({)와 닫는 중괄호 (}) 이외의 모든 문자를 나타냅니다. 여는 중괄호 뒤의 첫 번째 문자열은 특정 확장 동작을 제공 하는 클래스를 참조 해야 합니다 .이 경우에는 해당 하위 문자열이 진정한 클래스 이름의 일부인 경우 참조에서 하위 문자열 "Extension"을 생략할 수 있습니다. 이후에는 단일 공간이 나타날 수 있으며, 그 다음에 나오는 각 문자는 닫는 중괄호가 나타날 때까지 확장 구현에서 입력으로 사용 됩니다.  
  
 .Net XAML 구현에서는에서 <xref:System.Windows.Markup.MarkupExtension> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 지 원하는 모든 태그 확장의 기반으로 추상 클래스를 사용 하 고 다른 프레임 워크 또는 기술도 사용 합니다. 특수 하 게 구현 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 되는 태그 확장은 다른 기존 개체를 참조 하거나 런타임에 계산 될 개체에 대해 지연 된 참조를 만들 수 있는 수단을 제공 하기 위한 것입니다. 예를 들어 특정 속성에 일반적으로 사용 되는 값 대신 `{Binding}` 태그 확장을 지정 하 여 간단한 WPF 데이터 바인딩을 수행 합니다. 대부분의 WPF 태그 확장은 특성 구문이 가능 하지 않은 속성에 대 한 특성 구문을 사용 합니다. 예를 들어 개체 <xref:System.Windows.Style> 는 중첩 된 일련의 개체 및 속성을 포함 하는 비교적 복잡 한 형식입니다. Wpf의 스타일은 일반적으로의 <xref:System.Windows.ResourceDictionary>리소스로 정의 된 다음 리소스를 요청 하는 두 개의 WPF 태그 확장 중 하나를 통해 참조 됩니다. 태그 확장은 리소스 조회에 대 한 속성 값의 계산을 지연 하 고 다음 예제와 같이 특성 <xref:System.Windows.FrameworkElement.Style%2A> 구문을 사용 하 여 <xref:System.Windows.Style>속성 값을 제공 합니다.  
  
 `<Button Style="{StaticResource MyStyle}">My button</Button>`  
  
 여기서는 태그 확장 <xref:System.Windows.StaticResourceExtension> 구현을 제공 하는 클래스를 식별합니다.`StaticResource` 다음 문자열 `MyStyle` 은 기본 <xref:System.Windows.StaticResourceExtension> 이 아닌 생성자의 입력으로 사용 됩니다. 여기서 확장 문자열에서 가져온 매개 변수는 요청 <xref:System.Windows.ResourceKey>된를 선언 합니다. `MyStyle`는 리소스로 <xref:System.Windows.Style> 정의 된의 [x:Key](../../xaml-services/x-key-directive.md) 값 이어야 합니다. [StaticResource 태그 확장](staticresource-markup-extension.md) 사용은 리소스를 로드 시 정적 리소스 조회 논리를 <xref:System.Windows.Style> 통해 속성 값을 제공 하는 데 사용 하도록 요청 합니다.  
  
 태그 확장에 대한 자세한 내용은 [XAML 태그 확장 및 WPF XAML](markup-extensions-and-wpf-xaml.md)을 참조하세요. 일반 .net XAML 구현에서 사용 되는 태그 확장 및 기타 XAML 프로그래밍 기능에 대 한 참조는 [xaml 네임 스페이스 (x:)를 참조 하세요. 언어 기능](../../xaml-services/xaml-namespace-x-language-features.md). WPF 관련 태그 확장은 [WPF XAML 확장](wpf-xaml-extensions.md)을 참조 하세요.  
  
<a name="attached_properties"></a>   
## <a name="attached-properties"></a>연결된 속성  
 연결 된 속성은 특정 형식에서 속성을 소유 하 고 정의할 수 있지만 모든 요소에서 특성 또는 속성 요소로 설정할 수 있는 XAML로 도입 된 프로그래밍 개념입니다. 연결 된 속성을 사용 하는 기본 시나리오는 모든 요소에 대해 광범위 한 공유 개체 모델을 요구 하지 않고도 태그 구조의 자식 요소가 부모 요소에 정보를 보고할 수 있도록 하는 것입니다. 반대로, 연결 된 속성은 부모 요소에서 자식 요소에 대 한 정보를 보고 하는 데 사용할 수 있습니다. 연결 된 속성의 목적과 연결 된 속성을 만드는 방법에 대 한 자세한 내용은 [연결 된 속성 개요](attached-properties-overview.md)를 참조 하세요.  
  
 연결 된 속성은 *typeName*도 지정 한다는 표면적 속성 요소 구문과 유사한 구문을 사용 합니다. *propertyName* 조합입니다. 다음과 같은 두 가지 중요한 차이점이 있습니다.  
  
- *TypeName*을 사용할 수 있습니다. 특성 구문을 통해 연결 된 속성을 설정 하는 경우에도 *propertyName* 조합이 가능 합니다. 연결 된 속성은 속성 이름을 정규화 하는 경우에만 특성 구문의 요구 사항입니다.  
  
- 연결 된 속성에 대해 속성 요소 구문을 사용할 수도 있습니다. 그러나 일반적인 속성 요소 구문의 경우 지정 하는 *typeName* 은 property 요소를 포함 하는 개체 요소입니다. 연결 된 속성을 참조 하는 경우 *typeName* 은 포함 하는 개체 요소가 아니라 연결 된 속성을 정의 하는 클래스입니다.  
  
<a name="attached_events"></a>   
## <a name="attached-events"></a>연결된 이벤트  
 연결 된 이벤트는 특정 형식으로 이벤트를 정의할 수 있지만 모든 개체 요소에 대 한 처리기가 연결 될 수 있는 XAML에서 도입 된 다른 프로그래밍 개념입니다. WOF 구현에서 연결 된 이벤트를 정의 하는 형식은 서비스를 정의 하는 정적 형식이 고, 경우에 따라 연결 된 이벤트는 서비스를 노출 하는 형식의 라우트된 이벤트 별칭에 의해 노출 됩니다. 연결 된 이벤트에 대 한 처리기는 특성 구문을 통해 지정 됩니다. 연결 된 이벤트와 마찬가지로 특성 구문은 연결 된 이벤트에 대해 확장 되어 *typeName*을 허용 합니다. *eventname* 사용. 여기서 *typeName* 은 연결 된 이벤트 인프라 `Add` 에 `Remove` 대해 및 이벤트 처리기 접근자를 제공 하는 클래스이 고 *eventName* 은 이벤트 이름입니다.  
  
<a name="anatomy_of_a_xaml_page_root_element"></a>   
## <a name="anatomy-of-a-xaml-root-element"></a>XAML 루트 요소 분석  
 다음 표에서는 일반적인 XAML 루트 요소를 세분화 하 여 루트 요소의 특정 특성을 보여 줍니다.  
  
|||  
|-|-|  
|`<Page`|Root 요소의 개체 요소를 여는 중|  
|`xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`|Default ([!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]) XAML 네임 스페이스|  
|`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`|XAML 언어 XAML 네임 스페이스|  
|`x:Class="ExampleNamespace.ExampleCode"`|Partial 클래스에 대해 정의 된 코드 숨김으로 태그를 연결 하는 partial 클래스 선언입니다.|  
|`>`|루트에 대 한 개체 요소의 끝입니다. 요소가 자식 요소를 포함 하기 때문에 개체가 아직 닫혀 있지 않습니다.|  
  
<a name="optional_and_nonrecommended_xaml_usages"></a>   
## <a name="optional-and-nonrecommended-xaml-usages"></a>선택적 및 권장 되지 않는 XAML 용도  
 다음 섹션에서는 xaml 프로세서에서 기술적으로 지원 되지만 xaml 소스를 포함 하는 응용 프로그램을 개발할 때 사용자가 읽을 수 있는 XAML 파일을 방해 하는 자세한 정보 표시 또는 기타 미적 문제를 생성 하는 XAML 사용에 대해 설명 합니다.  
  
### <a name="optional-property-element-usages"></a>선택적 속성 요소 사용  
 선택적 속성 요소 사용에는 XAML 프로세서에서 암시적으로 고려 하는 요소 콘텐츠 속성을 명시적으로 작성 하는 작업이 포함 됩니다. 예를 들어의 <xref:System.Windows.Controls.Menu>콘텐츠를 선언 하는 경우의 <xref:System.Windows.Controls.ItemsControl.Items%2A> `<Menu.Items>` `<Menu.Items>` 컬렉션을 속성 요소 태그로 명시적으로 선언 하 고 <xref:System.Windows.Controls.Menu> , 대신에 각 <xref:System.Windows.Controls.MenuItem> 컬렉션을 삽입할 수 있습니다. 암시적 XAML 프로세서 동작을 사용 하는 것 보다의 <xref:System.Windows.Controls.Menu> 모든 자식 요소가 이어야 하 <xref:System.Windows.Controls.MenuItem> <xref:System.Windows.Controls.ItemsControl.Items%2A> 고 컬렉션에 배치 되어야 합니다. 경우에 따라 선택적 사용을 사용 하면 태그에 표시 된 개체 구조를 시각적으로 명확 하 게 파악할 수 있습니다. 또는 명시적 속성 요소를 사용 하는 경우에는 기술적으로 작동 하지만 시각적으로 혼동 되는 태그를 방지할 수 있습니다 (예: 특성 값 내 중첩 된 태그 확장).  
  
### <a name="full-typenamemembername-qualified-attributes"></a>전체 typeName. memberName 정규화 된 특성  
 형식 *이름*입니다. 특성에 대 한 *memberName* 폼은 실제로 라우트된 이벤트 사례 보다 훨씬 더 일반적으로 작동 합니다. 그러나 형식이 불필요 하 고 태그 스타일 및 가독성을 위해 필요한 경우에만이를 방지 해야 하는 경우도 있습니다. 다음 예제에서 <xref:System.Windows.Controls.Control.Background%2A> 특성에 대 한 세 개의 참조는 모두 동일 합니다.  
  
 [!code-xaml[XAMLOvwSupport#TypeNameProp](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#typenameprop)]  
  
 `Button.Background`에서 <xref:System.Windows.Controls.Button> 해당 속성에 대 한 정규화 된 조회가 성공 하 고<xref:System.Windows.Controls.Control.Background%2A> <xref:System.Windows.Controls.Button> (컨트롤에서 상속 됨) 개체 요소의 클래스 또는 기본 클래스 이기 때문에 작동 합니다. `Control.Background`클래스는 <xref:System.Windows.Controls.Control> 실제로을 정의 <xref:System.Windows.Controls.Control.Background%2A> 하 고 <xref:System.Windows.Controls.Control> <xref:System.Windows.Controls.Button> 기본 클래스 이기 때문에 작동 합니다.  
  
 그러나 다음 형식 *이름*입니다. *memberName* form 예제는 작동 하지 않으므로 주석으로 표시 됩니다.  
  
 [!code-xaml[XAMLOvwSupport#TypeNameBadProp](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#typenamebadprop)]  
  
 <xref:System.Windows.Controls.Label>는의 <xref:System.Windows.Controls.Control>다른 파생 클래스 이며, <xref:System.Windows.Controls.Label> 개체 요소 내에서 `Label.Background` 를 지정한 경우이 사용이 정상적으로 작동 합니다. 그러나는의 <xref:System.Windows.Controls.Button>클래스 또는 기본 클래스가 아니므로 지정 된 XAML 프로세서 동작은를 연결 된 속성으로 처리 `Label.Background` 하는 것입니다. <xref:System.Windows.Controls.Label> `Label.Background`는 사용 가능한 연결 된 속성이 아니므로이 사용이 실패 합니다.  
  
### <a name="basetypenamemembername-property-elements"></a>baseTypeName. memberName 속성 요소  
 *TypeName*과 비슷한 방법으로 *memberName* Form은 *basetypename*특성 구문에 대해 작동 합니다. *memberName* 구문은 속성 요소 구문에 대해 작동 합니다. 예를 들어 다음 구문은 작동 합니다.  
  
 [!code-xaml[XAMLOvwSupport#GoofyPE](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofype)]  
  
 여기서 property 요소는에 포함 되어 있는 `Control.Background` 경우에 `Button`도로 지정 되었습니다.  
  
 하지만 *typeName*과 동일 합니다. *memberName* 특성에 대 한 형식 *basetypename*. *memberName* 가 태그에서 잘못 된 스타일 이므로이를 방지 해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [XAML 개요(WPF)](xaml-overview-wpf.md)
- [XAML 네임 스페이스 (x:) 언어 기능](../../xaml-services/xaml-namespace-x-language-features.md)
- [WPF XAML 확장](wpf-xaml-extensions.md)
- [종속성 속성 개요](dependency-properties-overview.md)
- [TypeConverter 및 XAML](typeconverters-and-xaml.md)
- [WPF에 대한 XAML 및 사용자 지정 클래스](xaml-and-custom-classes-for-wpf.md)
