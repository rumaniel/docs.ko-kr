---
title: 여러 형식의 배열 마샬링
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- marshaling, Arrays sample
- data marshaling, Arrays sample
ms.assetid: c5ac9920-5b6e-4dc9-bf2d-1f6f8ad3b0bf
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b0c71284fbc925aa9bb10a8bf68cef581f78d7f4
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50088756"
---
# <a name="marshaling-different-types-of-arrays"></a>여러 형식의 배열 마샬링
배열은 동일한 형식의 요소를 하나 이상 포함하는 관리 코드의 참조 형식입니다. 배열은 참조 형식이지만 관리되지 않는 함수에 In 매개 변수로 전달됩니다. 이 동작은 관리되는 배열이 관리되는 개체에 전달되는 방식(In/Out 매개 변수로)과 일치하지 않습니다. 자세한 내용은 [복사 및 고정](copying-and-pinning.md)을 참조하세요.  
  
 다음 표에서는 배열에 대한 마샬링 옵션을 나열하고 사용법을 설명합니다.  
  
|배열|설명|  
|-----------|-----------------|  
|값 형식 정수.|정수 배열을 In 매개 변수로 전달합니다.|  
|참조 형식 정수.|정수 배열을 In/Out 매개 변수로 전달합니다.|  
|값 형식 정수(2차원).|정수 행렬을 In 매개 변수로 전달합니다.|  
|값 형식 문자열.|문자열 배열을 In 매개 변수로 전달합니다.|  
|정수를 포함하는 구조체.|정수를 포함하는 구조체 배열을 In 매개 변수로 전달합니다.|  
|문자열을 포함하는 구조체.|정수만 포함하는 구조체 배열을 In/Out 매개 변수로 전달합니다. 배열의 멤버를 변경할 수 있습니다.|  
  
## <a name="example"></a>예  
 이 샘플에서는 다음 형식의 배열을 전달하는 방법을 보여 줍니다.  
  
-   값 형식 정수 배열  
  
-   크기를 조정할 수 있는 참조 형식 정수 배열  
  
-   값 형식 정수의 다차원 배열(행렬)  
  
-   값 형식 문자열 배열  
  
-   정수를 포함하는 구조체 배열  
  
-   문자열을 포함하는 구조체 배열  
  
 배열이 참조에 의해 명시적으로 마샬링되지 않은 한 기본 동작은 배열을 In 매개 변수로 마샬링합니다. <xref:System.Runtime.InteropServices.InAttribute> 및 <xref:System.Runtime.InteropServices.OutAttribute> 특성을 명시적으로 적용하면 이 동작을 변경할 수 있습니다.  
  
 Arrays 샘플에서는 원래 함수 선언과 함께 표시되는 다음과 같은 관리되지 않는 함수를 사용합니다.  
  
-   PinvokeLib.dll에서 내보낸**TestArrayOfInts**   
  
    ```  
    int TestArrayOfInts(int* pArray, int pSize);  
    ```  
  
-   PinvokeLib.dll에서 내보낸**TestRefArrayOfInts**   
  
    ```  
    int TestRefArrayOfInts(int** ppArray, int* pSize);  
    ```  
  
-   PinvokeLib.dll에서 내보낸**TestMatrixOfInts**   
  
    ```  
    int TestMatrixOfInts(int pMatrix[][COL_DIM], int row);  
    ```  
  
-   PinvokeLib.dll에서 내보낸**TestArrayOfStrings**   
  
    ```  
    int TestArrayOfStrings(char** ppStrArray, int size);  
    ```  
  
-   PinvokeLib.dll에서 내보낸**TestArrayOfStructs**   
  
    ```  
    int TestArrayOfStructs(MYPOINT* pPointArray, int size);  
    ```  
  
-   PinvokeLib.dll에서 내보낸**TestArrayOfStructs2**   
  
    ```  
    int TestArrayOfStructs2 (MYPERSON* pPersonArray, int size);  
    ```  
  
 [PinvokeLib.dll](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/as6wyhwt(v=vs.100)) 은 앞에 나열된 함수 및 2개의 구조체 변수 **MYPOINT** 및 **MYPERSON**에 대한 구현을 포함하는 관리되지 않는 사용자 지정 라이브러리입니다. 구조체에는 다음과 같은 요소가 포함됩니다.  
  
```  
typedef struct _MYPOINT  
{  
   int x;   
   int y;   
} MYPOINT;  
  
typedef struct _MYPERSON  
{  
   char* first;   
   char* last;   
} MYPERSON;  
```  
  
 이 샘플에서 `MyPoint` 및 `MyPerson` 구조체에는 포함된 형식이 있습니다. <xref:System.Runtime.InteropServices.StructLayoutAttribute> 특성이 설정되어 멤버가 표시되는 순서대로 순차적으로 메모리에 정렬되게 합니다.  
  
 `LibWrap` 클래스에는 `App` 클래스가 호출하는 메서드 집합이 포함됩니다. 배열을 전달하는 방법에 대한 자세한 내용은 다음 샘플의 설명을 참조하세요. 참조 형식인 배열은 기본적으로 In 매개 변수로 전달됩니다. 호출자가 결과를 받으려면 배열을 포함하는 인수에 **InAttribute** 및 **OutAttribute** 를 명시적으로 적용해야 합니다.  
  
### <a name="declaring-prototypes"></a>프로토타입 선언  
 [!code-csharp[Conceptual.Interop.Marshaling#31](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/arrays.cs#31)]
 [!code-vb[Conceptual.Interop.Marshaling#31](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/arrays.vb#31)]  
  
### <a name="calling-functions"></a>함수 호출  
 [!code-csharp[Conceptual.Interop.Marshaling#32](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interop.marshaling/cs/arrays.cs#32)]
 [!code-vb[Conceptual.Interop.Marshaling#32](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interop.marshaling/vb/arrays.vb#32)]  
  
## <a name="see-also"></a>참고 항목  
 [형식 배열 마샬링](https://msdn.microsoft.com/library/049b1c1b-228f-4445-88ec-91bc7fd4b1e8(v=vs.100))  
 [플랫폼 호출 데이터 형식](https://msdn.microsoft.com/library/16014d9f-d6bd-481e-83f0-df11377c550f(v=vs.100))  
 [관리 코드에서 프로토타입 만들기](creating-prototypes-in-managed-code.md)
