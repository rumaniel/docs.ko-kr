---
title: '방법: Windows Api (Visual Basic)를 호출 합니다.'
ms.date: 07/20/2015
helpviewer_keywords:
- API calls [Visual Basic]
- Windows API, calling
- API calls [Visual Basic], platform invoke
- calls [Visual Basic], stored procedures
ms.assetid: 27d75f0a-54ab-4ee1-b91d-43513a19b12d
ms.openlocfilehash: 3769da28e1c9a27c8363b0d6ec639cedaf0f03be
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64624850"
---
# <a name="how-to-call-windows-apis-visual-basic"></a>방법: Windows Api (Visual Basic)를 호출 합니다.
정의 하 고 호출 하는이 예제는 `MessageBox` user32.dll의 함수 다음에 문자열을 전달 합니다.  
  
## <a name="example"></a>예제  
 [!code-vb[VbVbalrInterop#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrInterop/VB/Class1.vb#1)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- <xref:System> 네임스페이스에 대한 참조  
  
## <a name="robust-programming"></a>강력한 프로그래밍  
 다음 조건에서 예외가 발생합니다.  
  
- 메서드가 static이 아닙니다.는 추상 클래스 또는 이전에 정의 된 합니다. 부모 형식이 인터페이스 인지 길이의 *이름을* 또는 *dllName* 은 0입니다. (<xref:System.ArgumentException>)  
  
- *이름을* 하거나 *dllName* 는 `Nothing`합니다. (<xref:System.ArgumentNullException>)  
  
- 포함하는 형식은 `CreateType`을 사용하여 이전에 만든 것입니다. (<xref:System.InvalidOperationException>)  
  
## <a name="see-also"></a>참고자료

- [플랫폼 호출 자세히 보기](../../../framework/interop/consuming-unmanaged-dll-functions.md#a-closer-look-at-platform-invoke)
- [플랫폼 호출 예제](../../../framework/interop/platform-invoke-examples.md)
- [관리되지 않는 DLL 함수 사용](../../../framework/interop/consuming-unmanaged-dll-functions.md)
- [내보내기를 리플렉션 사용 하 여 메서드를 정의 합니다.](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/w63y4d4f(v=vs.100))
- [연습: Windows API 호출](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)
- [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)
