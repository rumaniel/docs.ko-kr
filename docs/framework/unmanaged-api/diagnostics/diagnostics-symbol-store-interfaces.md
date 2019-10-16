---
title: 진단 기호 저장소 인터페이스
ms.date: 03/30/2017
helpviewer_keywords:
- unmanaged interfaces [.NET Framework], debugging
- diagnostics symbol store interfaces [.NET Framework]
- interfaces [.NET Framework], diagnostics symbol store
- unmanaged interfaces [.NET Framework], diagnostics symbol store
- debugging interfaces [.NET Framework]
- interfaces [.NET Framework debugging]
ms.assetid: f96987d5-e6a5-478b-ac5e-302e16545cce
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6fca7359888b8b73b2e1cf709ab708d71abf0db6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61787896"
---
# <a name="diagnostics-symbol-store-interfaces"></a>진단 기호 저장소 인터페이스
이 항목에서는 컴파일러가 디버거에 사용에 대 한 기호 정보를 생성 하는 데 사용할 수 있는 관리 되지 않는 인터페이스를 설명 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [IBindingDisplay 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/ibindingdisplay-interface.md)  
 실행 중인 응용 프로그램에 대 한 현재 바인딩 정보를 표시 하는 메서드를 제공 합니다.  
  
 [IDebugAutoAttach 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/idebugautoattach-interface.md)  
 서버에서 호출한 디버거 자동 연결에 대 한 인터페이스를 정의 합니다.  
  
 [INotifyConnection2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/inotifyconnection2-interface.md)  
 등록 및 연결 알림 소스를 등록 취소에 대 한 메서드를 선언 합니다.  
  
 [INotifySink2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/inotifysink2-interface.md)  
 싱크 알림 위한 메서드를 선언합니다.  
  
 [INotifySource2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/inotifysource2-interface.md)  
 알림 필터를 설정 하는 것에 대 한 메서드를 선언 합니다.  
  
 [ISymENCUnmanagedMethod 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymencunmanagedmethod-interface.md)  
 편집 하며 계속 하기 기능에 대 한 정보를 제공합니다.  
  
 [ISymUnmanagedAsyncMethod 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethod-interface.md)  
 이 인터페이스를 읽기 보수인 [ISymUnmanagedAsyncMethodPropertiesWriter 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethodpropertieswriter-interface.md)합니다.  
  
 [ISymUnmanagedAsyncMethodPropertiesWriter 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedasyncmethodpropertieswriter-interface.md)  
 메서드 기호 별로 표시 되는 선택적 비동기 메서드 정보의 정의 허용합니다. 열린된 메서드를 사용 해야 합니다 (즉, 호출 사이 [OpenMethod 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-openmethod-method.md)하며 [CloseMethod 메서드](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-closemethod-method.md)).  
  
 [ISymUnmanagedBinder 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder-interface.md)  
 비관리 코드의 기호 바인더를 나타냅니다.  
  
 [ISymUnmanagedBinder2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder2-interface.md)  
 비관리 코드의 기호 바인더를 나타냅니다와 확장 된 `ISymUnmanagedBinder` 인터페이스입니다.  
  
 [ISymUnmanagedBinder3 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedbinder3-interface.md)  
 비관리 코드의 기호 바인더를 나타냅니다와 확장 된 `ISymUnmanagedBinder` 인터페이스입니다.  
  
 [ISymUnmanagedConstant 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedconstant-interface.md)  
 관리 되지 않는 상수에 대 한 액세스를 제공합니다.  
  
 [ISymUnmanagedDispose 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddispose-interface.md)  
 관리 되지 않는 리소스를 삭제합니다.  
  
 [ISymUnmanagedDocument 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocument-interface.md)  
 기호 저장소가 참조하는 문서를 나타냅니다.  
  
 [ISymUnmanagedDocumentWriter 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanageddocumentwriter-interface.md)  
 기호 저장소가 참조하는 문서에 쓰기 위한 메서드를 제공합니다.  
  
 [ISymUnmanagedENCUpdate 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedencupdate-interface.md)  
 편집 하며 계속 하기 기능에 대 한 메서드를 제공합니다.  
  
 [ISymUnmanagedMethod 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedmethod-interface.md)  
 기호 저장소 내의 메서드를 나타냅니다.  
  
 [ISymUnmanagedNamespace 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagednamespace-interface.md)  
 네임 스페이스를 나타냅니다.  
  
 [ISymUnmanagedReader 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md)  
 문서, 메서드 및 기호 저장소 내의 변수에 대 한 액세스를 제공 하는 기호 판독기를 나타냅니다.  
  
 [ISymUnmanagedReader2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader2-interface.md)  
 메서드 토큰을 편집 하 고 복사 버전 번호를 지정 하는 기호 판독기 메서드를 가져옵니다.  
  
 [ISymUnmanagedReaderSymbolSearchInfo 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreadersymbolsearchinfo-interface.md)  
 기호 검색 정보를 가져오는 메서드를 제공 합니다.  
  
 [ISymUnmanagedScope 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedscope-interface.md)  
 메서드 내에서 어휘 범위를 나타냅니다.  
  
 [ISymUnmanagedScope2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedscope2-interface.md)  
 인 메서드 내부의 어휘 범위를 나타내며 확장 된 `ISymUnmanagedScope` 범위 내에서 정의 된 상수에 대 한 정보를 가져오는 메서드를 사용 하 여 인터페이스...  
  
 [ISymUnmanagedSourceServerModule 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsourceservermodule-interface.md)  
 모듈에 대 한 원본 서버 데이터를 제공합니다.  
  
 [ISymUnmanagedSymbolSearchInfo 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsymbolsearchinfo-interface.md)  
 검색 경로 대 한 정보를 가져오는 메서드를 제공 합니다.  
  
 [ISymUnmanagedVariable 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedvariable-interface.md)  
 매개 변수, 지역 변수 또는 필드 등의 변수를 나타냅니다.  
  
 [ISymUnmanagedWriter 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-interface.md)  
 기호 작성기를 나타내며 문서 "," 시퀀스 위치 "," 어휘 범위 "및" 변수를 정의 하는 메서드를 제공 합니다.  
  
 [ISymUnmanagedWriter2 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter2-interface.md)  
 기호 작성기를 나타내며 문서 "," 시퀀스 위치 "," 어휘 범위 "및" 변수를 정의 하는 메서드를 제공 합니다. 확장 된 `ISymUnmanagedWriter` 인터페이스입니다.  
  
 [ISymUnmanagedWriter3 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter3-interface.md)  
 기호 작성기를 나타내며 문서 "," 시퀀스 위치 "," 어휘 범위 "및" 변수를 정의 하는 메서드를 제공 합니다. 확장 된 `ISymUnmanagedWriter` 인터페이스입니다.  
  
 [ISymUnmanagedWriter4 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter4-interface.md)  
 ISymUnmanagedWriter4 인터페이스입니다.  
  
 [ISymUnmanagedWriter5 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter5-interface.md)  
 ISymUnmanagedWriter5 인터페이스입니다.  
  
## <a name="related-sections"></a>관련 단원  
 [진단 기호 저장소 열거형](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-enumerations.md)  
  
 [진단 기호 저장소 구조체](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-structures.md)  
  
 [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
