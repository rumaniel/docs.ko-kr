---
title: 보안 및 공용 읽기 전용 배열 필드
ms.date: 03/30/2017
helpviewer_keywords:
- security [.NET Framework], public read-only array fields
ms.assetid: 3df28dee-2a9f-40ff-9852-bfdbe59c27f3
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3d36009fa4fc7b9299708768fe34a75f1fde6797
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69910733"
---
# <a name="security-and-public-read-only-array-fields"></a>보안 및 공용 읽기 전용 배열 필드
읽기 전용 공용 배열 필드를 수정할 수 있으므로 관리 되는 라이브러리의 읽기 전용 공용 배열 필드를 사용 하 여 응용 프로그램의 경계 동작 또는 보안을 정의 하지 마십시오.  
  
## <a name="remarks"></a>설명  
 일부 .NET framework 클래스에는 플랫폼별 경계 매개 변수를 포함 하는 읽기 전용 public 필드가 포함 됩니다.  예를 <xref:System.IO.Path.InvalidPathChars> 들어 필드는 파일 경로 문자열에 허용 되지 않는 문자를 설명 하는 배열입니다.  많은 유사한 필드가 .NET Framework 전체에 표시 됩니다.  
  
 와 같은 <xref:System.IO.Path.InvalidPathChars> 공용 읽기 전용 필드의 값은 코드 또는 코드의 응용 프로그램 도메인을 공유 하는 코드로 수정할 수 있습니다.  응용 프로그램의 경계 동작을 정의 하려면 다음과 같은 읽기 전용 공용 배열 필드를 사용 하면 안 됩니다.  이렇게 하면 악의적인 코드가 경계 정의를 변경 하 고 코드를 예기치 않은 방식으로 사용할 수 있습니다.  
  
 .NET Framework 버전 2.0 이상에서는 공용 배열 필드를 사용 하는 대신 새 배열을 반환 하는 메서드를 사용 해야 합니다.  예를 들어 <xref:System.IO.Path.InvalidPathChars> 필드를 사용 하는 대신 <xref:System.IO.Path.GetInvalidPathChars%2A> 메서드를 사용 해야 합니다.  
  
 .NET Framework 형식은 공용 필드를 사용 하 여 내부적으로 경계 형식을 정의 하지 않습니다.  대신 .NET Framework 별도의 전용 필드를 사용 합니다.  이러한 공용 필드의 값을 변경 해도 .NET Framework 형식의 동작은 변경 되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [보안 코딩 지침](../../standard/security/secure-coding-guidelines.md)
