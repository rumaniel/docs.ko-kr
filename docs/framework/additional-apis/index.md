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
ms.openlocfilehash: 84e2d07275194683661a75e422847bbe0ebf1383
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50198369"
---
# <a name="additional-class-libraries-and-apis"></a>추가 클래스 라이브러리 및 API

.NET Framework는 지속적으로 발전 합니다. 플랫폼 간 개발을 개선 하 고 새로운 기능을 일찍 소개를 대역 외 (OOB)에서 새로운 기능이 릴리스됩니다. 이 항목에서는 설명서를 제공하는 OOB 프로젝트를 나열합니다.  
  
또한 일부 라이브러리는 .NET Framework의 구현이나 특정 플랫폼을 대상으로 합니다. 예를 들어를 <xref:System.Text.CodePagesEncodingProvider> 클래스는.NET Framework를 사용 하 여 개발 하는 UWP 앱에 사용할 수 있는 코드 페이지 인코딩을 만듭니다. 이 항목에서는 이러한 라이브러리도 나열됩니다.  
  
## <a name="oob-projects"></a>OOB 프로젝트
  
| 프로젝트 | 설명 |  
| ------- | ----------- |  
| <xref:System.Collections.Immutable> | 해당 내용을 절대로 변경하지 않도록 보장하는 안전한 스레드인 컬렉션을 제공합니다. |
| <xref:System.Net.Http.WinHttpHandler> | Windows의 WinHTTP 인터페이스에 따라 <xref:System.Net.Http.HttpClient> 에 메시지 처리기를 제공합니다. |
| [System.Numerics.Vectors](https://msdn.microsoft.com/library/mt452176.aspx) | SIMD 하드웨어 기반 가속을 활용할 수 있는 벡터 형식 라이브러리입니다.| 
| <xref:System.Threading.Tasks.Dataflow> | TPL 데이터 흐름 라이브러리는 동시성 사용 응용 프로그램의 견고성을 높이는 데 도움이 되는 데이터 흐름 구성 요소를 제공합니다. |  

## <a name="platform-specific-libraries"></a>플랫폼별 라이브러리
  
| 프로젝트 | 설명 |  
| ------- | ----------- |  
| <xref:System.Text.CodePagesEncodingProvider> | 확장 된 <xref:System.Text.EncodingProvider> 클래스 코드 페이지 인코딩을 유니버설 Windows 플랫폼을 대상으로 하는 앱에 사용할 수 있도록 합니다. |  
  
## <a name="private-apis"></a>전용 API  

이러한 API는 제품 인프라를 지원하며 사용자 코드에서 직접 사용할 수 없습니다.  
  
| API 이름 |
| -------- |
| [System.Net.Connection 클래스](../../../docs/framework/additional-apis/connection.md) |
| [System.Net.Connection.m\_WriteList Field](../../../docs/framework/additional-apis/m_writelist.md) |
| [System.Net.ConnectionGroup 클래스](../../../docs/framework/additional-apis/connectiongroup.md) |
| [System.Net.ConnectionGroup.m\_ConnectionList Field](../../../docs/framework/additional-apis/m_connectionlist.md) |
| [System.Net.CoreResponseData 클래스](../../../docs/framework/additional-apis/coreresponsedata.md) |
| [System.Net.CoreResponseData.m\_ResponseHeaders Field](../../../docs/framework/additional-apis/coreresponsedata_m_responseheaders.md) |
| [System.Net.CoreResponseData.m\_StatusCode Field](../../../docs/framework/additional-apis/coreresponsedata_m_statuscode.md) |
| [System.Net.HttpWebRequest 합니다. \_AutoRedirects 필드](../../../docs/framework/additional-apis/_autoredirects.md) |
| [System.Net.HttpWebRequest 합니다. \_CoreResponse 필드](../../../docs/framework/additional-apis/httpwebrequest__coreresponse.md) |
| [System.Net.HttpWebRequest 합니다. \_HttpResponse 필드](../../../docs/framework/additional-apis/_httpresponse.md) |
| [System.Net.ServicePoint.m\_ConnectionGroupList Field](../../../docs/framework/additional-apis/m_connectiongrouplist.md) |
| [System.Net.ServicePointManager.s\_ServicePointTable Field](../../../docs/framework/additional-apis/s_servicepointtable.md) |
| [System.Windows.Diagnostics.VisualDiagnostics.s\_isDebuggerCheckDisabledForTestPurposes Field](../../../docs/framework/additional-apis/s-isdebuggercheckdisabledfortestpurposes-field.md) |
| [System.Windows.Forms.Design.DataMemberFieldEditor 클래스](../../../docs/framework/additional-apis/datamemberfieldeditor-class.md) |
| [System.Windows.Forms.Design.DataMemberListEditor 클래스](../../../docs/framework/additional-apis/datamemberlisteditor-class.md) |
  
## <a name="see-also"></a>참고자료

- [.NET Framework 및 번외 릴리스](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)
