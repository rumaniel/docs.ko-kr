---
title: '방법: 로컬 프로세스 간 통신에 익명 파이프 사용'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- anonymous pipes [.NET Framework]
- parent-child communication [.NET Framework]
- pipes [.NET Framework]
- one-way communication [.NET Framework]
- local computer communication [.NET Framework], pipes
ms.assetid: e7773c77-c646-4a01-8a96-a003d59fc4c9
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 810b29b4abde174e3634a03d5c7b5e0e43de11b8
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54637770"
---
# <a name="how-to-use-anonymous-pipes-for-local-interprocess-communication"></a>방법: 로컬 프로세스 간 통신에 익명 파이프 사용
익명 파이프는 로컬 컴퓨터에서 프로세스 간 통신을 제공합니다. 명명된 파이프보다 적은 기능을 제공하지만 오버로드를 더 적게 필요로 합니다. 익명 파이프를 사용하면 로컬 컴퓨터에서 프로세스 간 통신을 더욱 쉽게 만들 수 있습니다. 네트워크를 통한 통신에는 익명 파이프를 사용할 수 없습니다.  
  
 익명 파이프를 구현하려면, <xref:System.IO.Pipes.AnonymousPipeServerStream> 및 <xref:System.IO.Pipes.AnonymousPipeClientStream> 클래스를 사용합니다.  
  
## <a name="example"></a>예제  
 다음 예제는 익명 파이프를 사용하여 부모 프로세스에서 자식 프로세스로 문자열을 보내는 방법을 보여줍니다. 이 예제는 <xref:System.IO.Pipes.PipeDirection.Out>의 <xref:System.IO.Pipes.PipeDirection> 값을 사용하여 부모 프로세스에서 <xref:System.IO.Pipes.AnonymousPipeServerStream> 개체를 생성합니다. 그런 다음, 부모 프로세스는 클라이언트 핸들을 사용하여 <xref:System.IO.Pipes.AnonymousPipeClientStream> 개체를 생성함으로써 자식 프로세스를 만듭니다. 자식 프로세스에는 <xref:System.IO.Pipes.PipeDirection.In>의 <xref:System.IO.Pipes.PipeDirection> 값이 있습니다.  
  
 그런 다음, 부모 프로세스는 사용자가 제공한 문자열을 자식 프로세스로 보냅니다. 문자열이 자식 프로세스의 콘솔에 표시됩니다.  
  
 다음 예제는 서버 프로세스를 보여줍니다.  
  
 [!code-cpp[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/vb/program.vb#01)]  
  
## <a name="example"></a>예제  
 다음 예제는 클라이언트 프로세스를 보여줍니다. 서버 프로세스는 클라이언트 프로세스를 시작하고 해당 프로세스에 클라이언트 핸들을 제공합니다. 클라이언트 코드의 결과 실행 파일 이름은 `pipeClient.exe`이어야 하며 서버 프로세스를 실행하기 전에 서버 실행 파일과 동일한 디렉터리로 복사해야 합니다.  
  
 [!code-cpp[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/vb/program.vb#01)]  
  
## <a name="see-also"></a>참고 항목

- [파이프](../../../docs/standard/io/pipe-operations.md)
- [방법: 네트워크 프로세스 간 통신에 명명된 파이프 사용](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md)
