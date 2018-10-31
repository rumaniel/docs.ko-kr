---
title: 스트림 작성
ms.date: 03/30/2017
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
ms.openlocfilehash: 5e52b827f337892c33ec61b9affa1cc646a759c5
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48841179"
---
# <a name="composing-streams"></a>스트림 작성
백업 저장소는 디스크 또는 메모리와 같은 저장 매체입니다. 다양한 각 백업 저장소는 <xref:System.IO.Stream> 클래스의 구현으로 고유한 스트림을 구현합니다. 각 스트림 유형은 지정된 백업 저장소에 유입 또는 유출되는 바이트를 읽고 씁니다. 백업 저장소에 연결되는 스트림을 기본 스트림이라고 합니다. 기본 스트림에는 스트림을 백업 저장소에 연결하는 데 필요한 매개 변수가 있는 생성자가 있습니다. 예를 들어 <xref:System.IO.FileStream>에는 프로세스가 경로 매개 변수를 지정하는 생성자가 있습니다. 경로 매개 변수는 파일을 공유할 방식 등을 지정합니다.  
  
 <xref:System.IO> 클래스의 디자인은 간소화된 스트림 작성을 제공합니다. 원하는 기능을 제공하는 하나 이상의 통과 스트림에 기본 스트림을 연결할 수 있습니다. 기본 설정 유형을 쉽게 읽거나 쓸 수 있도록 체인 끝에 reader 또는 writer를 연결할 수 있습니다.  
  
 다음 코드 예제에서는 `MyFile.txt`를 버퍼링하기 위해 기존의 `MyFile.txt`를 바탕으로 **FileStream**을 만듭니다. (기본적으로 **FileStream**은 버퍼링됩니다.) 다음으로, **StreamReader**에 해당 생성자 인수로 전달되는 **FileStream**에서 문자를 읽도록 <xref:System.IO.StreamReader>를 만듭니다. <xref:System.IO.StreamReader.ReadLine%2A>은 <xref:System.IO.StreamReader.Peek%2A>가 더 이상 문자를 찾지 못할 때까지 읽습니다.  
  
 [!code-cpp[System.IO.StreamReader#20](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.StreamReader/CPP/source2.cpp#20)]
 [!code-csharp[System.IO.StreamReader#20](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source2.cs#20)]
 [!code-vb[System.IO.StreamReader#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source2.vb#20)]  
  
 다음 코드 예제에서는 `MyFile.txt`를 버퍼링하기 위해 기존의 `MyFile.txt`를 바탕으로 **FileStream**을 만듭니다. (기본적으로 **FileStream**은 버퍼링됩니다.) 다음으로, **BinaryReader**에 해당 생성자 인수로 전달되는 **FileStream**에서 바이트를 읽도록 **BinaryReader**를 만듭니다. <xref:System.IO.BinaryReader.ReadByte%2A>는 <xref:System.IO.BinaryReader.PeekChar%2A>이 더 이상 바이트를 찾지 못할 때까지 읽습니다.  
  
 [!code-cpp[System.IO.StreamReader#21](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.StreamReader/CPP/source3.cpp#21)]
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
