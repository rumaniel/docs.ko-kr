---
ms.openlocfilehash: 2f5511b7694f91893b731805119b85d1a5669a33
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859102"
---
### <a name="serialization-of-control-characters-with-datacontractjsonserializer-is-now-compatible-with-ecmascript-v6-and-v8"></a>DataContractJsonSerializer를 사용한 제어 문자의 serialization가 이제 ECMAScript V6 및 V8과 호환됨

|   |   |
|---|---|
|세부 정보|.NET framework 4.6.2 이하 버전에서는 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=name>이 ECMAScript V6 및 V8 표준과 호환되는 방식으로 \b, \f, \t 등의 일부 특수 제어 문자를 직렬화하지 않았습니다. .NET Framework 4.7부터는 이러한 제어 문자의 serialization가 ECMAScript V6 및 V8과 호환됩니다.|
|제안|.NET Framework 4.7을 대상으로 하는 앱의 경우 기본적으로 이 기능을 사용할 수 있습니다. 이 동작을 원치 않는 경우 app.config 또는 web.config 파일의 <code>&lt;runtime&gt;</code> 섹션에 다음 줄을 추가하여 이 기능을 옵트아웃(opt out)할 수 있습니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Runtime.Serialization.DoNotUseECMAScriptV6EscapeControlCharacter=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.7|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject(System.IO.Stream,System.Object)?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject(System.Xml.XmlDictionaryWriter,System.Object)?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.WriteObject(System.Xml.XmlWriter,System.Object)?displayProperty=nameWithType></li></ul>|

