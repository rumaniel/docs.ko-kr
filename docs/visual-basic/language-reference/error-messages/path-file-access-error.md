---
title: 경로-파일 액세스 오류입니다.
ms.date: 07/20/2015
f1_keywords:
- vbrID75
ms.assetid: 6ce3a161-7316-46bd-a785-0d50e5414020
ms.openlocfilehash: 4f18c9216aa24840bc205534a97124d12698cb98
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61799182"
---
# <a name="pathfile-access-error"></a>경로/파일 액세스 오류입니다.
파일 액세스 또는 디스크 액세스 작업을 하는 동안 운영 체제 경로 파일 이름 간에 연결을 만들 수 없습니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 파일 사양을 올바르게 형식이 있는지 확인 합니다. 정규화 된 (절대) 또는 상대 파일 이름을 포함할 수 있습니다 경로입니다. (다른 드라이브의 경로 이면) 드라이브 이름으로 시작 되는 정규화 된 경로 및 파일에 루트에서 명시적인 경로 나열 합니다. 정규화 되지 않은 모든 경로 현재 드라이브 및 디렉터리에 상대적입니다.  
  
2. 기존 읽기 전용 파일을 대체 하는 파일을 저장 하려고 시도 하지 않았습니다 있는지 확인 합니다. 이 경우 대상 파일의 읽기 전용 특성을 변경 하거나 다른 파일 이름을 사용 하 여 파일을 저장 합니다.  
  
3. 순차적 읽기 전용 파일을 열려고 시도 하지 않은 했는지 `Output` 또는 `Append` 모드입니다. 이 경우에서 파일을 열고 `Input` 모드 또는 파일의 읽기 전용 특성을 변경 합니다.  
  
4. 데이터베이스 또는 문서 내에서 Visual Basic 프로젝트를 변경 하지 않은 있는지 확인 합니다.  
  
## <a name="see-also"></a>참고자료

- [오류 형식](../../../visual-basic/programming-guide/language-features/error-types.md)
