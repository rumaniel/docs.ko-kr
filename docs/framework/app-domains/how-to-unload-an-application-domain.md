---
title: '방법: 애플리케이션 도메인 언로드'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Unload method
- application domains, unloading
- unloading application domains
ms.assetid: f356116d-e415-4f7c-a332-6e6a60227192
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f7419725f3822622a8e4210d4f3f5d8e9e59dbdd
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053127"
---
# <a name="how-to-unload-an-application-domain"></a>방법: 애플리케이션 도메인 언로드
애플리케이션 도메인 사용을 마쳤으면 <xref:System.AppDomain.Unload%2A?displayProperty=nameWithType> 메서드를 사용하여 언로드합니다. **Unload** 메서드는 지정된 애플리케이션 도메인을 정상적으로 종료합니다. 언로드 프로세스 중에는 새 스레드가 애플리케이션 도메인에 액세스할 수 없으며 모든 애플리케이션 도메인 특정 데이터 구조가 비워집니다.  
  
 애플리케이션 도메인에 로드된 어셈블리가 제거되고 더 이상 사용할 수 없습니다. 애플리케이션 도메인의 어셈블리가 도메인 중립적인 경우 해당 어셈블리의 데이터는 전체 프로세스가 종료될 때까지 메모리에 남아 있습니다. 따라서 도메인 중립 어셈블리를 언로드하려면 전체 프로세스를 종료하는 것이 유일한 메커니즘입니다. 경우에 따라 애플리케이션 도메인에 대한 언로드 요청이 제대로 작동하지 않아 <xref:System.CannotUnloadAppDomainException>이 발생할 수 있습니다.  
  
 다음 예제에서는 `MyDomain`이라는 새 애플리케이션 도메인을 만들고, 콘솔에 일부 정보를 출력한 다음, 해당 애플리케이션 도메인을 언로드합니다. 이 코드에서는 언로드된 애플리케이션 도메인의 이름을 콘솔에 출력하려고 합니다. 이 동작은 프로그램 끝에 있는 try/catch 문으로 처리되는 예외를 생성합니다.  
  
## <a name="example"></a>예제  
 [!code-cpp[System.AppDomain.Load#3](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source3.cpp#3)]
 [!code-csharp[System.AppDomain.Load#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source3.cs#3)]
 [!code-vb[System.AppDomain.Load#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source3.vb#3)]  
  
## <a name="see-also"></a>참고 항목

- [애플리케이션 도메인으로 프로그래밍](application-domains.md#programming-with-application-domains)
- [방법: 애플리케이션 도메인 만들기](how-to-create-an-application-domain.md)
- [애플리케이션 도메인 사용](use.md)
