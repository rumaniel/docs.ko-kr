---
title: WCF Data Services 클라이언트 유틸리티(DataSvcUtil.exe)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, generating client data classes
- WCF Data Services, client library
- WCF Data Services, consuming
ms.assetid: 9d0af606-929b-4c03-b307-3ef5f705afce
ms.openlocfilehash: 7632362339cf9e23599f4f688f98cbc1d0b32114
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894242"
---
# <a name="wcf-data-service-client-utility-datasvcutilexe"></a>WCF Data Services 클라이언트 유틸리티(DataSvcUtil.exe)

Datasvcutil.exe는 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 피드를 사용 하 고 .NET Framework 클라이언트 응용 프로그램에서 데이터 서비스에 액세스 하는 데 필요한 클라이언트 데이터 서비스 클래스를 생성 하는 WCF Data Services에서 제공 하는 명령줄 도구입니다. 이 유틸리티는 다음 메타데이터 소스를 사용하여 데이터 클래스를 생성할 수 있습니다.

- 데이터 서비스의 루트 URI 이 유틸리티는 데이터 서비스에서 노출하는 데이터 모델을 설명하는 서비스 메타데이터 문서를 요청합니다. 자세한 내용은 [OData: 서비스 메타 데이터](https://go.microsoft.com/fwlink/?LinkId=186070)문서.

- MC (개념 스키마 정의 언어)에 [정의된대로csdl(개념스키마정의언어)을사용하여정의된데이터모델파일(csdl)입니다.\] \[ 개념 스키마 정의 파일 형식](https://go.microsoft.com/fwlink/?LinkID=159072) 사양입니다.

- Entity Framework와 함께 제공되는 엔터티 데이터 모델 도구를 사용하여 만든 .edmx 파일. 자세한 내용은 [ \[MC-EDMX\]를 참조 하세요. Data Services 패키징 형식](https://go.microsoft.com/fwlink/?LinkID=178833) 지정에 대 한 엔터티 데이터 모델입니다.

자세한 내용은 [방법: 클라이언트 데이터 서비스 클래스](how-to-manually-generate-client-data-service-classes-wcf-data-services.md)를 수동으로 생성 합니다.

Datasvcutil.exe 도구는 .NET Framework 디렉터리에 설치 됩니다. 대부분의 경우이는 *c:\windows\ microsoft.net \framework\v4.0*에 있습니다. 64 비트 시스템의 경우 *C:\Windows\Microsoft.NET\Framework64\v4.0*에 있습니다. Visual Studio 용 개발자 명령 프롬프트에서 Datasvcutil.exe 도구에 액세스할 수도 있습니다.

## <a name="syntax"></a>구문

```console
datasvcutil /out:file [/in:file | /uri:serviceuri] [/dataservicecollection] [/language:devlang] [/nologo] [/version:ver] [/help]
```

## <a name="parameters"></a>매개 변수

|옵션|설명|
|------------|-----------------|
|`/dataservicecollection`|개체를 컨트롤에 바인딩하는 데 필요한 코드도 생성되도록 지정합니다.|
|`/help`<br /><br /> 또는<br /><br /> `/?`|이 도구의 명령 구문 및 옵션을 표시합니다.|
|`/in:` *\<file>*|.csdl 또는 .edmx 파일이나 파일이 있는 디렉터리를 지정합니다.|
|`/language:`[VB&#124;CSharp]|생성되는 소스 코드 파일의 언어를 지정합니다. 기본 언어는 C#입니다.|
|`/nologo`|저작권 메시지가 표시되지 않도록 합니다.|
|`/out:` *\<file>*|생성된 클라이언트 데이터 서비스 클래스가 포함되는 소스 코드 파일의 이름을 지정합니다.|
|`/uri:` *\<string>*|OData 피드의 URI입니다.|
|`/version:`[1.0&#124;2.0]|OData의 최대 허용 버전을 지정 합니다. 버전은 반환 된 데이터 서비스 메타 `DataServiceVersion` 데이터에서 DataService 요소의 특성에 따라 결정 됩니다. 자세한 내용은 [데이터 서비스 버전 관리](data-service-versioning-wcf-data-services.md)합니다. 매개 변수를 지정 `/dataservicecollection` 하는 경우 데이터 바인딩을 사용 `/version:2.0` 하도록 지정 해야 합니다.|

## <a name="see-also"></a>참고자료

- [데이터 서비스 클라이언트 라이브러리 생성](generating-the-data-service-client-library-wcf-data-services.md)
- [방법: 데이터 서비스 참조 추가](how-to-add-a-data-service-reference-wcf-data-services.md)
