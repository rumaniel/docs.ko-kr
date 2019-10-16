---
title: UriTemplate 샘플
ms.date: 03/30/2017
ms.assetid: 0aaf91d0-ce18-468d-8006-bc9bc2e48231
ms.openlocfilehash: 15799c1aaf3ed7df5f7721368dea426665dcf335
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044592"
---
# <a name="uritemplate-sample"></a>UriTemplate 샘플
<xref:System.UriTemplate> 클래스에서는 공통의 구조를 공유하는 URI 집합으로 작업하는 데 사용되는 메서드를 제공합니다. 이 샘플에서는 `UriTemplate`와 관련된 다음 핵심 개념을 보여 줍니다.  
  
- 템플릿 만들기용 구문.  
  
- `UriTemplate`에서 <xref:System.UriTemplate.BindByName%2A> 및 <xref:System.UriTemplate.BindByPosition%2A>을 사용하여 URI 인스턴스화.  
  
- <xref:System.UriTemplateTable.Match%2A> 및 `BindByName`의 역작업인 `BindByPosition`.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
2. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\UriTemplate`  
  
## <a name="see-also"></a>참고자료

- [UriTemplate 테이블](../../../../docs/framework/wcf/samples/uritemplate-table-sample.md)
- [UriTemplate 테이블 디스패처](../../../../docs/framework/wcf/samples/uritemplate-table-dispatcher-sample.md)
