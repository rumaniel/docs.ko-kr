---
title: 레코드 길이가 잘못되었습니다.
ms.date: 07/20/2015
f1_keywords:
- vbrID59
ms.assetid: 0926a3a4-177b-4452-9b33-d8a01e24cc21
ms.openlocfilehash: 7ec0a8c27f425ec717bca5d45d5dfd2b601c11d5
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665729"
---
# <a name="bad-record-length"></a>레코드 길이가 잘못되었습니다.
이 오류의 가능한 원인:  
  
- 에 지정 된 레코드 변수의 길이 `FileGet`, `FileGetObject`, `FilePut` 또는 `FilePutObject` 문은 해당에 지정 된 길이에서 다른 `FileOpen` 문.  
  
- 변수를 `FilePut` 또는 `FilePutObject` 문이 하거나 가변 길이 문자열을 포함 합니다.  
  
- 변수를 `FilePut` 또는 `FilePutObject` 되거나 포함 하는 `Variant` 형식입니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
1. 값에서 설명한 것 처럼 레코드 변수의 형식을 정의 하는 사용자 정의 형식에서 고정 길이 변수의 크기의 합이 동일한 지 확인 합니다 `FileOpen` 문의 `Len` 절.  
  
2. 경우에서 변수를 `FilePut` 또는 `FilePutObject` 문 또는 가변 길이 문자열을 포함에 가변 길이 문자열에 지정 된 레코드 길이 보다 짧은 2 개 이상의 문자 인지 확인 합니다 `Len` 절을 `FileOpen` 문입니다.  
  
3. 경우에서 변수를 `FilePut` 또는 `FilePutObject` 되거나 포함 하는 `Variant` 가변 길이 문자열에 지정 된 레코드 길이 보다 짧으면 4 바이트 이상 인지 확인 합니다 `Len` 절은 `FileOpen` 문을.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.FileSystem.FileGet%2A>
- <xref:Microsoft.VisualBasic.FileSystem.FileGetObject%2A>
- <xref:Microsoft.VisualBasic.FileSystem.FilePut%2A>
- <xref:Microsoft.VisualBasic.FileSystem.FilePutObject%2A>
