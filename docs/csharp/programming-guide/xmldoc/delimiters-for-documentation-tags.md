---
title: 문서 태그에 대한 구분 기호 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- XML [C#], delimiters
- /** */ delimiters for C# documentation tags
- /// delimiter for C# documentation
ms.assetid: 9b2bdd18-4f5c-4c0b-988e-fb992e0d233e
ms.openlocfilehash: c8d20284b7ef2e06fb987f94f05cbe1dde1dc431
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69928075"
---
# <a name="delimiters-for-documentation-tags-c-programming-guide"></a>문서 태그에 대한 구분 기호(C# 프로그래밍 가이드)
XML 문서 주석을 사용하려면 문서 주석이 시작되고 끝나는 위치를 컴파일러에 알리는 구분 기호가 필요합니다. XML 문서 태그에 다음과 같은 종류의 구분 기호를 사용할 수 있습니다.  
  
 `///`  
 한 줄 구분 기호입니다. 문서 예제에 표시되고 Visual C# 프로젝트 템플릿에 사용되는 형식입니다. 구분 기호 뒤에 공백 문자가 있으면 해당 문자는 XML 출력에 포함되지 않습니다.  
  
> [!NOTE]
> Visual Studio IDE에는 코드 편집기에서 `///` 구분 기호를 입력한 후 \<summary> 및 \</summary> 태그를 자동으로 삽입하고 이러한 태그 내에서 커서를 이동하는 스마트 주석 편집이라는 기능이 있습니다. 이 기능은 [옵션 대화 상자](/visualstudio/ide/reference/options-text-editor-csharp-advanced)에서 켜거나 끌 수 있습니다.  
  
 `/** */`  
 여러 줄 구분 기호입니다.  
  
 `/** */` 구분 기호를 사용할 때 따라야 하는 몇 가지 서식 설정 규칙이 있습니다.  
  
- `/**` 구분 기호가 포함된 줄에서 줄의 나머지 부분이 공백인 경우 해당 줄은 주석에 대해 처리되지 않습니다. `/**` 구분 기호 다음의 첫 번째 문자가 공백인 경우 해당 공백 문자는 무시되고 줄의 나머지 부분이 처리됩니다. 그러지 않으면 `/**` 구분 기호 다음 줄의 전체 텍스트가 주석의 일부로 처리됩니다.  
  
- `*/` 구분 기호가 포함된 줄에서 `*/` 구분 기호까지 공백만 있으면 해당 줄은 무시됩니다. 그러지 않으면 줄의 텍스트가 `*/` 구분 기호까지 주석의 일부로 처리되며, 다음 글머리 기호에서 설명하는 패턴 일치 규칙을 따릅니다.  
  
- `/**` 구분 기호로 시작하는 줄 다음 줄에 대해 컴파일러는 각 줄의 시작 부분에서 일반적인 패턴을 찾습니다. 패턴은 선택적 공백과 별표(`*`)로 구성되고 그다음에 더 많은 선택적 공백이 올 수 있습니다. 컴파일러가 `/**` 구분 기호나 `*/` 구분 기호로 시작되지 않는 각 줄의 시작 부분에서 일반적인 패턴을 찾으면 각 줄에 대해 해당 패턴을 무시합니다.  
  
 다음 예제에서는 이러한 규칙을 보여 줍니다.  
  
- 다음 주석에서 유일하게 처리되는 부분은 `<summary>`로 시작하는 줄입니다. 세 가지 태그 서식이 동일한 주석을 생성합니다.  
  
    ```csharp  
    /** <summary>text</summary> */   
  
    /**   
    <summary>text</summary>   
    */   
  
    /**   
     * <summary>text</summary>   
    */  
    ```  
  
- 컴파일러는 두 번째 및 세 번째 줄의 시작 부분에서 " * "의 일반적인 패턴을 식별합니다. 이 패턴은 출력에 포함되지 않습니다.  
  
    ```csharp  
    /**   
     * <summary>   
     * text </summary>*/   
    ```  
  
- 다음 주석에서는 세 번째 줄의 두 번째 문자가 별표가 아니기 때문에 컴파일러가 일반적인 패턴을 찾을 수 없습니다. 따라서 두 번째 및 세 번째 줄의 모든 텍스트가 주석의 일부로 처리됩니다.  
  
    ```csharp  
    /**   
     * <summary>   
       text </summary>  
    */   
    ```  
  
- 다음 주석에서는 두 가지로 이유로 컴파일러가 패턴을 찾을 수 없습니다. 첫째, 별표 앞의 공백 수가 일치하지 않습니다. 둘째, 다섯 번째 줄이 공백과 일치하지 않는 탭으로 시작합니다. 따라서 두 번째 줄부터 다섯 번째 줄까지 모든 텍스트가 주석의 일부로 처리됩니다.  
  
    ```csharp  
    /**   
      * <summary>   
      * text   
     *  text2   
        *  </summary>   
    */   
    ```  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [XML 문서 주석](./index.md)
- [/doc(C# 컴파일러 옵션)](../../language-reference/compiler-options/doc-compiler-option.md)
- [XML 문서 주석](./index.md)
