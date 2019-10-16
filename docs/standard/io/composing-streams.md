---
title: 스트림 작성
ms.date: 01/21/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- streams, base streams
- I/O [.NET Framework], composing streams
- Stream class, composing streams
- base streams
- streams, backing stores
ms.assetid: da761658-a535-4f26-a452-b30df47f73d5
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 452071e9726a95b4b3d9bb9cefe720d39bbc3e0c
ms.sourcegitcommit: b8ace47d839f943f785b89e2fff8092b0bf8f565
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2019
ms.locfileid: "55674349"
---
# <a name="compose-streams"></a>스트림 작성
백업 저장소(*backing store*)는 디스크 또는 메모리와 같은 스토리지 매체입니다. 다양한 각 백업 저장소는 <xref:System.IO.Stream> 클래스의 구현으로 고유한 스트림을 구현합니다. 

각 스트림 유형은 지정된 백업 저장소에 유입 또는 유출되는 바이트를 읽고 씁니다. 백업 저장소에 연결되는 스트림을 기본 스트림(*base stream*)이라고 합니다. 기본 스트림에는 스트림을 백업 저장소에 연결하는 데 필요한 매개 변수가 포함된 생성자가 있습니다. 예를 들어 <xref:System.IO.FileStream>에는 프로세스가 경로 매개 변수를 지정하는 생성자가 있으며, 이것은 프로세스가 파일을 공유하는 방법을 지정합니다.  

<xref:System.IO> 클래스 디자인은 간소화된 스트림 컴퍼지션을 제공합니다. 원하는 기능을 제공하는 하나 이상의 통과 스트림에 기본 스트림을 연결할 수 있습니다. 체인 끝에 reader 또는 writer를 연결할 수 있기 때문에 기본 형식을 쉽게 읽거나 쓸 수 있습니다.  

다음 코드 예제에서는 *MyFile.txt*를 버퍼링하기 위해 기존 *MyFile.txt*를 바탕으로 **FileStream**을 만듭니다. **FileStream**은 기본적으로 버퍼링됩니다.

>[!IMPORTANT]
>예제에서는 *MyFile.txt* 파일이 앱과 동일한 폴더에 이미 존재한다고 가정합니다.  

## <a name="example-use-streamreader"></a>예제: StreamReader 사용
다음 예제에서는 생성자 인수로 **StreamReader**에 전달되는 **FileStream**에서 문자를 읽는 <xref:System.IO.StreamReader>를 만듭니다. <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>은 <xref:System.IO.StreamReader.Peek%2A?displayProperty=nameWithType>에서 더 이상 문자를 찾지 못할 때까지 읽습니다.  
  
 [!code-csharp[System.IO.StreamReader#20](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source2.cs#20)]
 [!code-vb[System.IO.StreamReader#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source2.vb#20)]  
  
## <a name="example-use-binaryreader"></a>예제: BinaryReader 사용
다음 예제에서는 생성자 인수로 **BinaryReader**에 전달되는 **FileStream**에서 바이트를 읽는 <xref:System.IO.BinaryReader>를 만듭니다. <xref:System.IO.BinaryReader.ReadByte%2A>는 <xref:System.IO.BinaryReader.PeekChar%2A>에서 더 이상 바이트를 찾지 못할 때까지 읽습니다.  
  
 [!code-csharp[System.IO.StreamReader#21](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source3.cs#21)]
 [!code-vb[System.IO.StreamReader#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source3.vb#21)]  
  
## <a name="see-also"></a>참고 항목

- <xref:System.IO.StreamReader>
- <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=nameWithType>
- <xref:System.IO.StreamReader.Peek%2A?displayProperty=nameWithType>
- <xref:System.IO.FileStream>
- <xref:System.IO.BinaryReader>
- <xref:System.IO.BinaryReader.ReadByte%2A?displayProperty=nameWithType>
- <xref:System.IO.BinaryReader.PeekChar%2A?displayProperty=nameWithType>
