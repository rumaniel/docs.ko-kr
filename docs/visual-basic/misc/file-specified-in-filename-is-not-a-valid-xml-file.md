---
title: FileName에 지정된 파일은 유효한 XML 파일이 아닙니다.
ms.date: 07/20/2015
ms.assetid: c4c30bf3-e0ad-4bc8-89e0-2c3e49e9793b
ms.openlocfilehash: 5a54e5e7e7c75bb7d766b1bbda10f401fa8b99af
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65640846"
---
# <a name="file-specified-in-filename-is-not-a-valid-xml-file"></a>FileName에 지정된 파일은 유효한 XML 파일이 아닙니다.

제공한 파일 이름이 유효한 XML 파일이 아닙니다. XML 문서의 허용된 구조와 내용을 지정하려면 DTD(문서 종류 정의), Microsoft XDR(XML-Data Reduced) 스키마 또는 XSD(XML 스키마 정의 언어) 스키마를 사용하면 됩니다. XSD 스키마는.NET Framework에서 XML 문법을 지정 하는 기본 방법입니다.

> [!NOTE]
> 일부 이전 버전의 Visual Studio에서 **XML 디자이너**는 입력된 데이터 세트 및 XML 스키마용 디자이너입니다. **XML 디자이너** 는 XML 스키마 파일을 만들고 편집하는 데 계속 사용할 수 있습니다. 그러나 Visual Studio 2012에서는 만들고 형식화 된 데이터 집합 편집을 합니다 **데이터 집합 디자이너**합니다. 자세한 내용은 [만들기 및 형식화 된 데이터 집합 편집](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/314t4see(v=vs.120))합니다.

## <a name="to-correct-this-error"></a>이 오류를 해결하려면

- 올바른 파일 이름을 제공했는지 확인합니다.

- 확인하려는 XML 파일을 **XML 디자이너**로 로드하여 지정된 파일에 유효한 XML 파일이 포함되어 있는지 확인합니다. **XML** 메뉴에서 **XML 유효성 검사**를 클릭합니다. **작업 목록**에 오류가 표시됩니다.

- XML 파일에 연결된 XML 스키마가 있는 경우 요소가 정의된 구조에 표시되고 개별 요소의 콘텐츠가 스키마에서 지정된 선언된 데이터 형식에 맞는지 확인합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Xml>
- [방법: 파일 경로의 구문 분석](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
