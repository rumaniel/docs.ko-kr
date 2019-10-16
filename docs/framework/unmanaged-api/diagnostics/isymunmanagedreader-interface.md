---
title: ISymUnmanagedReader 인터페이스
ms.date: 03/30/2017
api_name:
- ISymUnmanagedReader
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedReader
helpviewer_keywords:
- ISymUnmanagedReader interface [.NET Framework debugging]
ms.assetid: aa3cc15d-058e-4e6f-b03e-39569646ba47
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0782533f773b69eeeb0b89175e5b22c61e822ed9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61986364"
---
# <a name="isymunmanagedreader-interface"></a>ISymUnmanagedReader 인터페이스
문서, 메서드 및 기호 저장소 내의 변수에 대 한 액세스를 제공 하는 기호 판독기를 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetDocument 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getdocument-method.md)|문서를 찾습니다.|  
|[GetDocuments 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getdocuments-method.md)|기호 저장소에 정의 된 모든 문서의 배열을 반환 합니다.|  
|[GetDocumentVersion 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getdocumentversion-method.md)|지정 된 문서의 지정 된 버전을 가져옵니다.|  
|[GetGlobalVariables 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getglobalvariables-method.md)|모든 전역 변수를 반환합니다.|  
|[GetMethod 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getmethod-method.md)|메서드 토큰을 지정 된 기호 판독기 메서드를 가져옵니다.|  
|[GetMethodByVersion 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getmethodbyversion-method.md)|지정 된 메서드 토큰 및 편집 복사 버전 번호를 기호 판독기 메서드를 가져옵니다.|  
|[GetMethodFromDocumentPosition 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getmethodfromdocumentposition-method.md)|문서에서 지정된 된 위치에 중단점을 포함 하는 메서드를 반환 합니다.|  
|[GetMethodsFromDocumentPosition 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getmethodsfromdocumentposition-method.md)|문서에서 지정된 된 위치에 중단점을 포함 하는 각 메서드의 배열을 반환 합니다.|  
|[GetMethodVersion 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getmethodversion-method.md)|메서드 버전을 가져옵니다.|  
|[GetNamespaces 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getnamespaces-method.md)|이 기호 저장소 내의 전역 범위에서 정의 된 네임 스페이스를 가져옵니다.|  
|[GetSymAttribute 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getsymattribute-method.md)|해당 이름을 기준으로 사용자 지정 특성을 가져옵니다.|  
|[GetSymbolStoreFileName 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getsymbolstorefilename-method.md)|기호 저장소의 디스크에 파일 이름을 제공합니다.|  
|[GetUserEntryPoint 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getuserentrypoint-method.md)|있는 경우 모듈의 사용자 진입점으로 지정 된 메서드를 반환 합니다.|  
|[GetVariables 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-getvariables-method.md)|해당 부모와 이름을 지정 하는 로컬이 아닌 변수를 반환 합니다.|  
|[Initialize 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-initialize-method.md)|이 판독기가 모듈의 파일 이름과 함께, 연결 되는 메타 데이터 가져오기 인터페이스를 사용 하 여 기호 판독기를 초기화 합니다.|  
|[ReplaceSymbolStore 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-replacesymbolstore-method.md)|기존 기호 저장소를 델타 기호 저장소로 바꿉니다.|  
|[UpdateSymbolStore 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-updatesymbolstore-method.md)|기존 기호 저장소를 델타 기호 저장소로 업데이트합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>참고자료

- [진단 기호 저장소 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedReader2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader2-interface.md)
