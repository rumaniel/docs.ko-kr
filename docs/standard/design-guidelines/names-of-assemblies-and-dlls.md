---
title: 어셈블리 및 DLL의 이름
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- names [.NET Framework], DLLs
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
- DLLs, names
ms.assetid: e800b610-31b4-4949-9c14-cb60e9f254be
author: KrzysztofCwalina
ms.openlocfilehash: 1aeef9e1be6e5fe747f440a8cb7f21095cb22f49
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945498"
---
# <a name="names-of-assemblies-and-dlls"></a>어셈블리 및 DLL의 이름
어셈블리는 단위 배포 및 관리 코드 프로그램에 대 한 id입니다. 어셈블리는 하나 이상의 파일에 걸쳐 수 있지만 일반적으로 어셈블리 일대일로 매핑되는 DLL입니다. 따라서 다음 어셈블리 명명 규칙에 매핑할 수 있는 유일한 DLL 명명 규칙을 설명이 합니다.  
  
 **✓ DO** 대량의 System.Data 등의 기능을 제안 하는 Dll 어셈블리의 이름을 선택 합니다.  
  
 어셈블리 및 DLL 이름을 네임 스페이스 이름에 해당 없지만 어셈블리 이름을 지정할 때 네임 스페이스의 이름을 따르는 것입니다. 경험에의 하면 어셈블리에 포함 된 네임 스페이스의 공통 접두사를 기준으로 DLL 이름을 지정 하는 것입니다. 예를 들어 두 개의 네임 스페이스를 사용 하 여 어셈블리 `MyCompany.MyTechnology.FirstFeature` 하 고 `MyCompany.MyTechnology.SecondFeature`를 호출할 수 `MyCompany.MyTechnology.dll`입니다.  
  
 **✓ CONSIDER** 다음 패턴에 따라 Dll 이름 지정:  
  
 `<Company>.<Component>.dll`  
  
 여기서 `<Component>` -점으로 구분 된 하나 이상의 절을 포함 합니다. 예를 들어:  
  
 `Litware.Controls.dll`.  
  
 *Portions © 2005, 2009 Microsoft Corporation. 모든 권리 보유.*  
  
 *사용 권한에서 교육, inc. 피어슨 재인쇄 [Framework 디자인 지침: 다시 사용할 수 있는.NET 라이브러리, 2nd Edition에 대 한 규칙, 관용구 패턴과](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina를 Brad Abrams Addison Wesley Professional에서 2008 년 10 월 22 일 Microsoft Windows 개발 시리즈의 일부로 게시 합니다.*  
  
## <a name="see-also"></a>참고자료

- [프레임워크 디자인 지침](../../../docs/standard/design-guidelines/index.md)
- [명명 지침](../../../docs/standard/design-guidelines/naming-guidelines.md)
