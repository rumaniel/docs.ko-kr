---
title: 사용 지침
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], usage guidelines
ms.assetid: 42215ffa-a099-4a26-b14e-fb2bdb6f95b7
author: KrzysztofCwalina
ms.openlocfilehash: 761570b899a2a36391eb81dc7f42e13fff1f14ef
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61778809"
---
# <a name="usage-guidelines"></a>사용 지침

이 섹션에서는 일반적인 형식을 사용 하 여 공개적으로 액세스할 수 있는 api에 대 한 지침을 포함 합니다. 기본 제공 프레임 워크 형식 (예: serialization 특성) 및 일반적인 연산자 오버 로드를 직접 사용 하 여 다룹니다.
  
<xref:System.IDisposable?displayProperty=nameWithType> 인터페이스는이 섹션에서는 다루지 않습니다 하지만 부분은 합니다 [Dispose 패턴](../../../docs/standard/design-guidelines/dispose-pattern.md) 섹션.

> [!NOTE]
> .NET Framework의 기본 제공 형식 지침 및 다른 일반적인 방법에 대 한 자세한 내용은 다음 참조 항목을 참조 하십시오: <xref:System.DateTime?displayProperty=nameWithType>, <xref:System.DateTimeOffset?displayProperty=nameWithType>, <xref:System.ICloneable?displayProperty=nameWithType>, <xref:System.IComparable%601?displayProperty=nameWithType>를 <xref:System.IEquatable%601?displayProperty=nameWithType>를 <xref:System.Nullable%601?displayProperty=nameWithType>, <xref:System.Object?displayProperty=nameWithType> , <xref:System.Uri?displayProperty=nameWithType>.

## <a name="in-this-section"></a>단원 내용

[배열](arrays.md)  
[특성](attributes.md)  
[컬렉션](guidelines-for-collections.md)  
[serialization](serialization.md)  
[System.Xml 사용법](system-xml-usage.md)  
[같음 연산자](equality-operators.md)  

*Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*

*사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
