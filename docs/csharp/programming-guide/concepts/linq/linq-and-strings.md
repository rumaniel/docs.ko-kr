---
title: LINQ 및 문자열(C#)
ms.date: 07/20/2015
ms.assetid: dbe2d657-b3f3-487e-b645-21fb2d71cd7b
ms.openlocfilehash: c7a1b86cc611d5f38ceab814b4594f5ad953fbc4
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54744624"
---
# <a name="linq-and-strings-c"></a>LINQ 및 문자열(C#)

LINQ를 사용하여 문자열 및 문자열 컬렉션을 쿼리하고 변환할 수 있습니다. 텍스트 파일의 반구조적 데이터에 특히 유용할 수 있습니다. LINQ 쿼리에 기존의 문자열 함수 및 정규식을 결합할 수 있습니다. 예를 들어 <xref:System.String.Split%2A?displayProperty=nameWithType> 또는 <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> 메서드를 사용하여 문자열 배열을 만든 다음 LINQ를 사용하여 쿼리하거나 수정할 수 있습니다. LINQ 쿼리의 `where` 절에 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A?displayProperty=nameWithType> 메서드를 사용할 수 있습니다. 또한 LINQ를 사용하여 정규식에서 반환된 <xref:System.Text.RegularExpressions.MatchCollection> 결과를 쿼리하거나 수정할 수 있습니다.

이 섹션에 설명된 기법을 사용하여 반구조적 텍스트 데이터를 XML로 변환할 수도 있습니다. 자세한 내용은 [방법: CSV 파일에서 XML 생성(C#)](how-to-generate-xml-from-csv-files.md)을 참조하세요.

이 섹션의 예제는 다음 두 가지 범주로 구분됩니다.

## <a name="querying-a-block-of-text"></a>텍스트 블록 쿼리

<xref:System.String.Split%2A?displayProperty=nameWithType> 메서드 또는 <xref:System.Text.RegularExpressions.Regex.Split%2A?displayProperty=nameWithType> 메서드를 사용하여 더 작은 문자열의 쿼리 가능 배열로 분할하면 텍스트 블록을 쿼리, 분석, 수정할 수 있습니다. 소스 텍스트를 단어, 문장, 단락, 페이지 또는 기타 기준으로 분할한 다음 쿼리에 필요한 경우 추가 분할을 수행할 수 있습니다.

- [방법: 문자열에서 단어가 나오는 횟수 세기(LINQ)(C#)](how-to-count-occurrences-of-a-word-in-a-string-linq.md)  
  간단한 텍스트 쿼리를 위해 LINQ를 사용하는 방법을 보여 줍니다.

- [방법: 지정된 단어 집합이 들어 있는 문장 쿼리(LINQ)(C#)](how-to-query-for-sentences-that-contain-a-specified-set-of-words-linq.md)

  임의의 경계에서 텍스트 파일을 분할하는 방법 및 각 부분에 대해 쿼리를 수행하는 방법을 보여 줍니다.

- [방법: 문자열의 문자 쿼리(LINQ)(C#)](how-to-query-for-characters-in-a-string-linq.md)

  문자열이 쿼리 가능한 형식인지를 보여 줍니다.

- [방법: LINQ 쿼리와 정규식 결합(C#)](how-to-combine-linq-queries-with-regular-expressions.md)

  필터링된 쿼리 결과에 대한 복잡한 패턴 일치를 위해 LINQ 쿼리에서 정규식을 사용하는 방법을 보여 줍니다.

## <a name="querying-semi-structured-data-in-text-format"></a>텍스트 형식의 반구조적 데이터 쿼리

다양한 형식의 텍스트 파일은 대체로 탭 또는 쉼표로 구분된 파일 또는 고정 길이 줄과 같은 유사한 형식을 가진 일련의 줄로 이루어져 있습니다. 이러한 텍스트 파일을 메모리로 읽어온 후 LINQ를 사용하여 줄을 쿼리 및/또는 수정할 수 있습니다. 또한 LINQ 쿼리는 여러 소스의 데이터를 결합하는 작업을 간소화합니다.

- [방법: 두 목록 간의 차집합 구하기(LINQ)(C#)](how-to-find-the-set-difference-between-two-lists-linq.md)

  한 목록에는 있지만 다른 목록에는 없는 모든 문자열을 찾는 방법을 보여 줍니다.

- [방법: 단어 또는 필드에 따라 텍스트 데이터 정렬 또는 필터링(LINQ)(C#)](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)

  단어 또는 필드에 따라 텍스트 줄을 정렬하는 방법을 보여 줍니다.

- [방법: 구분된 파일의 필드 다시 정렬(LINQ)(C#)](how-to-reorder-the-fields-of-a-delimited-file-linq.md)

  .csv 파일에서 줄의 필드 순서를 변경하는 방법을 보여 줍니다.

- [방법: 문자열 컬렉션 결합 및 비교(LINQ)(C#)](how-to-combine-and-compare-string-collections-linq.md)

  다양한 방법으로 문자열 목록을 조합하는 방법을 보여 줍니다.

- [방법: 여러 소스로 개체 컬렉션 채우기(LINQ)(C#)](how-to-populate-object-collections-from-multiple-sources-linq.md)

  여러 텍스트 파일을 데이터 소스로 사용하여 개체 컬렉션을 만드는 방법을 보여 줍니다.

- [방법: 서로 다른 파일의 콘텐츠 조인(LINQ)(C#)](how-to-join-content-from-dissimilar-files-linq.md)
  
  일치하는 키를 사용하여 두 목록의 문자열을 단일 문자열로 결합하는 방법을 보여 줍니다.

- [방법: 그룹을 사용하여 파일을 여러 파일로 분할(LINQ)(C#)](how-to-split-a-file-into-many-files-by-using-groups-linq.md)
  
  단일 파일을 데이터 소스로 사용하여 새 파일을 만드는 방법을 보여 줍니다.

- [방법: CSV 텍스트 파일의 열 값 컴퓨팅(LINQ)(C#)](how-to-compute-column-values-in-a-csv-text-file-linq.md)
  
  .csv 파일의 텍스트 데이터에 대해 수학적 계산을 수행하는 방법을 보여 줍니다.

## <a name="see-also"></a>참고 항목

- [LINQ(Language-Integrated Query)(C#)](index.md)
- [방법: CSV 파일에서 XML 생성](how-to-generate-xml-from-csv-files.md)
