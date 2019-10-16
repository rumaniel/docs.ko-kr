---
title: '방법: Point4D 구조체가 동일한지 여부 테스트'
ms.date: 03/30/2017
helpviewer_keywords:
- inequality [WPF], testing Point4D structures for
- equality [WPF], testing Point4D structures for
- testing [WPF], Point4D structures for equality
- Point4D structures [WPF], testing for inequality
- testing [WPF], Point4D structures for inequality
- Point4D structures [WPF], testing for equality
ms.assetid: e004a67e-db7f-4af8-a31f-e6b2a44ccf34
ms.openlocfilehash: ce1188e99ef2b0682427cc2e227aaccd27f7c4f4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62050638"
---
# <a name="how-to-test-point4d-structures-for-equality-and-inequality"></a>방법: Point4D 구조체가 동일한지 여부 테스트
이 예제에서는 테스트 <xref:System.Windows.Media.Media3D.Point4D> 같음 및 다름에 대 한 구조입니다.  
  
 다음 코드를 테스트 하는 방법을 보여 줍니다 <xref:System.Windows.Media.Media3D.Point4D> 같음 및 같지 않음 사용에 대 한 구조는 <xref:System.Windows.Media.Media3D.Point4D> 같음 메서드.  <xref:System.Windows.Media.Media3D.Point4D> 구조는 오버 로드 된 같음을 사용 하 여 같음 테스트 (`==`) 연산자를 오버 로드 된 같지 않음을 사용 하 여 다른 지에 대 한 다음 (`!=`) 연산자를 마지막으로 <xref:System.Windows.Media.Media3D.Point3D> 구조 및 <xref:System.Windows.Media.Media3D.Point4D> 구조 정적을 사용 하 여 같은지 확인 <xref:System.Windows.Media.Media3D.Point4D.Equals%2A> 메서드.  
  
## <a name="example"></a>예제  
 [!code-csharp[3DGallery_procedural_snip#Point4DEqualityExample_csharp](~/samples/snippets/csharp/VS_Snippets_Wpf/3DGallery_procedural_snip/CSharp/Misc3DOperationsExample.cs#point4dequalityexample_csharp)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Media3D.Point4D.op_Equality%2A>
- <xref:System.Windows.Media.Media3D.Point4D.op_Inequality%2A>
- <xref:System.Windows.Media.Media3D.Point4D.Equals%2A>
