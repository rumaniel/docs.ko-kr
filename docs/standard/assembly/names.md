---
title: 어셈블리 이름
ms.date: 08/19/2019
helpviewer_keywords:
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
ms.assetid: 8f8c2c90-f15d-400e-87e7-a757e4f04d0e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 22e35450460436e164db922fce76a53c437f6bdf
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835316"
---
# <a name="assembly-names"></a>어셈블리 이름
어셈블리 이름은 메타데이터에 저장되고 어셈블리 범위 및 애플리케이션에 의한 사용에 상당한 영향을 미칩니다. 강력한 이름의 어셈블리에는 어셈블리의 이름, 문화권, 공개 키 및 버전 번호가 포함된 정규화된 이름이 있습니다. 이 이름을 보통 표시 이름이라고 하고 로드된 어셈블리의 경우 <xref:System.Reflection.Assembly.FullName%2A> 속성을 사용하여 가져올 수 있습니다.  
  
 런타임은 이 정보를 사용하여 어셈블리를 찾고 같은 이름을 가진 다른 어셈블리와 구별합니다. 예를 들어 `myTypes`라는 강력한 이름의 어셈블리에는 다음과 같은 정규화된 이름이 있을 수 있습니다.  
  
```  
myTypes, Version=1.0.1234.0, Culture=en-US, PublicKeyToken=b77a5c561934e089c, ProcessorArchitecture=msil  
```  
  
> [!NOTE]
> .NET Framework 버전 2.0에서는 어셈블리의 프로세서별 버전을 허용하기 위해 프로세서 아키텍처가 어셈블리 ID에 추가됩니다. 프로세서 아키텍처를 통해서만 ID가 다른 어셈블리의 버전을 만들 수 있습니다(예: 32비트 및 64비트 프로세서별 버전). 강력한 이름에는 프로세서 아키텍처가 필요하지 않습니다. 자세한 내용은 <xref:System.Reflection.AssemblyName.ProcessorArchitecture%2A?displayProperty=nameWithType>을 참조하세요.  
  
 이 예제에서 정규화된 이름은 `myTypes` 어셈블리에 공개 키 토큰과 함께 강력한 이름이 있고, 영어(미국)에 대한 문화권 값이 있고, 버전 번호 1.0.1234.0이 있음을 나타냅니다. 해당 프로세서 아키텍처는 "msil"이며, 이는 운영 체제 및 프로세서에 따라 32비트 코드 또는 64비트 코드로 JIT(Just-In-Time) 컴파일될 것임을 의미합니다.  
  
 어셈블리의 형식을 요청하는 코드에는 정규화된 어셈블리 이름을 사용해야 합니다. 이것을 정규화된 바인딩이라고 합니다. .NET Framework에서 어셈블리를 참조할 경우 어셈블리 이름만 지정하는 부분 바인딩은 허용되지 않습니다.  
  
 .NET Framework를 구성하는 어셈블리에 대한 모든 어셈블리 참조에는 어셈블리의 정규화된 이름도 포함되어야 합니다. 예를 들어 버전 1.0의 System.Data .NET Framework 어셈블리에 대한 참조에는 다음이 포함됩니다.  
  
```  
System.data, version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089  
```  
  
 이 버전은 .NET Framework 버전 1.0과 함께 제공된 모든 .NET Framework 어셈블리의 버전 번호와 일치합니다. .NET Framework 어셈블리의 경우 문화권 값은 항상 중립적이고 공개 키는 위 예제에 표시된 것과 같습니다.  
  
 예를 들어 구성 파일에 어셈블리 참조를 추가하여 추적 수신기를 설정하기 위해 시스템 .NET Framework 어셈블리의 정규화된 이름을 포함합니다.  
  
```xml  
<add name="myListener" type="System.Diagnostics.TextWriterTraceListener, System, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" initializeData="c:\myListener.log" />  
```  
  
> [!NOTE]
> 런타임은 어셈블리에 바인딩할 때 어셈블리 이름의 대/소문자를 구분하지 않고 처리하지만 어셈블리에서 사용된 대/소문자를 보존합니다. Windows SDK의 여러 도구는 어셈블리 이름의 대/소문자를 구분해서 처리합니다. 최상의 결과를 위해서 대/소문자를 구분한 것처럼 어셈블리 이름을 관리하세요.  
  
## <a name="name-application-components"></a>애플리케이션 구성 요소 이름 지정  
 런타임은 어셈블리 ID를 확인할 때 파일 이름을 고려하지 않습니다. 어셈블리 이름, 버전, 문화권 및 강력한 이름으로 구성된 어셈블리 ID는 런타임에 대해 분명해야 합니다.  
  
 예를 들어 *myAssembly.dll*이라는 어셈블리를 참조하는 *myAssembly.exe*라는 어셈블리가 있는 경우 *myAssembly.exe*를 실행하면 바인딩이 올바르게 수행됩니다. 하지만 또 다른 애플리케이션이 <xref:System.AppDomain.ExecuteAssembly%2A?displayProperty=nameWithType> 메서드를 사용하여 *myAssembly.exe*를 실행하면 런타임은 *myAssembly.exe*가 `myAssembly`에 대한 바인딩을 요청할 때 `myAssembly`가 이미 로드되었다고 판단합니다. 이 경우 *myAssembly.dll*은 로드되지 않습니다. *myAssembly.exe*에 요청된 형식이 포함되어 있지 않으므로 <xref:System.TypeLoadException>이 발생합니다.  
  
 이 문제를 방지하려면 애플리케이션을 구성하는 어셈블리의 이름을 서로 다르게 지정하거나 같은 이름을 가진 어셈블리를 서로 다른 디렉터리에 포함하세요.  
  
> [!NOTE]
> .NET Framework에서는 강력한 이름의 어셈블리를 전역 어셈블리 캐시에 넣는 경우 어셈블리의 파일 이름이 어셈블리 이름( *.exe* 또는 *.dll* 등의 파일 이름 확장명 제외)과 일치해야 합니다. 예를 들어 어셈블리의 파일 이름이 *myAssembly.dll*이면 어셈블리 이름은 `myAssembly`여야 합니다. 루트 애플리케이션 디렉터리에만 배포된 프라이빗 어셈블리의 이름은 파일 이름과 다를 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [방법: 어셈블리의 정규화된 이름 식별](find-fully-qualified-name.md)
- [어셈블리 만들기](create.md)
- [강력한 이름의 어셈블리](strong-named.md)
- [전역 어셈블리 캐시](../../framework/app-domains/gac.md)
- [런타임에서 어셈블리를 찾는 방법](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [어셈블리를 사용한 프로그램](program.md)
