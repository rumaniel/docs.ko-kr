---
ms.openlocfilehash: ac929a8b3e9a7d56122f5699c51819ad483d1f5e
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804578"
---
### <a name="binaryformatter-can-fail-to-find-type-from-loadfrom-context"></a>BinaryFormatter가 LoadFrom 컨텍스트에서 형식을 찾지 못함

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5부터 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name>의 여러 가지 변경으로 인해 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=name>을 사용하여 LoadFrom 컨텍스트에서 로드된 형식을 역직렬화할 때 역직렬화의 차이가 발생할 수 있습니다. 이러한 변경 내용은 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=name>이 나중에 해당 형식으로 역직렬화를 시도할 때 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=name>이 다른 동작을 유발하는 형식을 로드하는 새로운 방법 때문입니다. 기본 직렬화 바인더는 XmlSerializer의 이전 동작에 따라 일부 상황에서 작동했을지라도 LoadFrom 컨텍스트를 자동으로 검색하지 않습니다. 변경 내용으로 인해 다른 컨텍스트에서 로드된 어셈블리에서 형식을 로드할 때 <xref:System.IO.FileNotFoundException?displayProperty=name>이 throw될 수 있습니다.|
|제안 해결 방법|이 예외가 표시되면 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=name>의 <code>Binder</code> 속성을 올바른 형식을 찾을 수 있는 사용자 지정 바인더로 설정할 수 있습니다.<pre><code class="lang-csharp">var formatter = new BinaryFormatter { Binder = new TypeFinderBinder() }&#13;&#10;</code></pre>그런 다음, 사용자 지정 바인더:<pre><code class="lang-csharp">public class TypeFinderBinder : SerializationBinder&#13;&#10;{&#13;&#10;private static readonly string s_assemblyName = Assembly.GetExecutingAssembly().FullName;&#13;&#10;&#13;&#10;public override Type BindToType(string assemblyName, string typeName)&#13;&#10;{&#13;&#10;return Type.GetType(String.Format(CultureInfo.InvariantCulture, &quot;{0}, {1}&quot;, typeName, s_assemblyName));&#13;&#10;}&#13;&#10;}&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(System.IO.Stream)?displayProperty=nameWithType></li><li><xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize(System.IO.Stream,System.Runtime.Remoting.Messaging.HeaderHandler)?displayProperty=nameWithType></li></ul>|
