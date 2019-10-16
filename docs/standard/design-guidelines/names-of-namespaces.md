---
title: 네임스페이스의 이름
ms.date: 10/22/2008
helpviewer_keywords:
- names [.NET Framework], conflicts
- names [.NET Framework], namespaces
- type names, conflicts
- namespaces [.NET Framework], names
- names [.NET Framework], type names
ms.assetid: a49058d2-0276-43a7-9502-04adddf857b2
author: KrzysztofCwalina
ms.openlocfilehash: b8b6ec195fd3f95a4255ea820f2bffcb3e27ba19
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615213"
---
# <a name="names-of-namespaces"></a>네임스페이스의 이름
으로 다른 명명 지침을 사용 하 여 목표 네임 스페이스의 이름을 지정할 때 만드는 것 충분 한 명확성 프레임 워크를 사용 하 여 즉시 무엇이 있는지 아는 네임 스페이스의 내용을 짧을 수 프로그래머입니다. 다음 템플릿 네임 스페이스 이름에 대 한 일반 규칙을 지정 합니다.  
  
 `<Company>.(<Product>|<Technology>)[.<Feature>][.<Subnamespace>]`  
  
 다음은 예제입니다.  
  
 `Fabrikam.Math`  
 `Litware.Security`  
  
 **✓ DO** 이름이 같은 다른 회사의 네임 스페이스를 방지 하기 위해 회사 이름이 있는 네임 스페이스 이름 접두사를 사용 합니다.  
  
 **✓ DO** 네임 스페이스 이름의 두 번째 수준에서 안정적이 고 버전에 관계 없이 제품 이름을 사용 합니다.  
  
 **X DO NOT** 사용 하 여 조직 계층의 기준으로 네임 스페이스 계층의 이름에 대 한 기업의 그룹 이름은 일시적인 경우가 있기 때문입니다. 그룹 관련된 기술에 대 한 네임 스페이스의 계층 구조를 구성 합니다.  
  
 **✓ DO** 기간이 PascalCasing, 및 별도 네임 스페이스 구성 요소를 사용 하 여 (예: `Microsoft.Office.PowerPoint`). 브랜드에서 않던 대/소문자를 사용 하는 경우 규칙 대/소문자 기본 네임 스페이스에서에서 파생 하는 경우에 사용자 브랜드에 정의 된 대/소문자를 따라야 합니다.  
  
 **✓ CONSIDER** 적절 한 복수형 네임 스페이스 이름을 사용 합니다.  
  
 예를 들어 `System.Collection` 대신 `System.Collections`을 사용합니다. 하지만 브랜드 이름 및 머리글자어가이 규칙에 대 한 예외를 됩니다. 예를 들어 `System.IOs` 대신 `System.IO`을 사용합니다.  
  
 **X DO NOT** 해당 네임 스페이스에서 네임 스페이스 및 형식에 대 한 동일한 이름을 사용 합니다.  
  
 예를 들어, 사용 하지 마십시오 `Debug` 네임 스페이스와 이름을 지정 하 고 다음 라는 클래스도 제공 `Debug` 동일한 네임 스페이스입니다. 여러 컴파일러에서는 해당 형식을 정규화 되어야 합니다.  
  
### <a name="namespaces-and-type-name-conflicts"></a>네임 스페이스 및 형식 이름 충돌  
 **X DO NOT** 와 같은 제네릭 형식 이름을 소개 `Element`, `Node`, `Log`, 및 `Message`합니다.  
  
 이렇게 이름을 입력으로 이어질 시나리오의 일반적인 충돌 가능성이 매우 높은 경우 제네릭 형식 이름을 정규화 해야 있습니다 (`FormElement`, `XmlNode`를 `EventLog`, `SoapMessage`).  
  
 네임 스페이스의 다른 범주에 대 한 형식 이름 충돌을 방지 하는 것에 대 한 지침이 있습니다.  
  
- **응용 프로그램 모델 네임 스페이스**  
  
     단일 응용 프로그램 모델에 속한 네임 스페이스는 종종 매우 함께 사용 하지만 다른 응용 프로그램 모델의 네임 스페이스를 사용 하 여 사용할 거의 없습니다. 예를 들어 합니다 <xref:System.Windows.Forms?displayProperty=nameWithType> 네임 스페이스와 함께 사용 되는 거의 <xref:System.Web.UI?displayProperty=nameWithType> 네임 스페이스입니다. 다음은 잘 알려진 응용 프로그램 모델 네임 스페이스 그룹 목록입니다.  
  
     `System.Windows*`   
     `System.Web.UI*`  
  
     **X DO NOT** 단일 응용 프로그램 모델 내에서는 네임 스페이스의 형식에 같은 이름을 지정 합니다.  
  
     예를 들어 이라는 형식을 추가 하지 마십시오 `Page` 에 <xref:System.Web.UI.Adapters?displayProperty=nameWithType> 네임 스페이스 때문에 <xref:System.Web.UI?displayProperty=nameWithType> 네임 스페이스에는 이미 명명 된 형식이 포함 되어 `Page`입니다.  
  
- **인프라 네임 스페이스**  
  
     이 그룹에 일반적인 응용 프로그램을 개발 하는 동안 거의 가져온 네임 스페이스를 포함 합니다. 예를 들어 `.Design` 네임 스페이스는 프로그래밍 개발 도구 때 주로 사용 됩니다. 이러한 네임 스페이스의 형식을 사용 하 여 충돌을 방지 합니다. 중요 하지 않습니다.  
  
- **핵심 네임 스페이스**  
  
     모든 핵심 네임 스페이스 포함 `System` 네임 스페이스를 응용 프로그램 모델 및 인프라 네임 스페이스를 제외 합니다. 특히, 핵심 네임 스페이스를 포함 `System`, `System.IO`를 `System.Xml`, 및 `System.Net`합니다.  
  
     **X DO NOT** 제공 핵심 네임 스페이스에서 종류와 충돌 하는 이름을 입력 합니다.  
  
     예를 들어, 사용 하지 마십시오 `Stream` 형식 이름으로 합니다. 충돌 <xref:System.IO.Stream?displayProperty=nameWithType>, 매우 일반적으로 형식을 사용 합니다.  
  
- **기술 네임 스페이스 그룹**  
  
     이 범주에 동일한 처음 두 개의 네임 스페이스 노드를 사용 하 여 모든 네임 스페이스를 포함 `(<Company>.<Technology>*`), 같은 `Microsoft.Build.Utilities` 및 `Microsoft.Build.Tasks`합니다. 것이 단일 기술을에 속하는 형식에 서로 충돌 하지 않는지 중요 합니다.  
  
     **X DO NOT** 단일 기술에서 다른 종류와 충돌 하는 형식 이름을 할당 합니다.  
  
     **X DO NOT** (없는 경우 기술 응용 프로그램 모델에 사용할 수 없습니다) 기술 네임 스페이스의 형식 및 응용 프로그램 모델 네임 스페이스는 간의 유형 이름 충돌을 소개 합니다.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [명명 지침](../../../docs/standard/design-guidelines/naming-guidelines.md)
