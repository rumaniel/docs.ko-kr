---
title: '방법: 사용자 지정 클레임 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d619976b-eda3-475e-ac23-c7988a2dceb0
ms.openlocfilehash: 399aba1a6ad70ae37355f529a291ab2f604af03f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70797080"
---
# <a name="how-to-create-a-custom-claim"></a>방법: 사용자 지정 클레임 만들기
WCF (Windows Communication Foundation)의 id 모델 인프라에서는 이러한 형식 및 권한으로 인스턴스를 만들기 <xref:System.IdentityModel.Claims.Claim> 위한 도우미 함수를 사용 하 여 기본 제공 클레임 형식 및 권한 집합을 제공 합니다. 이러한 기본 제공 클레임은 WCF에서 기본적으로 지 원하는 클라이언트 자격 증명 형식에 있는 정보를 모델링 하도록 디자인 되었습니다. 일반적으로 기본 제공 클레임으로 충분하지만 일부 애플리케이션에는 사용자 지정 클레임이 필요할 수 있습니다. 클레임은 클레임 형식, 클레임이 적용되는 리소스 및 해당 리소스에 대해 어설션되는 권한으로 구성됩니다. 이 항목에서는 사용자 지정 클레임을 만드는 방법에 대해 설명합니다.  
  
### <a name="to-create-a-custom-claim-that-is-based-on-a-primitive-data-type"></a>기본 데이터 형식을 기반으로 사용자 지정 클레임을 만들려면  
  
1. 클레임 형식, 리소스 값 및 권한을 <xref:System.IdentityModel.Claims.Claim.%23ctor%28System.String%2CSystem.Object%2CSystem.String%29> 생성자에 전달하여 사용자 지정 클레임을 만듭니다.  
  
    1. 클레임 형식의 고유 값을 결정합니다.  
  
         클레임 형식은 고유한 문자열 식별자입니다. 클레임 형식에 사용되는 문자열 식별자를 고유하게 설정하는 작업은 사용자 지정 클레임 디자이너가 담당합니다. WCF에 의해 정의 되는 클레임 형식 목록은 <xref:System.IdentityModel.Claims.ClaimTypes> 클래스를 참조 하세요.  
  
    2. 기본 데이터 형식과 리소스 값을 선택합니다.  
  
         리소스는 개체입니다. 리소스의 CLR 형식은 기본(예: <xref:System.String> 또는 <xref:System.Int32>)이나 serialize할 수 있는 모든 형식일 수 있습니다. WCF에 의해 다양 한 지점에서 클레임이 serialize 되기 때문에 리소스의 CLR 형식을 serialize 할 수 있어야 합니다. 기본 형식은 serialize할 수 있습니다.  
  
    3. WCF에서 정의한 권한을 선택 하거나 사용자 지정 권한에 대해 고유한 값을 선택 합니다.  
  
         권한은 고유한 문자열 식별자입니다. WCF에 의해 정의 되는 권한은 <xref:System.IdentityModel.Claims.Rights> 클래스에서 정의 됩니다.  
  
         권한에 사용되는 문자열 식별자를 고유하게 설정하는 작업은 사용자 지정 클레임 디자이너가 담당합니다.  
  
         다음 코드 예제에서는 `http://example.org/claims/simplecustomclaim` 권한을 사용하여 `Driver's License`라는 리소스에 대해 클레임 형식이 <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>인 사용자 지정 클레임을 만듭니다.  
  
     [!code-csharp[c_CustomClaim#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#4)]
     [!code-vb[c_CustomClaim#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#4)]  
  
### <a name="to-create-a-custom-claim-that-is-based-on-a-non-primitive-data-type"></a>기본이 아닌 데이터 형식을 기반으로 사용자 지정 클레임을 만들려면  
  
1. 클레임 형식, 리소스 값 및 권한을 <xref:System.IdentityModel.Claims.Claim.%23ctor%28System.String%2CSystem.Object%2CSystem.String%29> 생성자에 전달하여 사용자 지정 클레임을 만듭니다.  
  
    1. 클레임 형식의 고유 값을 결정합니다.  
  
         클레임 형식은 고유한 문자열 식별자입니다. 클레임 형식에 사용되는 문자열 식별자를 고유하게 설정하는 작업은 사용자 지정 클레임 디자이너가 담당합니다. WCF에 의해 정의 되는 클레임 형식 목록은 <xref:System.IdentityModel.Claims.ClaimTypes> 클래스를 참조 하세요.  
  
    2. serialize할 수 있는 기본이 아닌 리소스 형식을 선택하거나 정의합니다.  
  
         리소스는 개체입니다. WCF에 의해 다양 한 지점에서 클레임이 serialize 되기 때문에 리소스의 CLR 형식을 serialize 할 수 있어야 합니다. 기본 형식은 이미 serialize할 수 있습니다.  
  
         새 형식을 정의하는 경우 <xref:System.Runtime.Serialization.DataContractAttribute>를 클래스에 적용합니다. 또한 클레임의 일부로 serialize할 수 있어야 하는 새 형식의 모든 멤버에 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성을 적용합니다.  
  
         다음 코드 예제에서는 `MyResourceType`이라는 사용자 지정 리소스 형식을 정의합니다.  
  
         [!code-csharp[c_CustomClaim#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#2)] 
         [!code-vb[c_CustomClaim#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#2)]        
  
    3. WCF에서 정의한 권한을 선택 하거나 사용자 지정 권한에 대해 고유한 값을 선택 합니다.  
  
         권한은 고유한 문자열 식별자입니다. WCF에 의해 정의 되는 권한은 <xref:System.IdentityModel.Claims.Rights> 클래스에서 정의 됩니다.  
  
         권한에 사용되는 문자열 식별자를 고유하게 설정하는 작업은 사용자 지정 클레임 디자이너가 담당합니다.  
  
         다음 코드 예제에서는 `http://example.org/claims/complexcustomclaim` 권한을 사용하여 클레임 형식이 `MyResourceType`이고 사용자 지정 리소스 형식이 <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>인 사용자 지정 클레임을 만듭니다.  
  
         [!code-csharp[c_CustomClaim#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#5)] 
         [!code-vb[c_CustomClaim#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#5)]     
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 기본 리소스 형식의 사용자 지정 클레임과 기본이 아닌 리소스 형식의 사용자 지정 클레임을 만드는 방법을 보여 줍니다.  
  
 [!code-csharp[c_CustomClaim#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#0)]
 [!code-vb[c_CustomClaim#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#0)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.IdentityModel.Claims.Claim>
- <xref:System.IdentityModel.Claims.Rights>
- <xref:System.IdentityModel.Claims.ClaimTypes>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [ID 모델을 사용하여 클레임 및 권한 부여 관리](../feature-details/managing-claims-and-authorization-with-the-identity-model.md)
