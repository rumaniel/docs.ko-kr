---
title: 파일이 너무 커서 바이트 배열로 읽어 들일 수 없습니다.
ms.date: 07/20/2015
ms.assetid: 686630a6-a439-46c7-8d7b-34613ae4c5d8
ms.openlocfilehash: a842205e9184355e4ea750ea2eb32e4bcf05a14d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665111"
---
# <a name="file-is-too-large-to-read-into-a-byte-array"></a>파일이 너무 커서 바이트 배열로 읽어 들일 수 없습니다.
바이트 배열로 읽어 들일 하려는 파일의 크기는 4GB를 초과 합니다. `My.Computer.FileSystem.ReadAllBytes` 메서드는이 크기를 초과 하는 파일을 읽을 수 없습니다.  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 사용 된 <xref:System.IO.StreamReader> 파일을 읽을 수 있습니다. 자세한 내용은 [기본 사항의.NET Framework 파일 I/O 및 파일 시스템 (Visual Basic)](../../../visual-basic/developing-apps/programming/drives-directories-files/basics-of-net-framework-file-io-and-the-file-system.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllBytes%2A>
- <xref:System.IO.StreamReader>
- [Visual Basic을 사용한 파일 액세스](../../../visual-basic/developing-apps/programming/drives-directories-files/file-access.md)
- [방법: StreamReader 사용 하 여 파일에서 텍스트 읽기](../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-text-from-files-with-a-streamreader.md)
