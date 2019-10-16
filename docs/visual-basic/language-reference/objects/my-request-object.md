---
title: My. Request 개체 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- My.MyWebExtension.Request
- My.Request
helpviewer_keywords:
- My.Request object
ms.assetid: 93d5f0e2-6b60-4a2c-8652-d90216f6ad10
ms.openlocfilehash: da17872acb839cdcdfa7f80c3f58f26dc25d0ab5
ms.sourcegitcommit: 29a9b29d8b7d07b9c59d46628da754a8bff57fa4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69567467"
---
# <a name="myrequest-object"></a>My.Request 개체
요청된 페이지에 대한 <xref:System.Web.HttpRequest> 개체를 가져옵니다.  
  
## <a name="remarks"></a>설명  
 `My.Request` 개체에는 현재 HTTP 요청에 대한 정보가 포함됩니다.  
  
 `My.Request` 개체는 ASP.NET 애플리케이션에만 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `My.Request` 개체에서 헤더 컬렉션을 가져오고 `My.Response` 개체를 사용 하 여 ASP.NET 페이지에 씁니다.  
  
 [!code-aspx-vb[VbVbalrMyWeb#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyWeb/VB/Default.aspx#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Web.HttpRequest>
- [My.Response 개체](../../../visual-basic/language-reference/objects/my-response-object.md)
