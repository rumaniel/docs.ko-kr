---
title: 경합 ETW 이벤트-.NET
ms.date: 03/30/2017
helpviewer_keywords:
- contention events [.NET Framework]
- ETW, contention events (CLR)
ms.assetid: 6933e753-2f2a-425b-ae84-42138c957d76
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 95f56a6c8b51c58ed36d5d0de428bf57b728009c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61723942"
---
# <a name="contention-etw-events"></a>경합 ETW 이벤트

런타임에서 사용되는 <xref:System.Threading.Monitor?displayProperty=nameWithType> 잠금 또는 네이티브 잠금에 대한 경합이 있을 때마다 경합 이벤트가 발생합니다. 스레드가 잠금을 소유하는 동안 또 다른 스레드가 잠금을 기다리고 있으면 경합이 발생합니다.

다음 표에서는 경합 이벤트가 발생하는 키워드 및 이벤트 수준을 보여 줍니다. 자세한 내용은 [CLR ETW 키워드 및 수준](clr-etw-keywords-and-levels.md)합니다.

|이벤트를 발생시키기 위한 키워드|수준|
|-----------------------------------|-----------|
|`ContentionKeyword`(0x4000)|정보(4)|

다음 표에서 이벤트 정보를 보여 줍니다.

|이벤트(event)|이벤트 ID|발생 시기|
|-----------|--------------|-----------------|
|`ContentionStart_V1`|81|경합이 시작됩니다. 이 이벤트에는 스레드가 잠금을 획득하기 위해 대기하기 전의 회전 시간이 포함되지 않습니다. 이 이벤트는 스레드가 잠금을 획득하기 위해 대기하는 경우에만 발생합니다.|
|`ContentionStop`|91|경합이 종료됩니다.|

다음 표에서 이벤트 데이터를 보여 줍니다.

|필드 이름|데이터 형식|설명|
|----------------|---------------|-----------------|
|플래그|win:UInt8|0(관리), 1(네이티브).|
|ClrInstanceID|win:UInt16|CLR 인스턴스의 고유 ID.|

## <a name="see-also"></a>참고자료

- [CLR ETW 이벤트](clr-etw-events.md)
