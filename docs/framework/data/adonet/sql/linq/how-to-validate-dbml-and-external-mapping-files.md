---
title: '방법: DBML 및 외부 매핑 파일 유효성 검사'
ms.date: 03/30/2017
ms.assetid: d9ea37f5-0a9e-4401-8fc3-1e6fd44c49f9
ms.openlocfilehash: b5901705ac7c0692025ff1f4a4b78f976d62176d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793044"
---
# <a name="how-to-validate-dbml-and-external-mapping-files"></a>방법: DBML 및 외부 매핑 파일 유효성 검사

수정한 외부 매핑 파일 및 .dbml 파일은 해당 스키마 정의에 대해 유효성이 검사되어야 합니다. 이 항목에서는 Visual Studio 사용자에 게 유효성 검사 프로세스를 구현 하는 단계를 제공 합니다.

[!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]

### <a name="to-validate-a-dbml-or-xml-file"></a>.dbml 또는 XML 파일의 유효성을 검사하려면

1. Visual Studio **파일** 메뉴에서 **열기**를 가리킨 다음 **파일**을 클릭 합니다.

2. **파일 열기** 대화 상자에서 유효성 검사를 수행 하려는 .DBML 또는 XML 매핑 파일을 클릭 합니다.

    파일이 **XML 편집기**에서 열립니다.

3. 창을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.

4. **속성** 창에서 **스키마** 속성에 대 한 줄임표를 클릭 합니다.

    **XML 스키마** 대화 상자가 열립니다.

5. 원하는 목적에 맞는 적절한 스키마 정의를 확인합니다.

    - DbmlSchema.xsd는 .dbml 파일의 유효성 검사를 위한 스키마 정의입니다. 자세한 내용은 [LINQ to SQL에서 코드 생성](code-generation-in-linq-to-sql.md)을 참조 하세요.

    - LinqToSqlMapping.xsd는 외부 XML 매핑 파일의 유효성 검사를 위한 스키마 정의입니다. 자세한 내용은 [외부 매핑](external-mapping.md)을 참조 하세요.

6. 원하는 스키마 정의 행의 **사용** 열에서 드롭다운 상자를 클릭 하 여 연 다음 **이 스키마 사용**을 클릭 합니다.

    이제 스키마 정의 파일이 DBML 또는 XML 매핑 파일과 연관됩니다.

    다른 스키마 정의가 선택되지 않았는지 확인합니다.

7. **보기** 메뉴에서 **오류 목록**를 클릭 합니다.

    오류, 경고 또는 메시지가 생성되었는지 여부를 확인합니다. 생성된 것이 없는 경우 스키마 정의에 대해 XML 파일이 유효합니다.

## <a name="alternate-method-for-supplying-schema-definition"></a>스키마 정의 제공을 위한 대체 방법

어떤 이유로 든 적절 한 .xsd 파일이 **XML 스키마** 대화 상자에 표시 되지 않으면 도움말 항목에서 .xsd 파일을 다운로드할 수 있습니다. 다음 단계를 통해 Visual Studio XML 편집기에 필요한 유니코드 형식으로 다운로드 한 파일을 저장할 수 있습니다.

#### <a name="to-copy-a-schema-definition-file-from-a-help-topic"></a>도움말 항목에서 스키마 정의 파일을 복사하려면

1. 이 항목의 앞부분에서 설명한 대로 스키마 정의가 포함된 도움말 항목을 찾습니다.

    - .Dbml 파일은 [LINQ to SQL에서 코드 생성](code-generation-in-linq-to-sql.md)을 참조 하세요.

    - 외부 매핑 파일은 [외부 매핑](external-mapping.md)을 참조 하세요.

2. 코드 **복사** 를 클릭 하 여 코드 파일을 클립보드에 복사 합니다.

3. 메모장을 시작하여 새 파일을 만듭니다.

4. 클립보드에서 메모장 파일로 코드를 붙여넣습니다.

5. 메모장 **파일** 메뉴에서 다른 **이름으로 저장**을 클릭 합니다.

6. **인코딩** 상자에서 **유니코드**를 선택 합니다.

    > [!IMPORTANT]
    > 이렇게 하면 유니코드 16바이트 순서 마커(`FFFE`)가 텍스트 파일 앞에 추가됩니다.

7. **파일 이름** 상자에서 확장명이 .xsd 인 파일 이름을 만듭니다.

## <a name="see-also"></a>참고자료

- [참조](reference.md)
