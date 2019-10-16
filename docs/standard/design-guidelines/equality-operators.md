---
title: 같음 연산자
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- class library design guidelines [.NET Framework], Equals method
- class library design guidelines [.NET Framework], equality operator
- equality operator (==) [.NET Framework]
- Equals method
- == operator (equality) [.NET Framework]
ms.assetid: bc496a91-fefb-4ce0-ab4c-61f09964119a
author: KrzysztofCwalina
ms.openlocfilehash: ef1a0aff1ac59434d9d9a6f0371bf236f637050e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61960338"
---
# <a name="equality-operators"></a>같음 연산자
이 섹션에서는 같음 연산자를 오버 로드에 대해 설명 하 고 가리킵니다 `operator==` 고 `operator!=` 같음 연산자입니다.  
  
 **X DO NOT** 같음 연산자 있고 다른 선언 중 하나를 오버 로드 합니다.  
  
 **✓ DO** 되도록 <xref:System.Object.Equals%2A?displayProperty=nameWithType> 및 같음 연산자는 정확히 동일한 의미 체계와 비슷한 성능 특성입니다.  
  
 자주 따라서 `Object.Equals` 같음 연산자를 오버 로드 하는 경우 재정의 해야 합니다.  
  
 **X AVOID** 같음 연산자에서 예외를 throw 합니다.  
  
 예를 들어 인수 중 하나를 throw 하지 않고 null 이면 false를 반환 `NullReferenceException`합니다.  
  
## <a name="equality-operators-on-value-types"></a>값 형식에 같음 연산자  
 **✓ DO** 같음이 의미가 있을 경우에 값 형식에 같음 연산자를 오버 로드 합니다.  
  
 대부분의 프로그래밍 언어에서은의 기본 구현이 없는 `operator==` 값 형식에 대 한 합니다.  
  
## <a name="equality-operators-on-reference-types"></a>참조 형식에 같음 연산자  
 **X AVOID** 변경 가능한 참조 형식에 같음 연산자를 오버 로드 합니다.  
  
 다양 한 언어 참조 형식에 대 한 기본 같음 연산자가 있는 경우. 기본 제공 연산자에는 일반적으로 참조 같음 구현 하 고 값이 같은지를 기본 동작이 변경 될 때 많은 개발자가 알고 계십니까 키를 누릅니다.  
  
 이 문제는 불변성을 사용 하면 값이 같은지 참조 같음 사이의 차이점을 확인 하기가 훨씬 변경할 수 없는 참조 형식에 대 한 완화 됩니다.  
  
 **X AVOID** 참조 일치 하는 것 보다 크게 느려지지 구현 되는 경우에 참조 형식에 같음 연산자를 오버 로드 합니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [사용 지침](../../../docs/standard/design-guidelines/usage-guidelines.md)
