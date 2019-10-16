---
title: IMetaDataTables::GetColumn 메서드
ms.date: 02/25/2019
api_name:
- IMetaDataTables.GetColumn
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataTables::GetColumn
helpviewer_keywords:
- IMetaDataTables::GetColumn method [.NET Framework metadata]
- GetColumn method [.NET Framework metadata]
ms.assetid: 1032055b-cabb-45c5-a50e-7e853201b175
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 853f137d91e1b3eb4f3f65a06522618f8441dcb3
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053672"
---
# <a name="imetadatatablesgetcolumn-method"></a>IMetaDataTables::GetColumn 메서드
지정 된 테이블에 있는 지정 된 열 및 행의 셀에 포함 된 값에 대 한 포인터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetColumn (   
    [in]  ULONG   ixTbl,  
    [in]  ULONG   ixCol,  
    [in]  ULONG   rid,  
    [out] ULONG   *pVal  
);  
```  
  
## <a name="parameters"></a>매개 변수

 `ixTbl`  
 진행 테이블의 인덱스입니다.  
  
 `ixCol`  
 진행 테이블에 있는 열의 인덱스입니다.  
  
 `rid`  
 진행 테이블에 있는 행의 인덱스입니다.  
  
 `pVal`  
 제한이 셀의 값에 대 한 포인터입니다.  
 
## <a name="remarks"></a>설명

를 통해 `pVal` 반환 되는 값의 interpretion는 열의 형식에 따라 달라 집니다. 열 유형은 [IMetaDataTables. GetColumnInfo](imetadatatables-getcolumninfo-method.md)을 호출 하 여 확인할 수 있습니다.

- **Getcolumn** 메서드는 **Rid** 또는 **codedtoken** 형식의 열을 전체 32 비트 `mdToken` 값으로 자동으로 변환 합니다.
- 또한 8 비트 또는 16 비트 값을 자동으로 전체 32 비트 값으로 변환 합니다. 
- *힙* 유형 열의 경우 반환 된 *pVal* 는 해당 힙의 인덱스가 됩니다.

| 열 형식              | pVal contains | 설명                          |
|--------------------------|---------------|-----------------------------------|
| `0`..`iRidMax`<br>(0, 63)  | mdToken     | *pVal* 에는 전체 토큰이 포함 됩니다. 함수는 Rid를 전체 토큰으로 자동으로 변환 합니다. |
| `iCodedToken`..`iCodedTokenMax`<br>(64.95) | mdToken | 반환 될 때 *pVal* 는 전체 토큰을 포함 합니다. 함수는 CodedToken의 압축을 자동으로 전체 토큰으로 만듭니다. |
| `iSHORT`(96)            | Int16         | 자동으로 32 비트에 자동으로 서명 합니다.  |
| `iUSHORT`(97)           | UInt16        | 자동으로 32 비트에 자동으로 서명 합니다.  |
| `iLONG`(98)             | Int32         |                                        | 
| `iULONG`(99)            | UInt32        |                                        |
| `iBYTE`(100)            | Byte          | 자동으로 32 비트에 자동으로 서명 합니다.  |
| `iSTRING`(101)          | 문자열 힙 인덱스 | *pVal* 은 문자열 힙에 대 한 인덱스입니다. [IMetadataTables:: GetString](imetadatatables-getstring-method.md) 를 사용 하 여 실제 열 문자열 값을 가져옵니다. |
| `iGUID`(102)            | Guid 힙 인덱스 | *pVal* 는 Guid 힙의 인덱스입니다. [IMetadataTables:: GetGuid](imetadatatables-getguid-method.md) 를 사용 하 여 실제 열 Guid 값을 가져옵니다. |
| `iBLOB`(103)            | Blob 힙 인덱스 | *pVal* 는 Blob 힙에 대 한 인덱스입니다. [IMetadataTables:: GetBlob](imetadatatables-getblob-method.md) 을 사용 하 여 실제 열 Blob 값을 가져옵니다. |
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor  
  
 **라이브러리** Mscoree.dll에서 리소스로 사용 됩니다.  
  
 **.NET Framework 버전**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataTables 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatatables-interface.md)
- [IMetaDataTables2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatatables2-interface.md)
