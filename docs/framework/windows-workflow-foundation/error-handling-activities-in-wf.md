---
title: WF의 오류 처리 활동
ms.date: 03/30/2017
ms.assetid: 24b68bd3-cef5-4413-ab82-2e2625f209aa
ms.openlocfilehash: 410c481745cc62a55a2b6e840d82b01fcc7f5766
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61774025"
---
# <a name="error-handling-activities-in-wf"></a>WF의 오류 처리 활동
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]에서는 오류 처리 및 복구를 구현하기 위해 여러 시스템 제공 활동을 제공합니다. 자세한 내용은 [예외](exceptions.md)에 정의된 인터페이스의 private C++ 관련 구현입니다.  
  
## <a name="error-handling-activities"></a>오류 처리 작업  
  
|||  
|-|-|  
|<xref:System.Activities.Statements.Rethrow>|`TryCatch` 활동에서 throw된 마지막 예외를 다시 throw합니다.|  
|<xref:System.Activities.Statements.Throw>|예외를 throw합니다.|  
|<xref:System.Activities.Statements.TryCatch>|예외 처리를 구현합니다.|
