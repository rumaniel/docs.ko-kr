---
title: '방법: 리플렉션 공급자 (WCF Data Services)를 사용 하 여 피드 사용자 지정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, customizing
- WCF Data Services, customizing feeds
ms.assetid: 00c23dcf-9bb8-459a-a012-6c4d9bcad7e9
ms.openlocfilehash: 43f46729ba84356bcb6507779bef9e4fd35bc315
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790681"
---
# <a name="how-to-customize-feeds-with-the-reflection-provider-wcf-data-services"></a>방법: 리플렉션 공급자 (WCF Data Services)를 사용 하 여 피드 사용자 지정
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]를 사용하면 엔터티의 속성이 AtomPub 프로토콜에 정의된 사용하지 않은 요소에 매핑될 수 있도록 데이터 서비스 응답의 Atom serialization을 사용자 지정할 수 있습니다. 이 항목에서는 리플렉션 공급자를 사용하여 정의된 데이터 모델의 엔터티 형식에 대한 매핑 특성을 정의하는 방법을 보여 줍니다. 자세한 내용은 [사용자 지정 피드](feed-customization-wcf-data-services.md)합니다.  
  
 이 예제의 [데이터 모델은 방법: 리플렉션 공급자를 사용 하 여 데이터 서비스 만들기](create-a-data-service-using-rp-wcf-data-services.md)  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Order` 형식의 두 속성이 모두 기존 Atom 요소에 매핑됩니다. `Product` 형식의 `Item` 속성은 별도 네임스페이스에 있는 사용자 지정 피드 특성에 매핑됩니다.  
  
 [!code-csharp[Astoria Custom Feeds#CustomIQueryableFeeds](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_custom_feeds/cs/orderitems.svc.cs#customiqueryablefeeds)]
 [!code-vb[Astoria Custom Feeds#CustomIQueryableFeeds](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_custom_feeds/vb/orderitems.svc.vb#customiqueryablefeeds)]  
  
## <a name="example"></a>예제  
 위 예제에서는 URI `http://myservice/OrderItems.svc/Orders(0)?$expand=Items`에 대해 다음 결과를 반환합니다.  
  
 [!code-xml[Astoria Custom Feeds#IQueryableFeedResultInline](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria_custom_feeds/xml/iqueryablefeedresultinline.xml#iqueryablefeedresultinline)]  
  
## <a name="see-also"></a>참고자료

- [리플렉션 공급자](reflection-provider-wcf-data-services.md)
