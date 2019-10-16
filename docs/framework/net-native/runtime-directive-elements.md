---
title: 런타임 지시문 요소
ms.date: 03/30/2017
ms.assetid: 3fe5848c-ecd7-4136-970b-8e48d250bde6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 062f13ad92f37bb7ae29ed34dcf88f99f98e7612
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049268"
---
# <a name="runtime-directive-elements"></a>런타임 지시문 요소
런타임 지시문(rd.xml) 파일 형식은 다음 지시문 런타임 요소를 지원합니다. 계층적 표현에 대해서는 [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)를 참조하세요.  
  
 [\<Application>](application-element-net-native.md)  
 앱에서 사용하는 모든 형식에 런타임 리플렉션 정책을 적용합니다. 런타임에 해당 메타데이터를 리플렉션에 사용할 수 있는 애플리케이션 수준 형식 및 형식 멤버에 대한 컨테이너로 사용됩니다. 이 요소는 [\<Directives>](directives-element-net-native.md) 요소의 자식입니다.  
  
 [\<Assembly>](assembly-element-net-native.md)  
 런타임 정책을 어셈블리의 모든 형식에 적용합니다. 이 요소는 [\<Application>](application-element-net-native.md) 및 [\<Library>](library-element-net-native.md) 요소의 자식입니다.  
  
 [\<AttributeImplies>](attributeimplies-element-net-native.md)  
 포함 [\<Type>](type-element-net-native.md) 지시문이 특성이면 해당 특성이 적용되는 코드 요소에 런타임 정책을 적용합니다.  
  
 [\<Directives>](directives-element-net-native.md)  
 .NET 네이티브에 대 한 모든 런타임 지시문 파일의 루트 요소입니다. 해당 자식 요소는 [\<Application>](application-element-net-native.md) 및 [\<Library>](library-element-net-native.md)입니다.  
  
 [\<Event>](event-element-net-native.md)  
 런타임 정책을 이벤트에 적용합니다. 이 요소는 [\<Type>](type-element-net-native.md) 및 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 요소의 자식입니다.  
  
 [\<Field>](field-element-net-native.md)  
 런타임 정책을 필드에 적용합니다. 이 요소는 [\<Type>](type-element-net-native.md) 및 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 요소의 자식입니다.  
  
 [\<GenericParameter>](genericparameter-element-net-native.md)  
 제네릭 형식 또는 메서드의 매개 변수 형식에 런타임 정책을 적용합니다.  
  
 [\<ImpliesType>](impliestype-element-net-native.md)  
 포함 형식 또는 메서드에 런타임 정책이 적용된 경우 해당 정책을 형식에 적용합니다.  
  
 [\<Library>](library-element-net-native.md)  
 런타임 정책을 어셈블리의 모든 형식에 적용합니다. 이 요소는 [\<Application>](application-element-net-native.md) 및 [\<Library>](library-element-net-native.md) 요소의 자식입니다.  
  
 [\<Method>](method-element-net-native.md)  
 런타임 정책을 메서드에 적용합니다. 이 요소는 [\<Type>](type-element-net-native.md) 및 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 요소의 자식입니다.  
  
 [\<MethodInstantiation>](methodinstantiation-element-net-native.md)  
 생성된 제네릭 메서드에 런타임 정책을 적용합니다. 이 요소는 [\<Type>](type-element-net-native.md) 및 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 요소의 자식입니다.  
  
 [\<Namespace>](namespace-element-net-native.md)  
 네임스페이스의 모든 형식에 런타임 정책을 적용합니다.  
  
 [\<Parameter>](parameter-element-net-native.md)  
 메서드에 전달된 인수의 형식에 런타임 정책을 적용합니다.  
  
 [\<Property>](property-element-net-native.md)  
 런타임 정책을 속성에 적용합니다. 이 요소는 [\<Type>](type-element-net-native.md) 및 [\<TypeInstantiation>](typeinstantiation-element-net-native.md) 요소의 자식입니다.  
  
 [\<Subtypes>](subtypes-element-net-native.md)  
 포함 형식에서 상속된 모든 클래스에 런타임 정책을 적용합니다.  
  
 [\<Type>](type-element-net-native.md)  
 런타임 정책을 형식에 적용합니다.  
  
 [\<TypeInstantiation>](typeinstantiation-element-net-native.md)  
 생성된 제네릭 형식에 런타임 정책을 적용합니다.  
  
 [\<TypeParameter>](typeparameter-element-net-native.md)  
 메서드로 전달된 <xref:System.Type> 인수가 나타내는 형식에 런타임 정책을 적용합니다.  
  
## <a name="see-also"></a>참고자료

- [rd.xml 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)
