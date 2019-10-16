---
title: '방법: 전용 스토리지 필드 지정'
ms.date: 03/30/2017
ms.assetid: 5a40e816-cc6e-43a0-b32a-9caaa0ab6912
ms.openlocfilehash: e6e6a4e28fbfb327f25874844f28bcbafa6d2805
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793208"
---
# <a name="how-to-specify-private-storage-fields"></a>방법: 전용 스토리지 필드 지정
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 특성의속성을사용하여기본저장소필드<xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A>의이름을 지정합니다<xref:System.Data.Linq.Mapping.DataAttribute> .  
  
 코드 예는 <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A>를 참조하세요.  
  
### <a name="to-specify-the-name-of-an-underlying-storage-field"></a>기본 스토리지 필드의 이름을 지정하려면  
  
1. <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A> 특성에 <xref:System.Data.Linq.Mapping.ColumnAttribute> 속성을 추가합니다.  
  
2. 필드의 이름을 <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A> 속성의 값으로 지정합니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to SQL 개체 모델](the-linq-to-sql-object-model.md)
- [방법: 코드 편집기를 사용 하 여 엔터티 클래스 사용자 지정](how-to-customize-entity-classes-by-using-the-code-editor.md)
