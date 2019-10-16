---
title: 서비스 프레임워크 메타데이터
ms.date: 03/30/2017
ms.assetid: 76afc73a-0770-4084-93f3-6701a757911e
ms.openlocfilehash: f3e73df54b3389b2c9f27001953be147b27eb6f8
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991209"
---
# <a name="service-framework-metadata"></a>서비스 프레임워크 메타데이터
이 항목에서는 서비스 프레임워크 메타데이터에 의해 생성된 모든 예외를 보여 줍니다.  
  
## <a name="exception-list"></a>예외 목록  
  
|리소스 코드|리소스 문자열|  
|-------------------|---------------------|  
|AsyncEndCalledOnWrongChannel|비동기 End가 잘못된 채널에서 호출되었습니다.|  
|AsyncEndCalledWithAnIAsyncResult|비동기 End가 다른 Begin 메서드의 IAsyncResult와 함께 호출되었습니다.|  
|AttemptedToGetContractTypeForButThatTypeIs1|지정 된에 대 한 계약 형식을 가져오려고 했습니다. 형식이 ServiceContract가 아니고 ServiceContract를 상속 하지 않습니다.|  
|CannotHaveTwoOperationsWithTheSameName3|동일한 계약에 이름이 같은 두 개의 작업을 가질 수 없습니다. 지정된 형식의 지정된 메서드가 이 규칙을 위반합니다. 메서드 이름을 변경하거나 OperationContractAttribute의 Name 속성을 사용하여 작업 중 하나의 이름을 변경할 수 있습니다.|  
|CannotInheritTwoOperationsWithTheSameName3|이름이 같은 두 개의 다른 작업을 상속할 수 없습니다. 지정된 계약의 지정된 작업이 이 규칙을 위반합니다. 메서드 이름을 변경하거나 OperationContractAttribute의 Name 속성을 사용하여 작업 중 하나의 이름을 변경할 수 있습니다.|  
|CantCreateChannelWithManualAddressing|수동 주소 지정이 필요하지만 이중 통신만 지원하는 바인딩 및 요청/회신이 필요한 계약에 대한 채널을 만들 수 없습니다.|  
|DuplicateBehavior1|컬렉션에 값을 추가할 수 없습니다. 지정된 동일한 형식의 항목이 이미 컬렉션에 있습니다. 이 컬렉션은 각 형식의 인스턴스를 하나만 지원합니다.|  
|InAContractInheritanceHierarchyIfParentHasCallbackChildMustToo|지정된 기본 서비스 계약에 지정된 콜백 계약이 있으므로 지정된 파생 서비스 계약에서도 지정된 형식 또는 파생 형식을 해당 콜백 계약으로 지정해야 합니다.|  
|InvalidAsyncBeginMethodSignatureForMethod2|지정된 ServiceContract 형식의 지정된 메서드에 대한 잘못된 비동기 Begin 메서드 서명이 있습니다. Begin 메서드는 AsyncCallback 및 개체를 마지막 두 개의 인수로 가지고 IAsyncResult를 반환해야 합니다.|  
|InvalidAsyncEndMethodSignatureForMethod2|지정된 ServiceContract 형식의 지정된 메서드에 대한 잘못된 비동기 End 메서드 서명이 있습니다. End 메서드는 IAsyncResult를 마지막 인수로 가져야 합니다.|  
|MessagePropertiesArraySize0|전달된 배열이 이 컬렉션에 포함된 모든 속성을 보유할 수 있는 충분한 공간이 없습니다.|  
|OneWayAndFaultsIncompatible2|지정된 형식의 지정된 메서드가 IsOneWay=true로 표시되었으며 하나 이상의 FaultContractAttributes를 선언합니다. 단방향 메서드는 FaultContractAttributes를 선언할 수 없습니다. IsOneWay를 false로 변경하거나 FaultContractAttributes를 제거하십시오.|  
|UnsupportedWSDLOnlyOneMessage|지원되지 않는 웹 서비스 기술 언어입니다. 하나의 메시지 부분만 오류 메시지에 지원됩니다. 이 오류 메시지는 둘 이상의 메시지 부분을 참조합니다. 웹 서비스 기술 언어 파일에 대한 편집 액세스 권한이 있으면, 오류 메시지가 한 부분만 참조하도록 추가 메시지 부분을 제거함으로써 문제를 해결할 수 있습니다.|  
|UnsupportedWSDLTheFault|지원되지 않는 웹 서비스 기술 언어입니다. 오류 메시지 부분은 요소를 참조해야 합니다. 이 오류 메시지는 요소를 참조하지 않습니다. 웹 서비스 정의 언어 문서에 대한 편집 액세스 권한이 있으면, 'element' 특성을 사용하여 스키마 요소를 참조함으로써 문제를 해결할 수 있습니다.|  
|WsdlImportErrorDependencyDetail|지정된 다른 값이 종속되어 있는 지정된 값을 가져오는 동안 오류가 발생했습니다. Xpath도 지정되었습니다.|  
|XsdMissingRequiredAttribute1|지정된 필수 특성이 없습니다.|
