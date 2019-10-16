---
title: 형식 동등 및 포함된 Interop 형식
ms.date: 03/30/2017
helpviewer_keywords:
- type equivalence
- embedded interop types
- primary interop assemblies,not necessary in CLR version 4
- NoPIA
ms.assetid: 78892eba-2a58-4165-b4b1-0250ee2f41dc
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 137aeaab4e63adbb81c0f3d90718def10f906e6a
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66489241"
---
# <a name="type-equivalence-and-embedded-interop-types"></a>형식 동등 및 포함된 Interop 형식

.NET Framework 4부터 공용 언어 런타임은 관리되는 어셈블리가 interop 어셈블리에서 COM 형식에 대한 형식 정보를 가져오도록 요구하는 대신 COM 형식에 대한 형식 정보를 관리되는 어셈블리에 직접 포함하는 기능을 지원합니다. 포함된 형식 정보에는 관리되는 어셈블리에서 실제로 사용되는 형식 및 멤버만 포함되므로 두 개의 관리되는 어셈블리에서 동일한 COM 형식이 전혀 다르게 표시될 수 있습니다. 관리되는 어셈블리마다 COM 형식의 해당 보기를 나타내는 다른 <xref:System.Type> 개체가 있습니다. 공용 언어 런타임은 인터페이스, 구조체, 열거형 및 대리자에 대한 이러한 다양한 보기 간에 형식 동등을 지원합니다.

형식 동등은 관리되는 어셈블리 간에 전달되는 COM 개체를 수신 어셈블리에서 적절한 관리되는 형식으로 캐스팅할 수 있음을 의미합니다.

> [!NOTE]
> 형식 동등 및 포함된 interop 형식은 애플리케이션과 함께 interop 어셈블리를 배포할 필요가 없기 때문에 COM 구성 요소를 사용하는 애플리케이션 및 추가 기능의 배포를 간소화합니다. 공유 COM 구성 요소의 개발자는 이전 버전의 .NET Framework에서 해당 구성 요소를 사용하려는 경우 여전히 PIA(주 interop 어셈블리)를 만들어야 합니다.

## <a name="type-equivalence"></a>형식 동등

 COM 형식 동등은 인터페이스, 구조체, 열거형 및 대리자에 대해 지원됩니다. COM 형식은 다음 조건이 모두 true인 경우 동등합니다.

- 형식이 둘 다 인터페이스, 둘 다 구조체, 둘 다 열거형 또는 둘 다 대리자입니다.

- 다음 섹션에 설명된 대로 형식의 ID가 같습니다.

- [COM 형식에 형식 동등 표시](#marking-com-types-for-type-equivalence) 섹션에 설명된 대로 두 형식이 모두 형식 동등에 적합합니다.

### <a name="type-identity"></a>형식 ID

두 형식은 해당 범위 및 ID가 일치할 때, 즉 각각 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> 특성이 있고 두 특성에 일치하는 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A> 및 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A> 속성이 있는 경우 ID가 같다고 확인됩니다. <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A> 비교는 대/소문자를 구분하지 않습니다.

형식에 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> 특성이 없는 경우 또는 범위 및 식별자를 지정하지 않는 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> 특성이 있는 경우에도 다음과 같이 해당 형식의 동등을 고려할 수 있습니다.

- 인터페이스의 경우 <xref:System.Runtime.InteropServices.GuidAttribute> 값이 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A?displayProperty=nameWithType> 속성 대신 사용되고, <xref:System.Type.FullName%2A?displayProperty=nameWithType> 속성(즉, 네임스페이스를 포함하는 형식 이름)이 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A?displayProperty=nameWithType> 속성 대신 사용됩니다.

- 구조체, 열거형 및 대리자의 경우 포함하는 어셈블리의 <xref:System.Runtime.InteropServices.GuidAttribute>가 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A> 속성 대신 사용되고, <xref:System.Type.FullName%2A?displayProperty=nameWithType> 속성이 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A> 속성 대신 사용됩니다.

### <a name="marking-com-types-for-type-equivalence"></a>COM 형식에 형식 동등 표시

 다음 두 가지 방법으로 형식을 형식 동등에 적합한 것으로 표시할 수 있습니다.

- 형식에 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> 특성을 적용합니다.

- 형식을 COM 가져오기 형식으로 지정합니다. <xref:System.Runtime.InteropServices.ComImportAttribute> 특성이 있는 인터페이스는 COM 가져오기 형식입니다. 인터페이스, 구조체, 열거형 또는 대리자가 정의되어 있는 어셈블리에 <xref:System.Runtime.InteropServices.ImportedFromTypeLibAttribute> 특성이 있는 경우 해당 항목은 COM 가져오기 형식입니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Type.IsEquivalentTo%2A>
- [관리 코드에서 COM 형식 사용](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3y76b69k(v=vs.100))
- [형식 라이브러리를 어셈블리로 가져오기](importing-a-type-library-as-an-assembly.md)
