---
title: Windows 스토어 앱용 .NET을 위한 MEF
ms.date: 03/30/2017
ms.assetid: 7667770e-d163-4ad6-a303-085cf73db2f2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 255892e4dd3938028f488f80d8fba367590976f7
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051624"
---
# <a name="mef-for-net-for-windows-store-apps"></a>Windows 스토어 앱용 .NET을 위한 MEF
<xref:System.Composition?displayProperty=nameWithType> 및 자식 네임스페이스에는 MEF(Managed Extensibility Framework)를 사용하여 확장 가능한 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 개발하기 위한 형식이 포함되어 있습니다. 이러한 네임스페이스는 [!INCLUDE[win8](../../../includes/win8-md.md)] 운영 체제에 대한 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] 하위 집합의 일부입니다.  
  
 이 네임스페이스는 .NET Framework와 함께 배포되는 핵심 클래스 라이브러리의 일부가 아닙니다. 이 네임스페이스를 설치하려면 Visual Studio에서 프로젝트를 열고 **프로젝트** 메뉴에서 **NuGet 패키지 관리**를 선택한 다음, Microsoft.Composition 패키지를 온라인으로 검색합니다.  
  
- <xref:System.Composition?displayProperty=nameWithType>은 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱용 핵심 MEF를 구성하는 클래스를 제공합니다.  
  
- <xref:System.Composition.Convention?displayProperty=nameWithType>은 규칙 기반 구성 모델에서 MEF 사용을 지원하는 형식을 제공합니다.  
  
- <xref:System.Composition.Hosting?displayProperty=nameWithType>은 호스트 애플리케이션 개발자에게 유용한 MEF 형식을 제공합니다.  
  
- <xref:System.Composition.Hosting.Core?displayProperty=nameWithType>은 컴포지션 엔진에서 내부적으로 사용되는 MEF 형식을 제공합니다.  
  
 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] 및 여기에 포함된 네임스페이스 및 형식 목록에 대한 자세한 내용은 Windows 개발자 센터의 [Windows 스토어 앱용 .NET 개요](https://go.microsoft.com/fwlink/p/?LinkID=238312)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [Windows 스토어 앱용 .NET 개요](https://go.microsoft.com/fwlink/p/?LinkID=238312)
- [Windows 스토어 앱용 .NET – 지원되는 API](https://go.microsoft.com/fwlink/p/?LinkID=247912)
- [MEF(Managed Extensibility Framework)](index.md)
