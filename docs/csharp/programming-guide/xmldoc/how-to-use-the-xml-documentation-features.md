---
title: '방법: XML 문서 기능 사용 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 06/01/2018
helpviewer_keywords:
- XML documentation [C#]
- C# language, XML documentation features
ms.assetid: 8f33917b-9577-4c9a-818a-640dbbb0b399
ms.openlocfilehash: 06b0c3b7877337d8a5703403af98dbacdf3ea93c
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834171"
---
# <a name="how-to-use-the-xml-documentation-features"></a>방법: XML 문서 기능 사용

다음 샘플은 문서화된 형식에 대한 기본 개요를 제공합니다.

## <a name="example"></a>예

[!code-csharp[csProgGuideDocComments#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#15)]

이 예제에서는 다음 내용과 같은 내용의 .xml 파일을 생성합니다.

```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>xmlsample</name>
    </assembly>
    <members>
        <member name="T:TestClass">
            <summary>
            Class level summary documentation goes here.
            </summary>
            <remarks>
            Longer comments can be associated with a type or member through
            the remarks tag.
            </remarks>
        </member>
        <member name="F:TestClass._name">
            <summary>
            Store for the Name property.
            </summary>
        </member>
        <member name="M:TestClass.#ctor">
            <summary>
            The class constructor.
            </summary>
        </member>
        <member name="P:TestClass.Name">
            <summary>
            Name property.
            </summary>
            <value>
            A value tag is used to describe the property value.
            </value>
        </member>
        <member name="M:TestClass.SomeMethod(System.String)">
            <summary>
            Description for SomeMethod.
            </summary>
            <param name="s"> Parameter description for s goes here.</param>
            <seealso cref="T:System.String">
            You can use the cref attribute on any tag to reference a type or member 
            and the compiler will check that the reference exists.
            </seealso>
        </member>
        <member name="M:TestClass.SomeOtherMethod">
            <summary>
            Some other method.
            </summary>
            <returns>
            Return values are described through the returns tag.
            </returns>
            <seealso cref="M:TestClass.SomeMethod(System.String)">
            Notice the use of the cref attribute to reference a specific method.
            </seealso>
        </member>
        <member name="M:TestClass.Main(System.String[])">
            <summary>
            The entry point for the application.
            </summary>
            <param name="args"> A list of command line arguments.</param>
        </member>
        <member name="T:TestInterface">
            <summary>
            Documentation that describes the interface goes here.
            </summary>
            <remarks>
            Details about the interface go here.
            </remarks>
        </member>
        <member name="M:TestInterface.InterfaceMethod(System.Int32)">
            <summary>
            Documentation that describes the method goes here.
            </summary>
            <param name="n">
            Parameter n requires an integer argument.
            </param>
            <returns>
            The method returns an integer.
            </returns>
        </member>
    </members>
</doc>
```

## <a name="compiling-the-code"></a>코드 컴파일

예제를 컴파일하려면 다음 명령줄을 입력합니다.

`csc XMLsample.cs /doc:XMLsample.xml`

이 명령으로 TYPE 명령을 사용하거나 브라우저에서 볼 수 있는 XML 파일 *XMLsample.xml*이 생성됩니다.

## <a name="robust-programming"></a>강력한 프로그래밍

XML 문서는 ///로 시작합니다. 새 프로젝트를 만드는 경우 마법사에서 몇 개의 시작 /// 줄을 자동으로 넣습니다. 이러한 주석의 처리에는 몇 가지 제한이 있습니다.

- 문서는 잘 구성된 XML이어야 합니다. XML이 잘 구성되지 않은 경우 경고가 생성되고, 문서 파일에 오류가 발생했다는 주석이 포함됩니다.

- 개발자는 각자 고유한 태그 집합을 만들 수 있습니다. 권장 태그 집합이 있습니다([문서 주석에 대한 권장 태그](recommended-tags-for-documentation-comments.md) 참조). 권장 태그 중 일부는 특별한 의미가 있습니다.

  - \<param> 태그는 매개 변수를 설명하는 데 사용됩니다. 사용되는 경우 컴파일러는 매개 변수가 있고 모든 매개 변수가 문서에서 설명되었는지 확인합니다. 확인에 실패하면 컴파일러가 경고를 실행합니다.

  - `cref` 특성을 태그에 연결하여 코드 요소에 대한 참조를 제공할 수 있습니다. 컴파일러에서 이 코드 요소가 있는지 확인합니다. 확인에 실패하면 컴파일러가 경고를 실행합니다. 컴파일러는 `cref` 특성에 설명된 형식을 찾을 때 모든 `using` 문을 따릅니다.

  - \<summary> 태그는 Visual Studio 내의 IntelliSense에서 형식 또는 멤버에 대한 추가 정보를 표시하는 데 사용됩니다.

    > [!NOTE]
    > XML 파일은 형식 및 멤버에 대한 전체 정보를 제공하지 않습니다(예: 형식 정보가 포함되지 않음). 형식 또는 멤버에 대한 전체 정보를 가져오려면 실제 형식 또는 멤버에 대한 리플렉션과 함께 문서 파일을 사용해야 합니다.

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [/doc(C# 컴파일러 옵션)](../../language-reference/compiler-options/doc-compiler-option.md)
- [XML 문서 주석](./index.md)
- [DocFX 설명서 프로세서](https://dotnet.github.io/docfx/)
- [Sandcastle 설명서 프로세서](https://github.com/EWSoftware/SHFB)
