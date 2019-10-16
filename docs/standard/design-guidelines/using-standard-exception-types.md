---
title: 표준 예외 형식 사용
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- throwing exceptions, standard types
- catching exceptions
- exceptions, catching
- exceptions, throwing
ms.assetid: ab22ce03-78f9-4dca-8824-c7ed3bdccc27
author: KrzysztofCwalina
ms.openlocfilehash: b947c7cce057c060b1ab5054d1227f5703ccbf89
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62026343"
---
# <a name="using-standard-exception-types"></a>표준 예외 형식 사용
이 섹션에서는 프레임 워크 및 사용량의 세부 정보에서 제공 하는 표준 예외를 설명 합니다. 이 목록은 철저 한 있지는 않습니다. 다른 프레임 워크 예외 형식 사용에 대 한.NET Framework 참조 설명서를 참조 하십시오.  
  
## <a name="exception-and-systemexception"></a>예외 및 SystemException  
 **X DO NOT** throw <xref:System.Exception?displayProperty=nameWithType> 또는 <xref:System.SystemException?displayProperty=nameWithType>합니다.  
  
 **X DO NOT** catch `System.Exception` 또는 `System.SystemException` 프레임 워크 코드에 다시 throw 하려는 경우가 아니면 합니다.  
  
 **X AVOID** 위해서 `System.Exception` 또는 `System.SystemException`, 최상위 예외 처리기에서를 제외 하 고 있습니다.  
  
## <a name="applicationexception"></a>ApplicationException  
 **X DO NOT** throw 하거나이 로부터 파생할 <xref:System.ApplicationException>합니다.  
  
## <a name="invalidoperationexception"></a>InvalidOperationException  
 **✓ DO** throw 한 <xref:System.InvalidOperationException> 부적절 한 상태에 개체가 있으면 됩니다.  
  
## <a name="argumentexception-argumentnullexception-and-argumentoutofrangeexception"></a>ArgumentException, ArgumentNullException을 및 ArgumentOutOfRangeException  
 **✓ DO** throw <xref:System.ArgumentException> 또는 멤버에 잘못 된 인수가 전달 되 면 그 하위 중 하나입니다. 가장 많이 파생 된 예외 형식에 해당 하는 경우에 선호 합니다.  
  
 **✓ DO** 설정는 `ParamName` 속성의 서브 클래스 중 하나를 throw 할 때 `ArgumentException`합니다.  
  
 이 속성에는 예외를 throw 시킨 매개 변수의 이름을 나타냅니다. 생성자 오버 로드 중 하나를 사용 하 여 속성을 설정할 수 있는 참고 합니다.  
  
 **✓ DO** 사용 `value` 속성 setter의 암시적 값 매개 변수 이름에 대 한 합니다.  
  
## <a name="nullreferenceexception-indexoutofrangeexception-and-accessviolationexception"></a>Nullreferenceexception이 고, IndexOutOfRangeException AccessViolationException  
 **X DO NOT** 공개적으로 호출할 수 Api 명시적 또는 암시적으로 throw 할 수 있도록 <xref:System.NullReferenceException>, <xref:System.AccessViolationException>, 또는 <xref:System.IndexOutOfRangeException>합니다. 이러한 예외는 예약 및 실행 엔진에서 throw 되 고 대부분의 경우 버그를 나타냅니다.  
  
 이러한 예외가 throw 되지 않도록 확인 하는 인수를 수행 합니다. 시간이 지남에 따라 변경 될 수 있는 메서드의 구현 세부 정보를 노출 이러한 예외를 throw 합니다.  
  
## <a name="stackoverflowexception"></a>StackOverflowException  
 **X DO NOT** 명시적으로 throw <xref:System.StackOverflowException>합니다. CLR에서만 예외를 명시적으로 throw 되어야 합니다.  
  
 **X DO NOT** catch `StackOverflowException`합니다.  
  
 임의의 스택 오버플로 시 일관성을 유지 하는 관리 되는 코드를 쓸 거의 불가능 합니다. CLR의 관리 되지 않는 일부 임의 스택 오버플로를 철회 하는 대신 스택 오버플로 잘 정의 된 위치로 이동 하려면 프로브를 사용 하 여 일관성을 유지 합니다.  
  
## <a name="outofmemoryexception"></a>OutOfMemoryException  
 **X DO NOT** 명시적으로 throw <xref:System.OutOfMemoryException>합니다. 만 CLR 인프라에서 발생 하 여이 예외가입니다.  
  
## <a name="comexception-sehexception-and-executionengineexception"></a>ComException 고 SEHException, ExecutionEngineException  
 **X DO NOT** 명시적으로 throw <xref:System.Runtime.InteropServices.COMException>, <xref:System.ExecutionEngineException>, 및 <xref:System.Runtime.InteropServices.SEHException>합니다. 이러한 예외만 CLR 인프라에서 발생 하는입니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [예외 디자인 지침](../../../docs/standard/design-guidelines/exceptions.md)
