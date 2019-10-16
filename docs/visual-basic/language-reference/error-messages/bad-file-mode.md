---
title: 파일 모드가 잘못되었습니다.
ms.date: 07/20/2015
f1_keywords:
- vbrID54
ms.assetid: 74891e96-884b-4c8d-872d-cd11ae272372
ms.openlocfilehash: 9a59faf1b6f845858e36efcabdf0758e41ad75dc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64619740"
---
# <a name="bad-file-mode"></a>파일 모드가 잘못되었습니다.
파일 콘텐츠를 조작에 사용 된 문이 파일이 열린 모드에 적합 해야 합니다. 이 오류가 발생하는 원인은 다음과 같습니다.  
  
- A `FilePutObject` 또는 `FileGetObject` 문을 순차적 파일을 지정 합니다.  
  
- A `Print` 이외의 액세스 모드에 대 한 열린 파일을 지정 하는 문을 `Output` 또는 `Append`합니다.  
  
- `Input` 이외의 액세스 모드에 대 한 열린 파일을 지정 하는 문 `Input`  
  
- 읽기 전용 파일에 기록 하려고 했습니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 했는지 `FilePutObject` 하 고 `FileGetObject` 파일 열기에 대 한 참조만 `Random` 또는 `Binary` 액세스 합니다.  
  
- 했는지 `Print` 에 대 한 열린 파일을 지정 `Output` 또는 `Append` 액세스 모드입니다. 그렇지 않은 경우 다른 문을 사용 하 여 파일에서 데이터를 배치 하거나 적절 한 모드에서 파일을 다시 엽니다.  
  
- 했는지 `Input` 열린 파일을 지정 `Input`합니다. 그렇지 않은 경우 다른 문을 사용 하 여 데이터 파일에 배치 하거나 적절 한 모드에서 파일을 다시 엽니다.  
  
- 읽기 전용 파일에 작성 하는 경우 파일의 읽기/쓰기 상태를 변경 하거나 쓸 하려고 하지 마십시오.  
  
- `My.Computer.FileSystem` 개체에서 사용할 수 있는 기능을 사용합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.FileSystem>
- [문제 해결: 텍스트 파일 읽기 및 쓰기](../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)
