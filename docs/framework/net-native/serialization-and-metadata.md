---
title: Serialization 및 메타데이터
ms.date: 03/30/2017
ms.assetid: 619ecf1c-1ca5-4d66-8934-62fe7aad78c6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ec8180da9637ec2b2c4e1b432773b4f9f1ac908b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049178"
---
# <a name="serialization-and-metadata"></a>Serialization 및 메타데이터

앱이 개체를 serialize 및 deserialize하는 경우에는 런타임에 필요한 메타데이터가 제공되도록 런타임 지시문(.rd.xml) 파일에 항목을 추가해야 할 수 있습니다. serializer에는 두 가지 범주가 있으며 각 범주는 런타임 지시문 파일에서 서로 다른 방식으로 처리해야 합니다.  
  
- 리플렉션 기반 타사 serializer. 이러한 serializer의 경우 런타임 지시문 파일을 수정해야 합니다. 여기에 대해서는 다음 섹션에서 설명합니다.  
  
- .NET Framework 클래스 라이브러리에 포함된 리플렉션을 기반으로 하지 않는 serializer. 이러한 직렬 변환기의 경우 런타임 지시문 파일을 수정해야 할 수도 있습니다. 아래의 [Microsoft 직렬 변환기](#Microsoft) 섹션에서 여기에 대해 설명합니다.  
  
<a name="ThirdParty"></a>
## <a name="third-party-serializers"></a>타사 serializer

 Newtonsoft.JSON을 비롯한 타사 serializer는 대개 리플렉션을 기반으로 합니다. serialize된 데이터의 BLOB(Binary Large Object)가 지정되면 데이터의 필드는 대상 형식의 필드를 이름으로 조회하여 구체적 형식에 할당됩니다. 이러한 라이브러리를 사용하는 경우 `List<Type>` 컬렉션에서 직렬화 또는 deserialize하려는 각 <xref:System.Type> 개체에 대해 최소한 [MissingMetadataException](missingmetadataexception-class-net-native.md) 예외가 발생합니다.  
  
 이러한 serializer용 메타데이터 누락으로 인해 발생하는 문제를 해결하는 가장 쉬운 방법은 serialization에 사용할 형식을 `App.Models`와 같은 네임스페이스 하나에 수집하고 해당 네임스페이스에 `Serialize` 메타데이터 지시문을 적용하는 것입니다.  
  
```xml  
<Namespace Name="App.Models" Serialize="Required PublicAndInternal" />  
```  
  
 이 예제에 사용된 구문에 대한 자세한 내용은 [\<Namespace> 요소](namespace-element-net-native.md)를 참조하세요.  
  
<a name="Microsoft"></a>
## <a name="microsoft-serializers"></a>Microsoft serializer

 <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 및 <xref:System.Xml.Serialization.XmlSerializer> 클래스는 리플렉션을 사용하지는 않지만 serialize 또는 deserialize하려는 코드를 기반으로 코드는 생성해야 합니다. 각 serializer의 오버로드된 생성자는 serialize 또는 deserialize할 형식을 지정하는 <xref:System.Type> 매개 변수를 포함합니다. 코드에서 해당 형식을 지정하는 방법에 따라 수행해야 하는 작업이 정의됩니다. 여기에 대해서는 다음 두 섹션에서 설명합니다.  
  
### <a name="typeof-used-in-the-constructor"></a>생성자 내부에서 사용되는 typeof

 이러한 serialization 클래스의 생성자를 호출 하 고 메서드 호출에 C# [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator) 연산자를 포함 하는 경우에는 **추가 작업을 수행할 필요가 없습니다**. 예를 들어 serialization 클래스 생성자에 대한 다음의 각 호출에서 `typeof` 키워드는 생성자에 전달되는 식의 일부로 사용됩니다.  
  
 [!code-csharp[ProjectN#5](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#5)]  
  
 .NET 네이티브 컴파일러는이 코드를 자동으로 처리 합니다.  
  
### <a name="typeof-used-outside-the-constructor"></a>생성자 외부에서 사용되는 typeof

 다음 코드와 같이 이러한 serialization 클래스의 생성자를 호출 하 C# 고 생성자의 <xref:System.Type> 매개 변수에 제공 된 식 외부에서 [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator) 연산자를 사용 하는 경우 .NET 네이티브 컴파일러에서 형식을 확인할 수 없습니다.  
  
 [!code-csharp[ProjectN#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#6)]  
  
 이 경우 다음과 같은 항목을 추가하여 런타임 지시문 파일에서 형식을 지정해야 합니다.  
  
```xml  
<Type Name="DataSet" Browse="Required Public" />  
```  
  
 마찬가지로 다음 코드와 같이와 같은 <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29?displayProperty=nameWithType> 생성자를 호출 하 고 serialize 할 추가 <xref:System.Type> 개체의 배열을 제공 하는 경우 .NET 네이티브 컴파일러는 이러한 형식을 확인할 수 없습니다.  
  
 [!code-csharp[ProjectN#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#7)]  
  
 따라서 각 형식에 대한 다음과 같은 항목을 런타임 지시문 파일에 추가해야 합니다.  
  
```xml  
<Type Name="t" Browse="Required Public" />  
```  
  
 이 예제에 사용된 구문에 대한 자세한 내용은 [\<Type> 요소](type-element-net-native.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
- [런타임 지시문 요소](runtime-directive-elements.md)
- [\<형식 > 요소](type-element-net-native.md)
- [\<Namespace> 요소](namespace-element-net-native.md)
