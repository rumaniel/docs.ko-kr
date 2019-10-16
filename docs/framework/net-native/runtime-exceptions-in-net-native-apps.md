---
title: .NET 네이티브 앱의 런타임 예외
ms.date: 03/30/2017
ms.assetid: 5f050181-8fdd-4a4e-9d16-f84c22a88a97
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 27a2e0906343d115c47230c726efb74cd51d4c93
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049169"
---
# <a name="runtime-exceptions-in-net-native-apps"></a>.NET 네이티브 앱의 런타임 예외
디버그 및 릴리스 구성이 완전히 다르므로 해당 대상 플랫폼에서 유니버설 Windows 플랫폼 앱의 릴리스 빌드를 테스트하는 것이 중요합니다. 기본적으로 디버그 구성에서는 .NET 핵심 런타임을 사용하여 앱을 컴파일하지만 릴리스 구성에서는 .NET 네이티브를 사용하여 앱을 네이티브 코드로 컴파일합니다.  
  
> [!IMPORTANT]
> 앱의 릴리스 버전을 테스트할 때 발생할 수 있는 [MissingMetadataException](missingmetadataexception-class-net-native.md), [MissingInteropDataException](missinginteropdataexception-class-net-native.md)및 [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md) 예외를 처리 하는 방법에 대 한 자세한 내용은 "4 단계: [시작](getting-started-with-net-native.md) 항목에서 [리플렉션 및 .NET 네이티브](reflection-and-net-native.md) 및 [런타임 지시문 (Rd .xml) 구성 파일 참조](runtime-directives-rd-xml-configuration-file-reference.md)를 비롯 하 여 수동으로 누락 된 메타 데이터를 확인 합니다.  
  
## <a name="debug-and-release-builds"></a>디버그 및 릴리스 빌드  
 디버그 빌드가 .NET 핵심 런타임에 대해 실행될 때 네이티브 코드로 컴파일되지 않았습니다. 그러므로 일반적으로 모든 서비스가 앱에서 사용 가능한 런타임에 의해 제공됩니다.  
  
 반면, 릴리스 빌드는 해당 대상 플랫폼을 위해 네이티브 코드로 컴파일되고, 외부 런타임 및 라이브러리의 종속성이 대부분 제거되고, 최대 성능을 위해 코드를 최적화합니다.  
  
 .NET 네이티브를 사용하여 컴파일된 릴리스 빌드를 디버깅하는 경우:  
  
- 기본 .NET 디버깅 도구와는 다른 .NET 네이티브 디버그 엔진을 사용합니다.  
  
- 실행 파일의 크기가 가능한 만큼 줄어듭니다. .NET 네이티브에서 실행 파일의 크기를 줄이는 방법 중 하나는 런타임 예외 메시지를 크게 잘라내는 것입니다. 자세한 내용은 [Runtime exception messages](#Messages) 섹션을 참조하세요.  
  
- 코드가 매우 최적화됩니다. 이는 가능할 때마다 인라인 처리가 사용된다는 의미입니다. 인라인 처리는 외부 루틴에서 호출 루틴으로 코드를 이동합니다.   .NET 네이티브가 특수 런타임을 제공하고 적극적인 인라인 처리를 구현한다는 사실은 디버깅 시 표시되는 호출 스택에 영향을 줍니다.  자세한 내용은 [Runtime call stack](#CallStack) 섹션을 참조하세요.  
  
> [!NOTE]
> **.NET 네이티브 도구 체인을 사용하여 컴파일** 상자를 선택하거나 선택을 취소하여 디버그 및 릴리스 빌드가 .NET 네이티브 도구 체인을 사용하여 컴파일되는지 제어할 수 있습니다.   단, Windows 스토어는 항상 .NET 네이티브 도구 체인을 사용하여 프로덕션 버전의 앱을 컴파일합니다.  
  
<a name="Messages"></a>   
## <a name="runtime-exception-messages"></a>Runtime exception messages  
 애플리케이션 실행 파일 크기를 최소화하기 위해 .NET 네이티브에서는 예외 메시지의 전체 텍스트를 포함하지 않습니다. 결과적으로, 릴리스 빌드에서 런타임 예외가 throw될 경우 예외 메시지의 전체 텍스트가 표시되지 않을 수 있습니다. 대신 자세한 정보에 대한 링크와 하위 문자열로 구성될 수 있습니다. 예를 들어 예외 정보가 다음과 같이 나타날 수 있습니다.  
  
```output
Exception thrown: '$16_System.AggregateException' in Unknown Module.  
  
Additional information: AggregateException_ctor_DefaultMessage  
  
If there is a handler for this exception, the program may be safely continued.  
```  
  
 전체 예외 메시지를 표시하려면 디버그 빌드를 대신 실행합니다. 예를 들어 앞에서 릴리스 빌드에 나타난 예외 정보가 디버그 빌드에서는 다음과 같이 나타날 수 있습니다.  
  
```output
Exception thrown: 'System.AggregateException' in NativeApp.exe.  
  
Additional information: Value does not fall within the expected range.  
```  
  
<a name="CallStack"></a>   
## <a name="runtime-call-stack"></a>Runtime call stack  
 인라인 처리 및 기타 최적화로 인해 .NET 네이티브 도구 체인에 의해 컴파일된 앱에서 표시하는 호출 스택을 사용하면 런타임 예외 경로를 명확히 식별하지 못할 수 있습니다.  
  
 전체 스택을 얻으려면 디버그 빌드를 대신 실행합니다.  
  
## <a name="see-also"></a>참고자료

- [Windows 유니버설 앱 .NET 네이티브 디버깅](https://devblogs.microsoft.com/devops/debugging-net-native-windows-universal-apps/)
- [시작](getting-started-with-net-native.md)
