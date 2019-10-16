---
title: -checked(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /checked
helpviewer_keywords:
- checked compiler option [C#]
- -checked compiler option [C#]
- /checked compiler option [C#]
ms.assetid: fb7475d3-e6a6-4e6d-b86c-69e7a74c854b
ms.openlocfilehash: 4e07698e7abdad00983b61412fa2a57e651d4d46
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606991"
---
# <a name="-checked-c-compiler-options"></a>-checked(C# 컴파일러 옵션)
**-checked** 옵션은 데이터 형식 범위를 벗어나고 [checked](../keywords/checked.md) 또는 [unchecked](../keywords/unchecked.md) 키워드의 범위 내에 없는 값을 생성하는 정수 산술 문이 런타임 예외를 일으킬지 여부를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-checked[+ | -]  
```  
  
## <a name="remarks"></a>설명  
 `checked` 또는 `unchecked` 키워드의 범위 내에 있는 정수 산술 문에는 **-checked** 옵션이 영향을 미치지 않습니다.  
  
 `checked` 또는 `unchecked` 키워드의 범위에 없는 정수 산술 문이 데이터 형식 범위를 벗어난 값을 생성하고 **-checked+** (또는 **-checked**)가 컴파일에서 사용될 경우 해당 명령문은 런타임에 예외를 일으킵니다. **-checked-** 가 컴파일에 사용될 경우 해당 문은 런타임에 예외를 일으키지 않습니다.  
  
 이 옵션의 기본값은 **-checked-** 이며, 오버플로 검사는 해제되어 있습니다.
 
 경우에 따라 대형 애플리케이션을 빌드하는 데 사용되는 자동화된 도구가 +로 -checked를 설정합니다. -checked-를 사용하는 하나의 시나리오는 -checked-를 지정하여 도구의 글로벌 기본값을 재정의하는 것입니다.
 
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트 **속성** 페이지를 엽니다. 자세한 내용은 [프로젝트 디자이너, 빌드 페이지(C#)](/visualstudio/ide/reference/build-page-project-designer-csharp)를 참조하세요.  
  
2. **빌드** 속성 페이지를 클릭합니다.  
  
3. **고급** 단추를 클릭합니다.  
  
4. **산술 연산 오버플로/언더플로 확인** 속성을 수정합니다.  
  
 프로그래밍 방식으로 이 컴파일러 옵션에 액세스하려면 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.CheckForOverflowUnderflow%2A>를 참조하세요.  
  
## <a name="example"></a>예  
 다음 명령은 `t2.cs`를 컴파일합니다. 명령에서 `-checked`를 사용하면 `checked` 또는 `unchecked` 키워드의 범위에 없고 데이터 형식 범위를 벗어난 값을 생성하는 파일의 정수 산술 문이 런타임에 예외를 일으키도록 지정합니다.  
  
```console  
csc t2.cs -checked  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
