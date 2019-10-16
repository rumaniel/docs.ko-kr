---
ms.openlocfilehash: 8a92a426ac2c5eee6fba40bfc46281420466d648
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72237417"
---
### <a name="jsonelement-api-changes"></a>JsonElement API 변경 내용

.Net Core 3.0 미리 보기 7부터 일부 <xref:System.Text.Json.JsonElement> API가 검색성 및 사용성을 향상하도록 변경되었습니다.

#### <a name="change-description"></a>변경 내용 설명

.Net Core 3.0 미리 보기 7에서 <xref:System.Text.Json.JsonElement> API가 다음과 같이 검색 및 유용성을 향상하도록 변경되었습니다.

1. 모든 `WriteProperty` 메서드 오버로드가 <xref:System.Text.Json.JsonElement>에서 제거되었습니다. 이는 다음과 같은 코드에 영향을 줍니다.

   ```csharp
   using (JsonDocument doc = JsonDocument.Parse(jsonString))
   {
      JsonElement root = doc.RootElement;
      root.WriteProperty(propertyNameString, writer);
      // ..
      root.WriteProperty(propertyNameSpan, writer);
      // ..
      root.WriteProperty(propertyNameJsonEncoded, writer);
      // ..
      root.WriteProperty(utf8PropertyName, writer);
      //..
   }
   ```

1. `WriteValue`의 이름이 <xref:System.Text.Json.JsonElement.WriteTo%2A>로 바뀌었습니다. 이는 다음과 같은 코드에 영향을 줍니다.

   ```csharp
    using (JsonDocument doc = JsonDocument.Parse(jsonString))
    {
        JsonElement root = doc.RootElement;
        root.WriteValue(writer);
    }
    ```

1. 이제 <xref:System.Text.Json.JsonElement.WriteTo%2A>는 메서드 매개 변수가 `null`인 경우 <xref:System.ArgumentNullException>을 throw합니다.

#### <a name="version-introduced"></a>도입된 버전

3.0 미리 보기 7

#### <a name="recommended-action"></a>권장 작업

코드가 이러한 변경의 영향을 받는 경우 다음을 수행할 수 있습니다.

- <xref:System.Text.Json.JsonElement>에서 `WriteProperty` 오버로드에 대한 대체 API는 없습니다. 대신, <xref:System.Text.Json.JsonElement.WriteTo%2A> 메서드와 함께 <xref:System.Text.Json.Utf8JsonWriter.WritePropertyName%2A?displayProperty=nameWithType> 오버로드 중 하나를 호출하여 동일한 결과를 달성할 수 있습니다. 예:

   ```csharp
   using (JsonDocument doc = JsonDocument.Parse(jsonString))
   {
       JsonElement root = doc.RootElement;
       writer.WritePropertyName(propertyNameString);
       root.WriteTo(writer);
   }
   ```

- `WriteValue` 메서드의 이름을 <xref:System.Text.Json.JsonElement.WriteTo(System.Text.Json.Utf8JsonWriter)>로 바꿉니다. 메서드 매개 변수는 변경되지 않습니다. 예를 들어 이전 코드는 다음과 같이 변경해야 합니다.

   ```csharp
   using (JsonDocument doc = JsonDocument.Parse(jsonString))
   {
       JsonElement root = doc.RootElement;
       root.WriteTo(writer);
   }
   ```

- <xref:System.Text.Json.JsonElement.WriteTo%2A> 메서드에 대한 호출에서 <xref:System.ArgumentNullException>을 처리합니다.

#### <a name="affected-apis"></a>영향을 받는 API

- <xref:System.Text.Json.JsonElement>
- <xref:System.Text.Json.JsonElement.WriteTo%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

- `Overload:System.Text.Json.JsonElement.WriteProperty`
- `M:System.Text.Json.JsonElement.WriteValue(System.Text.Json.Utf8JsonWriter)`

-->
