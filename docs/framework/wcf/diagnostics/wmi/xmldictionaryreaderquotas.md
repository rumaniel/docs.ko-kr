---
title: XmlDictionaryReaderQuotas
ms.date: 03/30/2017
ms.assetid: 9b4ca8b4-0a89-4758-97ab-528a8ce18f07
ms.openlocfilehash: f1c12a0a60397a84d4e9ff0241c4182b4511af5c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61858431"
---
# <a name="xmldictionaryreaderquotas"></a>XmlDictionaryReaderQuotas
XmlDictionaryReaderQuotas  
  
## <a name="syntax"></a>구문  
  
```csharp
class XmlDictionaryReaderQuotas  
{  
  sint32 MaxArrayLength;  
  sint32 MaxBytesPerRead;  
  sint32 MaxDepth;  
  sint32 MaxNameTableCharCount;  
  sint32 MaxStringContentLength;  
};  
```  
  
## <a name="methods"></a>메서드  
 XmlDictionaryReaderQuotas 클래스는 메서드를 정의하지 않습니다.  
  
## <a name="properties"></a>속성  
 XmlDictionaryReaderQuotas 클래스에는 다음과 같은 속성이 있습니다.  
  
### <a name="maxarraylength"></a>MaxArrayLength  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 허용된 최대 배열 길이입니다.  
  
### <a name="maxbytesperread"></a>MaxBytesPerRead  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 각 읽기에 대해 반환되는 최대 허용 바이트입니다.  
  
### <a name="maxdepth"></a>MaxDepth  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 각 읽기에 대한 최대 중첩 노드 깊이입니다.  
  
### <a name="maxnametablecharcount"></a>MaxNameTableCharCount  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 표 이름에 허용된 최대 문자 수입니다.  
  
### <a name="maxstringcontentlength"></a>MaxStringContentLength  
 데이터 형식: sint32  
  
 액세스 형식: 읽기 전용  
  
 XML 요소 콘텐츠에 허용되는 최대 문자 수입니다.  
  
## <a name="requirements"></a>요구 사항  
  
|MOF|Servicemodel.mof에 선언되어 있습니다.|  
|---------|-----------------------------------|  
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Xml.XmlDictionaryReaderQuotas>
- <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>
