---
title: XML Schema Definition Tool (Xsd.exe)
ms.date: 03/30/2017
ms.assetid: a6e6e65c-347f-4494-9457-653bf29baac2
ms.openlocfilehash: 7a27b05a12017a3c0de6b0d036f480b3e7fdeda7
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392734"
---
# <a name="xml-schema-definition-tool-xsdexe"></a>XML Schema Definition Tool (Xsd.exe)

XML 스키마 정의 도구(Xsd.exe)를 사용하면 XDR, XML 및 XSD 파일 또는 런타임 어셈블리의 클래스에서 XML 스키마 또는 공용 언어 런타임 클래스를 생성할 수 있습니다.

## <a name="syntax"></a>구문

```console
xsd file.xdr [/outputdir:directory][/parameters:file.xml]
xsd file.xml [/outputdir:directory] [/parameters:file.xml]
xsd file.xsd {/classes | /dataset} [/element:element]
             [/enableLinqDataSet] [/language:language]
                          [/namespace:namespace] [/outputdir:directory] [URI:uri]
                          [/parameters:file.xml]
xsd {file.dll | file.exe} [/outputdir:directory] [/type:typename [...]][/parameters:file.xml]
```

## <a name="argument"></a>인수

|인수|설명|
|--------------|-----------------|
|*file.extension*|변환할 입력 파일을 지정합니다. 다음 중 하나에 해당 하는 확장명을 xdr, .xml, .xsd, .dll 또는 .exe 중 하나로 지정 해야 합니다.<br /><br /> XDR 스키마 파일(.xdr 확장명)을 지정하면 Xsd.exe는 XDR 스키마를 XSD 스키마로 변환됩니다. 출력 파일의 이름은 XDR 스키마와 동일하지만 확장명은 .xsd입니다.<br /><br /> XML 파일(.xml 확장명)을 지정하면 Xsd.exe는 해당 파일에 있는 데이터에서 스키마를 유추하여 XSD 스키마가 생성됩니다. 출력 파일의 이름은 XML 파일과 동일하지만 확장명은 .xsd입니다.<br /><br /> XML 스키마 파일(.xsd 확장명)을 지정하면 해당 XML 스키마에 해당하는 런타임 개체에 대한 소스 코드가 생성됩니다.<br /><br /> 런타임 어셈블리 파일(.exe 또는 .dll 확장명)을 지정하면 해당 어셈블리에 있는 하나 이상의 형식에 대해 스키마가 생성됩니다. `/type` 옵션을 사용하면 스키마를 생성할 대상 형식을 지정할 수 있습니다. 출력 스키마의 이름은 schema0.xsd, schema1.xsd 등과 같이 지정됩니다. 지정된 형식에서 `XMLRoot` 사용자 지정 특성을 사용하여 네임스페이스를 지정하는 경우에만 여러 개의 스키마가 생성됩니다.|

## <a name="general-options"></a>일반 옵션

|옵션|설명|
|------------|-----------------|
|**/h\[elp\]**|이 도구의 명령 구문 및 옵션을 표시합니다.|
|**/o\[utputdir\]:** _directory_|출력 파일의 디렉터리를 지정합니다. 이 인수는 한 번만 나타날 수 있으며, 기본값은 현재 디렉터리입니다.|
|**/?**|이 도구의 명령 구문 및 옵션을 표시합니다.|
|**/p\[arameters\]:** _file.xml_|지정한 .xml 파일의 여러 가지 작동 모드에 대한 읽기 옵션입니다. 약식 표현은 `/p:`입니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요.|

## <a name="xsd-file-options"></a>XSD 파일 옵션
 .xsd 파일에는 다음 옵션 중 하나만 지정해야 합니다.

|옵션|설명|
|------------|-----------------|
|**/c\[lasses\]**|지정된 스키마에 해당하는 클래스를 생성합니다. XML 데이터를 개체로 읽어오려면 <xref:System.Xml.Serialization.XmlSerializer.Deserialize%2A?displayProperty=nameWithType> 메서드를 사용합니다.|
|**/d\[ataset\]**|지정된 스키마에 해당하는 <xref:System.Data.DataSet>에서 파생된 클래스를 생성합니다. XML 데이터를 파생 클래스로 읽어오려면 <xref:System.Data.DataSet.ReadXml%2A?displayProperty=nameWithType> 메서드를 사용합니다.|

 .xsd 파일에는 다음 옵션을 지정할 수도 있습니다.

|옵션|설명|
|------------|-----------------|
|**/e @ no__t-1lement @ no__t:** _요소_|코드를 생성할 대상 스키마 요소를 지정합니다. 기본적으로 모든 요소가 입력되며, 이 인수는 한 번 이상 지정될 수 있습니다.|
|**/enableDataBinding**|생성된 모든 형식에 <xref:System.ComponentModel.INotifyPropertyChanged> 인터페이스를 구현하여 데이터 바인딩을 사용할 수 있습니다. 약식 표현은 `/edb`입니다.|
|**/enableLinqDataSet**|약식: `/eld`. 생성된 DataSet을 LINQ to DataSet을 사용하여 쿼리할 수 있도록 지정합니다. 이 옵션은 /dataset 옵션이 지정된 경우 사용됩니다. 자세한 내용은 [LINQ to DataSet 개요](../../../docs/framework/data/adonet/linq-to-dataset-overview.md) 및 [형식화된 데이터 세트 쿼리](../../../docs/framework/data/adonet/querying-typed-datasets.md)를 참조하세요. Linq 사용에 대 한 일반적인 내용은 linq [( C# 통합 언어 쿼리](../../csharp/programming-guide/concepts/linq/index.md) ) 또는 [linq (통합 언어 쿼리)-Visual Basic](../../visual-basic/programming-guide/concepts/linq/index.md)를 참조 하세요.|
|**/f @ no__t-1ields @ no__t**|속성 대신 필드를 생성합니다. 기본적으로 속성이 생성됩니다.|
|**/l\[anguage\]:** _language_|사용할 프로그래밍 언어를 지정합니다. `CS`(C#, 기본값), `VB`(Visual Basic), `JS`(JScript) 또는 `VJS`(Visual J#) 중에서 선택합니다. <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType>를 구현하는 클래스의 정규화된 이름을 지정할 수도 있습니다.|
|**/n\[amespace\]:** _namespace_|생성된 형식에 대한 런타임 네임스페이스를 지정합니다. 기본 네임스페이스는 `Schemas`입니다.|
|**/nologo**|배너를 표시하지 않습니다.|
|**/order**|모든 파티클 멤버에 대해 명시적인 순서 식별자를 생성합니다.|
|**/o\[ut\]:** _directoryName_|파일을 배치할 출력 디렉터리를 지정합니다. 기본값은 현재 디렉터리입니다.|
|**/u\[ri\]:** _uri_|코드를 생성할 대상 스키마 요소의 URI를 지정합니다. 이 URI가 존재하는 경우 `/element` 옵션을 사용하여 지정된 모든 요소에 적용됩니다.|

## <a name="dll-and-exe-file-options"></a>DLL 및 EXE 파일 옵션

|옵션|설명|
|------------|-----------------|
|**/t\[ype\]:** _typename_|스키마를 생성할 대상 형식의 이름을 지정합니다. 여러 개의 형식 인수를 지정할 수도 있습니다. *typename*에서 네임스페이스를 지정하지 않으면 Xsd.exe는 해당 어셈블리의 모든 형식과 지정된 형식을 일치시킵니다. *typename*에서 네임스페이스를 지정하면 지정한 형식만 일치됩니다. *typename*이 별표(\*)로 끝나는 경우에는 \* 앞의 문자열로 시작하는 모든 형식이 일치됩니다. `/type` 옵션을 생략하면 Xsd.exe는 해당 어셈블리의 모든 형식에 대해 스키마가 생성됩니다.|

## <a name="remarks"></a>설명

다음 표에서는 Xsd.exe에서 수행되는 작업을 보여 줍니다.

| | |
|------------|-----------------|
|XDR에서 XSD로|XDR 스키마 파일에서 XML 스키마를 생성합니다. XDR은 XML 기반 스키마의 초기 형식입니다.|
|XML에서 XSD로|XML 파일에서 XML 스키마를 생성합니다.|
|XSD에서 DataSet으로|XSD 스키마 파일에서 공용 언어 런타임 <xref:System.Data.DataSet> 클래스를 생성합니다. 이렇게 생성된 클래스에서는 일반 XML 데이터에 대한 강력한 개체 모델이 제공됩니다.|
|XSD에서 클래스로|XSD 스키마 파일에서 런타임 클래스를 생성합니다. 이렇게 생성된 클래스를 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>와 함께 사용하면 해당 스키마를 따르는 XML 코드를 읽고 쓸 수 있습니다.|
|클래스를 XSD로| 런타임 어셈블리 파일의 형식에서 XML 스키마를 생성합니다. 생성 된 스키마는 <xref:System.Xml.Serialization.XmlSerializer>에서 사용 하는 XML 형식을 정의 합니다.|

 Xsd.exe를 사용하면 W3C(World Wide Web 컨소시엄)에서 제시하는 XSD(XML Schema Definition) 언어를 따르는 XML 스키마만 조작할 수 있습니다. XML 스키마 정의 제안 또는 XML 표준에 대 한 자세한 내용은 <https://w3.org>을 참조 하세요.

## <a name="setting-options-with-an-xml-file"></a>XML 파일로 옵션 설정

`/parameters` 스위치를 사용하여 여러 가지 옵션을 설정하는 단일 XML 파일을 지정할 수 있습니다. 설정할 수 있는 옵션은 XSD.exe 도구를 사용하는 방법에 따라 다릅니다. 스키마 생성, 코드 파일 생성 또는 `DataSet` 기능이 있는 코드 파일 생성을 선택할 수 있습니다. 예를 들면, 스키마는 생성하지만 코드 파일은 생성하지 않을 때 `<assembly>` 요소를 실행 파일(.exe) 또는 형식 라이브러리 파일(.dll) 이름으로 설정할 수 있습니다. 다음 XML에서는 지정된 실행 파일에 `<generateSchemas>` 요소를 사용하는 방법을 보여 줍니다.

```xml
<!-- This is in a file named GenerateSchemas.xml. -->
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
<generateSchemas>
   <assembly>ConsoleApplication1.exe</assembly>
</generateSchemas>
</xsd>
```

위의 XML이 GenerateSchemas.xml이라는 파일에 포함된 경우 명령 프롬프트에서 다음을 입력하고 Enter 키를 눌러 `/parameters` 스위치를 사용합니다.

```console
 xsd /p:GenerateSchemas.xml
```

그러나 어셈블리에 있는 단일 형식의 스키마를 생성하는 경우 다음 XML을 사용할 수 있습니다.

```xml
<!-- This is in a file named GenerateSchemaFromType.xml. -->
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
<generateSchemas>
   <type>IDItems</type>
</generateSchemas>
</xsd>
```

위의 코드를 사용하려면 명령 프롬프트에서 어셈블리의 이름도 제공해야 합니다. 명령 프롬프트에서 다음을 입력합니다. 이 경우 XML 파일 이름이 GenerateSchemaFromType.xml이라고 가정합니다.

```console
xsd /p:GenerateSchemaFromType.xml ConsoleApplication1.exe
```

`<generateSchemas>` 요소에 대해 다음 옵션 중 하나만 지정해야 합니다.

|요소|설명|
|-------------|-----------------|
|\<assembly>|스키마를 생성하는 어셈블리를 지정합니다.|
|\<type>|스키마를 생성할 대상 어셈블리에 있는 유형을 지정합니다.|
|\<xml>|스키마를 생성할 대상 XML 파일을 지정합니다.|
|\<xdr>|스키마를 생성할 대상 XDR 파일을 지정합니다.|

코드 파일을 생성하려면 `<generateClasses>` 요소를 사용합니다. 다음 예제는 코드 파일을 생성합니다. 또한 생성된 파일의 프로그래밍 언어 및 네임스페이스를 설정할 수 있는 두 개의 특성이 표시됩니다.

```xml
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
<generateClasses language='VB' namespace='Microsoft.Serialization.Examples'/>
</xsd>
<!-- You must supply an .xsd file when typing in the command line.-->
<!-- For example: xsd /p:genClasses mySchema.xsd -->
```

 `<generateClasses>` 요소에 대해 설정할 수 있는 옵션은 다음과 같습니다.

|요소|설명|
|-------------|-----------------|
|\<element>|코드를 생성할 대상 .xsd 파일의 요소를 지정합니다.|
|\<schemaImporterExtensions>|<xref:System.Xml.Serialization.Advanced.SchemaImporterExtension> 클래스에서 파생된 형식을 지정합니다.|
|\<schema>|코드를 생성할 XML 스키마 파일을 지정합니다. 여러 \<schema> 요소를 사용하여 XML 스키마 파일을 여러 개 지정할 수 있습니다.|

다음 표에서는 `<generateClasses>` 요소에도 사용할 수 있는 특성을 보여 줍니다.

|특성|설명|
|---------------|-----------------|
|language|사용할 프로그래밍 언어를 지정합니다. `CS`(C#, 기본값), `VB`(Visual Basic), `JS`(JScript) 또는 `VJS`(Visual J#) 중에서 선택합니다. <xref:System.CodeDom.Compiler.CodeDomProvider>를 구현하는 클래스의 정규화된 이름을 지정할 수도 있습니다.|
|네임스페이스(namespace)|생성된 코드에 대한 네임스페이스를 지정합니다. 네임스페이스는 CLR 표준(예: 공백 없음 또는 백슬래시 문자)에 일치해야 합니다.|
|옵션|`none`, `properties`(public 필드 대신 속성 생성), `order` 또는 `enableDataBinding`(위의 XSD 파일 옵션 섹션의 `/order` 및 `/enableDataBinding` 스위치 참조) 값 중 하나|

 `DataSet` 요소를 사용하여 `<generateDataSet>` 코드를 생성하는 방식을 제어할 수도 있습니다. 다음 XML은 생성 된 코드가 `DataSet` 구조체 (예: <xref:System.Data.DataTable> 클래스)를 사용 하 여 지정 된 요소에 대 한 Visual Basic 코드를 만들도록 지정 합니다. 생성된 DataSet 구조체는 LINQ 쿼리를 지원합니다.

 ```xml
 <xsd xmlns='http://microsoft.com/dotnet/tools/xsd/'>
     <generateDataSet language='VB' namespace='Microsoft.Serialization.Examples' enableLinqDataSet='true'>
     </generateDataSet>
 </xsd>
```

`<generateDataSet>` 요소에 대해 설정할 수 있는 옵션은 다음과 같습니다.

|요소|설명|
|-------------|-----------------|
|\<schema>|코드를 생성할 XML 스키마 파일을 지정합니다. 여러 \<schema> 요소를 사용하여 XML 스키마 파일을 여러 개 지정할 수 있습니다.|

 다음 표에서는 `<generateDataSet>` 요소에 사용할 수 있는 특성을 보여 줍니다.

|특성|설명|
|---------------|-----------------|
|enableLinqDataSet|생성된 DataSet을 LINQ to DataSet을 사용하여 쿼리할 수 있도록 지정합니다. 기본값은 false입니다.|
|language|사용할 프로그래밍 언어를 지정합니다. `CS`(C#, 기본값), `VB`(Visual Basic), `JS`(JScript) 또는 `VJS`(Visual J#) 중에서 선택합니다. <xref:System.CodeDom.Compiler.CodeDomProvider>를 구현하는 클래스의 정규화된 이름을 지정할 수도 있습니다.|
|네임스페이스(namespace)|생성된 코드에 대한 네임스페이스를 지정합니다. 네임스페이스는 CLR 표준(예: 공백 없음 또는 백슬래시 문자)에 일치해야 합니다.|

 이러한 특성은 최상위 수준의 `<xsd>` 요소에서 설정할 수 있습니다. 이러한 옵션은 자식 요소(`<generateSchemas>`, `<generateClasses>` 또는 `<generateDataSet>`)에 사용할 수 있습니다. 다음 XML 코드는 "MyOutputDirectory"라는 출력 디렉터리에 "IDItems" 요소에 대한 코드를 생성합니다.

```xml
<xsd xmlns='http://microsoft.com/dotnet/tools/xsd/' output='MyOutputDirectory'>
<generateClasses>
    <element>IDItems</element>
</generateClasses>
</xsd>
```

다음 표에서는 `<xsd>` 요소에도 사용할 수 있는 특성을 보여 줍니다.

|특성|설명|
|---------------|-----------------|
|출력|생성된 스키마 또는 코드 파일을 지정할 디렉터리의 이름입니다.|
|nologo|배너를 표시하지 않습니다. `true` 또는 `false`로 설정합니다.|
|도움말|이 도구의 명령 구문 및 옵션을 표시합니다. `true` 또는 `false`로 설정합니다.|

## <a name="examples"></a>예
 다음 명령을 사용하여 `myFile.xdr` 에서 XML 스키마를 생성한 다음 현재 디렉터리에 저장합니다.

```console
xsd myFile.xdr
```

다음 명령을 사용하여 `myFile.xml` 스키마를 생성한 다음 지정된 디렉터리에 저장합니다.

```console
xsd myFile.xml /outputdir:myOutputDir
```

다음 명령은 C# 언어로 된 지정된 스키마와 일치하는 데이터 집합을 생성한 다음 현재 디렉터리에 `XSDSchemaFile.cs`로 저장합니다.

```console
xsd /dataset /language:CS XSDSchemaFile.xsd
```

다음 명령을 사용하여 어셈블리 `myAssembly.dll`에 있는 모든 형식에 대해 XML 스키마를 생성한 다음 현재 디렉터리에 `schema0.xsd`로 저장합니다.

```console
xsd myAssembly.dll
```

## <a name="see-also"></a>참조

- <xref:System.Data.DataSet>
- <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType>
- [도구](../../../docs/framework/tools/index.md)
- [명령 프롬프트](../../../docs/framework/tools/developer-command-prompt-for-vs.md)
- [LINQ to DataSet 개요](../../../docs/framework/data/adonet/linq-to-dataset-overview.md)
- [형식화된 데이터 세트 쿼리](../../../docs/framework/data/adonet/querying-typed-datasets.md)
- [LINQ (통합 언어 쿼리) (C#)](../../csharp/programming-guide/concepts/linq/index.md)
- [LINQ (통합 언어 쿼리) (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/index.md)
