---
title: LINQ 및 파일 디렉터리(C#)
ms.date: 07/20/2015
ms.assetid: b66c55e4-0f72-44e5-b086-519f9962335c
ms.openlocfilehash: 1d2109fe7f4f907317275188057fa6e5e71b2679
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69591981"
---
# <a name="linq-and-file-directories-c"></a>LINQ 및 파일 디렉터리(C#)
많은 파일 시스템 작업은 기본적으로 쿼리이므로 LINQ 접근 방식에 적합합니다.  
  
 이 섹션에서 쿼리는 비파괴적입니다. 쿼리는 원본 파일이나 폴더의 내용을 변경하는 데 사용되지 않으며, 쿼리로 인해 의도하지 않은 결과가 발생하지 않아야 한다는 규칙을 따릅니다. 일반적으로 소스 데이터를 수정하는 모든 코드(만들기/업데이트/삭제 작업을 수행하는 쿼리 포함)는 데이터를 쿼리만하는 코드와 별도로 유지되어야 합니다.  
  
 이 단원에는 다음 항목이 포함되어 있습니다.  
  
 [방법: 지정된 특성 또는 이름을 갖는 파일 쿼리(C#)](./how-to-query-for-files-with-a-specified-attribute-or-name.md)  
 하나 이상의 <xref:System.IO.FileInfo> 개체 속성을 검사하여 파일을 검색하는 방법을 보여 줍니다.  
  
 [방법: 확장명에 따라 파일 그룹화(LINQ)(C#)](./how-to-group-files-by-extension-linq.md)  
 파일 이름 확장명에 따라 <xref:System.IO.FileInfo> 개체의 그룹을 반환하는 방법을 보여 줍니다.  
  
 [방법: 폴더 집합의 전체 바이트 수 쿼리(LINQ)(C#)](./how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders-linq.md)  
 지정된 디렉터리 트리에 있는 모든 파일에서 전체 바이트 수를 반환하는 방법을 보여 줍니다.  
  
 [방법: 두 폴더의 내용 비교(LINQ)(C#)](./how-to-compare-the-contents-of-two-folders-linq.md)  
 두 개의 지정된 폴더에 있는 모든 파일뿐만 아니라 특정 폴더에만 있는 모든 파일도 반환하는 방법을 보여 줍니다.  
  
 [방법: 디렉터리 트리에서 가장 큰 파일을 하나 이상 쿼리(LINQ)(C#)](./how-to-query-for-the-largest-file-or-files-in-a-directory-tree-linq.md)  
 디렉터리 트리에서 가장 크거나 가장 작은 파일 또는 지정한 파일 수를 반환하는 방법을 보여 줍니다.  
  
 [방법: 디렉터리 트리의 중복 파일 쿼리(LINQ)(C#)](./how-to-query-for-duplicate-files-in-a-directory-tree-linq.md)  
 지정된 디렉터리 트리에서 둘 이상의 위치에 나타나는 모든 파일 이름을 그룹화하는 방법을 보여 줍니다. 또한 사용자 지정 비교자에 따라 보다 복잡한 비교를 수행하는 방법을 보여 줍니다.  
  
 [방법: 폴더의 파일 내용 쿼리(LINQ)(C#)](./how-to-query-the-contents-of-files-in-a-folder-lin.md)  
 트리의 폴더를 반복하고, 각 파일을 열고, 파일의 내용을 쿼리하는 방법을 보여 줍니다.  
  
## <a name="comments"></a>설명  
 파일 시스템의 내용을 정확하게 나타내고 예외를 정상적으로 처리하는 데이터 소스 만들기와 관련하여 몇 가지 복잡한 부분이 있습니다. 이 섹션의 예제에서는 지정된 루트 폴더와 모든 하위 폴더에 있는 모든 파일을 나타내는 <xref:System.IO.FileInfo> 개체의 스냅샷 컬렉션을 만듭니다. 각 <xref:System.IO.FileInfo>의 실제 상태는 쿼리 실행을 시작하고 종료하는 시간 사이에 변경될 수 있습니다. 예를 들어 <xref:System.IO.FileInfo> 개체 목록을 만들어 데이터 소스로 사용할 수 있습니다. 쿼리에서 `Length` 속성에 액세스하려고 하면 <xref:System.IO.FileInfo> 개체에서 파일 시스템에 액세스하여 `Length`의 값을 업데이트합니다. 파일이 더 이상 존재하지 않는 경우 파일 시스템을 직접 쿼리하지 않아도 쿼리에서 <xref:System.IO.FileNotFoundException>을 가져옵니다. 이 섹션의 일부 쿼리는 특정한 경우에 이러한 특정 예외를 사용하는 별도의 메서드를 사용합니다. 또 다른 옵션은 <xref:System.IO.FileSystemWatcher>를 사용하여 데이터 소스가 동적으로 업데이트되도록 하는 것입니다.  
  
## <a name="see-also"></a>참고 항목

- [LINQ to Objects(C#)](./linq-to-objects.md)
