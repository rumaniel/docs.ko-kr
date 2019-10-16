---
title: 파생된 수학 함수(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- arithmetic operations, derived math functions
- cosecant function
- arcsecant function
- arccotangent function
- functions [Visual Basic], derived math functions
- inverse functions
- math functions, derived
- derived math functions
- cotangent function
- angles
- secant function
- trigonometric functions
- logarithms
- arccosecant function
- hyperbolic functions
- arcsine function
- degrees
- arccosine function
ms.assetid: 63e449d8-9444-44fb-8db1-6d9cf346e2aa
ms.openlocfilehash: 0d0606c52d1d50fcc2fd8eea3ad2851c95b18a69
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61801896"
---
# <a name="derived-math-functions-visual-basic"></a>파생된 수학 함수(Visual Basic)
다음 표에서 기본 수학 함수의에서 파생 될 수 있는 비 내장 수치 연산 함수는 <xref:System.Math?displayProperty=nameWithType> 개체입니다. 기본 수학 함수를 추가 하 여 액세스할 수 있습니다 `Imports System.Math` 을 파일이 나 프로젝트입니다.  
  
|함수|해당 파생된 항목|  
|--------------|-------------------------|  
|시 컨 트 (Sec(x))|1 / Cos(x)|  
|코시 컨 트 (Csc(x))|1 / Sin(x)|  
|코탄젠트 (Ctan(x))|1 / Tan(x)|  
|역 사인 (Asin(x))|Atan(x / Sqrt(-x * x + 1))|  
|역 코사인 (Acos(x))|Atan(-x / Sqrt(-x * x + 1)) + 2 \* Atan(1)|  
|역 시 컨 트 (Asec(x))|2 * Atan(1) – Atan(Sign(x) / Sqrt(x \* x – 1))|  
|역 코시 컨 트 (Acsc(x))|Atan(Sign(x) / Sqrt(x * x – 1))|  
|역 코탄젠트 (Acot(x))|2 * Atan(1) - Atan(x)|  
|쌍 곡 사인 (Sinh(x))|(Exp(x) – Exp(-x)) / 2|  
|쌍 곡 코사인 (Cosh(x))|(Exp(x) + Exp(-x)) / 2|  
|Hyperbolic tangent (Tanh(x))|(Exp(x) – Exp(-x)) / (Exp(x) + Exp(-x))|  
|쌍 곡 시 컨 트 (Sech(x))|2 / (Exp(x) + Exp(-x))|  
|Hyperbolic cosecant (Csch(x))|2 / (Exp(x) – Exp(-x))|  
|Hyperbolic cotangent (Coth(x))|(Exp(x) + Exp(-x)) / (Exp(x) – Exp(-x))|  
|역 쌍 곡 사인 (Asinh(x))|Log(x + Sqrt(x * x + 1))|  
|역 쌍 곡 코사인 (Acosh(x))|Log(x + Sqrt(x * x – 1))|  
|역 쌍 곡 탄젠트 (Atanh(x))|Log((1 + x) / (1 – x)) / 2|  
|역 쌍 곡 시 컨 트 (AsecH(x))|Log((Sqrt(-x * x + 1) + 1) / x)|  
|역 쌍 곡 코시 컨 트 (Acsch(x))|Log((Sign(x) * Sqrt(x \* x + 1) + 1) / x)|  
|역 쌍 곡 코탄젠트 (Acoth(x))|로그 ((x + 1) / (x-1)) / 2|  
  
## <a name="see-also"></a>참고자료

- [수학 함수](../../../visual-basic/language-reference/functions/math-functions.md)
