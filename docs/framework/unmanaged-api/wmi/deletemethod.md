---
title: "DeleteMethod 함수 (관리 되지 않는 API 참조)"
description: "DeleteMethod 함수 CIM 클래스 정의에서 지정된 된 메서드를 삭제합니다."
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: reference
api_name: DeleteMethod
api_location: WMINet_Utils.dll
api_type: DLLExport
f1_keywords: DeleteMethod
helpviewer_keywords: DeleteMethod function [.NET WMI and performance counters]
topic_type: Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: d931cb76eeaf19ddeb80bdde412fabeea4b70203
ms.sourcegitcommit: a53799f81351ad9afb3007cd68846ce6aeeb10cb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2017
---
# <a name="deletemethod-function"></a><span data-ttu-id="00dde-103">DeleteMethod 함수</span><span class="sxs-lookup"><span data-stu-id="00dde-103">DeleteMethod function</span></span>
<span data-ttu-id="00dde-104">CIM 클래스 정의에서 지정된 된 메서드를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="00dde-104">Deletes the specified method from a CIM class definition.</span></span>

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
    
## <a name="syntax"></a><span data-ttu-id="00dde-105">구문</span><span class="sxs-lookup"><span data-stu-id="00dde-105">Syntax</span></span>  
  
```  
HRESULT Delete (
   [in] int               vFunc, 
   [in] IWbemClassObject* ptr, 
   [in] LPCWSTR           wszName 
); 
```  

## <a name="parameters"></a><span data-ttu-id="00dde-106">매개 변수</span><span class="sxs-lookup"><span data-stu-id="00dde-106">Parameters</span></span>

`vFunc`  
<span data-ttu-id="00dde-107">[in] 이 매개 변수를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00dde-107">[in] This parameter is unused.</span></span>

`ptr`  
<span data-ttu-id="00dde-108">[in] 에 대 한 포인터는 [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="00dde-108">[in] A pointer to an [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) instance.</span></span>

`wszName`  
<span data-ttu-id="00dde-109">[in] 클래스 테이블에서 제거 하는 메서드의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="00dde-109">[in] The name of the method to remove from the class table.</span></span> <span data-ttu-id="00dde-110">`wszName`유효한 포인터 여야 합니다. `LPCWSTR`합니다.</span><span class="sxs-lookup"><span data-stu-id="00dde-110">`wszName` must be a pointer to a valid `LPCWSTR`.</span></span>

## <a name="return-value"></a><span data-ttu-id="00dde-111">반환 값</span><span class="sxs-lookup"><span data-stu-id="00dde-111">Return value</span></span>

<span data-ttu-id="00dde-112">이 함수에서 반환 되는 다음 값에 정의 된는 *WbemCli.h* 헤더 파일 또는 있습니다를 정의할 수 상수로 코드:</span><span class="sxs-lookup"><span data-stu-id="00dde-112">The following values returned by this function are defined in the *WbemCli.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="00dde-113">상수</span><span class="sxs-lookup"><span data-stu-id="00dde-113">Constant</span></span>  |<span data-ttu-id="00dde-114">값</span><span class="sxs-lookup"><span data-stu-id="00dde-114">Value</span></span>  |<span data-ttu-id="00dde-115">설명</span><span class="sxs-lookup"><span data-stu-id="00dde-115">Description</span></span>  |
|---------|---------|---------|
| `WBEM_E_NOT_FOUND` | <span data-ttu-id="00dde-116">0x80041002</span><span class="sxs-lookup"><span data-stu-id="00dde-116">0x80041002</span></span> | <span data-ttu-id="00dde-117">지정된 된 메서드는 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00dde-117">The specified method does not exist.</span></span> |
| `WBEM_E_OUT_OF_MEMORY` | <span data-ttu-id="00dde-118">0x80041006</span><span class="sxs-lookup"><span data-stu-id="00dde-118">0x80041006</span></span> | <span data-ttu-id="00dde-119">메모리가 부족 하 여 작업을 완료할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00dde-119">There is not enough memory to complete the operation.</span></span> |
| `WBEM_S_NO_ERROR` | <span data-ttu-id="00dde-120">0</span><span class="sxs-lookup"><span data-stu-id="00dde-120">0</span></span> | <span data-ttu-id="00dde-121">함수 호출이 성공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="00dde-121">The function call was successful.</span></span>  |

## <a name="remarks"></a><span data-ttu-id="00dde-122">설명</span><span class="sxs-lookup"><span data-stu-id="00dde-122">Remarks</span></span>

<span data-ttu-id="00dde-123">이 함수에 대 한 호출을 래핑하는 [IWbemClassObject::DeleteMethod](https://msdn.microsoft.com/library/aa391439(v=vs.85).aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="00dde-123">This function wraps a call to the [IWbemClassObject::DeleteMethod](https://msdn.microsoft.com/library/aa391439(v=vs.85).aspx) method.</span></span>

<span data-ttu-id="00dde-124">삭제 방법에 대 한 지원 되지 않습니다 [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) CIM 인스턴스를 가리키는 포인터입니다.</span><span class="sxs-lookup"><span data-stu-id="00dde-124">Method deletion is not supported for [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) pointers that point to CIM instances.</span></span>

## <a name="requirements"></a><span data-ttu-id="00dde-125">요구 사항</span><span class="sxs-lookup"><span data-stu-id="00dde-125">Requirements</span></span>  
 <span data-ttu-id="00dde-126">**플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00dde-126">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="00dde-127">**헤더:** WMINet_Utils.idl</span><span class="sxs-lookup"><span data-stu-id="00dde-127">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="00dde-128">**.NET framework 버전:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="00dde-128">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="00dde-129">참고 항목</span><span class="sxs-lookup"><span data-stu-id="00dde-129">See also</span></span>  
[<span data-ttu-id="00dde-130">WMI 및 성능 카운터 (관리 되지 않는 API 참조)</span><span class="sxs-lookup"><span data-stu-id="00dde-130">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)