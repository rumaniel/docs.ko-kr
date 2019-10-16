---
title: 원본 Office Open XML 문서 만들기(C#)
ms.date: 07/20/2015
ms.assetid: 653c8cdb-73be-4dc2-927f-924cfb4ed9ed
ms.openlocfilehash: d6c4d8866bba58e86735099a62041894a9faa9b1
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70204158"
---
# <a name="creating-the-source-office-open-xml-document-c"></a>원본 Office Open XML 문서 만들기(C#)

이 항목에서는 이 자습서의 다른 예제에서 사용하는 Office Open XML WordprocessingML 문서를 만드는 방법을 보여 줍니다. 이러한 지침을 따르는 경우 출력은 각 예제에서 제공되는 출력과 일치합니다.

그러나 이 자습서의 예제는 모든 유효한 WordprocessingML 문서와 함께 작동합니다.

이 자습서에서 사용하는 문서를 만들려면 Microsoft Office 2007 이상이 설치되어 있거나 Word, Excel 및 PowerPoint 2007 파일 형식용 Microsoft Office 호환 기능 팩이 포함된 Microsoft Office 2003이 설치되어 있어야 합니다.

## <a name="creating-the-wordprocessingml-document"></a>WordprocessingML 문서 만들기

#### <a name="to-create-the-wordprocessingml-document"></a>WordprocessingML 문서를 만들려면

1. Microsoft Word 문서를 새로 만듭니다.

2. 다음 텍스트를 새 문서에 붙여 넣습니다.

    ```text
    Parsing WordprocessingML with LINQ to XML

    The following example prints to the console.

    using System;

    class Program {
        public static void Main(string[] args) {
            Console.WriteLine("Hello World");
        }
    }

    This example produces the following output:

    Hello World
    ```

3. "제목 1" 스타일로 첫 번째 줄의 서식을 지정합니다.

4. C# 코드가 포함된 줄을 선택합니다. 첫 번째 줄은 `using` 키워드로 시작합니다. 마지막 줄은 마지막 닫는 괄호입니다. courier 글꼴로 줄의 서식을 지정합니다. 새 스타일로 줄의 서식을 지정한 다음 새 스타일의 이름을 "Code"로 지정합니다.

5. 마지막으로 출력이 포함된 전체 줄을 선택하고 `Code` 스타일로 서식을 지정합니다.

6. 문서를 저장하고 SampleDoc.docx로 이름을 지정합니다.

    > [!NOTE]
    > Microsoft Word 2003을 사용하는 경우 **파일 형식** 드롭다운 목록에서 **Word 2007 문서**를 선택합니다.
