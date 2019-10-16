---
title: '방법: 모델 및 매핑 파일을 포함 리소스로 만들기'
ms.date: 03/30/2017
ms.assetid: 20dfae4d-e95a-4264-9540-f5ad23b462d3
ms.openlocfilehash: 371f8f0317295ee39d543b5637afb93102036b62
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854594"
---
# <a name="how-to-make-model-and-mapping-files-embedded-resources"></a>방법: 모델 및 매핑 파일을 포함 리소스로 만들기
Entity Framework를 사용 하면 모델 및 매핑 파일을 응용 프로그램의 포함 리소스로 배포할 수 있습니다. 포함된 모델 및 매핑 파일이 있는 어셈블리는 엔터티 연결과 동일한 애플리케이션 도메인에 로드해야 합니다. 자세한 내용은 [연결 문자열](connection-strings.md)을 참조하세요. 기본적으로 엔터티 데이터 모델 도구는 모델 및 매핑 파일을 포함 합니다. 모델 및 매핑 파일을 수동으로 정의 하는 경우이 절차를 사용 하 여 파일이 Entity Framework 응용 프로그램과 함께 포함 리소스로 배포 되도록 합니다.  
  
> [!NOTE]
> 포함 리소스를 유지하려면 모델 및 매핑 파일이 수정될 때마다 이 절차를 반복해야 합니다.  
  
### <a name="to-embed-model-and-mapping-files"></a>모델 및 매핑 파일을 포함하려면  
  
1. **솔루션 탐색기**에서 개념 파일 (csdl)을 선택 합니다.  
  
2. **속성** 창에서 **빌드 작업** 을 **포함 리소스**로 설정 합니다.  
  
3. 스토리지 파일(.ssdl) 및 매핑 파일(.msl)에 대해 1단계와 2단계를 반복합니다.  
  
4. **솔루션 탐색기**에서 app.config 파일을 두 번 클릭 한 다음 다음 형식 중 하나를 `Metadata` 기반으로 `connectionString` 특성의 매개 변수를 수정 합니다.  
  
    - `Metadata=` `res://<assemblyFullName>/<resourceName>;`  
  
    - `Metadata=` `res://*/<resourceName>;`  
  
    - `Metadata=res://*;`  
  
     자세한 내용은 [연결 문자열](connection-strings.md)을 참조하세요.  
  
## <a name="example"></a>예제  
 다음 연결 문자열은 [AdventureWorks Sales 모델](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)에 대 한 포함 된 모델 및 매핑 파일을 참조 합니다. 이 연결 문자열은 프로젝트의 App.config 파일에 저장됩니다.  

## <a name="see-also"></a>참고자료

- [모델링 및 매핑](modeling-and-mapping.md)
- [방법: 연결 문자열 정의](how-to-define-the-connection-string.md)
- [방법: EntityConnection 연결 문자열 작성](how-to-build-an-entityconnection-connection-string.md)
- [ADO.NET 엔터티 데이터 모델 도구](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
