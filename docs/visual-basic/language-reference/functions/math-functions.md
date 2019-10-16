---
title: 수학 함수(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- math functions, Visual Basic
- arithmetic operations, math functions
- math routines
- Atn function
ms.assetid: 4d2d82e7-6924-42fe-a4a7-b4dd5bebbd0c
ms.openlocfilehash: e5f87a8e367e8c9df65b979fea3781b42ee3ce83
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61801350"
---
# <a name="math-functions-visual-basic"></a>수학 함수(Visual Basic)
메서드는 <xref:System.Math?displayProperty=nameWithType> 클래스 삼각, 로그 및 기타 일반 수학 함수를 제공 합니다.  
  
## <a name="remarks"></a>설명  
 다음 표에서 메서드는 <xref:System.Math?displayProperty=nameWithType> 클래스입니다. Visual Basic 프로그램에서 사용할 수 있습니다.  
  
|.NET 메서드|설명|  
|---------------------------|-----------------|  
|<xref:System.Math.Abs%2A>|숫자의 절대값을 반환합니다.|  
|<xref:System.Math.Acos%2A>|코사인을 적용했을 때 지정된 숫자가 나오는 각도를 반환합니다.|  
|<xref:System.Math.Asin%2A>|사인을 적용했을 때 지정된 숫자가 나오는 각도를 반환합니다.|  
|<xref:System.Math.Atan%2A>|탄젠트를 적용했을 때 지정된 숫자가 나오는 각도를 반환합니다.|  
|<xref:System.Math.Atan2%2A>|탄젠트를 적용했을 때 지정된 두 숫자의 몫이 나오는 각도를 반환합니다.|  
|<xref:System.Math.BigMul%2A>|두 개의 32 비트 숫자의 전체 곱을 반환합니다.|  
|<xref:System.Math.Ceiling%2A>|보다 크거나 같은 지정 된 된 가장 작은 정수 값을 반환 `Decimal` 또는 `Double`합니다.|  
|<xref:System.Math.Cos%2A>|지정된 각도의 코사인을 반환합니다.|  
|<xref:System.Math.Cosh%2A>|지정된 각도의 하이퍼볼릭 코사인을 반환합니다.|  
|<xref:System.Math.DivRem%2A>|두 32 비트 또는 64 비트 부호 있는 정수의 몫을 반환 하 고도 출력 매개 변수에 나머지를 반환 합니다.|  
|<xref:System.Math.Exp%2A>|E (자연 로그의 밑) 거듭제곱 거듭제곱을 반환 합니다.|  
|<xref:System.Math.Floor%2A>|지정 된 보다 작거나 같은 최대 정수를 반환 `Decimal` 또는 `Double` 수입니다.|  
|<xref:System.Math.IEEERemainder%2A>|다른 지정된 된 숫자의 나누기 결과로 생성 되는 나머지 부분에서는 지정 된 번호를 반환 합니다.|  
|<xref:System.Math.Log%2A>|지정 된 기수로 지정된 된 숫자의 자연 (밑 e) 로그 또는 지정 된 숫자의 로그를 반환합니다.|  
|<xref:System.Math.Log10%2A>|밑을 10으로 사용하여 지정된 숫자의 로그를 반환합니다.|  
|<xref:System.Math.Max%2A>|두 숫자 중 더 큰 숫자를 반환합니다.|  
|<xref:System.Math.Min%2A>|두 개의 숫자 중 더 작은 숫자를 반환합니다.|  
|<xref:System.Math.Pow%2A>|지정된 숫자의 지정된 거듭제곱을 반환합니다.|  
|<xref:System.Math.Round%2A>|반환 된 `Decimal` 또는 `Double` 가장 가까운 정수 값 또는 지정된 된 개수의 소수 자릿수 값이 반올림 합니다.|  
|<xref:System.Math.Sign%2A>|반환 된 `Integer` 숫자의 부호를 나타내는 값입니다.|  
|<xref:System.Math.Sin%2A>|지정된 각도의 사인을 반환합니다.|  
|<xref:System.Math.Sinh%2A>|지정된 각도의 하이퍼볼릭 사인을 반환합니다.|  
|<xref:System.Math.Sqrt%2A>|지정된 숫자의 제곱근을 반환합니다.|  
|<xref:System.Math.Tan%2A>|지정된 각도의 탄젠트를 반환합니다.|  
|<xref:System.Math.Tanh%2A>|지정된 각도의 하이퍼볼릭 탄젠트를 반환합니다.|  
|<xref:System.Math.Truncate%2A>|지정 된 정수 부분을 계산 `Decimal` 또는 `Double` 수입니다.|  
  
 한정자 없이 이러한 함수를 사용 하려면 가져오기는 <xref:System.Math?displayProperty=nameWithType> 소스 파일의 맨 위에 다음 코드를 추가 하 여 프로젝트에 네임 스페이스:  
  
```vb
Imports System.Math  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 <xref:System.Math.Abs%2A> 메서드는 <xref:System.Math> 숫자의 절대값을 계산 하는 클래스입니다.  
  
```vb
' Returns 50.3.  
Dim MyNumber1 As Double = Math.Abs(50.3)  
' Returns 50.3.  
Dim MyNumber2 As Double = Math.Abs(-50.3)  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 <xref:System.Math.Atan%2A> 메서드는 <xref:System.Math> pi의 값을 계산 하는 클래스입니다.  
  
```vb
Public Function GetPi() As Double  
    ' Calculate the value of pi.  
    Return 4.0 * Math.Atan(1.0)  
End Function  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 <xref:System.Math.Cos%2A> 메서드는 <xref:System.Math> 각도의 코사인을 반환 하는 클래스입니다.  
  
```vb
Public Function Sec(ByVal angle As Double) As Double  
    ' Calculate the secant of angle, in radians.  
    Return 1.0 / Math.Cos(angle)  
End Function  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 <xref:System.Math.Exp%2A> 메서드를 <xref:System.Math> e의 거듭제곱을 반환 하는 클래스입니다.  
  
```vb
Public Function Sinh(ByVal angle As Double) As Double  
    ' Calculate hyperbolic sine of an angle, in radians.  
    Return (Math.Exp(angle) - Math.Exp(-angle)) / 2.0  
End Function  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 <xref:System.Math.Log%2A> 메서드는 <xref:System.Math> 숫자의 자연 로그를 반환 하는 클래스입니다.  
  
```vb
Public Function Asinh(ByVal value As Double) As Double  
    ' Calculate inverse hyperbolic sine, in radians.  
    Return Math.Log(value + Math.Sqrt(value * value + 1.0))  
End Function  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 <xref:System.Math.Round%2A> 메서드는 <xref:System.Math> 숫자를 가장 가까운 정수로 반올림 하는 클래스입니다.  
  
```vb
' Returns 3.  
Dim MyVar2 As Double = Math.Round(2.8)  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 <xref:System.Math.Sign%2A> 메서드는 <xref:System.Math> 숫자의 부호를 확인 하는 클래스입니다.  
  
```vb
' Returns 1.  
Dim MySign1 As Integer = Math.Sign(12)  
' Returns -1.  
Dim MySign2 As Integer = Math.Sign(-2.4)  
' Returns 0.  
Dim MySign3 As Integer = Math.Sign(0)  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 <xref:System.Math.Sin%2A> 메서드는 <xref:System.Math> 각도의 사인을 반환 하는 클래스입니다.  
  
```vb
Public Function Csc(ByVal angle As Double) As Double  
    ' Calculate cosecant of an angle, in radians.  
    Return 1.0 / Math.Sin(angle)  
End Function  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 <xref:System.Math.Sqrt%2A> 메서드는 <xref:System.Math> 숫자의 제곱근을 계산 하는 클래스입니다.  
  
```vb
' Returns 2.  
Dim MySqr1 As Double = Math.Sqrt(4)  
' Returns 4.79583152331272.  
Dim MySqr2 As Double = Math.Sqrt(23)  
' Returns 0.  
Dim MySqr3 As Double = Math.Sqrt(0)  
' Returns NaN (not a number).  
Dim MySqr4 As Double = Math.Sqrt(-4)  
```  
  
## <a name="example"></a>예제  
 이 예제에서는 합니다 <xref:System.Math.Tan%2A> 메서드는 <xref:System.Math> 각도의 탄젠트를 반환 하는 클래스입니다.  
  
```vb
Public Function Ctan(ByVal angle As Double) As Double  
    ' Calculate cotangent of an angle, in radians.  
    Return 1.0 / Math.Tan(angle)  
End Function  
```  
  
## <a name="requirements"></a>요구 사항  
 **클래스:** <xref:System.Math>  
  
 **네임스페이스:** <xref:System>  
  
 **어셈블리:** mscorlib (mscorlib.dll)  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.VBMath.Rnd%2A>
- <xref:Microsoft.VisualBasic.VBMath.Randomize%2A>
- <xref:System.Double.NaN>
- [파생된 수학 함수](../../../visual-basic/language-reference/keywords/derived-math-functions.md)
- [산술 연산자](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
