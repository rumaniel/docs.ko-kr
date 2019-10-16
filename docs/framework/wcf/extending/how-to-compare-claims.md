---
title: '방법: 클레임 비교'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- claims [WCF], comparing
- claims [WCF]
ms.assetid: 0c4ec84d-53df-408f-8953-9bc437f56c28
ms.openlocfilehash: 29254bd661e72b926b21695ccb646480c53b5475
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797105"
---
# <a name="how-to-compare-claims"></a>방법: 클레임 비교

WCF (Windows Communication Foundation)의 Id 모델 인프라는 권한 부여 검사를 수행 하는 데 사용 됩니다. 따라서 이 인프라의 일반적인 작업은 권한 부여 컨텍스트의 클레임과 요청한 작업을 수행하거나 요청한 리소스에 액세스하는 데 필요한 클레임을 비교하는 것입니다. 이 항목에서는 기본 제공 클레임 형식 및 사용자 지정 클레임 형식을 비롯한 클레임의 비교 방법에 대해 설명합니다. Id 모델 인프라에 대 한 자세한 내용은 [Id 모델을 사용 하 여 클레임 및 권한 부여 관리](../feature-details/managing-claims-and-authorization-with-the-identity-model.md)를 참조 하세요.

클레임 비교 작업에는 클레임의 세 부분(형식, 권한 및 리소스)을 다른 클레임의 해당 부분과 같은지 비교하는 작업이 포함됩니다. 다음 예제를 참조하세요.

[!code-csharp[c_CustomClaimComparison#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#9)]
[!code-vb[c_CustomClaimComparison#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#9)]

두 클레임에는 모두 <xref:System.IdentityModel.Claims.ClaimTypes.Name%2A> 클레임 형식, <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A> 권한 및 "someone" 문자열 리소스가 사용됩니다. 클레임의 세 부분이 모두 같기 때문에 클레임 자체가 동일합니다.

기본 제공 클레임 형식은 <xref:System.IdentityModel.Claims.Claim.Equals%2A> 메서드를 통해 비교됩니다. 클레임 관련 비교 코드는 필요한 경우에 사용됩니다. 다음은 두 개의 UPN(User Principal Name) 클레임이 주어진 예제입니다.

[!code-csharp[c_CustomClaimComparison#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#4)]
[!code-vb[c_CustomClaimComparison#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#4)]

이 <xref:System.IdentityModel.Claims.Claim.Equals%2A> 메서드의 비교 코드는를 반환 `true`하며, `example\someone` 이 경우는 "someone@example.com"와 동일한 도메인 사용자를 식별 합니다.

사용자 지정 클레임 형식도 <xref:System.IdentityModel.Claims.Claim.Equals%2A> 메서드를 통해 비교할 수 있습니다. 하지만 클레임의 <xref:System.IdentityModel.Claims.Claim.Resource%2A> 속성에 의해 반환된 형식이 기본 형식이 아닌 경우에는 <xref:System.IdentityModel.Claims.Claim.Equals%2A> 속성에 의해 반환된 값이 `true` 메서드별로 같을 경우에만 `Resource`에서 <xref:System.IdentityModel.Claims.Claim.Equals%2A>를 반환합니다. 이러한 사항이 적합하지 않은 경우 필요한 사용자 지정 처리 작업을 수행하려면, `Resource` 속성에 의해 반환된 사용자 지정 형식을 통해 <xref:System.IdentityModel.Claims.Claim.Equals%2A> 및 <xref:System.Object.GetHashCode%2A> 메서드를 재정의해야 합니다.

## <a name="comparing-built-in-claims"></a>기본 제공 클레임 비교

1. <xref:System.IdentityModel.Claims.Claim> 클래스의 두 인스턴스를 고려하여, 다음 코드에서와 같이 <xref:System.IdentityModel.Claims.Claim.Equals%2A>를 사용하여 비교 작업을 수행합니다.

     [!code-csharp[c_CustomClaimComparison#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#5)]
     [!code-vb[c_CustomClaimComparison#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#5)]

### <a name="comparing-custom-claims-with-primitive-resource-types"></a>기본 리소스 형식을 사용하는 사용자 지정 클레임 비교

1. 기본 리소스 형식을 사용하는 사용자 지정 클레임의 경우에는 다음 코드에서와 같이 기본 제공 클레임에 대한 비교를 수행할 수 있습니다.

     [!code-csharp[c_CustomClaimComparison#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#6)]
     [!code-vb[c_CustomClaimComparison#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#6)]

2. 구조체 또는 클래스 기반의 리소스 형식을 사용하는 사용자 지정 클레임의 경우에는 리소스 형식에서 <xref:System.IdentityModel.Claims.Claim.Equals%2A> 메서드를 재정의해야 합니다.

3. 우선 `obj` 매개 변수가 `null`인지 확인하고 null이면 `false`를 반환합니다.

     [!code-csharp[c_CustomClaimComparison#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#7)]
     [!code-vb[c_CustomClaimComparison#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#7)]

4. 그런 다음 <xref:System.Object.ReferenceEquals%2A>를 호출하고 `this` 및 `obj`를 매개 변수로 전달합니다. 이때 `true`를 반환하면 `true`가 반환됩니다.

     [!code-csharp[c_CustomClaimComparison#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#8)]
     [!code-vb[c_CustomClaimComparison#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#8)]

5. `obj`를 클래스 형식의 로컬 변수에 할당합니다. 이 작업에 실패할 경우 참조는 `null`이 됩니다. 이러한 경우에는 `false`가 반환됩니다.

6. 현재 클레임을 제공된 클레임과 올바르게 비교하는 데 필요한 사용자 지정 비교 작업을 수행합니다.

## <a name="example"></a>예제

다음 예제에서는 클레임 리소스 형식이 기본 형식이 아닌 경우의 사용자 지정 클레임 비교에 대해 보여 줍니다.

[!code-csharp[c_CustomClaimComparison#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaimcomparison/cs/c_customclaimcomparison.cs#0)]
[!code-vb[c_CustomClaimComparison#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaimcomparison/vb/source.vb#0)]

## <a name="see-also"></a>참고자료

- [ID 모델을 사용하여 클레임 및 권한 부여 관리](../feature-details/managing-claims-and-authorization-with-the-identity-model.md)
- [방법: 사용자 지정 클레임 만들기](how-to-create-a-custom-claim.md)
