---
title: 필터 선택
ms.date: 03/30/2017
ms.assetid: 67ab5af9-b9d9-4300-b3b1-41abb5a1fd10
ms.openlocfilehash: 908e905b4196409b00abccccae03436640cbe986
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045972"
---
# <a name="choosing-a-filter"></a>필터 선택
라우팅 서비스를 구성할 때는 올바른 메시지 필터를 선택하고 수신하는 메시지와 정확히 일치하도록 메시지 필터를 구성해야 합니다. 선택한 필터가 과도하게 광범위하거나 올바르게 구성되지 않은 경우 메시지가 잘못 라우트됩니다. 필터가 너무 제한적인 경우에는 일부 메시지에 유효한 경로가 제공되지 않을 수 있습니다.

## <a name="filter-types"></a>필터 형식

라우팅 서비스에 사용되는 필터를 선택할 때는 각 필터가 작동하는 방식뿐 아니라 들어오는 메시지의 일부로 제공되는 정보도 알고 있어야 합니다. 예를 들어 모든 메시지를 동일한 엔드포인트를 통해 받는 경우 Address 및 EndpointName 필터는 유용하지 않습니다. 이는 모든 메시지가 이러한 필터와 일치하기 때문입니다.

### <a name="action"></a>작업

Action 필터는 <xref:System.ServiceModel.Channels.MessageHeaders.Action%2A> 속성을 검사합니다. 메시지에 있는 Action 헤더의 내용이 필터 구성에 지정된 필터 데이터 값과 일치하면 이 필터는 `true`를 반환합니다. 다음 예제에서는 작업 필터 `FilterElement` 를 사용 하 여 `http://namespace/contract/operation/`값을 포함 하는 동작 헤더와 메시지를 일치 시키는를 정의 합니다.

```xml
<filter name="action1" filterType="Action" filterData="http://namespace/contract/operation/" />
```

```csharp
ActionMessageFilter action1 = new ActionMessageFilter(new string[] { "http://namespace/contract/operation" });
```

이 필터는 고유한 Action 헤더가 있는 메시지를 라우트할 때 사용해야 합니다.

### <a name="endpointaddress"></a>EndpointAddress

EndpointAddress 필터는 메시지를 수신하는 EndpointAddress를 검사합니다. 메시지를 수신하는 주소가 필터 구성에 지정된 필터 주소와 정확히 일치하면 이 필터는 `true`를 반환합니다. 다음 예제에서는 주소 필터 `FilterElement` 를 사용 하 여 "http://\<hostname >/vdir/s.svc/b"로 주소가 지정 된 모든 메시지를 일치 시키는를 정의 합니다.

```xml
<filter name="address1" filterType="EndpointAddress" filterData="http://host/vdir/s.svc/b" />
```

```csharp
EndpointAddressMessageFilter address1 = new EndpointAddressMessageFilter(new EndpointAddress("http://host/vdir/s.svc/b"), false);
```

> [!NOTE]
> 주소의 호스트 이름 부분은 클라이언트에서 정규화된 도메인 이름, NetBIOS 이름, IP 주소 또는 기타 이름을 사용하는지 여부에 따라 달라질 수 있습니다. 여러 값이 동일한 호스트를 참조할 수 있으므로 이 비교의 기본 동작은 일치를 수행할 때 주소의 호스트 이름 부분을 사용하지 않습니다.
>
> 이 동작은 라우팅 서비스를 프로그래밍 방식으로 구성할 때 비교 시 호스트 이름을 확인하도록 수정할 수 있습니다.

이 필터는 들어오는 메시지의 주소가 고유한 주소로 지정된 경우에 사용해야 합니다.

### <a name="endpointaddressprefix"></a>EndpointAddressPrefix

EndpointAddressPrefix 필터는 EndpointAddress 필터와 마찬가지로 메시지를 수신하는 EndpointAddress를 검사합니다. 그러나 EndpointAddressPrefix 필터는 필터 구성에 지정된 값으로 시작하는 주소를 일치시켜 와일드카드 역할을 합니다. 다음 예제에서는 EndpointAddressPrefix 필터 `FilterElement` 를 사용 하 여 `http://<hostname>/vdir*`주소가 지정 된 모든 메시지를 일치 시키는를 정의 합니다.

```xml
<filter name="prefix1" filterType="EndpointAddressPrefix" filterData="http://host/vdir" />
```

```csharp
PrefixEndpointAddressMessageFilter prefix1 = new PrefixEndpointAddressMessageFilter(new EndpointAddress("http://host/vdir/s.svc/b"), false);
```

> [!NOTE]
> 주소의 호스트 이름 부분은 클라이언트에서 정규화된 도메인 이름, NetBIOS 이름, IP 주소 또는 기타 이름을 사용하는지 여부에 따라 달라질 수 있습니다. 여러 값이 동일한 호스트를 참조할 수 있으므로 이 비교의 기본 동작은 일치를 수행할 때 주소의 호스트 이름 부분을 사용하지 않습니다.

이 필터는 공통 주소 접두사를 공유하는 들어오는 메시지를 라우트할 때 사용해야 합니다.

### <a name="and"></a>AND

AND 필터는 메시지 내의 값을 직접 필터링하지 않지만 두 개의 다른 필터를 결합하여 AND 필터가 `AND`를 반환하기 전에 두 필터가 모두 메시지와 일치해야 하는 `true` 조건을 만드는 데 사용될 수 있습니다. 이렇게 하면 모든 하위 필터가 일치할 때만 일치하는 복잡한 필터를 만들 수 있습니다. 다음 예제에서는 Address 필터와 Action 필터를 정의한 다음 이 두 필터를 기준으로 메시지를 평가하는 AND 필터를 정의합니다. Address 필터와 Action 필터가 둘 다 일치하면 AND 필터가 `true`를 반환합니다.

```xml
<filter name="address1" filterType="AddressPrefix" filterData="http://host/vdir"/>
<filter name="action1" filterType="Action" filterData="http://namespace/contract/operation/"/>
<filter name="and1" filterType="And" filter1="address1" filter2="action1" />
```

```csharp
EndpointAddressMessageFilter address1 = new EndpointAddressMessageFilter(new EndpointAddress("http://host/vdir/s.svc/b"), false);
ActionMessageFilter action1 = new ActionMessageFilter(new string[] { "http://namespace/contract/operation" });
StrictAndMessageFilter and1=new StrictAndMessageFilter(address1, action1);
```

이 필터는 여러 필터의 논리를 결합하여 일치를 수행해야 하는 시기를 결정해야 하는 경우에 사용해야 합니다. 예를 들어 특정 주소로 동작과 메시지의 특정 조합만 수신해야 하는 대상이 여러 개 있는 경우 AND 필터를 사용하여 필요한 Action 필터와 Address 필터를 결합할 수 있습니다.

### <a name="custom"></a>사용자 지정

사용자 지정 필터 형식을 선택할 때이 필터에 사용할 **Messagefilter** 구현을 포함 하는 어셈블리의 형식을 포함 하는 customtype 값을 제공 해야 합니다. 또한 filterData에는 사용자 지정 필터가 메시지를 평가할 때 필요할 수 있는 값이 들어 있어야 합니다. 다음 예제에서는 `FilterElement` MessageFilter 구현을 사용하는 `CustomAssembly.MyCustomMsgFilter`를 정의합니다.

```xml
<filter name="custom1" filterType="Custom" customType="CustomAssembly.MyCustomMsgFilter, CustomAssembly" filterData="Custom Data" />
```

```csharp
MyCustomMsgFilter custom1=new MyCustomMsgFilter("Custom Data");
```

에서 제공 [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)]하는 필터가 적용 되지 않는 메시지에 대해 사용자 지정 일치 논리를 수행 해야 하는 경우 **messagefilter** 클래스의 구현인 사용자 지정 필터를 만들어야 합니다. 예를 들어 들어오는 메시지의 필드를 필터에 구성으로 제공된 알려진 값의 목록과 비교하거나 특정 메시지 요소를 해시한 다음 해당 값을 검사하여 필터가 `true`를 반환해야 하는지 아니면 `false`를 반환해야 하는지 여부를 확인하는 사용자 지정 필터를 만들 수 있습니다.

### <a name="endpointname"></a>EndpointName

EndpointName 필터는 메시지를 수신한 엔드포인트의 이름을 검사합니다. 다음 예제에서는 EndpointName 필터 `FilterElement` 를 사용 하 여 "SvcEndpoint"에서 받은 메시지를 라우팅하는을 정의 합니다.

```xml
<filter name="name1" filterType="Endpoint" filterData="SvcEndpoint" />
```

```csharp
EndpointNameMessageFilter name1 = new EndpointNameMessageFilter("SvcEndpoint");
```

이 필터는 라우팅 서비스가 둘 이상의 명명된 서비스 엔드포인트를 노출하는 경우에 유용합니다. 예를 들어 라우팅 서비스가 메시지를 받을 때 사용하는 두 개의 엔드포인트를 노출할 수 있습니다. 이러한 두 엔드포인트는 하나는 메시지를 실시간으로 처리해야 하는 우수 고객용이고 다른 하나는 시간이 중요하지 않은 메시지를 받기 위한 것입니다.

일반적으로 전체 주소 일치를 사용하여 메시지가 수신된 엔드포인트를 확인할 수 있지만 엔드포인트 이름을 대신 사용하면, 특히 엔드포인트 이름이 필수 특성인 구성 파일을 사용하여 라우팅 서비스를 구성하는 경우 이 작업을 더 쉽고 빠르게 수행할 수 있고 오류가 발생할 가능성도 줄어듭니다.

### <a name="matchall"></a>MatchAll

MatchAll 필터는 수신되는 모든 메시지를 일치시킵니다. 이 필터는 수신되는 모든 메시지의 복사본을 저장하는 로깅 서비스와 같이 수신되는 모든 메시지를 항상 특정 엔드포인트에 라우트해야 하는 경우에 유용합니다. 다음 예제에서는 MatchAll 필터를 사용하는 `FilterElement`를 정의합니다.

```xml
<filter name="matchAll1" filterType="MatchAll" />
```

```csharp
MatchAllMessageFilter matchAll1 = new MatchAllMessageFilter();
```

### <a name="xpath"></a>XPath

XPath 필터를 사용하면 메시지 내의 특정 요소를 검사하는 데 사용되는 XPath 쿼리를 지정할 수 있습니다. XPath 필터링은 메시지 내의 XML 주소 지정 가능 항목을 직접 검사하는 데 사용할 수 있는 강력한 필터링 옵션이지만 수신하는 메시지의 구조를 잘 알고 있어야 사용할 수 있습니다. 다음 예제에서는 XPath 필터 `FilterElement` 를 사용 하 여 "ns" 네임 스페이스 접두사에서 참조 하는 네임 스페이스 내에서 "element" 라는 요소의 메시지를 검사 하는를 정의 합니다.

```xml
<filter name="xpath1" filterType="XPath" filterData="//ns:element" />
```

```csharp
XPathMessageFilter xpath1=new XPathMessageFilter("//ns:element");
```

이 필터는 수신하는 메시지에 특정 값이 포함되어 있다는 것을 알고 있는 경우에 유용합니다. 예를 들어 동일한 서비스의 두 버전을 호스팅하는 경우 더 새 버전의 서비스로 주소가 지정된 메시지에 고유한 사용자 지정 헤더 값이 포함되어 있다는 것을 알고 있으면 XPath를 사용하여 이 헤더를 찾아서 이 헤더에 있는 값을 파일 구성에 제공된 다른 값과 비교하여 필터가 일치하는지 확인할 수 있습니다.

XPath 쿼리에는 종종 길거나 복잡한 문자열 값인 고유한 네임스페이스가 포함되어 있기 때문에 XPath 필터를 사용하면 네임스페이스 테이블을 통해 네임스페이스에 대한 고유한 접두사를 정의할 수 있습니다. 네임 스페이스 테이블에 대 한 자세한 내용은 [메시지 필터](../../../../docs/framework/wcf/feature-details/message-filters.md)를 참조 하세요.

XPath 쿼리를 디자인 하는 방법에 대 한 자세한 내용은 [Xpath 구문](https://go.microsoft.com/fwlink/?LinkId=164592)을 참조 하세요.

## <a name="see-also"></a>참고자료

- [메시지 필터](../../../../docs/framework/wcf/feature-details/message-filters.md)
- [방법: 필터 사용](../../../../docs/framework/wcf/feature-details/how-to-use-filters.md)
