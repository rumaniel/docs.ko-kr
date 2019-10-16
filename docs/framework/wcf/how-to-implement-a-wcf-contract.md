---
title: '자습서: Windows Communication Foundation 서비스 계약 구현'
ms.date: 03/19/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- service contracts [WCF], implementing
ms.assetid: d5ab51ba-61ae-403e-b3c8-e2669e326806
ms.openlocfilehash: 05923dc0a2223da5e5fcda483abc1ee1dd2d643f
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928707"
---
# <a name="tutorial-implement-a-windows-communication-foundation-service-contract"></a>자습서: Windows Communication Foundation 서비스 계약 구현

이 자습서에서는 WCF (기본 Windows Communication Foundation) 응용 프로그램을 만드는 데 필요한 5 가지 작업 중 두 번째 작업에 대해 설명 합니다. 자습서에 대 한 개요를 보려면 [자습서: Windows Communication Foundation 응용 프로그램](getting-started-tutorial.md)을 시작 하세요.

WCF 응용 프로그램을 만들기 위한 다음 단계는 이전 단계에서 만든 WCF 서비스 인터페이스를 구현 하는 코드를 추가 하는 것입니다. 이 단계에서는 사용자 정의 `CalculatorService` `ICalculator` 인터페이스를 구현 하는 라는 클래스를 만듭니다. 다음 코드의 각 메서드는 계산기 작업을 호출 하 고 콘솔에 텍스트를 기록 하 여 테스트 합니다. 

이 자습서에서는 다음 작업을 수행하는 방법을 알아봅니다.
> [!div class="checklist"]
>
> - WCF 서비스 계약을 구현 하는 코드를 추가 합니다.
> - 솔루션을 빌드합니다.

## <a name="add-code-to-implement-the-wcf-service-contract"></a>WCF 서비스 계약을 구현 하는 코드 추가

**GettingStartedLib**에서 **Service1.cs** 또는 **Service1 .vb** 파일을 열고 해당 코드를 다음 코드로 바꿉니다.

```csharp
using System;
using System.ServiceModel;

namespace GettingStartedLib
{
    public class CalculatorService : ICalculator
    {
        public double Add(double n1, double n2)
        {
            double result = n1 + n2;
            Console.WriteLine("Received Add({0},{1})", n1, n2);
            // Code added to write output to the console window.
            Console.WriteLine("Return: {0}", result);
            return result;
        }

        public double Subtract(double n1, double n2)
        {
            double result = n1 - n2;
            Console.WriteLine("Received Subtract({0},{1})", n1, n2);
            Console.WriteLine("Return: {0}", result);
            return result;
        }

        public double Multiply(double n1, double n2)
        {
            double result = n1 * n2;
            Console.WriteLine("Received Multiply({0},{1})", n1, n2);
            Console.WriteLine("Return: {0}", result);
            return result;
        }

        public double Divide(double n1, double n2)
        {
            double result = n1 / n2;
            Console.WriteLine("Received Divide({0},{1})", n1, n2);
            Console.WriteLine("Return: {0}", result);
            return result;
        }
    }
}
```

```vb
Imports System.ServiceModel

Namespace GettingStartedLib

    Public Class CalculatorService
        Implements ICalculator

        Public Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Add
            Dim result As Double = n1 + n2
            ' Code added to write output to the console window.
            Console.WriteLine("Received Add({0},{1})", n1, n2)
            Console.WriteLine("Return: {0}", result)
            Return result
        End Function

        Public Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Subtract
            Dim result As Double = n1 - n2
            Console.WriteLine("Received Subtract({0},{1})", n1, n2)
            Console.WriteLine("Return: {0}", result)
            Return result

        End Function

        Public Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Multiply
            Dim result As Double = n1 * n2
            Console.WriteLine("Received Multiply({0},{1})", n1, n2)
            Console.WriteLine("Return: {0}", result)
            Return result

        End Function

        Public Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double Implements ICalculator.Divide
            Dim result As Double = n1 / n2
            Console.WriteLine("Received Divide({0},{1})", n1, n2)
            Console.WriteLine("Return: {0}", result)
            Return result

        End Function
    End Class
End Namespace
```

## <a name="edit-appconfig"></a>App.config 편집

코드에 대 한 변경 내용을 반영 하도록 **GettingStartedLib** 에서 **app.config** 를 편집 합니다.

- 시각적 C# 프로젝트의 경우:
  - 줄 14를 다음으로 변경`<service name="GettingStartedLib.CalculatorService">`
  - 줄 17을 다음으로 변경`<add baseAddress = "http://localhost:8000/GettingStarted/CalculatorService" />`
  - 줄 22를 다음으로 변경`<endpoint address="" binding="wsHttpBinding" contract="GettingStartedLib.ICalculator">`

- Visual Basic 프로젝트의 경우
  - 줄 14를 다음으로 변경`<service name="GettingStartedLib.GettingStartedLib.CalculatorService">`
  - 줄 17을 다음으로 변경`<add baseAddress = "http://localhost:8000/GettingStarted/CalculatorService" />`
  - 줄 22를 다음으로 변경`<endpoint address="" binding="wsHttpBinding" contract="GettingStartedLib.GettingStartedLib.ICalculator">`

## <a name="compile-the-code"></a>코드 컴파일

솔루션을 빌드하여 컴파일 오류가 없는지 확인 합니다. Visual Studio를 사용 하는 경우 **빌드** 메뉴에서 **솔루션 빌드** 를 선택 하거나 **ctrl**+**Shift**+**B**를 누릅니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업을 수행하는 방법을 알아보았습니다.
> [!div class="checklist"]
>
> - WCF 서비스 계약을 구현 하는 코드를 추가 합니다.
> - 솔루션을 빌드합니다.

다음 자습서로 이동 하 여 WCF 서비스를 실행 하는 방법을 알아보세요.

> [!div class="nextstepaction"]
> [자습서: 기본 WCF 서비스를 호스트 하 고 실행 합니다.](how-to-host-and-run-a-basic-wcf-service.md)
