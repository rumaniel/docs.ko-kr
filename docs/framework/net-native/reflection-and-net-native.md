---
title: 리플렉션 및 .NET 네이티브
ms.date: 03/30/2017
ms.assetid: 91c9eae4-c641-476c-a06e-d7ce39709763
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 17b567fe0f476e689a9775c5c73ebf068424e840
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049280"
---
# <a name="reflection-and-net-native"></a>리플렉션 및 .NET 네이티브
.NET Framework의 관리 개발에서는 리플렉션 API를 통한 메타 프로그래밍이 지원됩니다. 리플렉션을 통해 앱의 개체를 검사하고, 검사를 통해 검색된 개체에 대해 메서드를 호출하고, 런타임에 새 형식을 생성하고, 기타 여러 동적 코드 시나리오를 지원할 수 있습니다. 또한 serialization과 deserialization도 지원되므로 개체의 필드 값을 유지했다가 나중에 복원할 수 있습니다. 이러한 모든 시나리오에서는 .NET Framework JIT(Just-In-Time) 컴파일러가 사용 가능한 메타데이터를 기반으로 네이티브 코드를 생성해야 합니다.  
  
 .NET 네이티브 런타임은 JIT 컴파일러를 포함 하지 않습니다. 따라서 필요한 모든 네이티브 코드를 미리 생성해야 합니다. 추론 집합을 사용하여 생성해야 하는 코드를 결정할 수 있지만 이러한 추론이 가능한 모든 프로그래밍 시나리오에 적용되는 것은 아닙니다.  그러므로 [런타임 지시문](runtime-directives-rd-xml-configuration-file-reference.md)을 사용하여 이러한 메타 프로그래밍 시나리오에 대한 힌트를 제공해야 합니다. 필요한 메타데이터 또는 구현 코드를 런타임에 사용할 수 없는 경우 앱에서는 [MissingMetadataException](missingmetadataexception-class-net-native.md), [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 또는 [MissingInteropDataException](missinginteropdataexception-class-net-native.md) 예외를 throw합니다. 이 예외를 제거하는 런타임 지시문 파일에 대한 적절한 항목을 생성하는 두 가지 문제 해결사를 이용할 수 있습니다.  
  
- 형식의 경우 [MissingMetadataException 문제 해결사](https://dotnet.github.io/native/troubleshooter/type.html) 입니다.  
  
- 메서드의 경우 [MissingMetadataException 문제 해결사](https://dotnet.github.io/native/troubleshooter/method.html) 입니다.  
  
> [!NOTE]
> 런타임 지시문 파일이 필요한 이유에 대한 배경 정보를 제공하는 .NET 네이티브 컴파일 프로세스의 개요는 [.NET 네이티브 및 컴파일](net-native-and-compilation.md)을 참조하세요.  
  
 또한 .NET 네이티브를 사용 하면 .NET Framework 클래스 라이브러리의 전용 멤버를 반영할 수 없습니다. 예를 들어 .NET Framework 클래스 라이브러리 형식의 필드를 검색하기 위해 <xref:System.Reflection.TypeInfo.DeclaredFields%2A?displayProperty=nameWithType> 속성을 호출하면 공용 필드 또는 보호된 필드만 반환됩니다.  
  
 다음 항목에서는 앱에서 리플렉션과 serialization을 지원하는 데 필요한 개념 및 참조 설명서를 제공합니다.  
  
- [리플렉션을 사용하는 API](apis-that-rely-on-reflection.md)  
  
- [리플렉션 API 참조](net-native-reflection-api-reference.md)  
  
- [런타임 지시문(rd.xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)  
  
## <a name="see-also"></a>참고자료

- [.NET Native로 앱 컴파일](index.md)
- [.NET 네이티브 및 컴파일](net-native-and-compilation.md)
