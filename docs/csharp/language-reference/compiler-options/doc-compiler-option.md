---
title: /doc(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- FileProperties.BuildAction
- /doc
helpviewer_keywords:
- comments, C# code
- XML documentation [C#], comments in source files
- doc compiler option [C#]
- Visual C#, XML documentation for
- -doc compiler option [C#]
- /doc compiler option [C#]
ms.assetid: 849eea59-c936-4311-bad8-d07404480f2a
ms.openlocfilehash: 21605b30867d7be0b906b431253c183e655bea82
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922478"
---
# <a name="-doc-c-compiler-options"></a>/doc(C# 컴파일러 옵션)
**-doc** 옵션을 사용하면 XML 파일에 문서 주석을 삽입할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-doc:file  
```  
  
## <a name="arguments"></a>인수  
 `file`  
 XML에 대한 출력 파일로, 컴파일의 소스 코드 파일에 있는 주석으로 채워집니다.  
  
## <a name="remarks"></a>설명  
 소스 코드 파일에서 다음 항목 앞에 나오는 문서 주석을 처리하여 XML 파일에 추가할 수 있습니다.  
  
- [class](../keywords/class.md), [delegate](../keywords/delegate.md) 또는 [interface](../keywords/interface.md) 같은 사용자 정의 형식  
  
- 필드, [이벤트](../keywords/event.md), [속성](../../programming-guide/classes-and-structs/using-properties.md) 또는 메서드 같은 멤버  
  
 Main을 포함하는 소스 코드 파일이 먼저 XML로 출력됩니다.  
  
 [IntelliSense](/visualstudio/ide/using-intellisense) 기능에서 사용하기 위해 생성된 .xml 파일을 사용하려면 .xml 파일의 이름을 지원하려는 어셈블리와 동일하게 지정한 다음 .xml 파일이 어셈블리와 동일한 디렉터리에 있도록 해야 합니다. 따라서 어셈블리가 Visual Studio 프로젝트에서 참조되면 .xml 파일도 검색됩니다. 자세한 내용은 [코드 주석 제공](/visualstudio/ide/supplying-xml-code-comments)을 참조하세요.  
  
 [-target:module](./target-module-compiler-option.md)을 사용하여 컴파일하지 않으면 컴파일의 출력 파일에 대한 어셈블리 매니페스트를 포함하는 파일의 이름을 지정하는 \<assembly>\</assembly> 태그가 `file`에 포함됩니다.  
  
> [!NOTE]
> -doc 옵션은 모든 입력 파일에 적용됩니다. 또는 Progect Settings에서 설정한 경우 프로젝트의 모든 파일에 적용됩니다. 특정 파일 또는 코드 섹션에 대한 문서 주석 관련 경고를 사용하지 않으려면 [#pragma warning](../preprocessor-directives/preprocessor-pragma-warning.md)을 사용하세요.  
  
 코드의 주석에서 문서를 생성하는 방법은 [문서 주석에 대한 권장 태그](../../programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)를 참조하세요.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트 **속성** 페이지를 엽니다.  
  
2. **빌드** 탭을 클릭합니다.  
  
3. **XML 문서 파일** 속성을 수정합니다.  
  
 이 컴파일러 옵션을 프로그래밍 방식으로 설정하는 방법에 대한 자세한 내용은 <xref:VSLangProj80.CSharpProjectConfigurationProperties3.DocumentationFile%2A>을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
