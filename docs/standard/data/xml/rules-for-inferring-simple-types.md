---
title: 단순 형식 유추 규칙
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 394624d6-4da0-430a-8a88-46efe40f14de
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 15e7692abfe06ec9e9f91a3b229bf99971eaecc1
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54550502"
---
# <a name="rules-for-inferring-simple-types"></a>단순 형식 유추 규칙
<xref:System.Xml.Schema.XmlSchemaInference> 클래스가 특성 및 요소에 대한 데이터 형식을 유추하는 방법을 설명합니다.  
  
 <xref:System.Xml.Schema.XmlSchemaInference> 클래스는 특성 및 요소에 대한 데이터 형식을 단순 형식으로 유추합니다. 이 단원에서는 유추 가능한 형식, 여러 다른 값이 단일 형식으로 조정되는 방식 및 스키마 정의 `xsi` 특성을 처리하는 방법을 설명합니다.  
  
## <a name="inferred-types"></a>유추된 형식  
 <xref:System.Xml.Schema.XmlSchemaInference> 클래스는 요소 및 특성 값을 단순 형식으로 유추하고 결과 스키마에 형식 특성을 포함시킵니다. 유추된 모든 형식은 단순 형식입니다. 기본 형식 또는 패싯은 결과로 생성된 스키마에 포함되지 않습니다.  
  
 값은 XML 문서에서 발견될 때마다 개별적으로 검사합니다. 값을 검사할 때 값의 형식을 유추합니다. 특성 또는 요소에 대해 형식이 유추되고 현재 유추된 형식과 일치하지 않는 특성 또는 요소 값이 발견되면 <xref:System.Xml.Schema.XmlSchemaInference> 클래스는 각 규칙 집합에 대해 형식을 승격합니다. 이 규칙은 이 항목 뒷부분의 형식 승격 단원에서 자세히 다룹니다.  
  
 다음 표에서는 결과 스키마에 대해 유추 가능한 형식의 목록을 보여 줍니다.  
  
|단순 형식|설명|  
|-----------------|-----------------|  
|boolean|True, False, 0, 1.|  
|byte|-128에서 127까지의 범위에 있는 정수입니다.|  
|unsignedByte|0에서 255까지의 범위에 있는 정수입니다.|  
|short|-32768에서 32767까지의 범위에 있는 정수입니다.|  
|unsignedShort|0에서 65535까지의 범위에 있는 정수입니다.|  
|int|-2147483648에서 2147483647까지의 범위에 있는 정수입니다.|  
|unsignedInt|0에서 4294967295까지의 범위에 있는 정수입니다.|  
|long|-9223372036854775808에서 9223372036854775807까지의 범위에 있는 정수입니다.|  
|unsignedLong|0에서 18446744073709551615까지의 범위에 있는 정수입니다.|  
|정수|"-" 접두사를 붙일 수 있는 유한한 숫자입니다.|  
|decimal|전체 자릿수가 0에서 28까지인 숫자 값입니다.|  
|float|십진수 뒤에 옵션으로 "E"가 오거나 "e" 다음에 정수 값을 써서 지수를 표현합니다. -16777216에서 16777216까지의 범위에 있는 10진수 값입니다. 지수 값의 범위는 -149에서 104까지입니다.<br /><br /> float를 사용하면 특수한 값으로 무한대 또는 숫자가 아닌 값을 표현할 수 있습니다. float에 대한 특수 값은 0, -0, INF, -INF, NaN 등입니다.|  
|double|10진수 값의 범위가 -9007199254740992에서 9007199254740992까지이고 지수 값의 범위가 -1075에서 970까지인 것만 제외하고 float와 동일합니다.<br /><br /> double을 사용하면 특수한 값으로 무한대 또는 숫자가 아닌 값을 표현할 수 있습니다. float에 대한 특수 값은 0, -0, INF, -INF, NaN 등입니다.|  
|duration|W3C duration 형식입니다.|  
|dateTime|W3C dateTime 형식입니다.|  
|시간|W3C time 형식입니다.|  
|date|연도 값의 범위는 0001에서 9999까지입니다.|  
|gYearMonth|W3C 양력 연도와 월 형식입니다.|  
|string|한 자 이상의 유니코드 문자입니다.|  
  
## <a name="type-promotion"></a>형식 승격  
 <xref:System.Xml.Schema.XmlSchemaInference> 클래스는 특성 및 요소 값을 한 번에 하나씩 검사합니다. 값이 나타나면 가장 제한되고 부호 없는 형식이 유추됩니다. 특성 또는 요소에 대해 형식이 유추되었고 현재 유추된 값과 일치하지 않는 새로운 값을 발견하는 경우, 유추된 형식은 현재 유추된 형식 및 새 값에 모두 적용되는 새로운 형식으로 승격됩니다. <xref:System.Xml.Schema.XmlSchemaInference> 클래스는 유추된 형식을 승격할 때 이전 값을 고려합니다.  
  
 예를 들어, 다음 두 XML 문서의 XML 조각을 고려하세요.  
  
 `<MyElement1 attr1="12" />`  
  
 `<MyElement1 attr1="52344" />`  
  
 첫 번째 `attr1` 값이 나타나면 `attr1` 값을 기준으로 `unsignedByte`의 형식이 `12`로 유추됩니다. 두 번째 `attr1`이 나타나면 그 형식은 현재 유추된 형식 `unsignedShort` 및 현재 값 `unsignedByte`를 기준으로 `52344`로 승격됩니다.  
  
 이번에는 다음 두 XML 문서의 XML을 고려하세요.  
  
 `<MyElement2 attr2="0" />`  
  
 `<MyElement2 attr2="true" />`  
  
 첫 번째 `attr2` 값이 나타나면 `attr2` 값을 기준으로 `unsignedByte`의 형식이 `0`로 유추됩니다. 두 번째 `attr2`가 나타나면 `string` 클래스는 유추된 형식을 승격시킬 때 이전 값을 고려하기 때문에 그 형식은 현재 유추된 형식 `unsignedByte` 및 현재 값 `true`를 기준으로 <xref:System.Xml.Schema.XmlSchemaInference>으로 승격됩니다. 하지만 위에서 설명한 대로 `attr2`의 두 인스턴스가 다른 두 XML 문서가 아닌 같은 XML 문서에 나타나면 `attr2`는 `boolean`으로 유추됩니다.  
  
### <a name="ignored-attributes-from-the-httpswwww3org2001xmlschema-instance-namespace"></a><https://www.w3.org/2001/XMLSchema-instance> 네임스페이스에서 무시된 특성

다음은 스키마 유추에서 무시된 스키마 정의 특성입니다.  
  
|특성|설명|  
|---------------|-----------------|  
|`xsi:type`|요소가 지정된 `xsi:type`과 만나면 `xsi:type`은 무시됩니다.|  
|`xsi:nil`|`xsi:nil` 특성이 있는 요소가 나타나면 유추된 스키마의 요소 선언은 `nillable="true"` 값을 가집니다. `xsi:nil`로 설정된 `true` 특성이 있는 요소는 자식 요소를 가질 수 없습니다.|  
|`xsi:schemaLocation`|`xsi:schemaLocation`이 나타나면 무시됩니다.|  
|`xsi:noNamespaceSchemaLocation`|`xsi:noNamespaceSchemaLocation`이 나타나면 무시됩니다.|  
  
## <a name="see-also"></a>참고 항목

- [XML SOM(스키마 개체 모델)](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)
- [XML 문서에서 스키마 유추](../../../../docs/standard/data/xml/inferring-schemas-from-xml-documents.md)
- [스키마 노드 형식 및 구조 유추 규칙](../../../../docs/standard/data/xml/rules-for-inferring-schema-node-types-and-structure.md)
