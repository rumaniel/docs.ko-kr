---
title: '자습서: Windows Communication Foundation 서비스 계약 정의'
ms.date: 03/19/2019
helpviewer_keywords:
- service contracts [WCF], defining
dev_langs:
- CSharp
- VB
ms.assetid: 67bf05b7-1d08-4911-83b7-a45d0b036fc3
ms.openlocfilehash: ba88fc6ba4cba8d46ed1b43080d471b1b7c4bd75
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928882"
---
# <a name="tutorial-define-a-windows-communication-foundation-service-contract"></a>자습서: Windows Communication Foundation 서비스 계약 정의

이 자습서에서는 WCF (기본 Windows Communication Foundation) 응용 프로그램을 만드는 데 필요한 5 가지 작업 중 첫 번째 작업에 대해 설명 합니다. 자습서에 대 한 개요를 보려면 [자습서: Windows Communication Foundation 응용 프로그램](getting-started-tutorial.md)을 시작 하세요.

WCF 서비스를 만들 때 첫 번째 작업은 서비스 계약을 정의 하는 것입니다. 서비스 계약은 서비스가 지원하는 작업을 지정합니다. 작업은 웹 서비스 메서드로 간주될 수 있습니다. Visual C# 또는 VB (Visual Basic) 인터페이스를 정의 하 여 서비스 계약을 만듭니다. 인터페이스에는 다음과 같은 특징이 있습니다.

- 인터페이스의 각 메서드는 특정 서비스 작업에 해당합니다. 
- 각 인터페이스에 대해 <xref:System.ServiceModel.ServiceContractAttribute> 특성을 적용 해야 합니다.
- 각 작업/메서드에 대해 <xref:System.ServiceModel.OperationContractAttribute> 특성을 적용 해야 합니다. 

이 자습서에서는 다음 작업을 수행하는 방법을 알아봅니다.
> [!div class="checklist"]
>
> - **WCF 서비스 라이브러리** 프로젝트를 만듭니다.
> - 서비스 계약 인터페이스를 정의 합니다.

## <a name="create-a-wcf-service-library-project-and-define-a-service-contract-interface"></a>WCF 서비스 라이브러리 프로젝트를 만들고 서비스 계약 인터페이스를 정의 합니다.

1. 관리자 권한으로 Visual Studio를 엽니다. 이렇게 하려면 **시작** 메뉴에서 Visual Studio 프로그램 **을 선택 하** > 고 바로 가기 메뉴에서**관리자 권한으로 실행** 을 선택 합니다.

2. **WCF 서비스 라이브러리** 프로젝트를 만듭니다.

   1. **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.

   2. **새 프로젝트** 대화 상자의 왼쪽에서  **C# 비주얼** 또는 **Visual Basic**을 확장 한 다음 **WCF** 범주를 선택 합니다. Visual Studio는 창의 가운데 섹션에 프로젝트 템플릿 목록을 표시 합니다. **WCF 서비스 라이브러리**를 선택 합니다.

      > [!NOTE]
      > **WCF** 프로젝트 템플릿 범주가 표시 되지 않으면 Visual Studio의 **Windows Communication Foundation** 구성 요소를 설치 해야 할 수 있습니다. **새 프로젝트** 대화 상자에서 왼쪽에 있는 **Visual Studio 설치 관리자 열기** 링크를 선택 합니다. **개별 구성 요소** 탭을 선택한 다음 **개발 활동** 범주 아래에서 **Windows Communication Foundation** 을 찾아 선택 합니다. **수정** 을 선택 하 여 구성 요소 설치를 시작 합니다.

   3. 창의 아래쪽 섹션에서 **솔루션 이름**에 대해 시작 된 **이름** 및 *getGettingStartedLib* 를 입력 합니다. 

   4. **확인**을 선택합니다.

      Visual Studio는 세 개의 파일이 있는 프로젝트를 만듭니다. *IService1.cs* (또는 Visual Basic 프로젝트의 경우 *IService1* , *Service1.cs* (또는 Visual Basic 프로젝트의 경우 *Service1 .vb* ) 및 *app.config*. Visual Studio는 다음과 같은 파일을 정의 합니다. 
      - *IService1* 파일에는 서비스 계약의 기본 정의가 포함 되어 있습니다. 
      - *Service1* 파일에는 서비스 계약의 기본 구현이 포함 되어 있습니다. 
      - *App.config* 파일에는 VISUAL Studio WCF 서비스 호스트 도구를 사용 하 여 기본 서비스를 로드 하는 데 필요한 구성 정보가 포함 되어 있습니다. WCF 서비스 호스트 도구에 대 한 자세한 내용은 [Wcf 서비스 호스트 (wcfsvchost.exe)](wcf-service-host-wcfsvchost-exe.md)를 참조 하십시오.

      > [!NOTE]
      > Visual Basic 개발자 환경 설정을 사용 하 여 Visual Studio를 설치한 경우 솔루션이 숨겨질 수 있습니다. 이 경우 **도구** 메뉴에서 **옵션** 을 선택한 다음 **옵션** 창에서 **프로젝트 및 솔루션** > **일반** 을 선택 합니다. **솔루션 항상 표시**를 선택 합니다. 또한 **만들어질 때 새 프로젝트 저장** 이 선택 되어 있는지 확인 합니다.

3. **솔루션 탐색기**에서 **IService1.cs** 또는 **IService1** 파일을 열고 해당 코드를 다음 코드로 바꿉니다.

    ```csharp
    using System;
    using System.ServiceModel;

    namespace GettingStartedLib
    {
            [ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]
            public interface ICalculator
            {
                [OperationContract]
                double Add(double n1, double n2);
                [OperationContract]
                double Subtract(double n1, double n2);
                [OperationContract]
                double Multiply(double n1, double n2);
                [OperationContract]
                double Divide(double n1, double n2);
            }
    }
    ```

    ```vb
    Imports System.ServiceModel

    Namespace GettingStartedLib

        <ServiceContract(Namespace:="http://Microsoft.ServiceModel.Samples")> _
        Public Interface ICalculator

            <OperationContract()> _
            Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double
            <OperationContract()> _
            Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double
            <OperationContract()> _
            Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double
            <OperationContract()> _
            Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double
        End Interface
    End Namespace
    ```

     이 계약은 온라인 계약을 정의합니다. 인터페이스는 `ICalculator` <xref:System.ServiceModel.ServiceContractAttribute> 특성으로 표시 됩니다 (단순화 `ServiceContract`). 이 특성은 계약 이름을 명확 하 게 구분 하는 네임 스페이스를 정의 합니다. 이 코드는 각 계산기 작업을 <xref:System.ServiceModel.OperationContractAttribute> 특성 (로 `OperationContract`간소화)으로 표시 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업을 수행하는 방법을 알아보았습니다.
> [!div class="checklist"]
>
> - WCF 서비스 라이브러리 프로젝트를 만듭니다.
> - 서비스 계약 인터페이스를 정의 합니다.

WCF 서비스 계약을 구현 하는 방법에 대해 알아보려면 다음 자습서로 이동 합니다.

> [!div class="nextstepaction"]
> [자습서: WCF 서비스 계약 구현](how-to-implement-a-wcf-contract.md)
