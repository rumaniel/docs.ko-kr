---
title: '방법: EdmGen.exe를 사용하여 모델 및 매핑 파일 유효성 검사'
ms.date: 03/30/2017
ms.assetid: 2641906a-971a-4d0b-8aee-13fabc02a1cc
ms.openlocfilehash: 4495ff3c5d55779e9db113a2a59361b643841382
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251385"
---
# <a name="how-to-use-edmgenexe-to-validate-model-and-mapping-files"></a>방법: EdmGen.exe를 사용하여 모델 및 매핑 파일 유효성 검사
이 항목에서는 [EDM 생성기 (edmgen.exe)](edm-generator-edmgen-exe.md) 도구를 사용 하 여 모델 및 매핑 파일의 유효성을 검사 하는 방법을 보여 줍니다. 자세한 내용은 [엔터티 데이터 모델](../entity-data-model.md)를 참조 하세요.  
  
### <a name="to-validate-the-school-model-using-edmgenexe"></a>EdmGen.exe를 사용하여 School 모델의 유효성을 검사하려면  
  
1. School 데이터베이스를 만듭니다. 자세한 내용은 [School 샘플 데이터베이스 만들기](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399731(v=vs.100))를 참조 하세요.  
  
2. School 모델을 생성합니다. 자세한 내용은 [방법: Edmgen.exe를 사용 하 여 모델 및 매핑 파일](how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)을 생성 합니다.  
  
3. 명령 프롬프트에서 줄 바꿈 없이 다음 명령을 실행합니다.  
  
    ```console
    "%windir%\Microsoft.NET\Framework\v4.0.30319\edmgen.exe" /mode:ValidateArtifacts /inssdl:.\School.ssdl /inmsl:.\School.msl /incsdl:.\School.csdl  
    ```  
  
## <a name="see-also"></a>참고자료

- [방법: Entity Framework 프로젝트 수동 구성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100))
- [ADO.NET 엔터티 데이터 모델 도구](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
- [방법: 뷰를 미리 생성 하 여 쿼리 성능 향상](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896240(v=vs.100))
- [방법: Edmgen.exe를 사용 하 여 개체 계층 코드 생성](how-to-use-edmgen-exe-to-generate-object-layer-code.md)
