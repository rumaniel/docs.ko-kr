---
title: ISymUnmanagedWriter 인터페이스
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter
helpviewer_keywords:
- ISymUnmanagedWriter interface [.NET Framework debugging]
ms.assetid: 7d6733ec-f081-4166-bc17-de09e16dc304
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4ac95cd5b79a2e1762fa9adf29d4d7926ab4ab7a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61986065"
---
# <a name="isymunmanagedwriter-interface"></a>ISymUnmanagedWriter 인터페이스
기호 작성기를 나타내며 문서 "," 시퀀스 위치 "," 어휘 범위 "및" 변수를 정의 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[Abort 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-abort-method.md)|기호 저장소에 기호를 커밋하지 않고 기호 작성기를 닫습니다.|  
|[Close 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-close-method.md)|기호를 기호 저장소에 커밋한 후 기호 작성기를 닫습니다.|  
|[CloseMethod 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-closemethod-method.md)|현재 메서드를 닫습니다. 메서드 종료 되 면 그 없습니다 자세한 기호를 정의할 수 있습니다.|  
|[CloseNamespace 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-closenamespace-method.md)|닫히는 네임 스페이스를 가장 최근에 열립니다.|  
|[CloseScope 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-closescope-method.md)|현재 어휘 범위를 닫습니다.|  
|[DefineConstant 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-defineconstant-method.md)|상수 값에 대 한 이름을 정의합니다.|  
|[DefineDocument 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-definedocument-method.md)|소스 문서를 정의합니다.|  
|[DefineField 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-definefield-method.md)|메서드를 단일 변수를 정의 합니다.|  
|[DefineGlobalVariable 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-defineglobalvariable-method.md)|단일 전역 변수를 정의합니다.|  
|[DefineLocalVariable 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-definelocalvariable-method.md)|현재 어휘 범위에 단일 변수를 정의합니다.|  
|[DefineParameter 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-defineparameter-method.md)|현재 메서드의 단일 매개 변수를 정의합니다.|  
|[DefineSequencePoints 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-definesequencepoints-method.md)|현재 메서드 내에서 시퀀스 위치 그룹을 정의합니다.|  
|[GetDebugInfo 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-getdebuginfo-method.md)|컴파일러가 이식 가능한 실행 파일 (PE) 파일 헤더의 디버그 디렉터리 항목을 작성 하는 데 필요한 정보를 반환 합니다.|  
|[Initialize 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-initialize-method.md)|이 작성기가 연결 될 하는 메타 데이터 내보내기 인터페이스를 설정 하 고 디버깅 기호를 쓸 출력 파일 이름을 설정 합니다.|  
|[Initialize2 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-initialize2-method.md)|이 작성기가 연결 될 하는 메타 데이터 내보내기 인터페이스 설정는 디버깅 기호를 쓸 수 있으며 프로그램 데이터베이스 (PDB) 파일의 최종 위치를 설정 합니다. 출력 파일 이름을 설정 합니다.|  
|[OpenMethod 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-openmethod-method.md)|정보는 기호를 내보내는 메서드를 엽니다.|  
|[OpenNamespace 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-opennamespace-method.md)|새 네임스페이스를 엽니다.|  
|[OpenScope 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-openscope-method.md)|현재 메서드에서 새 어휘 범위를 엽니다.|  
|[RemapToken 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-remaptoken-method.md)|메타 데이터를 내보낼 때 메타 데이터 토큰을 다시 매핑할 된 기호 작성기를에 알립니다.|  
|[SetMethodSourceRange 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-setmethodsourcerange-method.md)|True 이면 시작 및 끝 소스 파일 내의 메서드를 지정합니다.|  
|[SetScopeRange 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-setscoperange-method.md)|지정된 어휘 범위에 대한 오프셋 범위를 정의합니다.|  
|[SetSymAttribute 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-setsymattribute-method.md)|해당 이름을 기준으로 사용자 지정 특성을 정의 합니다.|  
|[SetUserEntryPoint 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-setuserentrypoint-method.md)|이 모듈에 대 한 진입점을 되는 사용자 정의 메서드를 지정 합니다.|  
|[UsingNamespace 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-usingnamespace-method.md)|지정된 된 정규화 된 네임 스페이스 이름이 열린 어휘 범위 내에서 되는 것을 지정 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>참고자료

- [진단 기호 저장소 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-interfaces.md)
- [ISymUnmanagedWriter2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter2-interface.md)
- [ISymUnmanagedWriter3 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter3-interface.md)
