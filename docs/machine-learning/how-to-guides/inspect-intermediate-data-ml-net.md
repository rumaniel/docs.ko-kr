---
title: ML.NET을 처리하는 동안 중간 데이터 검사
description: ML.NET에서 ML.NET 기계 학습 파이프라인 로딩, 처리 및 모델 학습 단계 중에 중간 데이터를 검사하는 방법을 알아봅니다.
ms.date: 06/25/2019
author: luisquintanilla
ms.author: luquinta
ms.custom: mvc, how-to, title-hack-0625
ms.openlocfilehash: d6ddeb523fb229eb0ebc9c2f22809312060e4266
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67402386"
---
# <a name="inspect-intermediate-data-during-processing"></a>처리하는 동안 중간 데이터 검사

ML.NET에서 로딩, 처리 및 모델 학습 단계 중에 중간 데이터를 검사하는 방법을 알아봅니다. 중간 데이터는 기계 학습 파이프라인에 있는 각 스테이지의 출력입니다.

아래에 표시된 것과 같이 [`IDataView`](xref:Microsoft.ML.IDataView)에 로드되는 중간 데이터는 ML.NET에서 여러 가지 방법으로 검사할 수 있습니다.
 
```csharp
HousingData[] housingData = new HousingData[]
{
    new HousingData
    {
        Size = 600f,
        HistoricalPrices = new float[] { 100000f ,125000f ,122000f },
        CurrentPrice = 170000f
    },
    new HousingData
    {
        Size = 1000f,
        HistoricalPrices = new float[] { 200000f, 250000f, 230000f },
        CurrentPrice = 225000f
    },
    new HousingData
    {
        Size = 1000f,
        HistoricalPrices = new float[] { 126000f, 130000f, 200000f },
        CurrentPrice = 195000f
    },
    new HousingData
    {
        Size = 850f,
        HistoricalPrices = new float[] { 150000f,175000f,210000f },
        CurrentPrice = 205000f
    },
    new HousingData
    {
        Size = 900f,
        HistoricalPrices = new float[] { 155000f, 190000f, 220000f },
        CurrentPrice = 210000f
    },
    new HousingData
    {
        Size = 550f,
        HistoricalPrices = new float[] { 99000f, 98000f, 130000f },
        CurrentPrice = 180000f
    }
};
```

## <a name="convert-idataview-to-ienumerable"></a>IDataView를 IEnumerable로 변환

[`IDataView`](xref:Microsoft.ML.IDataView)를 검사하는 가장 빠른 방법 중 하나는 [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601)로 변환하는 것입니다. [`IDataView`](xref:Microsoft.ML.IDataView)를 [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601)로 변환하려면 [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*) 메서드를 사용합니다. 

성능을 최적화하려면 `reuseRowObject`를 `true`로 설정합니다. 이렇게 하면 데이터 세트에서 각각의 행에 대해 새 개체를 만드는 것과는 반대로 평가되고 있는 현재 행의 데이터로 같은 개체를 지연 입력합니다.

```csharp
// Create an IEnumerable of HousingData objects from IDataView
IEnumerable<HousingData> housingDataEnumerable =
    mlContext.Data.CreateEnumerable<HousingData>(data, reuseRowObject: true);

// Iterate over each row
foreach (HousingData row in housingDataEnumerable)
{
    // Do something (print out Size property) with current Housing Data object being evaluated
    Console.WriteLine(row.Size);
}
```

## <a name="accessing-specific-indices-with-ienumerable"></a>IEnumerable을 사용하여 특정 인덱스에 액세스

데이터나 특정 인덱스의 일부에만 액세스해야 할 경우 [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*)을 사용하고 `reuseRowObject` 매개 변수 값을 `false`로 설정하여 데이터 세트에서 요청된 각 행에 대해 새 개체를 만듭니다. 그런 다음, [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601)을 배열 또는 목록으로 변환합니다.

> [!WARNING]
> [`CreateEnumerable`](xref:Microsoft.ML.DataOperationsCatalog.CreateEnumerable*)의 결과를 배열 또는 목록으로 변환하면 요청된 모든 [`IDataView`](xref:Microsoft.ML.IDataView) 행이 메모리에 로드되어 성능에 영향을 미칠 수 있습니다.

컬렉션을 만든 후에는 데이터에 대해 작업을 수행할 수 있습니다. 아래 코드 조각에서는 데이터 세트의 처음 세 행을 취하여 평균 현재 가격을 계산합니다.

```csharp
// Create an Array of HousingData objects from IDataView
HousingData[] housingDataArray =
    mlContext.Data.CreateEnumerable<HousingData>(data, reuseRowObject: false)
        .Take(3)
        .ToArray();

// Calculate Average CurrentPrice of First Three Elements
HousingData firstRow = housingDataArray[0];
HousingData secondRow = housingDataArray[1];
HousingData thirdRow = housingDataArray[2];
float averageCurrentPrice = (firstRow.CurrentPrice + secondRow.CurrentPrice + thirdRow.CurrentPrice) / 3;
``` 

## <a name="inspect-values-in-a-single-column"></a>단일 열의 값 검사

모델 빌드 프로세스 중 어디서나 [`IDataView`](xref:Microsoft.ML.IDataView)의 단일 열에 있는 값은 [`GetColumn`](xref:Microsoft.ML.Data.ColumnCursorExtensions.GetColumn*) 메서드를 사용하여 액세스할 수 있습니다. [`GetColumn`](xref:Microsoft.ML.Data.ColumnCursorExtensions.GetColumn*) 메서드는 모든 값을 한 열에 [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601)으로 반환합니다.

```csharp
IEnumerable<float> sizeColumn = data.GetColumn<float>("Size").ToList();
```

## <a name="inspect-idataview-values-one-row-at-a-time"></a>한 번에 한 행씩 IDataView 값 검사

[`IDataView`](xref:Microsoft.ML.IDataView)는 지연 계산됩니다. 이 문서의 이전 섹션에서 설명한 대로 [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601)로 변환하지 않고 [`IDataView`](xref:Microsoft.ML.IDataView) 행에 대해 반복하려면 [`GetRowCursor`](xref:Microsoft.ML.IDataView.GetRowCursor*) 메서드를 사용하여 [`DataViewRowCursor`](xref:Microsoft.ML.DataViewRowCursor)를 만들고 [`IDataView`](xref:Microsoft.ML.IDataView)의 [DataViewSchema](xref:Microsoft.ML.DataViewSchema)를 매개 변수로 전달합니다. 그런 다음, 행에 대해 반복하기 위해 [`MoveNext`](xref:Microsoft.ML.DataViewRowCursor.MoveNext*) 커서 메서드를 [`ValueGetter`](xref:Microsoft.ML.ValueGetter%601) 대리자와 함께 사용하여 각 열에서 해당 값을 추출합니다.

> [!IMPORTANT]
> 성능을 위해 ML.NET에서 사용하는 벡터는 네이티브 컬렉션 형식(즉 `Vector`,`float[]`)이 아닌 [`VBuffer`](xref:Microsoft.ML.Data.VBuffer%601)입니다. 

```csharp
// Get DataViewSchema of IDataView
DataViewSchema columns = data.Schema;

// Create DataViewCursor
using (DataViewRowCursor cursor = data.GetRowCursor(columns))
{
    // Define variables where extracted values will be stored to
    float size = default;
    VBuffer<float> historicalPrices = default;
    float currentPrice = default;

    // Define delegates for extracting values from columns
    ValueGetter<float> sizeDelegate = cursor.GetGetter<float>(columns[0]);
    ValueGetter<VBuffer<float>> historicalPriceDelegate = cursor.GetGetter<VBuffer<float>>(columns[1]);
    ValueGetter<float> currentPriceDelegate = cursor.GetGetter<float>(columns[2]);
    
    // Iterate over each row
    while (cursor.MoveNext())
    {
        //Get values from respective columns
        sizeDelegate.Invoke(ref size);
        historicalPriceDelegate.Invoke(ref historicalPrices);
        currentPriceDelegate.Invoke(ref currentPrice);
    }
}
```

## <a name="preview-result-of-pre-processing-or-training-on-a-subset-of-the-data"></a>데이터 하위 집합에 대한 사전 처리 또는 학습 결과 미리 보기

> [!WARNING]
> `Preview`는 디버깅용으로 성능이 저하될 수 있으므로 프로덕션 코드에는 사용할 수 있습니다.

모델 빌드 프로세스는 실험적인 반복 작업입니다. 데이터 하위 집합에 대한 사전 처리나 기계 학습 모델 교육 후 데이터가 어떻게 되는지 미리 보려면 [`DataDebuggerPreview`](xref:Microsoft.ML.Data.DataDebuggerPreview)를 반환하는 [`Preview`](xref:Microsoft.ML.DebuggerExtensions.Preview*) 메서드를 사용합니다. 결과는 `ColumnView` 및 `RowView` 속성이 있는 개체로, 모두 [`IEnumerable`](xref:System.Collections.Generic.IEnumerable%601)이며 특정 열이나 행에 값을 포함합니다. `maxRows` 매개 변수를 통해 변환을 적용할 행 수를 지정합니다.

![데이터 디버거 미리 보기 개체](./media/inspect-intermediate-data-ml-net/data-debugger-preview-01.png)

[`IDataView`](xref:Microsoft.ML.IDataView) 검사 결과는 다음과 비슷하게 표시됩니다.

![데이터 디버거 미리 보기 행 보기](./media/inspect-intermediate-data-ml-net/data-debugger-preview-02.png)
