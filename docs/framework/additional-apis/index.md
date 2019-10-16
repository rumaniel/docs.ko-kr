---
title: 추가 클래스 라이브러리 및 API
ms.date: 01/29/2018
helpviewer_keywords:
- Additional class libraries
- Additional managed libraries
- .NET Framework out-of-band releases
- out-of-band releases
ms.assetid: cf2d9006-b631-4e5d-81cd-20aab78c60f1
author: mairaw
ms.author: mairaw
ms.topic: conceptual
ms.openlocfilehash: 0aed6f32bbd3ffdc9446e9d17be2d90c62444ee1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053251"
---
# <a name="additional-class-libraries-and-apis"></a>추가 클래스 라이브러리 및 API

.NET Framework 지속적으로 진화 하 고 있습니다. 플랫폼 간 개발을 개선 하 고 새로운 기능을 조기에 도입 하기 위해 새로운 기능이 대역 외 (OOB) 출시 됩니다. 이 항목에서는 설명서를 제공하는 OOB 프로젝트를 나열합니다.  
  
또한 일부 라이브러리는 .NET Framework의 구현이나 특정 플랫폼을 대상으로 합니다. 예를 들어 클래스 <xref:System.Text.CodePagesEncodingProvider> 는 .NET Framework을 사용 하 여 개발 된 UWP 앱에서 코드 페이지 인코딩을 사용할 수 있도록 합니다. 이 항목에서는 이러한 라이브러리도 나열됩니다.  
  
## <a name="oob-projects"></a>OOB 프로젝트
  
| 프로젝트 | 설명 |  
| ------- | ----------- |  
| <xref:System.Collections.Immutable> | 해당 내용을 절대로 변경하지 않도록 보장하는 안전한 스레드인 컬렉션을 제공합니다. |
| <xref:System.Net.Http.WinHttpHandler> | Windows의 WinHTTP 인터페이스에 따라 <xref:System.Net.Http.HttpClient> 에 메시지 처리기를 제공합니다. |
| <xref:System.Numerics> | SIMD 하드웨어 기반 가속을 활용할 수 있는 벡터 형식 라이브러리입니다.| 
| <xref:System.Threading.Tasks.Dataflow> | TPL 데이터 흐름 라이브러리는 동시성 사용 애플리케이션의 견고성을 높이는 데 도움이 되는 데이터 흐름 구성 요소를 제공합니다. |  

## <a name="platform-specific-libraries"></a>플랫폼별 라이브러리
  
| 프로젝트 | 설명 |  
| ------- | ----------- |  
| <xref:System.Text.CodePagesEncodingProvider> | <xref:System.Text.EncodingProvider> 클래스를 확장 하 여 유니버설 Windows 플랫폼를 대상으로 하는 앱에서 코드 페이지 인코딩을 사용할 수 있도록 합니다. |  
  
## <a name="private-apis"></a>전용 API  

이러한 API는 제품 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.  
  
| API 이름 |
| -------- |
| [시스템 .Net 연결 클래스](connection.md) |
| [System.Net.Connection.m\_WriteList Field](m_writelist.md) |
| [시스템 .Net ConnectionGroup 클래스](connectiongroup.md) |
| [System.Net.ConnectionGroup.m\_ConnectionList Field](m_connectionlist.md) |
| [CoreResponseData 클래스](coreresponsedata.md) |
| [System.Net.CoreResponseData.m\_ResponseHeaders Field](coreresponsedata_m_responseheaders.md) |
| [System.Net.CoreResponseData.m\_StatusCode Field](coreresponsedata_m_statuscode.md) |
| [시스템 .Net HttpWebRequest. \_AutoRedirects 필드](_autoredirects.md) |
| [시스템 .Net HttpWebRequest. \_CoreResponse 필드](httpwebrequest__coreresponse.md) |
| [시스템 .Net HttpWebRequest. \_Httpresponse.cache 필드](_httpresponse.md) |
| [System.Net.ServicePoint.m\_ConnectionGroupList Field](m_connectiongrouplist.md) |
| [System.Net.ServicePointManager.s\_ServicePointTable Field](s_servicepointtable.md) |
| [System.Windows.Diagnostics.VisualDiagnostics.s\_isDebuggerCheckDisabledForTestPurposes Field](s-isdebuggercheckdisabledfortestpurposes-field.md) |
| [DataMemberFieldEditor 클래스입니다.](datamemberfieldeditor-class.md) |
| [DataMemberListEditor 클래스입니다.](datamemberlisteditor-class.md) |
  
## <a name="see-also"></a>참고자료

- [.NET Framework 및 번외 릴리스](../get-started/the-net-framework-and-out-of-band-releases.md)
