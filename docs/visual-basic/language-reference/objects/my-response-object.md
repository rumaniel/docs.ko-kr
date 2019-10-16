---
title: My.settings 개체 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- My.MyWebExtension.Response
- My.Response
helpviewer_keywords:
- My.Response object
ms.assetid: 626359bc-3165-40b4-bfaf-2c610e26eb5b
ms.openlocfilehash: a50701998011c25c600c2a3763459c1aba3cc59a
ms.sourcegitcommit: 29a9b29d8b7d07b9c59d46628da754a8bff57fa4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69567458"
---
# <a name="myresponse-object"></a>My.Response 개체
와 연결 <xref:System.Web.HttpResponse> 된 개체를 가져옵니다. <xref:System.Web.UI.Page> 이 개체를 사용하여 HTTP 응답 데이터를 클라이언트에 보낼 수 있고 이 개체는 해당 응답에 대한 정보를 포함합니다.  
  
## <a name="remarks"></a>설명  
 개체 `My.Response` 는 페이지와 관련 <xref:System.Web.HttpResponse> 된 현재 개체를 포함 합니다.  
  
 개체 `My.Response` 는 ASP.NET 응용 프로그램에만 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `My.Request` 개체에서 헤더 컬렉션을 가져오고 `My.Response` 개체를 사용 하 여 ASP.NET 페이지에 씁니다.  
  
 [!code-aspx-vb[VbVbalrMyWeb#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyWeb/VB/Default.aspx#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Web.HttpResponse>
- [My.Request 개체](../../../visual-basic/language-reference/objects/my-request-object.md)
