---
title: Tlbexp 도우미 함수(관리되지 않는 API 참조)
ms.date: 03/30/2017
helpviewer_keywords:
- exporter tool [.NET Framework]
- TlbRef.dll
- Tlbexp.exe
- Type Library Exporter
ms.assetid: 5c0a3d14-5f26-4267-94a9-82c30f8db09a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a95ff535a4d0847fbd4b8af28f873b67a1829a4f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798829"
---
# <a name="tlbexp-helper-functions-unmanaged-api-reference"></a>Tlbexp 도우미 함수(관리되지 않는 API 참조)
[형식 라이브러리 내보내기 도구](../../tools/tlbexp-exe-type-library-exporter.md)(Tlbexp.exe)는 TlbRef.dll이라는 동적 링크 라이브러리를 로드합니다. 이 DLL에는 어셈블리-형식 라이브러리 전환 프로세스 중 내보내기 도구에서 사용하는 인터페이스 하나와 도우미 함수 두 개가 포함되어 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [GetTypeLibInfo 함수](gettypelibinfo-function.md)  
 형식 라이브러리에 대한 지역화 및 운영 체제 정보를 제공합니다.  
  
 [LoadTypeLibWithResolver 함수](loadtypelibwithresolver-function.md)  
 [ITypeLibResolver 인터페이스](itypelibresolver-interface.md) 구현을 통해 형식 라이브러리를 로드하고 참조된 형식 라이브러리를 확인합니다.  
  
 [ITypeLibResolver 인터페이스](itypelibresolver-interface.md)  
 형식 라이브러리의 정규화된 경로를 반환하는 [ResolveTypeLib 메서드](resolvetypelib-method.md)를 제공합니다.
