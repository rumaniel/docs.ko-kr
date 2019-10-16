---
title: 배열에 대한 기본 마샬링
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- interop marshaling, arrays
- arrays, interop marshaling
ms.assetid: 8a3cca8b-dd94-4e3d-ad9a-9ee7590654bc
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 96300808ba3024a138678494200b10ef722c6fd9
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894240"
---
# <a name="default-marshaling-for-arrays"></a>배열에 대한 기본 마샬링
전체적으로 관리 코드로 구성된 애플리케이션에서는 공용 언어 런타임이 배열 형식을 In/Out 매개 변수로 전달합니다. 반면 interop 마샬러는 기본적으로 배열을 In 매개 변수로 전달합니다.  
  
 [고정 최적화](copying-and-pinning.md)를 통해 blittable 배열은 같은 아파트의 개체와 상호 작용할 때 In/Out 매개 변수로 사용되는 것으로 보일 수 있습니다. 그러나 나중에 컴퓨터 간 프록시를 생성하는 데 사용되는 형식 라이브러리에 코드를 내보내고 해당 라이브러리를 사용하여 아파트 간에 호출을 마샬링할 경우 호출은 실제 In 매개 변수 동작으로 되돌아갈 수 있습니다.  
  
 배열은 본질적으로 복잡하고 관리되는 배열과 관리되지 않는 배열을 구별하면 다른 비 blittable 형식보다 더 많은 정보를 보장합니다.  
  
## <a name="managed-arrays"></a>관리되는 배열  
 관리되는 배열 형식은 달라질 수 있지만 <xref:System.Array?displayProperty=nameWithType> 클래스는 모든 배열 형식의 기본 클래스입니다. **System.Array** 클래스에는 배열의 순위, 길이 및 하한/상한을 결정하기 위한 속성과 배열을 액세스, 정렬, 검색, 복사, 생성하기 위한 메서드가 있습니다.  
  
 이러한 배열 형식의 경우 동적이고 기본 클래스 라이브러리에서 정의된 해당 정적 형식이 없습니다. 각 요소 형식 및 순위의 조합을 개별 배열 형식으로 생각하면 편리합니다. 따라서 정수의 1차원 배열은 double 형식의 1차원 배열과 형식이 다릅니다. 마찬가지로 정수의 2차원 배열은 정수의 1차원 배열과 다릅니다. 형식을 비교할 경우 배열의 경계를 고려하지 않습니다.  
  
 다음 표와 같이 관리되는 배열의 인스턴스에는 특수 요소 형식, 순위 및 하한이 있어야 합니다.  
  
|관리되는 배열 형식|요소 형식|순위|하한|시그니처 표기법|  
|------------------------|------------------|----------|-----------------|------------------------|  
|**ELEMENT_TYPE_ARRAY**|형식으로 지정됩니다.|순위로 지정됩니다.|필요한 경우 경계로 지정됩니다.|*type* **[** *n*,*m* **]**|  
|**ELEMENT_TYPE_CLASS**|알 수 없음|알 수 없음|알 수 없음|**System.Array**|  
|**ELEMENT_TYPE_SZARRAY**|형식으로 지정됩니다.|1|0|*type* **[** *n* **]**|  
  
## <a name="unmanaged-arrays"></a>관리되지 않는 배열  
 관리되지 않는 배열은 고정 또는 가변 길이가 포함된 COM 스타일 안전 배열 또는 C 스타일 배열입니다. 안전 배열은 연결된 배열 데이터의 형식, 순위 및 경계를 제공하는 자체 설명 배열입니다. C 스타일 배열은 고정 하한이 0인 1차원 형식 배열입니다. 마샬링 서비스는 두 가지 배열 형식에 대한 지원을 모두 제한했습니다.  
  
## <a name="passing-array-parameters-to-net-code"></a>.NET 코드에 배열 매개 변수 전달  
 C 스타일 배열 및 안전 배열은 둘 다 비관리 코드에서 안전 배열 또는 C 스타일 배열로 .NET 코드에 전달될 수 있습니다. 다음 표에서는 관리되지 않는 형식 값과 가져온 형식을 보여 줍니다.  
  
|관리되지 않는 형식|가져온 형식|  
|--------------------|-------------------|  
|**SafeArray(** *Type* **)**|**ELEMENT_TYPE_SZARRAY** **\<** *ConvertedType* **>**<br /><br /> 순위 = 1, 하한 = 0. 관리되는 시그니처에서 제공된 경우에만 크기가 알려집니다. 순위 = 1 또는 하한 = 0이 아닌 안전 배열은 **SZARRAY**로 마샬링될 수 없습니다.|  
|*Type*  **[]**|**ELEMENT_TYPE_SZARRAY** **\<** *ConvertedType* **>**<br /><br /> 순위 = 1, 하한 = 0. 관리되는 시그니처에서 제공된 경우에만 크기가 알려집니다.|  
  
### <a name="safe-arrays"></a>안전 배열  
 안전 배열을 형식 라이브러리에서 .NET 어셈블리로 가져온 경우 배열은 알려진 형식(예: **int**)의 1차원 배열로 변환됩니다. 매개 변수에 적용되는 같은 형식 변환 규칙이 배열 요소에도 적용됩니다. 예를 들어 **BSTR** 형식의 안전 배열은 문자열의 관리되는 배열이 되고 변형의 안전 배열은 개체의 관리되는 배열이 됩니다. **SAFEARRAY** 요소 형식은 형식 라이브러리에서 캡처되고 <xref:System.Runtime.InteropServices.UnmanagedType> 열거형의 **SAFEARRAY** 값에 저장됩니다.  
  
 형식 라이브러리에서 안전 배열의 순위와 범위를 확인할 수 없으므로 순위는 1로, 하한은 0으로 가정됩니다. [형식 라이브러리 가져오기(Tlbimp.exe)](../tools/tlbimp-exe-type-library-importer.md)에서 생성하는 관리되는 시그니처에 순위와 범위를 정의해야 합니다. 런타임에 메서드에 전달되는 순위가 다른 경우 <xref:System.Runtime.InteropServices.SafeArrayRankMismatchException>이 throw됩니다. 런타임에 전달되는 배열 형식이 다른 경우 <xref:System.Runtime.InteropServices.SafeArrayTypeMismatchException>이 throw됩니다. 다음 예제에서는 관리 및 비관리 코드의 안전 배열을 보여 줍니다.  
  
 **관리되지 않는 시그니처**  
  
```cpp
HRESULT New1([in] SAFEARRAY( int ) ar);  
HRESULT New2([in] SAFEARRAY( DATE ) ar);  
HRESULT New3([in, out] SAFEARRAY( BSTR ) *ar);  
```  
  
 **관리되는 시그니처**  
  
```vb  
Sub New1(<MarshalAs(UnmanagedType.SafeArray, SafeArraySubType:=VT_I4)> _  
   ar() As Integer)  
Sub New2(<MarshalAs(UnmanagedType.SafeArray, SafeArraySubType:=VT_DATE)> _   
   ar() As DateTime)  
Sub New3(ByRef <MarshalAs(UnmanagedType.SafeArray, SafeArraySubType:=VT_BSTR)> _   
   ar() As String)  
```  
  
```csharp  
void New1([MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VT_I4)] int[] ar) ;  
void New2([MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VT_DATE)]   
   DateTime[] ar);  
void New3([MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VT_BSTR)]   
   ref String[] ar);  
```  
  
 Tlbimp.exe에서 생성된 메서드 시그니처가 **ELEMENT_TYPE_SZARRAY** 대신 **ELEMENT_TYPE_ARRAY**의 요소 형식을 나타내도록 수정될 경우 다차원 또는 0이 아닌 경계 안전 배열은 관리 코드로 마샬링될 수 있습니다. 또는 Tlbimp.exe에서 **/sysarray** 스위치를 사용하여 모든 배열을 <xref:System.Array?displayProperty=nameWithType> 개체로 가져올 수 있습니다. 전달되는 배열이 다차원으로 알려진 경우에는 Tlbimp.exe에서 생성된 MSIL(Microsoft Intermediate Language) 코드를 편집하고 다시 컴파일할 수 있습니다. MSIL 코드를 수정하는 방법에 대한 자세한 내용은 [런타임 호출 가능 래퍼 사용자 지정](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100))을 참조하세요.  
  
### <a name="c-style-arrays"></a>C 스타일 배열  
 C 스타일 배열을 형식 라이브러리에서 .NET 어셈블리로 가져온 경우 배열은 **ELEMENT_TYPE_SZARRAY**로 변환됩니다.  
  
 배열 요소 형식은 형식 라이브러리에서 결정되고 가져오는 동안 보존됩니다. 매개 변수에 적용되는 같은 변환 규칙이 배열 요소에도 적용됩니다. 예를 들어 **LPStr** 형식 배열은 **String** 형식 배열이 됩니다. Tlbimp.exe는 배열 형식을 캡처하고 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성을 매개 변수에 적용합니다.  
  
 배열 순위는 1과 같은 것으로 가정합니다. 순위가 1보다 크면 배열은 열 중심 순서에서 1차원 배열로 마샬링됩니다. 하한은 항상 0과 같습니다.  
  
 형식 라이브러리에는 고정 또는 가변 길이의 배열이 포함될 수 있습니다. 형식 라이브러리에는 가변 길이 배열을 마샬링하는 데 필요한 정보가 없으므로 Tlbimp.exe는 형식 라이브러리에서 고정 길이 배열만 가져올 수 있습니다. 고정 길이 배열에서 크기는 형식 라이브러리에서 가져오고 매개 변수에 적용되는 **MarshalAsAttribute**에서 캡처합니다.  
  
 다음 예제와 같이 가변 길이 배열이 포함된 형식 라이브러리를 수동으로 정의해야 합니다.  
  
 **관리되지 않는 시그니처**  
  
```cpp
HRESULT New1(int ar[10]);  
HRESULT New2(double ar[10][20]);  
HRESULT New3(LPWStr ar[10]);  
```  
  
 **관리되는 시그니처**  
  
```vb  
Sub New1(<MarshalAs(UnmanagedType.LPArray, SizeConst=10)> _  
   ar() As Integer)  
Sub New2(<MarshalAs(UnmanagedType.LPArray, SizeConst=200)> _  
   ar() As Double)  
Sub New2(<MarshalAs(UnmanagedType.LPArray, _  
   ArraySubType=UnmanagedType.LPWStr, SizeConst=10)> _  
   ar() As String)  
```  
  
```csharp  
void New1([MarshalAs(UnmanagedType.LPArray, SizeConst=10)] int[] ar);  
void New2([MarshalAs(UnmanagedType.LPArray, SizeConst=200)] double[] ar);  
void New2([MarshalAs(UnmanagedType.LPArray,   
   ArraySubType=UnmanagedType.LPWStr, SizeConst=10)] String[] ar);  
```  
  
 IDL(Interface Definition Language) 소스의 배열에 **size_is** 또는 **length_is** 특성을 적용하여 클라이언트에 크기를 전달할 수 있지만 MIDL(Microsoft 인터페이스 정의 언어) 컴파일러는 해당 정보를 형식 라이브러리에 전파하지 않습니다. 크기를 모르면 interop 마샬링 서비스가 배열 요소를 마샬링할 수 없습니다. 따라서 가변 길이 배열은 참조 인수로 가져옵니다. 예:  
  
 **관리되지 않는 시그니처**  
  
```cpp
HRESULT New1(int ar[]);  
HRESULT New2(int ArSize, [size_is(ArSize)] double ar[]);  
HRESULT New3(int ElemCnt, [length_is(ElemCnt)] LPStr ar[]);  
```  
  
 **관리되는 시그니처**  
  
```vb  
Sub New1(ByRef ar As Integer)  
Sub New2(ByRef ar As Double)  
Sub New3(ByRef ar As String)  
```  
  
```csharp  
void New1(ref int ar);    
void New2(ref double ar);    
void New3(ref String ar);   
```  
  
 Tlbimp.exe에서 생성된 MSIL(Microsoft Intermediate Language) 코드를 편집하고 다시 컴파일하여 마샬러에 배열을 제공할 수 있습니다. MSIL 코드를 수정하는 방법에 대한 자세한 내용은 [런타임 호출 가능 래퍼 사용자 지정](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/e753eftz(v=vs.100))을 참조하세요. 배열의 요소 수를 지정하려면 다음 방법 중 하나로 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 형식을 관리되는 메서드 정의의 배열 매개 변수에 적용합니다.  
  
- 배열의 요소 수가 포함된 또 다른 매개 변수를 식별합니다. 매개 변수는 위치로 식별되고 첫 번째 매개 변수는 0입니다.     
  
    ```vb  
    Sub [New](ElemCnt As Integer, _  
       \<MarshalAs(UnmanagedType.LPArray, SizeParamIndex:=1)> _  
       ar() As Integer)  
    ```  
  
    ```csharp  
    void New(  
       int ElemCnt,   
       [MarshalAs(UnmanagedType.LPArray, SizeParamIndex=0)] int[] ar );  
    ```  
  
- 배열 크기를 상수로 정의합니다. 예:  
  
    ```vb  
    Sub [New](\<MarshalAs(UnmanagedType.LPArray, SizeConst:=128)> _  
       ar() As Integer)  
    ```  
  
    ```csharp  
    void New(  
       [MarshalAs(UnmanagedType.LPArray, SizeConst=128)] int[] ar );  
    ```  
  
 비관리 코드에서 관리 코드로 배열을 마샬링할 경우 마샬러는 매개 변수와 연결된 **MarshalAsAttribute**를 확인하여 배열 크기를 결정합니다. 배열 크기를 지정하지 않으면 하나의 요소만 마샬링됩니다.  
  
> [!NOTE]
> **MarshalAsAttribute**는 관리 배열을 비관리 코드에 마샬링하는 작업에 영향을 주지 않습니다. 해당 방향의 배열 크기는 검사에 의해 결정됩니다. 관리되는 배열의 하위 집합을 마샬링할 방법은 없습니다.  
  
 interop 마샬러는 **CoTaskMemAlloc** 및 **CoTaskMemFree** 메서드를 사용하여 메모리를 할당 및 검색합니다. 비관리 코드에서 수행되는 메모리 할당에는 이러한 메서드도 사용해야 합니다.  
  
## <a name="passing-arrays-to-com"></a>COM에 배열 전달  
 모든 관리되는 배열 형식은 관리 코드에서 비관리 코드로 전달할 수 있습니다. 다음 표와 같이 관리되는 형식과 이 형식에 적용되는 특성에 따라 배열에는 안전 배열 또는 C 스타일 배열로 액세스할 수 있습니다.  
  
|관리되는 배열 형식|내보내기 형식|  
|------------------------|-----------------|  
|**ELEMENT_TYPE_SZARRAY** **\<** *type* **>**|<xref:System.Runtime.InteropServices.UnmanagedType> **.SafeArray(** *type* **)**<br /><br /> **UnmanagedType.LPArray**<br /><br /> 형식은 시그니처로 제공됩니다. 순위는 항상 1이고 하한은 항상 0입니다. 크기는 항상 런타임에 알려집니다.|  
|**ELEMENT_TYPE_ARRAY** **\<** *type* **>** **\<** *rank* **>** [ **\<** *bounds* **>** ]|**UnmanagedType.SafeArray(** *type* **)**<br /><br /> **UnmanagedType.LPArray**<br /><br /> 형식, 순위, 경계는 시그니처로 제공됩니다. 크기는 항상 런타임에 알려집니다.|  
|**ELEMENT_TYPE_CLASS** **\<** <xref:System.Array?displayProperty=nameWithType> **>**|**UT_Interface**<br /><br /> **UnmanagedType.SafeArray(** *type* **)**<br /><br /> 형식, 순위, 경계 및 크기는 항상 런타임에 알려집니다.|  
  
 LPSTR 또는 LPWSTR이 포함된 구조체 배열에 관련된 OLE 자동화에는 제한이 있습니다.  따라서 **String** 필드는 **UnmanagedType.BSTR**로 마샬링되어야 합니다. 그렇지 않으면 예외가 throw됩니다.  
  
### <a name="element_type_szarray"></a>ELEMENT_TYPE_SZARRAY  
 **ELEMENT_TYPE_SZARRAY** 매개 변수(1차원 배열)가 포함된 메서드를 .NET 어셈블리에서 형식 라이브러리로 내보내면 배열 매개 변수가 지정된 형식의 **SAFEARRAY**로 변환됩니다. 같은 변환 규칙이 배열 요소 형식에 적용됩니다. 관리되는 배열의 콘텐츠는 관리되는 메모리에서 **SAFEARRAY**로 자동으로 복사됩니다. 예:  
  
#### <a name="managed-signature"></a>관리되는 시그니처  
  
```vb  
Sub [New](ar() As Long)  
Sub [New](ar() As String)  
```  
  
```csharp  
void New(long[] ar );  
void New(String[] ar );  
```  
  
#### <a name="unmanaged-signature"></a>관리되지 않는 서명  
  
```cpp
HRESULT New([in] SAFEARRAY( long ) ar);
HRESULT New([in] SAFEARRAY( BSTR ) ar);  
```  
  
 안전 배열의 순위는 항상 1이고 하한은 항상 0입니다. 크기는 런타임에 전달 중인 관리되는 배열 크기에 따라 결정됩니다.  
  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성을 사용하여 배열을 C 스타일 배열로 마샬링할 수도 있습니다. 예:  
  
#### <a name="managed-signature"></a>관리되는 시그니처  
  
```vb  
Sub [New](<MarshalAs(UnmanagedType.LPArray, SizeParamIndex:=1)> _  
   ar() As Long, size as Integer)  
Sub [New](<MarshalAs(UnmanagedType.LPArray, SizeParamIndex:=1)> _  
   ar() As String, size as Integer)  
Sub [New](<MarshalAs(UnmanagedType.LPArray, _  
   ArraySubType= UnmanagedType.LPStr, SizeParamIndex:=1)> _  
   ar() As String, size as Integer)  
```  
  
```csharp  
void New([MarshalAs(UnmanagedType.LPArray, SizeParamIndex=1)]   
   long [] ar, int size );  
void New([MarshalAs(UnmanagedType.LPArray, SizeParamIndex=1)]   
   String [] ar, int size );  
void New([MarshalAs(UnmanagedType.LPArray, ArraySubType=   
   UnmanagedType.LPStr, SizeParamIndex=1)]   
   String [] ar, int size );  
```  
  
#### <a name="unmanaged-signature"></a>관리되지 않는 서명  
  
```cpp
HRESULT New(long ar[]);
HRESULT New(BSTR ar[]);
HRESULT New(LPStr ar[]);  
```  
  
 마샬러에는 배열을 마샬링하는 데 필요한 길이 정보가 있지만 배열 길이는 대개 호출 수신자에게 길이를 전달하기 위한 개별 인수로 전달됩니다.  
  
### <a name="element_type_array"></a>ELEMENT_TYPE_ARRAY  
 **ELEMENT_TYPE_ARRAY** 매개 변수가 포함된 메서드를 .NET 어셈블리에서 형식 라이브러리로 내보내면 배열 매개 변수가 지정된 형식의 **SAFEARRAY**로 변환됩니다. 관리되는 배열의 콘텐츠는 관리되는 메모리에서 **SAFEARRAY**로 자동으로 복사됩니다. 예:  
  
#### <a name="managed-signature"></a>관리되는 시그니처  
  
```vb  
Sub [New](ar(,) As Long)  
Sub [New](ar(,) As String)  
```  
  
```csharp  
void New( long [,] ar );  
void New( String [,] ar );  
```  
  
#### <a name="unmanaged-signature"></a>관리되지 않는 서명  
  
```cpp
HRESULT New([in] SAFEARRAY( long ) ar);
HRESULT New([in] SAFEARRAY( BSTR ) ar);  
```  
  
 안전 배열의 순위, 크기 및 경계는 런타임에 관리되는 배열의 특징에 따라 결정됩니다.  
  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성을 적용하여 배열을 C 스타일 배열로 마샬링할 수도 있습니다. 예:  
  
#### <a name="managed-signature"></a>관리되는 시그니처  
  
```vb  
Sub [New](<MarshalAs(UnmanagedType.LPARRAY, SizeParamIndex:=1)> _  
   ar(,) As Long, size As Integer)  
Sub [New](<MarshalAs(UnmanagedType.LPARRAY, _  
   ArraySubType:=UnmanagedType.LPStr, SizeParamIndex:=1)> _  
   ar(,) As String, size As Integer)  
```  
  
```csharp  
void New([MarshalAs(UnmanagedType.LPARRAY, SizeParamIndex=1)]   
   long [,] ar, int size );  
void New([MarshalAs(UnmanagedType.LPARRAY,   
   ArraySubType= UnmanagedType.LPStr, SizeParamIndex=1)]   
   String [,] ar, int size );  
```  
  
#### <a name="unmanaged-signature"></a>관리되지 않는 서명  
  
```cpp
HRESULT New(long ar[]);
HRESULT New(LPStr ar[]);  
```  
  
 중첩 배열은 마샬링할 수 없습니다. 예를 들어 다음 시그니처는 [형식 라이브러리 내보내기(Tlbexp.exe)](../tools/tlbexp-exe-type-library-exporter.md)를 통해 내보낼 경우 오류를 생성합니다.  
  
#### <a name="managed-signature"></a>관리되는 시그니처  
  
```vb  
Sub [New](ar()()() As Long)  
```  
  
```csharp  
void New(long [][][] ar );  
```  
  
### <a name="element_type_class-systemarray"></a>ELEMENT_TYPE_CLASS \<System.Array>  
 <xref:System.Array?displayProperty=nameWithType> 매개 변수가 포함된 메서드를 .NET 어셈블리에서 형식 라이브러리로 내보내면 배열 매개 변수가 **_Array** 인터페이스로 변환됩니다. 관리되는 배열의 콘텐츠는 **_Array** 인터페이스의 메서드 및 속성을 통해서만 액세스할 수 있습니다. <xref:System.Runtime.InteropServices.MarshalAsAttribute> 특성을 사용하여 **System.Array**를 **SAFEARRAY**로 마샬링할 수도 있습니다. 안전 배열로 마샬링될 경우 배열 요소는 변형으로 마샬링됩니다. 예:  
  
#### <a name="managed-signature"></a>관리되는 시그니처  
  
```vb  
Sub New1( ar As System.Array )  
Sub New2( <MarshalAs(UnmanagedType.Safe array)> ar As System.Array )  
```  
  
```csharp  
void New1( System.Array ar );  
void New2( [MarshalAs(UnmanagedType.Safe array)] System.Array ar );  
```  
  
#### <a name="unmanaged-signature"></a>관리되지 않는 서명  
  
```cpp
HRESULT New([in] _Array *ar);
HRESULT New([in] SAFEARRAY(VARIANT) ar);  
```  
  
### <a name="arrays-within-structures"></a>구조체가 있는 배열  
 관리되지 않는 구조체에는 포함된 배열이 있을 수 있습니다. 기본적으로 이러한 포함된 배열 필드는 SAFEARRAY로 마샬링됩니다. 다음 예제에서 `s1`은 구조체 자체 내에서 직접 할당되는 포함된 배열입니다.  
  
#### <a name="unmanaged-representation"></a>관리되지 않는 표현  
  
```cpp
struct MyStruct {  
    short s1[128];  
}  
```  
  
 배열은 <xref:System.Runtime.InteropServices.MarshalAsAttribute> 필드를 설정해야 하는 <xref:System.Runtime.InteropServices.UnmanagedType>으로 마샬링될 수 있습니다. 크기는 상수로만 설정할 수 있습니다. 다음 코드에서는 `MyStruct`의 해당 관리되는 정의를 보여 줍니다.  
  
```vb  
Public Structure <StructLayout(LayoutKind.Sequential)> MyStruct  
   Public <MarshalAs(UnmanagedType.ByValArray, SizeConst := 128)> _  
     s1() As Short  
End Structure  
```  
  
```csharp  
[StructLayout(LayoutKind.Sequential)]  
public struct MyStruct {  
   [MarshalAs(UnmanagedType.ByValArray, SizeConst=128)] public short[] s1;  
}  
```  
  
## <a name="see-also"></a>참고 항목

- [기본 마샬링 동작](default-marshaling-behavior.md)
- [Blittable 형식 및 비 Blittable 형식](blittable-and-non-blittable-types.md)
- [방향 특성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/77e6taeh(v=vs.100))
- [복사 및 고정](copying-and-pinning.md)
