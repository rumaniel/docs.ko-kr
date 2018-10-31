---
title: .NET 클래스 라이브러리 개요
ms.date: 02/08/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- classes [.NET Framework], library overview
- classes [.NET Core], library overview
- .NET, library overview
- class objects value type
- naming conventions [.NET Framework]
- types, .NET Framework
- user-defined types
- Visual Basic, data types
- data types [.NET Framework], C++
- Visual C#, data types
- libraries, .NET Framework class library
- data types [.NET Framework], F#
- System namespace
- F#, data types
- .NET Framework, class library
- type system [.NET Framework]
- data types [.NET Framework]
- value types
- data types [.NET Framework], Visual Basic
- Common Language Specification
- namespaces [.NET Framework]
- floating point value type
- class library [.NET Framework]
- CLS
- logical value type
- .NET Framework class library, about
- built-in types
- namespaces [.NET Framework], about namespaces
- Visual C++, data types
- members [.NET Framework], type
- data types [.NET Framework], C#
- integer value type
- base types, class library
ms.assetid: 7e4c5921-955d-4b06-8709-101873acf157
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: acc51287a8c670da63d0ec421aa232864ea91c2b
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50185851"
---
# <a name="net-class-library-overview"></a>.NET 클래스 라이브러리 개요

.NET 구현에는 개발 과정을 지원 및 최적화하고 시스템 기능에 대한 액세스를 제공하는 클래스, 인터페이스, 대리자 및 값 형식이 포함되어 있습니다. 언어 간의 원활한 상호 운용성을 위해 대부분의 .NET 형식은 CLS(공용 언어 사양) 규격을 따르므로 CLS 규격 컴파일러를 사용하는 모든 프로그래밍 언어에서 사용될 수 있습니다.  
  
 .NET 형식은 .NET 응용 프로그램, 구성 요소 및 컨트롤 빌드의 기초가 됩니다. .NET 구현에는 다음과 같은 기능을 수행하는 형식이 포함되어 있습니다.  
  
-   기본 데이터 형식 및 예외를 나타냅니다.  
  
-   데이터 구조를 캡슐화합니다.  
  
-   I/O를 수행합니다.  
  
-   로드된 형식에 대한 정보에 액세스합니다.  
  
-   .NET Framework 보안 검사를 호출합니다.  
  
-   데이터 액세스, 리치 클라이언트 쪽 GUI, 서버에서 제어 가능한 클라이언트 쪽 GUI를 제공합니다.  
  
 .NET에서는 강력한 인터페이스 집합뿐만 아니라 추상 및 구체(비추상) 클래스도 제공합니다. 구체 클래스를 있는 그대로 사용할 수도 있고 여러 가지 경우에 구체 클래스에서 직접 클래스를 파생시켜 사용할 수도 있습니다. 인터페이스의 기능을 사용하려면 해당 인터페이스를 구현하는 클래스를 만들거나 해당 인터페이스를 구현하는 .NET 클래스 중 하나에서 클래스를 파생시킵니다.  
  
## <a name="naming-conventions"></a>명명 규칙

 .NET 형식에서는 계층 구조를 의미하는 스키마의 이름을 지정하는데 점 구문을 사용합니다. 이 방법을 사용하면 관련 형식을 네임스페이스로 그룹화하여 보다 쉽게 검색하고 참조할 수 있습니다. 전체 이름에서 첫 번째 부분(가장 오른쪽 점의 오른쪽 부분)은 해당 네임스페이스의 이름이고, 마지막 부분은 형식 이름입니다. 예를 들어 `System.Collections.Generic.List<T>`는 `System.Collections.Generic` 네임스페이스에 속하는 `List<T>` 형식을 나타냅니다. <xref:System.Collections.Generic>의 형식은 제네릭 컬렉션에 대한 작업에 사용할 수 있습니다.  
  
 이 이름 지정 체계를 사용하면 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 확장하는 라이브러리 개발자가 손쉽게 계층 구조의 그룹 형식을 만들고 일관되고 이해하기 쉬운 이름을 그룹에 지정할 수 있습니다. 또한 형식을 전체 이름, 즉 네임스페이스와 형식 이름별로 명확하게 식별할 수 있으므로 형식 이름 간의 충돌을 방지할 수 있습니다. 라이브러리 개발자는 다음과 같은 규칙을 사용하여 네임스페이스의 이름을 만듭니다.  
  
 *CompanyName*.*TechnologyName*  
  
 예를 들어, 네임스페이스 `Microsoft.Word`는 이 지침을 따릅니다.  
  
 명명 패턴을 사용하여 관련 형식을 네임스페이스로 그룹화하면 효과적으로 클래스 라이브러리를 빌드하고 문서화할 수 있습니다. 하지만 이 명명 스키마는 표시 여부, 멤버 액세스, 상속성, 보안 또는 바인딩에는 영향을 주지 않습니다. 하나의 네임스페이스가 여러 어셈블리에 분할될 수 있으며 하나의 어셈블리에 여러 네임스페이스의 형식이 포함될 수 있습니다. 어셈블리는 공용 언어 런타임에서 버전 관리, 배포, 보안, 로딩 및 표시 여부에 대한 형식적 구조를 제공합니다.  
  
 네임스페이스 및 형식 이름에 대한 자세한 내용은 [공용 형식 시스템](../../docs/standard/base-types/common-type-system.md)을 참조하세요.  
  
## <a name="system-namespace"></a>System 네임스페이스

 <xref:System> 네임스페이스는 .NET의 기본 형식에 대한 루트 네임스페이스입니다. 이 네임스페이스에는 모든 응용 프로그램에서 사용하는 <xref:System.Object>(상속 계층 구조의 루트), <xref:System.Byte>, <xref:System.Char>, <xref:System.Array>, <xref:System.Int32>, <xref:System.String> 등의 기본 데이터 형식을 나타내는 클래스가 포함됩니다. 이 형식의 대부분은 프로그래밍 언어에서 사용하는 기본 데이터 형식에 해당합니다. .NET Framework 형식을 사용하여 코드를 작성할 때 .NET Framework의 기본 데이터 형식이 필요하면 사용 중인 프로그래밍 언어의 해당 키워드를 사용할 수 있습니다.  
  
 다음 표에서는 .NET에서 제공하는 기본 형식 목록을 보여 주며 각 형식에 대해 간단히 설명한 다음 Visual Basic, C#, C++ 및 F#의 해당 형식을 나타냅니다.  
  
|범주|클래스 이름|설명|Visual Basic 데이터 형식|C# 데이터 형식|C++/CLI 데이터 형식|F# 데이터 형식|  
|--------------|----------------|-----------------|----------------------------|-------------------|---------------------|-----------------------|  
|정수|<xref:System.Byte>|8비트 부호 없는 정수입니다.|**Byte**|**byte**|**unsigned char**|**byte**|  
||<xref:System.SByte>|8비트 부호 있는 정수입니다.<br /><br /> CLS 규격을 따르지 않음|**SByte**|**sbyte**|**char**<br /> 또는<br /> **signed** **char**|**sbyte**|  
||<xref:System.Int16>|16비트 부호 있는 정수입니다.|**Short**|**short**|**short**|**int16**|  
||<xref:System.Int32>|32비트 부호 있는 정수입니다.|**Integer**|**int**|**int**<br /><br /> 또는<br /><br /> **long**|**int**|  
||<xref:System.Int64>|64비트 부호 있는 정수입니다.|**Long**|**long**|**__int64**|**int64**|  
||<xref:System.UInt16>|16비트 부호 없는 정수입니다.<br /><br /> CLS 규격을 따르지 않음|**UShort**|**ushort**|**unsigned short**|**uint16**|  
||<xref:System.UInt32>|32비트 부호 없는 정수입니다.<br /><br /> CLS 규격을 따르지 않음|**UInteger**|**uint**|**unsigned int**<br /> 또는<br /> **unsigned long**|**uint32**|  
||<xref:System.UInt64>|64비트 부호 없는 정수입니다.<br /><br /> CLS 규격을 따르지 않음|**ULong**|**ulong**|**unsigned __int64**|**uint64**|  
|부동 소수점|<xref:System.Single>|단정밀도(32비트) 부동 소수점 숫자|**Single**|**float**|**float**|**float32**</br> 또는</br>**single**|  
||<xref:System.Double>|배정밀도(64비트) 부동 소수점 숫자|**double**|**double**|**double**|**float**</br> 또는 </br> **double**|  
|논리|<xref:System.Boolean>|부울 값(true 또는 false)|**Boolean**|**bool**|**bool**|**bool**|  
|기타|<xref:System.Char>|유니코드(16비트) 문자|**Char**|**char**|**wchar_t**|**char**|  
||<xref:System.Decimal>|10진수(128비트) 값|**Decimal**|**decimal**|**Decimal**|**decimal**|  
||<xref:System.IntPtr>|내부 플랫폼에 따라 크기가 결정되는 부호 있는 정수(32비트 플랫폼에서는 32비트 값이고 64비트 플랫폼에서는 64비트 값임)|**IntPtr**<br /><br /> 기본 제공 형식이 아님|**IntPtr**<br /><br /> 기본 제공 형식이 아님|**IntPtr**<br /><br /> 기본 제공 형식이 아님|**unativeint**|  
||<xref:System.UIntPtr>|내부 플랫폼에 따라 크기가 결정되는 부호 없는 정수(32비트 플랫폼에서는 32비트 값이고 64비트 플랫폼에서는 64비트 값임)<br /><br /> CLS 규격을 따르지 않음|**UIntPtr**<br /><br /> 기본 제공 형식이 아님|**UIntPtr**<br /><br /> 기본 제공 형식이 아님|**UIntPtr**<br /><br /> 기본 제공 형식이 아님|**unativeint**|  
||<xref:System.Object>|개체 계층 구조의 루트|**개체**|**object**|**Object^**|**obj**|  
||<xref:System.String>|유니코드 문자로 구성된 변경할 수 없는 고정 길이의 문자열|**String**|**string**|**String^**|**string**|  
  
 <xref:System> 네임스페이스에는 기본 데이터 형식 외에도 예외를 처리하는 클래스에서 응용 프로그램 도메인 및 가비지 수집기 등의 핵심 런타임 개념을 다루는 클래스에 이르는 100개 이상의 클래스가 들어 있습니다. 또한 <xref:System> 네임스페이스에는 2차 네임스페이스도 많이 들어 있습니다.  
  
 네임스페이스에 대한 자세한 내용은 [.NET API 브라우저](https://docs.microsoft.com/dotnet/api)를 사용하여 .NET 클래스 라이브러리를 참조하세요. API 참조 설명서는 각 네임스페이스, 해당 유형 및 해당 멤버의 각각에 대한 설명서를 제공합니다.  
  
## <a name="see-also"></a>참고 항목

- [공용 형식 시스템](../../docs/standard/base-types/common-type-system.md)  
- [.NET API 브라우저](https://docs.microsoft.com/dotnet/api)  
- [개요](../../docs/framework/get-started/overview.md)
