---
title: 스키마를 가져와 클래스 생성
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, schema import and export
- XsdDataContractImporter class
ms.assetid: b9170583-8c34-43bd-97bb-6c0c8dddeee0
ms.openlocfilehash: dc33088c3519bfd088ed64a4de087c5086890804
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918475"
---
# <a name="importing-schema-to-generate-classes"></a>스키마를 가져와 클래스 생성
WCF (Windows Communication Foundation)에서 사용할 수 있는 스키마에서 클래스를 생성 하려면 <xref:System.Runtime.Serialization.XsdDataContractImporter> 클래스를 사용 합니다. 이 항목에서는 프로세스와 변형에 대해 설명합니다.  
  
## <a name="the-import-process"></a>가져오기 프로세스
 스키마 가져오기 프로세스는 <xref:System.Xml.Schema.XmlSchemaSet>로 시작되고 <xref:System.CodeDom.CodeCompileUnit>을 생성합니다.  
  
 는 `XmlSchemaSet` XSD (XML 스키마 정의 언어) 스키마 문서 집합을 나타내는 .NET Framework SOM (스키마 개체 모델)의 일부입니다. XSD 문서 집합에서 `XmlSchemaSet` 개체를 만들려면 <xref:System.Xml.Schema.XmlSchema>를 사용하여 각 문서를 <xref:System.Xml.Serialization.XmlSerializer> 개체로 deserialize하고 이러한 개체를 새 `XmlSchemaSet`에 추가합니다.  
  
 는 `CodeCompileUnit` 추상 방식으로 .NET Framework 코드를 나타내는 CodeDOM (.NET Framework 코드 문서 개체 모델)의 일부입니다. `CodeCompileUnit`에서 실제 코드를 생성하려면 <xref:System.CodeDom.Compiler.CodeDomProvider> 또는 <xref:Microsoft.CSharp.CSharpCodeProvider> 클래스 같은 <xref:Microsoft.VisualBasic.VBCodeProvider> 클래스의 하위 클래스를 사용합니다.  
  
### <a name="to-import-a-schema"></a>스키마를 가져오려면  
  
1. <xref:System.Runtime.Serialization.XsdDataContractImporter>의 인스턴스를 만듭니다.  
  
2. 선택 사항입니다. 생성자의 `CodeCompileUnit`를 전달합니다. 스키마를 가져오는 중 생성된 형식은 빈 `CodeCompileUnit`로 시작하지 않고 이 `CodeCompileUnit` 인스턴스에 추가됩니다.  
  
3. 선택 사항입니다. <xref:System.Runtime.Serialization.XsdDataContractImporter.CanImport%2A> 메서드 중 하나를 호출합니다. 메서드는 지정된 스키마가 올바른 데이터 계약 스키마이고 가져올 수 있는지 여부를 결정합니다. `CanImport` 메서드는 `Import`(다음 단계)와 동일한 오버로드를 갖습니다.  
  
4. 오버로드된 `Import` 메서드 중 하나(예: <xref:System.Runtime.Serialization.XsdDataContractImporter.Import%28System.Xml.Schema.XmlSchemaSet%29> 메서드)를 호출합니다.  
  
     가장 간단한 오버로드는 `XmlSchemaSet`를 사용하고 익명 형식을 포함하여 해당 스키마 집합에 있는 모든 형식을 가져옵니다. 기타 오버로드를 사용하면 XSD 형식이나 가져올 형식 목록을 <xref:System.Xml.XmlQualifiedName> 또는 `XmlQualifiedName` 개체 컬렉션 형태로 지정할 수 있습니다. 이 경우 지정된 형식만 가져옵니다. 오버로드는 <xref:System.Xml.Schema.XmlSchemaElement>에서 특정 요소를 가져오는 `XmlSchemaSet` 및 연결된 형식(익명 형식인지 여부에 관계없이)을 사용합니다. 이 오버로드는 이 요소에 대해 생성된 형식의 데이터 계약 이름을 나타내는 `XmlQualifiedName`을 반환합니다.  
  
     `Import` 메서드를 여러 번 호출하면 동일한 `CodeCompileUnit`에 여러 항목이 추가됩니다. 형식이 이미 있으면 `CodeCompileUnit` 에 생성되지 않습니다. `Import` 개체를 여러 개 사용하는 대신 동일한 `XsdDataContractImporter`에서 `XsdDataContractImporter`를 여러 번 호출합니다. 중복 형식이 생성되지 않도록 하려면 이 방법을 사용하는 것이 좋습니다.  
  
    > [!NOTE]
    > 가져오기 중 오류가 발생하면 `CodeCompileUnit`는 예기치 않은 상태가 됩니다. 실패한 가져오기에서 생성된 `CodeCompileUnit`를 사용하면 보안상 취약해질 수 있습니다.  
  
5. `CodeCompileUnit` 속성을 통해 <xref:System.Runtime.Serialization.XsdDataContractImporter.CodeCompileUnit%2A> 에 액세스합니다.  
  
### <a name="import-options-customizing-the-generated-types"></a>가져오기 옵션: 생성 된 형식 사용자 지정  
 <xref:System.Runtime.Serialization.XsdDataContractImporter.Options%2A>의 <xref:System.Runtime.Serialization.XsdDataContractImporter> 속성을 <xref:System.Runtime.Serialization.ImportOptions> 클래스의 인스턴스로 설정하여 가져오기 프로세스의 다양한 측면을 제어할 수 있습니다. 여러 가지 옵션은 생성되는 형식에 직접 영향을 줍니다.  
  
#### <a name="controlling-the-access-level-generateinternal-or-the-internal-switch"></a>액세스 수준 제어(GenerateInternal 또는 /internal 스위치)  
 이는 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)의 **/sinternal** 스위치에 해당 합니다.  
  
 일반적으로 public 형식은 private 필드 및 일치하는 공용 데이터 멤버 속성을 사용하여 스키마에서 생성됩니다. 대신 내부 형식을 생성하려면 <xref:System.Runtime.Serialization.ImportOptions.GenerateInternal%2A> 속성을 `true`로 설정합니다.  
  
 다음 예제에서는 <xref:System.Runtime.Serialization.ImportOptions.GenerateInternal%2A> 속성이 `true.`로 설정된 경우 내부 클래스로 변환되는 스키마를 보여 줍니다.  
  
 [!code-csharp[c_SchemaImportExport#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#2)]
 [!code-vb[c_SchemaImportExport#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#2)]  
  
#### <a name="controlling-namespaces-namespaces-or-the-namespace-switch"></a>네임스페이스 제어(Namespaces 또는 /namespace 스위치)  
 이는 `Svcutil.exe` 도구의 **/namespace** 스위치에 해당 합니다.  
  
 일반적으로 스키마에서 생성 된 형식은 [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)에 설명 된 매핑에 따라 특정 .NET Framework 네임 스페이스에 해당 하는 각 XSD 네임 스페이스와 함께 .NET Framework 네임 스페이스로 생성 됩니다. <xref:System.Runtime.Serialization.ImportOptions.Namespaces%2A>에 대한 <xref:System.Collections.Generic.Dictionary%602> 속성으로 이 매핑을 사용자 지정할 수 있습니다. 사전에서 지정 된 XSD 네임 스페이스를 찾은 경우 일치 하는 .NET Framework 네임 스페이스도 사전에서 가져옵니다.  
  
 예를 들어 다음 스키마를 생각해 볼 수 있습니다.  
  
 [!code-xml[c_SchemaImportExport#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/common/source.config#10)]  
  
 다음 예제에서는 `Namespaces` 속성을 사용 하 여 `http://schemas.contoso.com/carSchema` 네임 스페이스를 "Contoso. 자동차"에 매핑합니다.  
  
 [!code-csharp[c_SchemaImportExport#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#8)]
 [!code-vb[c_SchemaImportExport#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#8)]  
  
#### <a name="adding-the-serializableattribute-generateserializable-or-the-serializable-switch"></a>SerializableAttribute 추가(GenerateSerializable 또는 /serializable 스위치)  
 이는 `Svcutil.exe` 도구의 **도구의/serializable** 스위치에 해당 합니다.  
  
 경우에 따라 스키마에서 생성 된 형식을 .NET Framework 런타임 serialization 엔진 (예: <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter?displayProperty=nameWithType> <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> 및 클래스)과 함께 사용할 수 있도록 하는 것이 중요 합니다. .NET Framework 원격 기능에 형식을 사용 하는 경우에 유용 합니다. 이 기능을 사용하려면 일반적인 <xref:System.SerializableAttribute> 특성 외에도 <xref:System.Runtime.Serialization.DataContractAttribute> 특성을 생성된 형식에 적용해야 합니다. `GenerateSerializable` 가져오기 옵션이 `true`로 설정되어 있으면 이 특성이 자동으로 생성됩니다.  
  
 다음 예제에서는 `Vehicle` 가져오기 옵션을 `GenerateSerializable`로 설정하여 생성된 `true` 클래스를 보여 줍니다.  
  
 [!code-csharp[c_SchemaImportExport#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#4)]
 [!code-vb[c_SchemaImportExport#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#4)]  
  
#### <a name="adding-data-binding-support-enabledatabinding-or-the-enabledatabinding-switch"></a>데이터 바인딩 지원 추가(EnableDataBinding 또는 /enableDataBinding 스위치)  
 이는 Svcutil.exe 도구의 **/enableDataBinding** 스위치에 해당 합니다.  
  
 경우에 따라 스키마에서 생성된 형식을 그래픽 사용자 인터페이스 구성 요소에 바인딩하여 이러한 형식의 인스턴스를 업데이트할 경우 자동으로 UI가 업데이트되도록 할 수도 있습니다. `XsdDataContractImporter`는 속성을 변경할 경우 이벤트가 트리거되는 방식으로 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 구현하는 형식을 생성할 수 있습니다. Windows Presentation Foundation (WPF)와 같이이 인터페이스를 지 원하는 클라이언트 UI 프로그래밍 환경에서 사용할 형식을 생성 하는 경우이 기능을 사용 하려면 <xref:System.Runtime.Serialization.ImportOptions.EnableDataBinding%2A> 속성을로 `true` 설정 합니다.  
  
 다음 예제에서는 `Vehicle`을 <xref:System.Runtime.Serialization.ImportOptions.EnableDataBinding%2A>로 설정하여 생성된 `true` 클래스를 보여 줍니다.  
  
 [!code-csharp[C_SchemaImportExport#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#5)]
 [!code-vb[C_SchemaImportExport#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#5)]  
  
### <a name="import-options-choosing-collection-types"></a>가져오기 옵션: 컬렉션 형식 선택  
 XML의 두 가지 특수 패턴은 항목 컬렉션, 즉 항목 목록 및 한 항목과 다른 항목 간의 연결을 나타냅니다. 다음은 문자열 목록의 예입니다.  
  
 [!code-xml[C_SchemaImportExport#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/common/source.config#11)]  
  
 다음은 문자열과 정수(`city name` 및 `population`) 간의 연결 예입니다.  
  
 [!code-xml[C_SchemaImportExport#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/common/source.config#12)]  
  
> [!NOTE]
> 모든 연결을 목록으로 간주할 수도 있습니다. 예를 들어 앞의 연결을 두 개의 필드(문자열 필드 및 정수 필드)가 있는 복잡한 `city` 개체 목록으로 간주할 수 있습니다. 두 패턴은 모두 XSD 스키마에서 하나로 표현됩니다. 목록과 연결을 구분할 수 있는 방법이 없으므로 WCF와 관련 된 특별 한 주석이 스키마에 존재 하지 않는 한 이러한 패턴은 항상 목록으로 처리 됩니다. 주석은 지정된 패턴이 연결을 나타냄을 가리킵니다. 자세한 내용은 [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)를 참조 하세요.  
  
 일반적으로 목록은 컬렉션에 대 한 표준 명명 패턴을 따르는지 여부에 따라 제네릭 목록에서 또는 .NET Framework 배열로 파생 되는 컬렉션 데이터 계약으로 가져옵니다. 이에 대해서는 [데이터 계약의 컬렉션 형식](../../../../docs/framework/wcf/feature-details/collection-types-in-data-contracts.md)에 자세히 설명 되어 있습니다. 연결은 일반적으로 <xref:System.Collections.Generic.Dictionary%602> 또는 사전 개체에서 파생된 컬렉션 데이터 계약으로 가져옵니다. 예를 들어 다음 스키마를 생각해 볼 수 있습니다.  
  
 [!code-xml[c_SchemaImportExport#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/common/source.config#13)]  
  
 이 스키마는 다음과 같이 가져옵니다(읽기 쉽도록 속성 대신 필드가 표시됨).  
  
 [!code-csharp[c_SchemaImportExport#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#6)]
 [!code-vb[c_SchemaImportExport#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#6)]  
  
 이러한 스키마 패턴에 대해 생성된 컬렉션 형식을 사용자 지정할 수 있습니다. 예를 들어 형식을 목록 상자에 바인딩하고 컬렉션 콘텐츠를 변경할 때 자동으로 업데이트되도록 <xref:System.ComponentModel.BindingList%601> 클래스 대신 <xref:System.Collections.Generic.List%601>에서 파생된 컬렉션을 생성할 수 있습니다. 이렇게 하려면 <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A> 클래스의 <xref:System.Runtime.Serialization.ImportOptions> 속성을 사용할 컬렉션 형식(이후부터는 참조된 형식) 목록으로 설정합니다. 컬렉션을 가져올 때는 이 참조된 컬렉션 형식 목록이 검색되고, 가장 일치하는 컬렉션이 있으면 해당 컬렉션이 사용됩니다. 목록은 지원되는 모든 컬렉션 형식에 대해 일치되지만 연결은 제네릭 또는 비제네릭 <xref:System.Collections.IDictionary> 인터페이스를 구현하는 형식에 대해서만 일치됩니다.  
  
 예를 들어 <xref:System.Runtime.Serialization.ImportOptions.ReferencedCollectionTypes%2A> 속성을 <xref:System.ComponentModel.BindingList%601>로 설정하면 앞의 예에서 `people` 형식은 다음과 같이 생성됩니다.  
  
 [!code-csharp[C_SchemaImportExport#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#7)]
 [!code-vb[C_SchemaImportExport#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#7)]  
  
 폐쇄형 제네릭이 가장 일치하는 항목으로 간주됩니다. 예를 들어 `BindingList(Of Integer)` 및 <xref:System.Collections.ArrayList> 형식이 참조된 형식의 컬렉션으로 전달되는 경우 스키마에 있는 모든 정수 목록을 `BindingList(Of Integer)`로 가져옵니다. 예를 들어 다른 모든 목록 `List(Of String)`는 `ArrayList`로 가져옵니다.  
  
 제네릭 `IDictionary` 인터페이스를 구현하는 형식이 참조된 형식 컬렉션에 추가되는 경우 형식 매개 변수를 완전히 열거나 완전히 닫아야 합니다.  
  
 복제는 허용되지 않습니다. 예를 들어 `List(Of Integer)` 및 `Collection(Of Integer)`을 모두 참조된 형식에 추가할 수는 없습니다. 이렇게 하면 스키마에 정수 목록이 있을 때 사용할 항목을 결정할 수 없습니다. 중복 문제를 노출하는 형식이 스키마에 있는 경우에만 중복이 감지됩니다. 예를 들어 가져온 스키마에 정수 목록이 없는 경우 `List(Of Integer)` 및 `Collection(Of Integer)`을 참조된 형식 컬렉션에 모두 포함할 수 있지만 둘 다 영향을 미치지 않습니다.  
  
 참조된 컬렉션 형식 메커니즘은 기본 형식의 컬렉션뿐만 아니라 다른 컬렉션의 컬렉션을 비롯한 복합 형식의 컬렉션에서도 효과적으로 작동합니다.  
  
 속성 `ReferencedCollectionTypes` 은 svcutil.exe 도구의 **/collectiontype** 스위치에 해당 합니다. 여러 컬렉션 형식을 참조 하려면 **/Collectiontype** 스위치를 여러 번 지정 해야 합니다. 형식이 Mscorlib.dll에 없으면 **/reference** 스위치를 사용 하 여 해당 어셈블리도 참조 해야 합니다.  
  
#### <a name="import-options-referencing-existing-types"></a>가져오기 옵션: 기존 형식 참조  
 경우에 따라 스키마의 형식은 기존 .NET Framework 형식에 해당 하며 이러한 형식을 처음부터 생성 하지 않아도 됩니다. 이 단원의 내용은 비컬렉션 형식에만 적용됩니다. 컬렉션 형식에 대해서는 이전 단원을 참조하세요.  
  
 예를 들어 개인을 나타낼 때 항상 사용할 회사 수준의 표준 "Person" 데이터 계약 형식이 있을 수 있습니다. 일부 서비스에서 이 형식을 사용하고 서비스 메타데이터에 해당 스키마가 나타날 때마다 각 서비스에 대해 새 형식을 생성하는 대신 이 스키마를 가져올 때 기존 `Person` 형식을 다시 사용할 수 있습니다.  
  
 이렇게 하려면 다시 사용할 .NET Framework 형식의 목록을 속성이 <xref:System.Runtime.Serialization.ImportOptions.ReferencedTypes%2A> <xref:System.Runtime.Serialization.ImportOptions> 클래스에서 반환 하는 컬렉션에 전달 합니다. 이러한 형식에 스키마 형식의 이름 및 네임스페이스와 일치하는 데이터 계약 이름 및 네임스페이스가 있으면 구조 비교가 수행됩니다. 형식에 일치 하는 이름과 일치 하는 구조가 모두 있는 것으로 확인 되 면 기존 .NET Framework 형식이 새 형식을 생성 하는 대신 다시 사용 됩니다. 이름만 일치하고 구조가 일치하지 않으면 예외가 throw됩니다. 형식을 참조할 때(예: 새 선택적 데이터 멤버를 추가할 때) 버전 관리는 허용되지 않습니다. 구조는 정확하게 일치해야 합니다.  
  
 해당 이름과 네임스페이스를 가진 스키마 형식을 가져오지 않는 한 동일한 데이터 계약 이름과 네임스페이스를 가진 여러 형식을 참조된 형식 컬렉션에 추가할 수 있습니다. 이렇게 하면 실제로 스키마에서 발생하지 않는 형식의 중복에 대해 염려하지 않고 어셈블리의 모든 형식을 쉽게 컬렉션에 추가할 수 있습니다.  
  
 속성 `ReferencedTypes` 은 svcutil.exe 도구의 특정 작업 모드에서 **/reference** 스위치에 해당 합니다.  
  
> [!NOTE]
> Svcutil.exe 또는 (Visual Studio에서) **서비스 참조 추가** 도구를 사용 하는 경우 mscorlib.dll의 모든 형식이 자동으로 참조 됩니다.  
  
#### <a name="import-options-importing-non-datacontract-schema-as-ixmlserializable-types"></a>가져오기 옵션: 비 DataContract 스키마를 IXmlSerializable 형식으로 가져오기  
 <xref:System.Runtime.Serialization.XsdDataContractImporter>는 스키마의 제한된 하위 집합을 지원합니다. 지원되지 않는 스키마 구문이 있으면(예: XML 특성) 예외와 함께 가져오기 시도가 실패합니다. 그러나 <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> 속성을 `true`로 설정하면 지원되는 스키마 범위가 확장됩니다. `true`는 <xref:System.Runtime.Serialization.XsdDataContractImporter>로 설정된 경우 <xref:System.Xml.Serialization.IXmlSerializable> 인터페이스를 구현하는 형식을 생성합니다. 이 경우 이러한 형식의 XML 표현에 직접 액세스할 수 있습니다.  
  
##### <a name="design-considerations"></a>디자인 고려 사항  
  
- 약한 형식의 XML 표현을 직접 사용하기 어려울 수도 있습니다. <xref:System.Xml.Serialization.XmlSerializer> 같은 대체 serialization 엔진을 사용하여 강력한 형식의 데이터 계약과 호환되지 않는 스키마 작업을 수행해 보세요. 자세한 내용은 [XmlSerializer 클래스 사용](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md)을 참조 하세요.  
  
- <xref:System.Runtime.Serialization.XsdDataContractImporter> 속성이 <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A>로 설정되어 있어도 일부 스키마 구문은 `true`로 가져올 수 없습니다. 이 경우에도 <xref:System.Xml.Serialization.XmlSerializer>를 사용해 보세요.  
  
- <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> 가 또는 `true` 일`false` 때 모두 지원 되는 정확한 스키마 구문은 [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)에 설명 되어 있습니다.  
  
- 생성된 <xref:System.Xml.Serialization.IXmlSerializable> 형식의 스키마는 가져오고 내보낼 때 충실도를 유지하지 않습니다. 즉, 생성된 형식에서 스키마를 내보내고 클래스로 가져오면 원래 스키마가 반환되지 않습니다.  
  
 <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> 옵션을 앞에서 설명한 <xref:System.ServiceModel.Description.ServiceContractGenerator.ReferencedTypes%2A> 옵션과 결합할 수 있습니다. <xref:System.Xml.Serialization.IXmlSerializable> 구현으로 생성해야 하는 형식의 경우 <xref:System.ServiceModel.Description.ServiceContractGenerator.ReferencedTypes%2A> 기능을 사용할 때 구조적 검사를 건너뜁니다.  
  
 이 <xref:System.Runtime.Serialization.ImportOptions.ImportXmlType%2A> 옵션은 svcutil.exe 도구의 **/importxmltypes** 스위치에 해당 합니다.  
  
##### <a name="working-with-generated-ixmlserializable-types"></a>생성된 IXmlSerializable 형식 작업  
 생성된 `IXmlSerializable` 형식에는 <xref:System.Xml.XmlNode> 개체 배열을 반환하는 "nodesField"라는 private 필드가 있습니다. 이러한 형식의 인스턴스를 deserialize하는 경우 XML 문서 개체 모델을 사용하여 이 필드를 통해 직접 XML 데이터에 액세스할 수 있습니다. 이 형식의 인스턴스를 serialize하는 경우 이 필드를 원하는 XML 데이터로 설정하면 serialize됩니다.  
  
 이 작업은 `IXmlSerializable` 구현을 통해 수행됩니다. 생성된 `IXmlSerializable` 형식에서 <xref:System.Xml.Serialization.IXmlSerializable.ReadXml%2A> 구현은 <xref:System.Runtime.Serialization.XmlSerializableServices.ReadNodes%2A> 클래스의 <xref:System.Runtime.Serialization.XmlSerializableServices> 메서드를 호출합니다. 메서드는 <xref:System.Xml.XmlReader>를 통해 제공된 XML을 <xref:System.Xml.XmlNode> 개체 배열로 변환하는 도우미 메서드입니다. <xref:System.Xml.Serialization.IXmlSerializable.WriteXml%2A> 구현은 반대 작업을 수행하고 `XmlNode` 개체 배열을 <xref:System.Xml.XmlWriter> 호출 시퀀스로 변환합니다. 이 작업은 <xref:System.Runtime.Serialization.XmlSerializableServices.WriteNodes%2A> 메서드를 사용하여 수행됩니다.  
  
 생성된 `IXmlSerializable` 클래스에서 스키마 내보내기 프로세스를 실행할 수 있습니다. 앞에서 설명했듯이 원래 스키마가 반환되지는 않습니다. 대신 XSD 형식에 대 한 와일드 카드인 "anyType" 표준 XSD 형식이 표시 됩니다.  
  
 이는 생성 `IXmlSerializable` 된 클래스에 <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 특성을 적용 하 고 <xref:System.Runtime.Serialization.XmlSerializableServices.AddDefaultSchema%2A> 메서드를 호출 하 여 "anyType" 형식을 생성 하는 메서드를 지정 하 여 수행 됩니다.  
  
> [!NOTE]
> <xref:System.Runtime.Serialization.XmlSerializableServices> 형식은 이 특정 기능을 지원하기 위한 용도로만 제공됩니다. 다른 용도로는 사용하지 않는 것이 좋습니다.  
  
#### <a name="import-options-advanced-options"></a>가져오기 옵션: 고급 옵션  
 다음은 고급 가져오기 옵션입니다.  
  
- <xref:System.Runtime.Serialization.ImportOptions.CodeProvider%2A> 속성 생성된 클래스에 대한 코드를 생성하는 데 사용할 <xref:System.CodeDom.Compiler.CodeDomProvider>를 지정합니다. 가져오기 메커니즘은 <xref:System.CodeDom.Compiler.CodeDomProvider>에서 지원하지 않는 기능을 피하려고 합니다. <xref:System.Runtime.Serialization.ImportOptions.CodeProvider%2A> 가 설정 되지 않은 경우 .NET Framework 기능의 전체 집합이 제한 없이 사용 됩니다.  
  
- <xref:System.Runtime.Serialization.ImportOptions.DataContractSurrogate%2A> 속성 이 속성을 사용하여 <xref:System.Runtime.Serialization.IDataContractSurrogate> 구현을 지정할 수 있습니다. <xref:System.Runtime.Serialization.IDataContractSurrogate>는 가져오기 프로세스를 사용자 지정합니다. 자세한 내용은 [데이터 계약 서로게이트](../../../../docs/framework/wcf/extending/data-contract-surrogates.md)를 참조 하세요. 기본적으로 서로게이트는 사용되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.XsdDataContractImporter>
- <xref:System.Runtime.Serialization.XsdDataContractExporter>
- <xref:System.Runtime.Serialization.ImportOptions>
- [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)
- [데이터 계약 서로게이트](../../../../docs/framework/wcf/extending/data-contract-surrogates.md)
- [스키마 가져오기 및 내보내기](../../../../docs/framework/wcf/feature-details/schema-import-and-export.md)
- [클래스에서 스키마 내보내기](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md)
- [데이터 계약 스키마 참조](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)
