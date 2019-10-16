---
title: ISymUnmanagedDocument 인터페이스
ms.date: 03/30/2017
api_name:
- ISymUnmanagedDocument
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedDocument
helpviewer_keywords:
- ISymUnmanagedDocument interface [.NET Framework debugging]
ms.assetid: 5c26b366-6e81-467c-9dd0-02dd26fee0a3
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 33213aced635549dd439cf679d89367a71baa7c7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61939778"
---
# <a name="isymunmanageddocument-interface"></a>ISymUnmanagedDocument 인터페이스
기호 저장소가 참조하는 문서를 나타냅니다. 문서는 uniform resource locator (URL) 및 문서 형식 GUID에 따라 정의 됩니다. URL을 사용 하 여 저장 하는 방법에 관계 없이 문서를 찾을 수 있으며 문서 유형 GUID 수 있습니다. 문서 소스를 기호 저장소에 저장 하 고이 인터페이스를 통해 검색할 수 있습니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[FindClosestLine 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-findclosestline-method.md)|줄 시퀀스 위치가 될 수 있고이 문서에 지정 된 시퀀스 위치가 되는 가장 가까운 줄을 반환 합니다.|  
|[GetCheckSum 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-getchecksum-method.md)|체크섬을 가져옵니다.|  
|[GetCheckSumAlgorithmId 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-getchecksumalgorithmid-method.md)|체크섬 알고리즘 식별자를 가져오거나 체크섬이 없는 경우에 모두 0으로 GUID를 반환 합니다.|  
|[GetDocumentType 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-getdocumenttype-method.md)|이 문서의 문서 유형을 가져옵니다.|  
|[GetLanguage 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-getlanguage-method.md)|이 문서의 언어 식별자를 가져옵니다.|  
|[GetLanguageVendor 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-getlanguagevendor-method.md)|이 문서의 언어 공급 업체를 가져옵니다.|  
|[GetSourceLength 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-getsourcelength-method.md)|포함 소스의 길이(바이트)를 가져옵니다.|  
|[GetSourceRange 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-getsourcerange-method.md)|지정 된 버퍼에 지정된 된 포함된 된 소스 범위를 반환합니다.|  
|[GetURL 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-geturl-method.md)|이 문서에 대 한 URL을 반환합니다.|  
|[HasEmbeddedSource 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-hasembeddedsource-method.md)|반환 `true` 문서에 소스가 디버깅 기호;에 포함 되어 있으면 반환이 고, 그렇지 `false`합니다.|  
  
## <a name="see-also"></a>참고자료

- [진단 기호 저장소 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-interfaces.md)
