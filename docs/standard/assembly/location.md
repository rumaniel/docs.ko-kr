---
title: 어셈블리 위치
ms.date: 08/20/2019
helpviewer_keywords:
- locating assemblies
- assemblies [.NET Framework], location
ms.assetid: 9f1f41a7-2954-49d3-a2c0-62b6ef4d40ab
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6427f7d005c43ef9e83387e865f71009b683a7c4
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972656"
---
# <a name="assembly-location"></a>어셈블리 위치
어셈블리 위치에 따라 공용 언어 런타임이 참조 시 해당 위치를 찾을 수 있는지 여부가 결정되고 어셈블리를 다른 어셈블리와 공유할 수 있는지 여부도 결정될 수 있습니다. 다음 위치에 어셈블리를 배포할 수 있습니다.  
  
- 애플리케이션의 디렉터리 또는 하위 디렉터리.  
  
     어셈블리를 배포할 수 있는 가장 일반적인 위치입니다. 애플리케이션 루트 디렉터리의 하위 디렉터리는 언어 또는 문화권에 따라 다를 수 있습니다. 어셈블리에 문화권 특성의 정보가 있으면 어셈블리는 애플리케이션 디렉터리 아래 하위 디렉터리에 문화권 이름과 함께 포함되어야 합니다.  
  
- 전역 어셈블리 캐시  
  
     공용 언어 런타임이 설치되는 모든 위치에 설치되는 컴퓨터 수준 코드 캐시입니다. 대부분의 경우 어셈블리를 여러 애플리케이션과 공유하려고 하면 어셈블리를 전역 어셈블리 캐시에 배포해야 합니다.  
  
- HTTP 서버에.  
  
     HTTP 서버에 배포되는 어셈블리에는 강력한 이름이 있어야 합니다. 애플리케이션 구성 파일의 코드베이스 섹션에 있는 어셈블리를 가리킵니다.  
  
## <a name="see-also"></a>참고 항목

- [어셈블리 만들기](create.md)
- [전역 어셈블리 캐시](../../framework/app-domains/gac.md)
- [런타임에서 어셈블리를 찾는 방법](../../framework/deployment/how-the-runtime-locates-assemblies.md)
- [어셈블리를 사용한 프로그램](program.md)
