---
title: '방법: Visual Basic StringBuilder를 사용 하 여 문자열 만들기'
ms.date: 07/20/2015
helpviewer_keywords:
- StringBuilder class
- strings [Visual Basic], using StringBuilder
ms.assetid: 9c042880-aa16-432e-9ccb-cd00abda9ae3
ms.openlocfilehash: 19e036abc9d25ec7fdfd6c33ebb420ec4f503cbc
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700101"
---
# <a name="how-to-create-strings-using-a-stringbuilder-in-visual-basic"></a>방법: Visual Basic StringBuilder를 사용 하 여 문자열 만들기

이 예제에서는 <xref:System.Text.StringBuilder> 클래스를 사용 하 여 여러 개의 작은 문자열에서 긴 문자열을 생성 합니다. @No__t-0 클래스는 여러 문자열을 연결 하는 `&=` 연산자 보다 더 효율적입니다.

## <a name="example"></a>예제

다음 예에서는 <xref:System.Text.StringBuilder> 클래스의 인스턴스를 만들고 해당 인스턴스에 1000 문자열을 추가한 다음 해당 문자열 표현을 반환 합니다.

 [!code-vb[VbVbalrStrings#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#70)]

## <a name="see-also"></a>참조

- [StringBuilder 클래스 사용](../../../../standard/base-types/stringbuilder.md)
- [&= 연산자](../../../language-reference/operators/and-assignment-operator.md)
- [문자열](index.md)
- [새 문자열 만들기](../../../../standard/base-types/creating-new.md)
- [문자열 조작](../../../../standard/base-types/manipulating-strings.md)
