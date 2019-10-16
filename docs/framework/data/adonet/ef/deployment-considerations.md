---
title: 배포 고려 사항(Entity Framework)
ms.date: 03/30/2017
ms.assetid: 3a847a22-4eb8-4565-b18b-453bbca070db
ms.openlocfilehash: 3e78fc413e50deda67aa8992179e500afa671f8d
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251610"
---
# <a name="deployment-considerations-entity-framework"></a>배포 고려 사항(Entity Framework)
이 항목에서는 데이터 액세스를 위해 ADO.NET Entity Framework를 사용하는 애플리케이션 배포에 대한 정보를 제공합니다. Entity Framework에 대 한 자세한 내용은 [시작](getting-started.md)을 참조 하세요.  
  
 Entity Framework에서는 Visual Studio에서 개발을 용이하게 하는 통합된 도구 집합을 제공합니다. 자세한 내용은 [ADO.NET 엔터티 데이터 모델 Tools](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))를 참조 하세요. 이 항목에서 Entity Framework 기반 애플리케이션을 배포하기 위해 특정 기술을 사용하는 방법을 설명하지는 않습니다.  
  
 Visual Studio에서는 ClickOnce 배포와 같은 애플리케이션 배포에 대한 기능을 제공합니다. 자세한 내용은 Visual Studio 설명서의 [응용 프로그램 및 구성 요소 배포](/visualstudio/deployment/deploying-applications-services-and-components) 를 참조 하세요.  
  
 Entity Framework를 사용하는 애플리케이션을 배포할 때 다음 사항을 고려해야 합니다.  
  
- Entity Framework는 .NET Framework 3.5 서비스 팩 1(SP1)과 함께 시작하는 .NET Framework의 구성 요소입니다. Entity Framework 기반 애플리케이션을 배포할 때 .NET Framework 3.5 SP1 이상 버전이 설치되어 있어야 합니다.  
  
- 엔터티 데이터 모델 마법사를 통해 개념적 모델이 생성되면 애플리케이션 구성 파일에서 연결 문자열이 만들어집니다. 모델 및 매핑 파일이 애플리케이션 리소스로 포함되거나 출력 디렉터리에 복사될 수 있습니다. 기본적으로 모델 및 매핑 파일은 포함된 애플리케이션 리소스로 배포됩니다. Entity Designer 파일의 `Metadata Artifact Processing` 속성을 사용하여 이러한 옵션 중 하나를 선택합니다. 자세한 내용은 [방법: 모델 및 매핑 파일을 출력 디렉터리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716709(v=vs.100))에 복사 합니다.  
  
- CSDL(개념 스키마 정의 언어), SSDL(스토리지 스키마 정의 언어) 및 MSL(매핑 사양 언어)로 표현되는 모델 및 매핑 정보가 연결 문자열에 의해 지정된 위치에 애플리케이션과 함께 배포됩니다. 자세한 내용은 [연결 문자열](connection-strings.md)을 참조하세요.  
  
- 모델 및 매핑 정보를 애플리케이션 리소스로 포함하는 경우 개념적 모델이 업데이트될 때마다 애플리케이션을 다시 컴파일하고 다시 배포해야 합니다.  
  
- Entity Framework는 .NET Framework의 구성 요소이므로 .NET Framework 사용권 계약에 허용된 대로 애플리케이션과 함께 재배포할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET Entity Framework](index.md)
- [개발 및 배포 고려 사항](development-and-deployment-considerations.md)
