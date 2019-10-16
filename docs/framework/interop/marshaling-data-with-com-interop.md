---
title: COM Interop를 사용하여 데이터 마샬링
ms.date: 09/07/2017
helpviewer_keywords:
- COM interop, data marshaling
- marshaling data, COM interop
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3dd667f681e9b6749f33d6ccfd91035477c56030
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051695"
---
# <a name="marshaling-data-with-com-interop"></a>COM Interop를 사용하여 데이터 마샬링
COM interop는 관리 코드에서 COM 개체를 사용하고 관리되는 개체를 COM에 노출하는 기능을 모두 지원합니다. COM과의 데이터 마샬링 지원은 광범위하며 거의 항상 올바른 마샬링 동작을 제공합니다.  
  
 Windows SDK에는 다음과 같은 COM interop 도구가 포함됩니다.  
  
- [형식 라이브러리 가져오기(Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md) - COM 형식 라이브러리를 interop 어셈블리로 변환합니다. 이 어셈블리에서 interop 마샬링 서비스는 관리되는 메모리와 관리되지 않는 메모리 간에 데이터 마샬링을 수행하는 래퍼를 생성합니다.  
  
- [형식 라이브러리 내보내기(Tlbexp.exe)](../tools/tlbexp-exe-type-library-exporter.md) - 어셈블리에서 COM 형식 라이브러리를 생성하고 메서드 호출 중 마샬링을 수행하는 래퍼를 생성합니다.  
  
 다음 섹셕은 마샬러에 추가 형식 정보를 제공할 수 있는(제공해야 하는) 경우 interop 래퍼를 사용자 지정하는 프로세스를 설명하는 항목으로 연결됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[방법: 수동으로 래퍼 만들기](how-to-create-wrappers-manually.md)   
관리 소스 코드에서 COM 래퍼를 수동으로 만드는 방법을 설명합니다. 
 
 [방법: 관리 코드 DCOM을 WCF로 마이그레이션](how-to-migrate-managed-code-dcom-to-wcf.md)  
 보다 안전한 솔루션을 위해 관리되는 DCOM 코드를 WCF로 마이그레이션하는 방법을 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [COM 데이터 형식](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sak564ww(v=vs.100))  
 해당 관리되는 데이터 형식과 관리되지 않는 데이터 형식을 제공합니다.  
  
 [COM 호출 가능 래퍼 사용자 지정](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/3bwc828w(v=vs.100))  
 디자인 타임에 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성을 사용하여 데이터 형식을 명시적으로 마샬링하는 방법을 설명합니다.  
  
 [런타임 호출 가능 래퍼 사용자 지정](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100))  
 interop 어셈블리에서 형식의 마샬링 동작을 조정하는 방법 및 COM 형식을 수동으로 조정하는 방법을 설명합니다.  
  
 [고급 COM 상호 운용성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bd9cdfyx(v=vs.100))  
 COM 구성 요소를 .NET Framework 애플리케이션으로 통합하는 방법에 대한 추가정보 링크를 제공합니다.  
  
 [어셈블리와 형식 라이브러리 간 변환 요약](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/xk1120c3(v=vs.100))  
 어셈블리에서 형식 라이브러리로 내보내기 변환 프로세스를 설명합니다.  
  
 [형식 라이브러리를 어셈블리로 변환 요약](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))  
 형식 라이브러리에서 어셈블리 가져오기 변환 프로세스를 설명합니다.  
  
 [제네릭 형식을 통한 상호 운용](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms229590(v=vs.100))  
 COM 상호 운용성을 위해 제네릭 형식을 사용할 때 지원되는 작업을 설명합니다.
