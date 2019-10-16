---
title: 일반 명명 규칙
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- names [.NET Framework], conflicts
- type names, conflicts
- language-specific type names
- names [.NET Framework], about naming guidelines
- names [.NET Framework], abbreviations
- abbreviation naming guidelines
- acronym naming guidelines
- Hungarian notation
- names [.NET Framework], type names
- names [.NET Framework], acronyms
ms.assetid: d3a77ea1-75d2-4969-a8c3-3e1e3e1aaedc
author: KrzysztofCwalina
ms.openlocfilehash: ae1b7ce83f6698cef470aabf07a12d89042ab8a3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62026395"
---
# <a name="general-naming-conventions"></a>일반 명명 규칙
이 섹션에서는 일반 명명 규칙 단어 선택와 관련 된 약어 및 머리글자어 및 권장 사항을 사용 하 여 언어별 이름을 사용 하지 않도록 하는 방법에 대 한 지침을 설명 합니다.  
  
## <a name="word-choice"></a>단어 선택  
 **✓ DO** 쉽게 읽을 수 있는 식별자 이름을 선택 합니다.  
  
 예를 들어, 명명 된 속성 `HorizontalAlignment` 좀 더 영어-읽기 보다 `AlignmentHorizontal`합니다.  
  
 **✓ DO** 가독성 간결한 설명을 위해 보다 우선 합니다.  
  
 속성 이름을 `CanScrollHorizontally` 보다 나은 `ScrollableX` (x 축에는 모호한 참조).  
  
 **X DO NOT** 밑줄, 하이픈 또는 기타 영숫자가 아닌 문자를 사용 합니다.  
  
 **X DO NOT** 헝가리 식 표기법을 사용 합니다.  
  
 **X AVOID** 널리의 키워드와 충돌 하는 식별자를 사용 하 여 프로그래밍 언어를 사용 합니다.  
  
 규칙 4의는 언어 사양 CLS (공용)에 따라 모든 규격 언어 식별자로 해당 언어의 키워드를 사용 하는 명명 된 항목에 대 한 액세스를 허용 하는 메커니즘을 제공 해야 합니다. C#의 경우, 예를 들어, 사용 하는 @ 기호가 경우에서 이스케이프 메커니즘으로 합니다. 그러나 것이 좋습니다 여전히는 메서드를 사용 하는 이스케이프 시퀀스 없이 개를 사용 하 여 훨씬 더 어렵기 때문에 일반적인 키워드를 방지 하려면.  
  
## <a name="using-abbreviations-and-acronyms"></a>머리 글자어와 약어를 사용 하 여  
 **X DO NOT** 식별자 이름의 일부로 약어 또는 축약을 사용 합니다.  
  
 사용 예를 들어 `GetWindow` 대신 `GetWin`합니다.  
  
 **X DO NOT** 폭넓게 활용 되 고 필요한 경우에 있는 경우에 하지 않은 머리글자어를 사용 합니다.  
  
## <a name="avoiding-language-specific-names"></a>언어별 이름을 방지  
 **✓ DO** 형식 이름에 대 한 언어별 키워드 보다는 특별 한 의미가 있는 이름을 사용 합니다.  
  
 예를 들어 `GetLength` 보다 더 나은 이름이 `GetInt`합니다.  
  
 **✓ DO** 드문 경우 식별자 의미가 없는 해당 형식 이상의 때의 언어 관련 이름 대신 일반 CLR 형식 이름을 사용 합니다.  
  
 변환할 메서드 예를 들어 <xref:System.Int64> 명명할 `ToInt64`가 아닌 `ToLong` (때문에 <xref:System.Int64> 은 C#에 대 한 CLR 이름-특정 별칭 `long`). 다음 표에서 몇 가지 기본 데이터 형식을 CLR을 사용 하 여 형식 이름 (해당 형식 이름은 뿐만 아니라 C#, Visual Basic의 경우 및 C++).  
  
|C#|Visual Basic|C++|CLR|  
|---------|------------------|-----------|---------|  
|**sbyte**|**SByte**|**char**|**SByte**|  
|**byte**|**Byte**|**unsigned char**|**Byte**|  
|**short**|**Short**|**short**|**Int16**|  
|**ushort**|**UInt16**|**unsigned short**|**UInt16**|  
|**int**|**Integer**|**int**|**Int32**|  
|**uint**|**UInt32**|**unsigned int**|**UInt32**|  
|**long**|**Long**|**__int64**|**Int64**|  
|**ulong**|**UInt64**|**unsigned __int64**|**UInt64**|  
|**float**|**Single**|**float**|**Single**|  
|**double**|**Double**|**double**|**Double**|  
|**bool**|**Boolean**|**bool**|**Boolean**|  
|**char**|**Char**|**wchar_t**|**Char**|  
|**string**|**String**|**String**|**String**|  
|**object**|**개체**|**개체**|**개체**|  
  
 **✓ DO** 와 같은 일반 이름을 사용 하 여 `value` 또는 `item`, 형식 이름 식별자 의미가 없는 및 매개 변수의 형식이 중요 하지 않은 경우 드문 경우에서를 반복할 필요 없이 합니다.  
  
## <a name="naming-new-versions-of-existing-apis"></a>새 버전의 기존 Api 이름  
 **✓ DO** 기존 API의 새 버전을 만들 때 기존 API와 유사한 이름을 사용 합니다.  
  
 이렇게 하면 Api 간의 관계를 강조 표시 합니다.  
  
 **✓ DO** 선호 기존 API의 새 버전을 나타내는 접두사 보다는 접미사를 추가 합니다.  
  
 설명서를 검색할 때 검색 데 도움이 되는이 IntelliSense를 사용 하 여 또는입니다. 대부분의 브라우저 및 IntelliSense 식별자 사전순으로 표시 되므로 새로운 Api를 가까운 API의 이전 버전을 구성할 수 됩니다.  
  
 **✓ CONSIDER** 접두사 또는 접미사를 추가 하는 대신 새로운, 하지만 의미 있는 식별자를 사용 하 여 합니다.  
  
 **✓ DO** 특히 API의 기존 이름이 경우 (즉,이 산업 표준) 쉽게 알아볼 수 있는 유일한 이름이 어떤 의미 있는 추가 하는 경우 접미사 (또는 이름을 변경) 되지 않은 경우 응용 프로그램에 기존 API의 새 버전을 나타내기 위해 숫자 접미사를 사용 합니다. ropriate 옵션입니다.  
  
 **X DO NOT** "Ex" (또는 유사한)를 사용 하 여 이전 버전의 동일한 API와 구분 식별자에 대 한 접미사입니다.  
  
 **✓ DO** 32 비트 정수 대신 64 비트 정수 (long 정수)에서 작동 하는 Api의 버전을 도입할 때 "64" 접미사를 사용 합니다. 기존 32 비트 API 있는 경우이 방법을 사용 해야 64 비트 버전만 사용 하 여 새로운 Api에 대 한 수행 하지 마십시오.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [명명 지침](../../../docs/standard/design-guidelines/naming-guidelines.md)
