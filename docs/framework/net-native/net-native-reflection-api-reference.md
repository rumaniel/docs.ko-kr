---
title: .NET 네이티브 리플렉션 API 참조
ms.date: 03/30/2017
ms.assetid: 0429c049-22a3-4ba1-9cc8-f6ee91e31d9c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9c1fbef46231fed3af0d335e9396b301fe503254
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049387"
---
# <a name="net-native-reflection-api-reference"></a>.NET 네이티브 리플렉션 API 참조
.NET 네이티브에는 다음과 같은 세 가지 새 예외 형식이 포함 되어 있습니다. [System.runtime.compilerservices, MissingInteropDataException](missinginteropdataexception-class-net-native.md), [MissingMetadataException](missingmetadataexception-class-net-native.md)및 [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md)를 실행 해야 합니다. 세 가지 예외 형식 모두에 대해 다음 사항을 확인하세요.  
  
 이러한 형식은 내부용으로만 사용됩니다.  
 이러한 세 가지 예외 형식은 .NET 네이티브 도구 체인만 사용 하기 위한 것입니다. 예외는 .NET 네이티브 도구 체인에서 프로그램 실행을 계속할 수 없는 누락 된 데이터를 검색 하는 경우에 throw 됩니다.  
  
 이러한 예외를 코드에서 처리하지 마세요.  
 이러한 예외는 애플리케이션에 필요한 메타데이터가 없거나( [MissingInteropDataException](missinginteropdataexception-class-net-native.md) 및 [MissingMetadataException](missingmetadataexception-class-net-native.md) 예외), 애플리케이션에 필요한 구현 코드가 누락되었음( [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 예외)을 나타냅니다. 런타임 지시문(.rd.xml) 파일을 수정하여 필요한 메타데이터 또는 구현 코드를 런타임에 사용 가능하게 하는 방식으로 이러한 예외 조건을 수정합니다. 자세한 내용은 [Runtime Directives (rd.xml) Configuration File Reference](runtime-directives-rd-xml-configuration-file-reference.md)을 참조하십시오. [MissingMetadataException](missingmetadataexception-class-net-native.md) 및 [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 예외를 제거하는 런타임 지시문 파일에 대한 적절한 항목을 제공하는 두 개의 문제 해결사를 사용할 수 있습니다.  
  
- 형식의 경우 [MissingMetadataException 문제 해결사](https://dotnet.github.io/native/troubleshooter/type.html) 입니다.  
  
- 메서드의 경우 [MissingMetadataException 문제 해결사](https://dotnet.github.io/native/troubleshooter/method.html) 입니다.  
  
> [!NOTE]
> 이 참조는 .NET 네이티브에 고유한 세 가지 예외 형식을 설명 합니다. .NET Framework core 리플렉션 API에 대 한 참조 설명서는 <xref:System.Reflection> <xref:System.Reflection.Context> 및 <xref:System.Reflection.Emit> 네임 스페이스를 참조 하세요. .NET Framework 핵심 interop API에 대한 참조 설명서는 <xref:System.Runtime.InteropServices>를 참조하세요.  
  
## <a name="systemreflection-namespace"></a>System.Reflection 네임스페이스  
 <xref:System.Reflection> 네임스페이스에는 .NET Framework의 리플렉션에 사용되는 핵심 형식이 포함되어 있습니다. .NET 네이티브의 경우 두 가지 새 예외 형식도 포함 합니다.  
  
|클래스|설명|  
|-----------|-----------------|  
|[MissingMetadataException](missingmetadataexception-class-net-native.md)|리플렉션을 사용하여 존재하지 않는 메타데이터를 검색하면 throw되는 예외입니다.|  
|[MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md)|형식 또는 형식 멤버의 메타데이터를 사용할 수는 있지만 해당 구현이 제거된 경우 throw되는 예외입니다.|  
  
 이 네임스페이스의 다른 형식에 대한 설명서는 .NET Framework 설명서 집합에서 <xref:System.Reflection> 를 참조하세요.  
  
## <a name="systemruntimecompilerservices-namespace"></a>System.Runtime.CompilerServices 네임스페이스  
 <xref:System.Runtime.CompilerServices> 네임스페이스는 언어 컴파일러에서 사용자용으로 디자인된 형식을 포함합니다. .NET 네이티브의 경우 새 예외 형식이 포함 되어 있습니다.  
  
|클래스|설명|  
|-----------|-----------------|  
|[MissingInteropDataException](missinginteropdataexception-class-net-native.md)|수동 마샬링 메서드를 호출했는데 정적 분석 또는 런타임 지시문 파일에서 형식의 메타데이터를 찾을 수 없을 때 throw되는 예외입니다.|  
  
 이 네임스페이스의 다른 형식에 대한 설명서는 .NET Framework 설명서 집합에서 <xref:System.Runtime.CompilerServices> 를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [MissingInteropDataException 클래스](missinginteropdataexception-class-net-native.md)
- [MissingMetadataException 클래스](missingmetadataexception-class-net-native.md)
- [MissingRuntimeArtifactException 클래스](missingruntimeartifactexception-class-net-native.md)
- [시작](getting-started-with-net-native.md)
