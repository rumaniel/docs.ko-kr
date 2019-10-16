---
title: UriTemplate 및 UriTemplateTable
ms.date: 03/30/2017
ms.assetid: 5cbbe03f-4a9e-4d44-9e02-c5773239cf52
ms.openlocfilehash: f51d6fa5c78d97cf11a3c0005be7656013b30e90
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69955275"
---
# <a name="uritemplate-and-uritemplatetable"></a>UriTemplate 및 UriTemplateTable
웹 개발자는 서비스가 응답하는 URI의 셰이프 및 레이아웃을 설명할 수 있어야 합니다. WCF (Windows Communication Foundation)에는 개발자가 Uri를 제어할 수 있도록 두 개의 새로운 클래스가 추가 되었습니다. <xref:System.UriTemplate>및 <xref:System.UriTemplateTable> 는 WCF에서 URI 기반 디스패치 엔진의 기본을 형성 합니다. 이러한 클래스를 자체적으로 사용할 수도 있으므로 개발자는 WCF 서비스를 구현 하지 않고도 템플릿 및 URI 매핑 메커니즘을 활용할 수 있습니다.  
  
## <a name="templates"></a>템플릿  
 템플릿을 사용하면 상대 URI 집합을 설명할 수 있습니다. 다음 표의 URI 템플릿 집합은 다양한 날씨 정보를 검색하는 시스템을 정의하는 방법을 보여 줍니다.  
  
|보기|템플릿|  
|----------|--------------|  
|전국 예보|weather/national|  
|시/도 예보|weather/{state}|  
|구/군/시 예보|weather/{state}/{city}|  
|활동 예보|weather/{state}/{city}/{activity}|  
  
 이 표에서는 구조적으로 비슷한 URI 집합을 보여 줍니다. 각 항목은 URI 템플릿에 해당합니다. 중괄호 안에 있는 세그먼트는 변수를 설명하고 중괄호 밖에 있는 세그먼트는 리터럴 문자열을 설명합니다. 개발자는 WCF 템플릿 클래스를 사용 하 여 들어오는 URI (예: "/weather/wa/seattle/cycling")를 가져와서이를 설명 하는 템플릿 ("/weather/{state}/{city}/{activity}")에 일치 시킬 수 있습니다.  
  
## <a name="uritemplate"></a>UriTemplate  
 <xref:System.UriTemplate>은 URI 템플릿을 캡슐화하는 클래스입니다. 생성자는 템플릿을 정의하는 문자열 매개 변수를 사용합니다. 이 문자열에는 다음 단원에 설명된 형식의 템플릿이 포함되어 있습니다. <xref:System.UriTemplate> 클래스는 수신 URI를 템플릿에 일치시키고, 템플릿에서 URI를 생성하고, 템플릿에 사용되는 변수 이름 컬렉션을 검색하고, 두 템플릿이 동일한지 확인하고, 템플릿의 문자열을 반환할 수 있는 메서드를 제공합니다.  
  
 <xref:System.UriTemplate.Match%28System.Uri%2CSystem.Uri%29>는 기본 주소와 후보 URI을 사용하고 URI을 템플릿에 일치시키려고 시도합니다. 일치가 성공적으로 수행되면 <xref:System.UriTemplateMatch> 인스턴스가 반환됩니다. <xref:System.UriTemplateMatch> 개체에는 기본 URI, 후보 URI, 쿼리 매개 변수의 이름/값 컬렉션, 상대 경로 세그먼트 배열, 일치된 변수의 이름/값 컬렉션, 일치를 수행하는 데 사용된 <xref:System.UriTemplate> 인스턴스, 후보 URI의 일치하지 않는 부분을 포함하는 문자열(템플릿에 와일드카드가 있는 경우에 사용됨) 및 템플릿에 연결된 개체 등이 포함되어 있습니다.  
  
> [!NOTE]
> <xref:System.UriTemplate> 클래스는 후보 URI를 템플릿에 일치시킬 때 구성표 및 포트 번호를 무시합니다.  
  
 템플릿에서 URI를 생성할 수 있게 해주는 두 메서드(<xref:System.UriTemplate.BindByName%28System.Uri%2CSystem.Collections.Specialized.NameValueCollection%29> 및 <xref:System.UriTemplate.BindByPosition%28System.Uri%2CSystem.String%5B%5D%29>)가 있습니다. <xref:System.UriTemplate.BindByName%28System.Uri%2CSystem.Collections.Specialized.NameValueCollection%29>은 기본 주소와 매개 변수의 이름/값 컬렉션을 사용합니다. 이러한 매개 변수는 템플릿이 바인딩될 때 변수를 대체합니다. <xref:System.UriTemplate.BindByPosition%28System.Uri%2CSystem.String%5B%5D%29>은 이름/값 쌍을 사용하고 왼쪽에서 오른쪽으로 대체합니다.  
  
 <xref:System.UriTemplate.ToString>은 템플릿 문자열을 반환합니다.  
  
 <xref:System.UriTemplate.PathSegmentVariableNames%2A> 속성은 템플릿 문자열의 경로 세그먼트에 사용되는 변수 이름 컬렉션을 포함합니다.  
  
 <xref:System.UriTemplate.IsEquivalentTo%28System.UriTemplate%29>는 <xref:System.UriTemplate>을 매개 변수로 사용하고 두 템플릿이 일치하는지 여부를 지정하는 부울 값을 반환합니다. 자세한 내용은이 항목의 뒷부분에 나오는 템플릿 동등성 단원을 참조 하십시오.  
  
 <xref:System.UriTemplate>은 HTTP URI 문법을 따르는 모든 URI 구성표와 함께 사용되도록 만들어졌습니다. 다음은 지원되는 URI 구성표의 예입니다.  
  
- http://  
  
- https://  
  
- net.tcp://  
  
- net.pipe://  
  
- sb://  
  
 file:// 및 urn://와 같은 구성표는 HTTP URI 문법을 따르지 않으며 URI 템플릿과 함께 사용되면 예측할 수 없는 결과를 발생시킵니다.  
  
### <a name="template-string-syntax"></a>템플릿 문자열 구문  
 템플릿에는 경로, 선택적 쿼리 및 선택적 조각의 세 부분이 있습니다. 예제를 보려면 다음 템플릿을 참조하십시오.  
  
```  
"/weather/{state}/{city}?forecast={length)#frag1  
```  
  
 경로는 "/weather/{state}/{city}"로 구성되고, 쿼리는 "?forecast={length}"로 구성되며, 조각은 "#frag1"로 구성됩니다.  
  
 선행/후행 슬래시는 경로 식에서 선택적 요소입니다. 쿼리 식과 조각 식 모두 완전히 생략할 수 있습니다. 경로는 '/'로 구분 된 일련의 세그먼트로 구성 되며, 각 세그먼트는 리터럴 값, 변수 이름 ({중괄호}로 작성 됨) 또는 와일드 카드 ('\*'로 작성 됨)를 포함할 수 있습니다. 이전 템플릿에서 "\weather\ 세그먼트는 리터럴 값이고 "{state}" 및 "{city}"는 변수입니다. 변수는 중괄호의 내용에서 해당 이름을 사용 하 고 나중에이를 구체적인 값으로 대체 하 여 *폐쇄형 URI*를 만들 수 있습니다. 와일드 카드는 선택 사항 이지만 URI의 끝에만 표시 될 수 있으며,이는 논리적으로 "나머지 경로"와 일치 합니다.  
  
 쿼리 식 (있는 경우)은 ' & '로 구분 된 순서가 지정 되지 않은 일련의 이름/값 쌍을 지정 합니다. 쿼리 식의 요소는 리터럴 쌍(x=2) 또는 변수 쌍(x={var})이 될 수 있습니다. 쿼리의 오른쪽에만 변수 식을 포함할 수 있습니다. ({someName} = {someValue}는 허용되지 않습니다. 짝이 없는 값(?x)은 사용할 수 없습니다. 빈 쿼리 식과 단일 '? '로 구성 된 쿼리 식의 차이는 없습니다. ("모든 쿼리"를 의미 합니다.  
  
 조각 식은 리터럴 값으로 구성될 수 있으며 변수는 사용할 수 없습니다.  
  
 템플릿 문자열 내의 모든 템플릿 변수 이름은 고유해야 합니다. 템플릿 변수 이름은 대/소문자를 구분하지 않습니다.  
  
 올바른 템플릿 문자열의 예:  
  
- ""  
  
- "/shoe"  
  
- "/shoe/\*"  
  
- "{shoe}/boat"  
  
- "{shoe}/{boat}/bed/{quilt}"  
  
- "신발/{보트}"  
  
- "신발/{보트}/\*"  
  
- "shoe/boat?x=2"  
  
- "shoe/{boat}?x={bed}"  
  
- "신발/{보트}? x = {침대} & y = 대역"  
  
- "?x={shoe}"  
  
- "shoe?x=3&y={var}  
  
 잘못된 템플릿 문자열의 예:  
  
- "{신발}/{SHOE}/x = 2"-변수 이름이 중복 됩니다.  
  
- "{신발}/boat/? 침대 = {신발}"-변수 이름이 중복 됩니다.  
  
- "? x = 2 & x = 3" – 쿼리 문자열의 이름/값 쌍은 리터럴인 경우에도 고유 해야 합니다.  
  
- "? x = 2 &" – 쿼리 문자열의 형식이 잘못 되었습니다.  
  
- "? 2 & x = {신발}"-쿼리 문자열은 이름/값 쌍 이어야 합니다.  
  
- "? y = 2 & & X = 3" – 쿼리 문자열은 이름/값 쌍 이어야 하며 이름은 ' & '로 시작할 수 없습니다.  
  
### <a name="compound-path-segments"></a>복합 경로 세그먼트  
 복합 경로 세그먼트를 사용하면 단일 URI 경로 세그먼트에 여러 변수는 물론 리터럴과 함께 사용하는 변수를 포함할 수 있습니다. 다음은 올바른 복합 경로 세그먼트의 예입니다.  
  
- /filename.{ext}/  
  
- /{filename}.jpg/  
  
- /{filename}.{ext}/  
  
- /{a}.{b}someLiteral{c}({d})/  
  
 다음은 잘못된 경로 세그먼트의 예입니다.  
  
- /{} -변수의 이름을 지정 해야 합니다.  
  
- /{shoe}{boat} - 변수를 리터럴로 구분해야 합니다.  
  
### <a name="matching-and-compound-path-segments"></a>복합 및 일치하는 경로 세그먼트  
 복합 경로 세그먼트를 사용하면 단일 경로 세그먼트 내에 여러 변수가 포함된 UriTemplate을 정의할 수 있습니다. 예를 들어, 다음 템플릿 문자열에 있습니다. "Addresses/{state}. {city} "두 변수 (주 및 도시)는 동일한 세그먼트 내에서 정의 됩니다. 이 템플릿은와 `http://example.com/Washington.Redmond` 같은 url과 일치 하지만와 같은 `http://example.com/Washington.Redmond.Microsoft`url도 일치 합니다. 후자의 경우 상태 변수는 "워싱턴"을 포함 하 고 city 변수에는 "Redmond. Microsoft"가 포함 됩니다. 이 경우 모든 텍스트(‘/’ 제외)가 {city} 변수와 일치합니다. "추가" 텍스트와 일치 하지 않는 템플릿을 원하는 경우 다음과 같이 별도의 템플릿 세그먼트에 변수를 추가 합니다. "Addresses/{state}/{city}.  
  
### <a name="named-wildcard-segments"></a>명명된 와일드카드 세그먼트  
 명명 된 와일드 카드 세그먼트는 해당 변수 이름이 와일드 카드 문자 '\*'로 시작 하는 경로 변수 세그먼트입니다. 다음 템플릿 문자열에는 이름이 “shoe”인 명명된 와일드카드 세그먼트가 포함되어 있습니다.  
  
```  
"literal/{*shoe}"  
```  
  
 와일드카드 세그먼트는 다음 규칙을 따라야 합니다.  
  
- 각각의 템플릿 문자열에 대해서는 명명된 와일드카드 세그먼트가 최대 하나만 있을 수 있습니다.  
  
- 명명된 와일드카드 세그먼트는 경로의 맨 오른쪽 세그먼트에 표시되어야 합니다.  
  
- 명명된 와일드카드 세그먼트는 동일한 템플릿 문자열 내에서 익명 와일드카드 세그먼트와 함께 사용할 수 없습니다.  
  
- 명명된 와일드카드 세그먼트의 이름은 고유해야 합니다.  
  
- 명명된 와일드카드 세그먼트는 기본값을 가질 수 없습니다.  
  
- 명명 된 와일드 카드 세그먼트는 "/"로 끝날 수 없습니다.  
  
### <a name="default-variable-values"></a>기본 변수 값  
 기본 변수 값을 사용하면 템플릿 내에서 변수에 대한 기본값을 지정할 수 있습니다. 기본 변수는 변수를 UriTemplate 생성자에 전달된 컬렉션으로 선언하는 중괄호로 지정할 수 있습니다. 다음 템플릿에서는 기본값을 포함하는 변수를 사용하여 <xref:System.UriTemplate>을 지정하는 두 가지 방법을 보여 줍니다.  
  
```csharp
UriTemplate t = new UriTemplate("/test/{a=1}/{b=5}");  
```  
  
 이 템플릿은 기본값 `a`을 사용하여 이름이 `1`인 변수를 선언하고 기본값 `b`를 사용하여 이름이 `5`인 변수를 선언합니다.  
  
> [!NOTE]
> 경로 세그먼트 변수만 기본값을 가질 수 있습니다. 쿼리 문자열 변수, 복합 세그먼트 변수 및 명명된 와일드카드 변수는 기본값을 가질 수 없습니다.  
  
 다음 코드에서는 후보 URI와 일치할 때 기본 변수 값을 처리하는 방법을 보여 줍니다.  
  
```csharp
Uri baseAddress = new Uri("http://localhost:8000/");

UriTemplate t = new UriTemplate("/{state=WA}/{city=Redmond}/", true);
Uri candidate = new Uri("http://localhost:8000/OR");

UriTemplateMatch m1 = t.Match(baseAddress, candidate);

Console.WriteLine($"Template: {t}");
Console.WriteLine($"Candidate URI: {candidate}");

// Display contents of BoundVariables
Console.WriteLine("BoundVariables:");
foreach (string key in m1.BoundVariables.AllKeys)
{
    Console.WriteLine($"\t{key}={m1.BoundVariables[key]}");
}
// The output of the above code is  
// Template: /{state=WA}/{city=Redmond}/
// Candidate URI: http://localhost:8000/OR
// BoundVariables:
//         STATE=OR
//         CITY=Redmond
```  
  
> [!NOTE]
> 과 `http://localhost:8000///` 같은 uri는 앞의 코드에 나열 된 템플릿과 일치 하지 않지만와 `http://localhost:8000/` 같은 uri는 일치 하지 않습니다.  
  
 다음 코드에서는 템플릿을 사용하여 URI를 만들 때 기본 변수 값을 처리하는 방법을 보여 줍니다.  
  
```csharp
Uri baseAddress = new Uri("http://localhost:8000/");  
Dictionary<string,string> defVals = new Dictionary<string,string> {{"a","1"}, {"b", "5"}};  
UriTemplate t = new UriTemplate("/test/{a}/{b}", defVals);  
NameValueCollection vals = new NameValueCollection();  
vals.Add("a", "10");  
  
Uri boundUri = t.BindByName(baseAddress, vals);  
Console.WriteLine("BaseAddress: {0}", baseAddress);  
Console.WriteLine("Template: {0}", t.ToString());  
  
Console.WriteLine("Values: ");  
foreach (string key in vals.AllKeys)  
{  
    Console.WriteLine("\tKey = {0}, Value = {1}", key, vals[key]);  
}  
Console.WriteLine("Bound URI: {0}", boundUri);  
  
// The output of the preceding code is  
// BaseAddress: http://localhost:8000/  
// Template: /test/{a}/{b}  
// Values:  
//     Key = a, Value = 10  
// Bound URI: http://localhost:8000/test/10/5  
```  
  
변수에 기본값 `null`이 지정되면 약간의 추가 제약 조건이 있습니다. 템플릿 문자열의 맨 오른쪽 세그먼트 내에 변수가 포함되어 있는 경우 또는 세그먼트 오른쪽에 있는 모든 세그먼트가 기본값 `null`을 가지는 경우 변수가 기본값 `null`을 가질 수 있습니다. 다음은 기본값이 `null`인 올바른 템플릿 문자열입니다.  
  
- `UriTemplate t = new UriTemplate("shoe/{boat=null}");`

- `UriTemplate t = new UriTemplate("{shoe=null}/{boat=null}");`
  
- `UriTemplate t = new UriTemplate("{shoe=1}/{boat=null}");`

 다음은 기본값이 인 잘못 된 템플릿 문자열입니다 `null`.  
  
- `UriTemplate t = new UriTemplate("{shoe=null}/boat"); // null default must be in the right most path segment`
  
- `UriTemplate t = new UriTemplate("{shoe=null}/{boat=x}/{bed=null}"); // shoe cannot have a null default because boat does not have a default null value`

### <a name="default-values-and-matching"></a>기본값 및 일치  
 기본값을 가진 템플릿을 사용하여 후보 URI와 일치시킬 때 후보 URI에 값이 지정되지 않은 경우 <xref:System.UriTemplateMatch.BoundVariables%2A> 컬렉션에 기본값이 지정됩니다.  
  
### <a name="template-equivalence"></a>템플릿 동등성  
 모든 템플릿의 리터럴이 일치 하 고 동일한 세그먼트에 변수가 있는 경우 두 템플릿이 *구조적으로 동일한* 것으로 간주 됩니다. 예를 들어 다음 템플릿은 구조적으로 동등합니다.  
  
- /a/{var1}/b b/{var2}?x=1&y=2  
  
- a/{x}/b%20b/{var1}?y=2&x=1  
  
- a/{y}/B%20B/{z}/?y=2&x=1  
  
 다음 몇 가지 사항에 주의해야 합니다.  
  
- 템플릿에 선행 슬래시가 있는 경우 첫 번째 슬래시만 무시됩니다.  
  
- 템플릿 문자열의 구조적 동등성을 비교할 때 변수 이름과 경로 세그먼트의 대/소문자는 무시되고, 쿼리 문자열의 대/소문자는 구분됩니다.  
  
- 쿼리 문자열은 순서가 없습니다.  
  
## <a name="uritemplatetable"></a>UriTemplateTable  
 <xref:System.UriTemplateTable> 클래스는 개발자의 선택 개체에 바인딩된 <xref:System.UriTemplate> 개체의 연결 테이블을 나타냅니다. <xref:System.UriTemplateTable>를 호출하기 전에 <xref:System.UriTemplate>에 하나 이상의 <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29>이 있어야 합니다. <xref:System.UriTemplateTable>가 호출되기 이전에는 <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29>의 내용을 변경할 수 있습니다. <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29>가 호출되면 유효성 검사가 수행됩니다. 수행되는 유효성 검사 형식은 `allowMultiple`에 대한 <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29> 매개 변수 값에 따라 다릅니다.  
  
 <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29>를 전달하여 `false`를 호출하면 <xref:System.UriTemplateTable>에서 테이블에 템플릿이 없는지 확인합니다. 구조적으로 동등한 템플릿이 있으면 예외를 throw합니다. 하나의 템플릿만 수신 URI와 일치하게 하려면 <xref:System.UriTemplateTable.MatchSingle%28System.Uri%29>과 함께 사용합니다.  
  
 <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29>를 전달하여 `true`를 호출하면 <xref:System.UriTemplateTable>에서 <xref:System.UriTemplateTable>에 구조적으로 동등한 여러 템플릿을 포함하도록 허용합니다.  
  
 <xref:System.UriTemplate>에 추가된 <xref:System.UriTemplateTable> 개체 집합에 쿼리 문자열이 있는 경우 해당 문자열은 모호하지 않아야 합니다. 동일한 쿼리 문자열을 사용할 수 있습니다.  
  
> [!NOTE]
> <xref:System.UriTemplateTable>에서 HTTP가 아닌 구성표를 사용하는 기본 주소를 허용하는 동안 후보 URI를 템플릿에 일치시킬 때 구성표 및 포트 번호가 무시됩니다.  
  
### <a name="query-string-ambiguity"></a>쿼리 문자열 모호성  
 동일한 경로를 공유하는 템플릿은 여러 템플릿과 일치하는 URI가 있을 경우 모호한 쿼리 문자열을 포함합니다.  
  
 다음 쿼리 문자열 집합은 모호하지 않습니다.  
  
- ?x=1  
  
- ?x=2  
  
- ?x=3  
  
- ?x=1&y={var}  
  
- ?x=2&z={var}  
  
- ?x=3  
  
- ?x=1  
  
- ?  
  
- ? x={var}  
  
- ?  
  
- ?m=get&c=rss  
  
- ?m=put&c=rss  
  
- ?m=get&c=atom  
  
- ?m=put&c=atom  
  
 다음 쿼리 문자열 템플릿 집합은 모호합니다.  
  
- ?x=1  
  
- ?x={var}  
  
 "x=1" - 두 템플릿 모두와 일치합니다.  
  
- ?x=1  
  
- ?y=2  
  
 "x = 1 & y = 2"는 두 템플릿과 모두 일치 합니다. 쿼리 문자열이 일치하는 템플릿보다 더 많은 쿼리 문자열 변수를 포함할 수 있기 때문입니다.  
  
- ?x=1  
  
- ?x=1&y={var}  
  
 "x = 1 & y = 3"은 두 템플릿과 모두 일치 합니다.  
  
- ?x=3&y=4  
  
- ?x=3&z=5  
  
> [!NOTE]
> 문자 á와 Á는 URI 경로 또는 <xref:System.UriTemplate> 경로 세그먼트 리터럴에 표시될 경우 서로 다른 문자로 간주됩니다. 그러나 문자 a와 A는 동일한 문자로 간주됩니다. 문자 á와 Á는 <xref:System.UriTemplate> {variableName} 또는 쿼리 문자열에 표시될 경우 동일한 문자로 간주됩니다. a와 A도 동일한 문자로 간주됩니다.  
  
## <a name="see-also"></a>참고자료

- [WCF 웹 HTTP 프로그래밍 모델 개요](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)
- [WCF 웹 HTTP 프로그래밍 개체 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)
- [UriTemplate](../../../../docs/framework/wcf/samples/uritemplate-sample.md)
- [UriTemplate 테이블](../../../../docs/framework/wcf/samples/uritemplate-table-sample.md)
- [UriTemplate 테이블 디스패처](../../../../docs/framework/wcf/samples/uritemplate-table-dispatcher-sample.md)
