---
title: -warn(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /warn
helpviewer_keywords:
- warning level [C#]
- /w compiler option [C#]
- -w compiler option [C#]
- -warn compiler option [C#]
- /warn compiler option [C#]
- w compiler option [C#]
- warn compiler option [C#]
ms.assetid: 5f80ff59-4991-4382-9f9a-77da18446e71
ms.openlocfilehash: 5b05e944a37e16fc1fcc422271be00c09a271a33
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69602397"
---
# <a name="-warn-c-compiler-options"></a>-warn(C# 컴파일러 옵션)
**-warn** 옵션은 컴파일러에서 표시할 경고 수준을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-warn:option  
```  
  
## <a name="arguments"></a>인수  
 `option`  
 컴파일에 표시할 경고 수준: 숫자가 낮을수록 높은 심각도 경고만 표시되고 숫자가 높을수록 많은 경고가 표시됩니다. 유효한 값은 0-4입니다.  
  
|경고 수준|의미|  
|-------------------|-------------|  
|0|모든 경고 메시지 내보내기를 끕니다.|  
|1|심각한 경고 메시지를 표시합니다.|  
|2|수준 1 경고와 덜 심각한 특정 경고(예: 클래스 멤버 숨기기에 대한 경고)를 표시합니다.|  
|3|수준 2 경고와 덜 심각한 특정 경고(예: 항상 `true` 또는 `false`로 평가되는 식에 대한 경고)를 표시합니다.|  
|4(기본값)|모든 수준 3 경고와 정보 경고를 표시합니다.|  
  
## <a name="remarks"></a>설명  
 오류 또는 경고에 대한 정보를 가져오려면 도움말 색인에서 오류 코드를 조회할 수 있습니다. 오류 또는 경고에 대한 정보를 가져오는 다른 방법은 [C# 컴파일러 오류](../compiler-messages/index.md)를 참조하세요.  
  
 모든 경고를 오류로 처리하려면 [-warnaserror](./warnaserror-compiler-option.md)를 사용합니다. 특정 경고를 사용하지 않으려면 [-nowarn](./nowarn-compiler-option.md)을 사용합니다.  
  
 **-w**는 **-warn**의 약식 형태입니다.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트 **속성** 페이지를 엽니다.  
  
2. **빌드** 속성 페이지를 클릭합니다.  
  
3. **경고 수준** 속성을 수정합니다.  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.WarningLevel%2A>을 참조하세요.  
  
## <a name="example"></a>예  
 `in.cs`를 컴파일하고 컴파일러에서 수준 1 경고만 표시하도록 합니다.  
  
```console  
csc -warn:1 in.cs  
```  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
