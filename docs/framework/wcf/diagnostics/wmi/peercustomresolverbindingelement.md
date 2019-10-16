---
title: PeerCustomResolverBindingElement
ms.date: 03/30/2017
ms.assetid: 9ccc2770-a20e-4dff-9970-f56ad8aec2b5
ms.openlocfilehash: c7f8fd23133cd83ad87a00134b9755b94f531d8b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61963061"
---
# <a name="peercustomresolverbindingelement"></a>PeerCustomResolverBindingElement

PeerCustomResolverBindingElement

## <a name="syntax"></a>구문

```csharp
class PeerCustomResolverBindingElement : PeerResolverBindingElement
{
    string Address;
    string Binding;
};
```

## <a name="methods"></a>메서드

PeerCustomResolverBindingElement 클래스는 메서드를 정의하지 않습니다.

## <a name="properties"></a>속성

 PeerCustomResolverBindingElement 클래스에는 다음과 같은 속성이 있습니다.

### <a name="address"></a>주소

데이터 형식: string

액세스 형식: 읽기 전용

피어 사용자 지정 확인자의 주소입니다.

### <a name="binding"></a>바인딩

데이터 형식: string

액세스 형식: 읽기 전용

바인딩의 구성 이름입니다.

## <a name="requirements"></a>요구 사항

|MOF|Servicemodel.mof에 선언되어 있습니다.|
|---------|-----------------------------------|
|네임스페이스|root\ServiceModel에 정의되어 있습니다.|

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.PeerCustomResolverBindingElement>
