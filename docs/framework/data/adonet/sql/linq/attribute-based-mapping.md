---
title: 특성 기반 매핑
ms.date: 03/30/2017
ms.assetid: 6dd89999-f415-4d61-b8c8-237d23d7924e
ms.openlocfilehash: 1e11a2efc3d1afa56a27d6e2c60149a509511080
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248072"
---
# <a name="attribute-based-mapping"></a>특성 기반 매핑
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]특성을 적용 하거나 외부 매핑 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 파일을 사용 하 여 SQL Server 데이터베이스를 개체 모델에 매핑합니다. 이 항목에서는 특성 기반 접근 방법에 대해 간략하게 설명합니다.  
  
 가장 기본적인 형식인 경우에 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 데이터베이스를 <xref:System.Data.Linq.DataContext>에 매핑하고 테이블을 클래스에 매핑하며 열과 관계를 이러한 클래스의 속성에 매핑합니다. 또한 특성을 사용하여 개체 모델에서 상속 계층 구조를 매핑할 수도 있습니다. 자세한 내용은 [방법: Visual Basic 또는 C# ](how-to-generate-the-object-model-in-visual-basic-or-csharp.md)에서 개체 모델을 생성 합니다.  
  
 Visual Studio를 사용 하는 개발자는 일반적으로 개체 관계형 디자이너를 사용 하 여 특성 기반 매핑을 수행 합니다. SQLMetal 명령줄 도구를 사용하거나 특성을 직접 코딩할 수도 있습니다. 자세한 내용은 [방법: Visual Basic 또는 C# ](how-to-generate-the-object-model-in-visual-basic-or-csharp.md)에서 개체 모델을 생성 합니다.  
  
> [!NOTE]
> 이외에도 외부 XML 파일을 사용하여 매핑할 수도 있습니다. 자세한 내용은 [외부 매핑](external-mapping.md)을 참조 하세요.  
  
 다음 단원에서는 특성 기반 매핑에 대해 더 자세히 설명합니다. 자세한 내용은 <xref:System.Data.Linq.Mapping> 네임스페이스를 참조하세요.  
  
## <a name="databaseattribute-attribute"></a>DatabaseAttribute 특성  
 연결에서 이름이 제공되지 않은 경우 데이터베이스의 기본 이름을 지정하려면 이 특성을 사용합니다. 이 특성은 선택 사항이지만 이 특성을 사용할 경우 다음 표에 설명된 대로 <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> 속성을 적용해야 합니다.  
  
|속성|형식|기본값|Description|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>|문자열|<xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A>을 참조하세요.|해당 <xref:System.Data.Linq.Mapping.DatabaseAttribute.Name%2A> 속성과 함께 사용되어 데이터베이스의 이름을 지정합니다.|  
  
 자세한 내용은 <xref:System.Data.Linq.Mapping.DatabaseAttribute>을 참조하세요.  
  
## <a name="tableattribute-attribute"></a>TableAttribute 특성  
 클래스를 데이터베이스 테이블 또는 데이터베이스 뷰와 연결된 엔터티 클래스로 지정하려면 이 특성을 사용합니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 이 특성이 있는 클래스를 영구 클래스로 처리합니다. 다음 표에서는 <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A> 속성에 대해 설명합니다.  
  
|속성|형식|기본값|설명|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.TableAttribute.Name%2A>|문자열|클래스 이름과 동일한 문자열|클래스를 데이터베이스 테이블과 연결된 엔터티 클래스로 지정합니다.|  
  
 자세한 내용은 <xref:System.Data.Linq.Mapping.TableAttribute>을 참조하세요.  
  
## <a name="columnattribute-attribute"></a>ColumnAttribute 특성  
 엔터티 클래스의 멤버가 데이터베이스 테이블의 열을 나타내도록 지정하려면 이 특성을 사용합니다. 이 특성은 모든 필드나 속성에 적용할 수 있습니다.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]이 변경 내용을 데이터베이스에 저장할 때 열로 식별된 멤버만 검색 및 유지됩니다. 이 특성이 없는 멤버는 비영구적인 것으로 간주되며 삽입 또는 업데이트를 위해 전송되지 않습니다.  
  
 다음 표에서는 이 특성의 속성을 설명합니다.  
  
|속성|형식|기본값|설명|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A>|AutoSync|Never|삽입 또는 업데이트 작업 후에 값을 검색하도록 CLR(공용 언어 런타임)에 지시합니다.<br /><br /> 옵션: 항상, Never, OnUpdate, OnInsert입니다.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A>|Boolean|`true`|열이 null 값을 포함할 수 있다는 것을 나타냅니다.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A>|String|유추된 데이터베이스 열 형식|데이터베이스 형식과 한정자를 사용하여 데이터베이스 열의 형식을 지정합니다.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.Expression%2A>|String|Empty|데이터베이스에서 계산 열을 정의합니다.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A>|Boolean|`false`|열이 데이터베이스가 자동으로 생성하는 값을 포함한다는 것을 나타냅니다.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsDiscriminator%2A>|Boolean|`false`|열이 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 상속 계층 구조에 대한 판별자 값을 포함한다는 것을 나타냅니다.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsPrimaryKey%2A>|Boolean|`false`|이 클래스 멤버가 테이블의 기본 키이거나 기본 키의 일부인 열을 나타낸다는 것을 지정합니다.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A>|Boolean|`false`|멤버의 열 형식을 데이터베이스 타임스탬프 또는 버전 번호로 식별합니다.|  
|<xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A>|UpdateCheck|멤버에 대한 `Always`이 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsVersion%2A>가 아니면 `true`|[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]이 낙관적 동시성 충돌 감지에 접근하는 방법을 지정합니다.|  
  
 자세한 내용은 <xref:System.Data.Linq.Mapping.ColumnAttribute>을 참조하세요.  
  
> [!NOTE]
> AssociationAttribute 및 ColumnAttribute Storage 속성 값은 대/소문자를 구분합니다. 예를 들어 AssociationAttribute.Storage 속성의 특성에 사용하는 값은 코드의 다른 곳에서 사용하는 해당 속성 이름과 대/소문자가 동일해야 합니다. 이 일반적으로 대/소문자 구분, Visual Basic을 포함 하지 않는 이더라도 모든.NET 프로그래밍 언어에 적용 됩니다. Storage 속성에 대한 자세한 내용은 <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A?displayProperty=nameWithType>를 참조하세요.  
  
## <a name="associationattribute-attribute"></a>AssociationAttribute 특성  
 외래 키와 기본 키 사이의 관계와 같은 데이터베이스 내 연결을 나타내려면 이 특성을 사용하여 속성을 지정합니다. 관계에 대 한 자세한 내용은 [방법: 데이터베이스 관계 매핑](how-to-map-database-relationships.md)을 참조하세요.  
  
 다음 표에서는 이 특성의 속성을 설명합니다.  
  
|속성|형식|기본값|설명|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.DeleteOnNull%2A>|Boolean|`false`|외래 키 멤버가 모두 null을 허용하지 않는 연결에 배치되는 경우 연결이 null로 설정되면 개체를 삭제합니다.|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.DeleteRule%2A>|String|없음|삭제 동작을 연결에 추가합니다.|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.IsForeignKey%2A>|Boolean|`false`|true이면 데이터베이스 관계를 나타내는 연결의 외래 키로 멤버를 지정합니다.|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.IsUnique%2A>|Boolean|`false`|true이면 외래 키에 대한 고유성 제약 조건을 나타냅니다.|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.OtherKey%2A>|String|관련 클래스의 ID|대상 엔터티 클래스의 하나 이상의 멤버를 연결 반대쪽의 키 값으로 지정합니다.|  
|<xref:System.Data.Linq.Mapping.AssociationAttribute.ThisKey%2A>|String|포함하는 클래스의 ID|연결 이쪽의 키 값을 나타낼 이 엔터티 클래스의 멤버를 지정합니다.|  
  
 자세한 내용은 <xref:System.Data.Linq.Mapping.AssociationAttribute>을 참조하세요.  
  
> [!NOTE]
> AssociationAttribute 및 ColumnAttribute Storage 속성 값은 대/소문자를 구분합니다. 예를 들어 AssociationAttribute.Storage 속성의 특성에 사용하는 값은 코드의 다른 곳에서 사용하는 해당 속성 이름과 대/소문자가 동일해야 합니다. 이 일반적으로 대/소문자 구분, Visual Basic을 포함 하지 않는 이더라도 모든.NET 프로그래밍 언어에 적용 됩니다. Storage 속성에 대한 자세한 내용은 <xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A?displayProperty=nameWithType>를 참조하세요.  
  
## <a name="inheritancemappingattribute-attribute"></a>InheritanceMappingAttribute 특성  
 상속 계층 구조를 매핑하려면 이 특성을 사용합니다.  
  
 다음 표에서는 이 특성의 속성을 설명합니다.  
  
|속성|형식|기본값|Description|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.Code%2A>|String|없음 값을 제공해야 함|판별자의 코드 값을 지정합니다.|  
|<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.IsDefault%2A>|Boolean|`false`|true이면 저장소의 판별자 값이 지정된 값 중 하나와 일치하지 않을 경우 이 형식의 개체를 인스턴스화합니다.|  
|<xref:System.Data.Linq.Mapping.InheritanceMappingAttribute.Type%2A>|형식|없음 값을 제공해야 함|계층 구조에서 클래스의 형식을 지정합니다.|  
  
 자세한 내용은 <xref:System.Data.Linq.Mapping.InheritanceMappingAttribute>을 참조하세요.  
  
## <a name="functionattribute-attribute"></a>FunctionAttribute 특성  
 데이터베이스의 저장 프로시저나 사용자 정의 함수를 나타내는 것으로 메서드를 지정하려면 이 특성을 사용합니다.  
  
 다음 표에서는 이 특성의 속성을 설명합니다.  
  
|속성|형식|기본값|Description|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.FunctionAttribute.IsComposable%2A>|Boolean|`false`|false이면 저장 프로시저에 대한 매핑을 나타냅니다. true이면 사용자 정의 함수에 대한 매핑을 나타냅니다.|  
|<xref:System.Data.Linq.Mapping.FunctionAttribute.Name%2A>|문자열|데이터베이스에 있는 이름과 동일한 문자열|저장 프로시저 또는 사용자 정의 함수의 이름을 지정합니다.|  
  
 자세한 내용은 <xref:System.Data.Linq.Mapping.FunctionAttribute>을 참조하세요.  
  
## <a name="parameterattribute-attribute"></a>ParameterAttribute 특성  
 저장 프로시저 메서드에서 입력 매개 변수를 매핑하려면 이 특성을 사용합니다.  
  
 다음 표에서는 이 특성의 속성을 설명합니다.  
  
|속성|형식|기본값|Description|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.ParameterAttribute.DbType%2A>|문자열|없음|데이터베이스 형식을 지정합니다.|  
|<xref:System.Data.Linq.Mapping.ParameterAttribute.Name%2A>|문자열|데이터베이스에 있는 매개 변수 이름과 동일한 문자열|매개 변수의 이름을 지정합니다.|  
  
 자세한 내용은 <xref:System.Data.Linq.Mapping.ParameterAttribute>을 참조하세요.  
  
## <a name="resulttypeattribute-attribute"></a>ResultTypeAttribute 특성  
 결과 형식을 지정하려면 이 특성을 사용합니다.  
  
 다음 표에서는 이 특성의 속성을 설명합니다.  
  
|속성|형식|기본값|설명|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.ResultTypeAttribute.Type%2A>|형식|(None)|<xref:System.Data.Linq.IMultipleResults>를 반환하는 저장 프로시저에 매핑되는 메서드에 사용됩니다. 저장 프로시저에 대해 유효하거나 필요한 형식 매핑을 선언합니다.|  
  
 자세한 내용은 <xref:System.Data.Linq.Mapping.ResultTypeAttribute>을 참조하세요.  
  
## <a name="dataattribute-attribute"></a>DataAttribute 특성  
 이름 및 전용 스토리지 필드를 지정하려면 이 특성을 사용합니다.  
  
 다음 표에서는 이 특성의 속성을 설명합니다.  
  
|속성|형식|기본값|Description|  
|--------------|----------|-------------|-----------------|  
|<xref:System.Data.Linq.Mapping.DataAttribute.Name%2A>|String|데이터베이스에 있는 이름과 동일|테이블, 열 등의 이름을 지정합니다.|  
|<xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A>|String|공용 접근자|기본 스토리지 필드의 이름을 지정합니다.|  
  
 자세한 내용은 <xref:System.Data.Linq.Mapping.DataAttribute>을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [참조](reference.md)
