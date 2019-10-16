---
title: .NET의 파이프 작업
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- pipes [.NET Framework]
- pipe operations [.NET Framework]
- interprocess communication [.NET Framework], pipes
- I/O [.NET Framework], pipes
ms.assetid: 7b964ebd-7a4f-4d28-8194-7841f9e4c702
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0f02f7a8a327e117b92ef826b8dcd7fc742c9b4c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64647806"
---
# <a name="pipe-operations-in-net"></a>.NET의 파이프 작업
파이프는 프로세스 간 통신을 위한 수단을 제공합니다. 파이프에는 다음과 같이 두 가지 유형이 있습니다.  
  
- 익명 파이프  
  
     익명 파이프는 로컬 컴퓨터에서 프로세스 간 통신을 제공합니다. 익명 파이프에는 명명된 파이프보다 적은 오버헤드가 필요하지만 그만큼 제한된 서비스를 제공합니다. 익명 파이프는 단방향이므로 네트워크에서 사용할 수 없습니다. 익명 파이프는 단일 서버 인스턴스만 지원합니다. 익명 파이프는 스레드 간 통신 또는 자식 프로세스가 생성될 때 자식 프로세스에 파이프 핸들을 쉽게 전달할 수 있는 부모와 자식 프로세스 간 통신에 유용합니다.  
  
     .NET에서는 <xref:System.IO.Pipes.AnonymousPipeServerStream> 및 <xref:System.IO.Pipes.AnonymousPipeClientStream> 클래스를 사용하여 익명 파이프를 구현합니다.  
  
     [방법: 로컬 프로세스 간 통신에 익명 파이프 사용](../../../docs/standard/io/how-to-use-anonymous-pipes-for-local-interprocess-communication.md)을 참조하세요.  
  
- 명명된 파이프  
  
     명명된 파이프는 파이프 서버와 하나 이상의 파이프 클라이언트 간의 프로세스 간 통신을 제공합니다. 명명된 파이프는 단방향 또는 양방향일 수 있습니다. 명명된 파이프는 메시지 기반 통신을 지원하며, 명명된 파이프를 통해 여러 클라이언트가 동일한 파이프 이름을 사용하여 서버 프로세스에 동시에 연결할 수 있습니다. 명명된 파이프는 가장을 지원함으로써 연결 프로세스가 원격 서버에서 고유한 권한을 사용할 수 있도록 합니다.  
  
     .NET에서는 <xref:System.IO.Pipes.NamedPipeServerStream> 및 <xref:System.IO.Pipes.NamedPipeClientStream> 클래스를 사용하여 명명된 파이프를 구현합니다.  
  
     [방법: 네트워크 프로세스 간 통신에 명명된 파이프 사용](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [파일 및 스트림 I/O](../../../docs/standard/io/index.md)
- [방법: 로컬 프로세스 간 통신에 익명 파이프 사용](../../../docs/standard/io/how-to-use-anonymous-pipes-for-local-interprocess-communication.md)
- [방법: 네트워크 프로세스 간 통신에 명명된 파이프 사용](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md)
