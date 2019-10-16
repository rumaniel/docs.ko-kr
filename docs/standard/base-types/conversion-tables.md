---
title: .NET의 형식 변환표
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- widening conversions
- narrowing conversions
- type conversion, table
- converting types, narrowing conversions
- converting types, widening conversions
- base types, converting
- tables [.NET Framework], type conversions
- data types [.NET Framework], converting
ms.assetid: 0ea65c59-85eb-4a52-94ca-c36d3bd13058
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f018ed182e6354bbc6e6873f0df1b35e023c9c17
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54512348"
---
# <a name="type-conversion-tables-in-net"></a>.NET의 형식 변환표
확대 변환은 한 형식의 값을 크기가 같거나 더 큰 다른 형식으로 변환할 때 발생합니다. 축소 변환은 한 형식의 값을 크기가 더 작은 다른 형식의 값으로 변환할 때 발생합니다. 이 항목의 표에서는 두 가지 유형의 변환에서 모두 나타나는 동작을 설명합니다.  
  
## <a name="widening-conversions"></a>확대 변환  
 다음 표에서는 정보 손실 없이 수행할 수 있는 확대 변환에 대해 설명합니다.  
  
|형식|데이터 손실 없이 다음 형식으로 변환할 수 있음|  
|----------|-------------------------------------------|  
|<xref:System.Byte>|<xref:System.UInt16>, <xref:System.Int16>, <xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.SByte>|<xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int16>|<xref:System.Int32>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.UInt16>|<xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Char>|<xref:System.UInt16>, <xref:System.UInt32>, <xref:System.Int32>, <xref:System.UInt64>, <xref:System.Int64>, <xref:System.Single>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int32>|<xref:System.Int64>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.UInt32>|<xref:System.Int64>, <xref:System.UInt64>, <xref:System.Double>, <xref:System.Decimal>|  
|<xref:System.Int64>|<xref:System.Decimal>|  
|<xref:System.UInt64>|<xref:System.Decimal>|  
|<xref:System.Single>|<xref:System.Double>|  
  
 <xref:System.Single> 또는 <xref:System.Double>로의 일부 확대 변환에서는 정밀도 손실이 발생할 수 있습니다. 다음 표에서는 때때로 정보 손실이 발생할 수 있는 확대 변환에 대해 설명합니다.  
  
|형식|다음 형식으로 변환할 수 있음|  
|----------|-------------------------|  
|<xref:System.Int32>|<xref:System.Single>|  
|<xref:System.UInt32>|<xref:System.Single>|  
|<xref:System.Int64>|<xref:System.Single>, <xref:System.Double>|  
|<xref:System.UInt64>|<xref:System.Single>, <xref:System.Double>|  
|<xref:System.Decimal>|<xref:System.Single>, <xref:System.Double>|  
  
## <a name="narrowing-conversions"></a>축소 변환  
 <xref:System.Single> 또는 <xref:System.Double>로의 축소 변환에서는 정보 손실이 발생할 수 있습니다. 대상 형식이 소스 크기를 제대로 표시할 수 없는 경우 결과 형식이 상수 `PositiveInfinity` 또는 `NegativeInfinity`로 설정됩니다. `PositiveInfinity`는 양수를 0으로 나눈 결과이며 <xref:System.Single> 또는 <xref:System.Double> 값이 `MaxValue` 필드 값을 초과하는 경우에도 반환됩니다. `NegativeInfinity`는 음수를 0으로 나눈 결과이며 <xref:System.Single> 또는 <xref:System.Double> 값이 `MinValue` 필드 값보다 작은 경우에도 반환됩니다. <xref:System.Double>에서 <xref:System.Single>로 변환하면 `PositiveInfinity` 또는 `NegativeInfinity`가 발생할 수 있습니다.  
  
 축소 변환 시 다른 데이터 형식에 대한 정보 손실도 발생할 수 있습니다. 그러나 변환 중인 형식의 값이 대상 형식의 `MaxValue` 및 `MinValue` 필드에 지정된 범위를 벗어나면 <xref:System.OverflowException>이 throw되며, 런타임에서 변환을 검사하여 대상 형식의 값이 해당 `MaxValue` 또는 `MinValue`를 초과하지 않는지 확인합니다. <xref:System.Convert?displayProperty=nameWithType> 클래스로 수행하는 변환은 항상 이런 방식으로 검사됩니다.  
  
 다음 표에서는 <xref:System.Convert?displayProperty=nameWithType> 사용 시 <xref:System.OverflowException>을 throw하는 변환 또는 변환 중인 형식의 값이 정의된 결과 형식 범위를 벗어나는지 확인한 모든 변환을 보여줍니다.  
  
|형식|다음 형식으로 변환할 수 있음|  
|----------|-------------------------|  
|<xref:System.Byte>|<xref:System.SByte>|  
|<xref:System.SByte>|<xref:System.Byte>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64>|  
|<xref:System.Int16>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.UInt16>|  
|<xref:System.UInt16>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>|  
|<xref:System.Int32>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>,<xref:System.UInt32>|  
|<xref:System.UInt32>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>|  
|<xref:System.Int64>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>,<xref:System.UInt32>,<xref:System.UInt64>|  
|<xref:System.UInt64>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>|  
|<xref:System.Decimal>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
|<xref:System.Single>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
|<xref:System.Double>|<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.UInt16>, <xref:System.Int32>, <xref:System.UInt32>, <xref:System.Int64>, <xref:System.UInt64>|  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Convert?displayProperty=nameWithType>
- [.NET에서 형식 변환](../../../docs/standard/base-types/type-conversion.md)
