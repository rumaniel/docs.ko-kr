---
title: 메타데이터 인터페이스
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged interfaces [.NET Framework], metadata
- metadata interfaces [.NET Framework]
- interfaces (.NET Framework metadata]
ms.assetid: f5cdac93-a28c-48ef-8a19-5773376e9e7c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8a704d531b1c49ffe653009e0e90f33b7a126e91
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62049819"
---
# <a name="metadata-interfaces"></a>메타데이터 인터페이스
이 섹션에서는 .NET Framework 형식, 메서드, 필드 등이 노출하는 메타데이터에 대한 액세스를 제공하는 관리되지 않는 인터페이스를 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [ICeeGen 인터페이스](../../../../docs/framework/unmanaged-api/metadata/iceegen-interface.md)  
 동적 코드 컴파일에 대한 메서드를 제공합니다.  
  
 [IHostFilter 인터페이스](../../../../docs/framework/unmanaged-api/metadata/ihostfilter-interface.md)  
 처리할 메타데이터 토큰을 표시하기 위한 런타임 호스트에 대한 메서드를 제공합니다.  
  
 [IMapToken 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imaptoken-interface.md)  
 가져온 메타데이터 서명과 내보낸 메타데이터 서명 간 매핑 기능을 제공합니다.  
  
 [IMetaDataAssemblyEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)  
 CLR(공용 언어 런타임)에서 리소스를 확인하고 소비하는 데 사용되는 자체 설명 모델을 지원하는 메서드를 제공합니다.  
  
 [IMetaDataAssemblyImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md)  
 어셈블리 매니페스트에 액세스하여 이를 검사하는 메서드를 제공합니다.  
  
 [IMetaDataConverter 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataconverter-interface.md)  
 형식 라이브러리를 메타데이터 서명에 매핑하고 서로 변환하는 메서드를 제공합니다.  
  
 [IMetaDataDispenser 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-interface.md)  
 `IMetaDataDispenser`는 사용되지 않습니다. 대신 `IMetaDataDispenserEx`를 사용하세요.  
  
 [IMetaDataDispenserEx 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-interface.md)  
 메타데이터를 만들거나 수정할 메모리 영역을 매핑하는 메서드를 제공합니다.  
  
 [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)  
 현재 정의된 범위에서 어셈블리에 대한 메타데이터를 만들고 수정 및 저장하는 메서드를 제공합니다.  
  
 [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)  
 <xref:System.Type?displayProperty=nameWithType> 형식 매개 변수가 있는 메서드와 생성자의 메타데이터 서명을 정의 및 수정하는 메서드를 제공합니다.  
  
 [IMetaDataError 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataerror-interface.md)  
 어셈블리에 대한 메타데이터 서명을 확인하는 동안 오류를 보고하는 콜백 메커니즘을 제공합니다.  
  
 [IMetaDataFilter 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatafilter-interface.md)  
 이미 수행된 반복 작업을 방지하려고 메타데이터 토큰을 표시 및 필터링하는 메서드를 제공합니다.  
  
 [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)  
 다른 어셈블리에서 형식을 가져오고 조작하는 메서드를 제공합니다.  
  
 [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)  
 제네릭 형식 작업 기능을 제공하도록 `IMetaDataImport`를 확장합니다.  
  
 [IMetaDataInfo 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatainfo-interface.md)  
 디스크에 있는 파일에서 메모리로의 메타데이터 매핑에 대한 정보를 가져오는 메서드를 제공합니다.  
  
 [IMetaDataTables 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatatables-interface.md)  
 테이블에서 메타데이터 정보를 스토리지 및 검색하는 메서드를 제공합니다.  
  
 [IMetaDataTables2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatatables2-interface.md)  
 메타데이터 스트림 작업을 수행하는 메서드를 포함하도록 `IMetaDataTables`를 확장합니다.  
  
 [IMetaDataValidate 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatavalidate-interface.md)  
 메타데이터 서명의 유효성을 검사하는 데 사용할 메서드를 제공합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [메타데이터 전역 정적 함수](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)  
  
 [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)  
  
 [메타데이터 구조체](../../../../docs/framework/unmanaged-api/metadata/metadata-structures.md)  
  
 [메타데이터 공용 구조체](../../../../docs/framework/unmanaged-api/metadata/metadata-unions.md)
