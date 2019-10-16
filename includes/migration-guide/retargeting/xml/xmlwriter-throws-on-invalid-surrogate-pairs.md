---
ms.openlocfilehash: b7f31060fd845f7618479fd064350b3cb5532fd3
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804471"
---
### <a name="xmlwriter-throws-on-invalid-surrogate-pairs"></a>잘못된 서로게이트 쌍에서 XmlWriter가 throw함

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5.2 또는 이전 버전을 대상으로 하는 앱의 경우 예외 대체(fallback) 처리를 사용하여 잘못된 서로게이트 쌍을 작성해도 항상 예외가 발생하지는 않습니다. .NET Framework 4.6을 대상으로 하는 앱의 경우 잘못된 서로게이트 쌍을 쓰려고 하면 <xref:System.ArgumentException?displayProperty=name>을 throw합니다.|
|제안 해결 방법|필요한 경우 .NET Framework 4.5.2 이전 버전을 대상으로 하여 이 중단을 피할 수 있습니다. 또는 잘못된 서로게이트 쌍을 쓰기 전에 유효한 xml로 사전 처리할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.6|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Xml.XmlWriter.WriteAttributeString(System.String,System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteAttributeString(System.String,System.String,System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteAttributeString(System.String,System.String,System.String,System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteAttributeStringAsync(System.String,System.String,System.String,System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteCData(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteCDataAsync(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteChars(System.Char[],System.Int32,System.Int32)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteCharsAsync(System.Char[],System.Int32,System.Int32)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteComment(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteCommentAsync(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteEntityRef(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteEntityRefAsync(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteRaw(System.Char[],System.Int32,System.Int32)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteProcessingInstruction(System.String,System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteProcessingInstructionAsync(System.String,System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteRaw(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteRawAsync(System.Char[],System.Int32,System.Int32)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteRawAsync(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteString(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteStringAsync(System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteSurrogateCharEntity(System.Char,System.Char)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteSurrogateCharEntityAsync(System.Char,System.Char)?displayProperty=nameWithType></li><li><xref:System.Xml.XmlWriter.WriteValue(System.String)?displayProperty=nameWithType></li></ul>|

