---
title: '방법: 로그 파일 열기 및 추가'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- log files, opening
- streams, opening and appending to log file
- log files, appending to
- I/O [.NET Framework], log files
ms.assetid: 74423362-1721-49cb-aa0a-e04005f72a06
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 35a7d481cf82818054a852f7c2e142f615022fcb
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48848155"
---
# <a name="how-to-open-and-append-to-a-log-file"></a>방법: 로그 파일 열기 및 추가
<xref:System.IO.StreamWriter> 및 <xref:System.IO.StreamReader>는 스트림에서 문자를 쓰고 문자를 읽습니다. 다음 코드 예제는 입력을 위해 `log.txt` 파일을 열거나, 파일이 존재하지 않는 경우 파일을 만들고 파일의 끝에 정보를 추가합니다. 그러면 파일의 콘텐츠가 디스플레이의 표준 출력에 기록됩니다. 이 예제의 대안으로, 정보를 단일 문자열 또는 문자열 배열로 저장할 수 있으며, <xref:System.IO.File.WriteAllText%2A> 또는 <xref:System.IO.File.WriteAllLines%2A> 메서드를 동일한 기능을 수행하는 데 사용할 수도 있습니다.  
  
> [!NOTE]
>  Visual Basic 사용자는 로그 파일을 생성하거나 로그 파일에 쓰기 위해 <xref:Microsoft.VisualBasic.Logging.Log> 클래스 또는 <xref:Microsoft.VisualBasic.FileIO.FileSystem> 클래스에서 제공하는 메서드 및 속성을 사용하도록 선택할 수 있습니다.  
  
## <a name="example"></a>예  
 [!code-csharp[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source2.cs#2)]
 [!code-vb[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source2.vb#2)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO.StreamWriter>  
- <xref:System.IO.StreamReader>  
- <xref:System.IO.File.AppendText%2A?displayProperty=nameWithType>  
- <xref:System.IO.File.OpenText%2A?displayProperty=nameWithType>  
- <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>  
- [방법: 디렉터리 및 파일 열거](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)  
- [방법: 새로 만든 데이터 파일 읽기 및 쓰기](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)  
- [방법: 파일의 텍스트 읽기](../../../docs/standard/io/how-to-read-text-from-a-file.md)  
- [방법: 파일에 텍스트 쓰기](../../../docs/standard/io/how-to-write-text-to-a-file.md)  
- [방법: 문자열에서 문자 읽기](../../../docs/standard/io/how-to-read-characters-from-a-string.md)  
- [방법: 문자열에 문자 쓰기](../../../docs/standard/io/how-to-write-characters-to-a-string.md)  
- [파일 및 스트림 I/O](../../../docs/standard/io/index.md)
