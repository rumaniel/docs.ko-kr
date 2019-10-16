---
title: '방법: .NET에서 기본적인 문자열 조작 수행'
description: 여러 문자열 메서드를 호출하는 예제를 참조하세요.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [.NET Framework], examples
ms.assetid: 121d1eae-251b-44c0-8818-57da04b8215e
author: rpetrusha
ms.author: ronpet
ms.custom: seodec18
ms.openlocfilehash: 11f8043745c631a642b437339240cbf06fc8df5b
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53130639"
---
# <a name="how-to-perform-basic-string-manipulations-in-net"></a>방법: .NET에서 기본적인 문자열 조작 수행
다음 예제에서는 [기본적인 문자열 작업](../../../docs/standard/base-types/basic-string-operations.md) 항목에 설명된 메서드 중 일부를 사용하여 실제 응용 프로그램에서 발견될 수 있는 방식으로 문자열 조작을 수행하는 클래스를 생성합니다. `MailToData` 클래스는 개인의 이름과 주소를 별도 속성에 저장하고 `City`, `State` 및 `Zip` 필드를 사용자에게 표시할 단일 문자열로 결합하는 방법을 제공합니다. 또한 이 클래스를 사용하면 사용자가 구/군/시, 시/도 및 우편 번호 정보를 단일 문자열로 입력할 수 있습니다. 응용 프로그램에서 단일 문자열을 자동으로 구문 분석하고 해당 속성에 적절한 정보를 입력합니다.  
  
 편의상, 이 예제에서는 명령줄 인터페이스가 있는 콘솔 응용 프로그램을 사용합니다.  
  
## <a name="example"></a>예  
 [!code-csharp[Conceptual.String.BasicOps#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/basicops.cs#1)]
 [!code-vb[Conceptual.String.BasicOps#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/basicops.vb#1)]  
  
 앞의 코드를 실행하면 사용자 이름과 주소를 입력하라는 메시지가 표시됩니다. 응용 프로그램은 해당 속성에 정보를 저장하고 구/군/시, 시/도 및 우편 번호 정보를 표시하는 단일 문자열을 만들어 사용자에게 다시 정보를 표시합니다.  
  
## <a name="see-also"></a>참고 항목

- [기본적인 문자열 작업](../../../docs/standard/base-types/basic-string-operations.md)
