---
title: -delaysign
ms.date: 03/10/2018
helpviewer_keywords:
- delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
ms.assetid: c76e61a4-1884-4252-9fb2-377f99caa690
ms.openlocfilehash: 66edc45c622b78187469ccc0631beb53b68049b0
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002304"
---
# <a name="-delaysign"></a>-delaysign
어셈블리를 완전히 서명할지, 아니면 부분적으로 서명할지를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-delaysign[+ | -]  
```  
  
## <a name="arguments"></a>인수  
 `+` &#124; `-`  
 (선택 사항) 어셈블리에 완전히 서명하려면 `-delaysign-`를 사용하고 어셈블리에 공개 키를 추가 하 고 서명 된 해시의 공간을 예약 하려면 `-delaysign+`을 사용 합니다. 기본값은 `-delaysign-`입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 옵션은 [-keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md) 또는 [-keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)와 함께 사용 하는 경우에만 적용 됩니다.  
  
 완전히 서명된 어셈블리를 요청할 경우 컴파일러는 매니페스트(어셈블리 메타데이터)가 포함된 파일을 해시하고 프라이빗 키로 해당 해시에 서명합니다. 결과로 생성되는 디지털 서명은 매니페스트가 포함된 파일에 저장됩니다. 어셈블리의 서명이 연기 된 경우 컴파일러는 서명을 계산 및 저장 하지 않고 나중에 서명을 추가할 수 있도록 파일에 공간을 예약 합니다.  
  
 예를 들어 `-delaysign+`을 사용 하 여 조직의 개발자는 테스터가 전역 어셈블리 캐시에 등록 하 고 사용할 수 있는 어셈블리의 서명 되지 않은 테스트 버전을 배포할 수 있습니다. 어셈블리에 대 한 작업이 완료 되 면 조직의 개인 키를 담당 하는 사람이 어셈블리에 완전히 서명할 수 있습니다. 이 compartmentalization는 조직의 개인 키를 공개 하지 않도록 보호 하는 동시에 모든 개발자가 어셈블리를 사용할 수 있도록 합니다.  
  
 어셈블리 서명에 대 한 자세한 내용은 [강력한 이름의 어셈블리 만들기 및 사용](../../../standard/assembly/create-use-strong-named.md) 을 참조 하세요.  
  
### <a name="to-set--delaysign-in-the-visual-studio-integrated-development-environment"></a>Visual Studio 통합 개발 환경에서 delaysign로 설정  
  
1. **솔루션 탐색기**에서 프로젝트를 선택합니다. **프로젝트** 메뉴에서 **속성**을 클릭합니다.   
  
2. **서명** 탭을 클릭합니다.  
  
3. **서명 연기** 상자에서 값을 설정 합니다.  
  
## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [-keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)
- [-keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
