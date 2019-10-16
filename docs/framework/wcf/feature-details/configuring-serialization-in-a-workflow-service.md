---
title: 워크플로 서비스에서 Serialization 구성
ms.date: 03/30/2017
ms.assetid: aa70b290-a2ee-4c3c-90ea-d0a7665096ae
ms.openlocfilehash: 0e0f03a30aa8e8679cf849aa75948e0bc2314fe5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61857511"
---
# <a name="configuring-serialization-in-a-workflow-service"></a>워크플로 서비스에서 Serialization 구성
워크플로 서비스는 Windows Communication Foundation (WCF) 서비스 및 중 하나를 사용 하 여는 옵션이 있으므로 합니다 <xref:System.Runtime.Serialization.DataContractSerializer> (기본값) 또는 <xref:System.Xml.Serialization.XmlSerializer>합니다. 워크플로가 아닌 서비스를 작성할 때 사용할 직렬화기 형식은 서비스 또는 작업 계약에서 지정됩니다. WCF 워크플로 서비스를 만들 때 코드에서 이러한 계약을 지정 하지 않으면 하지만 계약 유추를 통해 런타임에 생성 대신 합니다. 계약 유추에 대 한 자세한 내용은 참조 하세요. [워크플로에서 계약 사용 하 여](../../../../docs/framework/wcf/feature-details/using-contracts-in-workflow.md)입니다.  직렬화기는 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 속성을 사용하여 지정됩니다. 다음 그림과 같이 디자이너에서 이 속성을 설정할 수 있습니다.  
  
 ![속성 창에서 SerializerOption 속성을 설정 합니다.](./media/configuring-serialization-in-a-workflow-service/setting-serializer-property.png)  
  
 다음 예제와 같이 코드에서 직렬화기를 설정할 수도 있습니다.  
  
```csharp  
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
```  
  
  워크플로 서비스에서 알려진 형식도 지정할 수 있습니다. 알려진 형식에 대 한 자세한 내용은 참조 하세요. [데이터 계약 알려진 형식을](data-contract-known-types.md)합니다. 디자이너나 코드에서 알려진 형식을 지정할 수 있습니다. 를 디자이너에서 알려진된 형식을 지정 하려면에서 KnownTypes 속성 옆에 있는 줄임표 (...) 단추를 클릭 합니다 **속성 창** 에 대 한는 <xref:System.ServiceModel.Activities.Receive> 다음 그림과에서 같이 작업 합니다.   
  
 ![KnownTypes 속성 대화 상자 스크린샷입니다.](./media/configuring-serialization-in-a-workflow-service/known-types-properties.png)  
  
 에 대 한 검색 하 고 알려진된 형식을 지정할 수 있는 형식 컬렉션 편집기가 표시 됩니다.  
  
 ![형식 컬렉션 편집기의 스크린샷입니다.](./media/configuring-serialization-in-a-workflow-service/type-collection-editor.gif)  
  
 클릭 합니다 **새 유형을 추가** 에 연결 하 고 선택 하거나 검색 유형에 대 한 드롭다운을 사용 하 여 알려진된 형식 컬렉션에 추가 합니다. 코드에서 알려진 형식을 지정하려면 다음 예제와 같이 <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A> 속성을 사용합니다.  
  
```csharp
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
            approveExpense.KnownTypes.Add(typeof(Travel));  
            approveExpense.KnownTypes.Add(typeof(Meal));  
```
