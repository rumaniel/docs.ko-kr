---
title: .NET 보안 분석기 - .NET
description: .NET Framework 분석기 패키지에서 .NET 보안 분석기를 사용하여 보안 위험을 찾아 해결하는 방법을 알아봅니다.
author: billwagner
ms.author: wiwagn
ms.date: 01/25/2018
ms.technology: dotnet-standard
ms.openlocfilehash: da5e72b96fec35404e7e9ae7930f3430143487d2
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929303"
---
# <a name="the-net-framework-analyzer"></a>.NET Framework 분석기

.NET Framework 분석기를 사용하여 .NET Framework 기반 애플리케이션 코드에서 잠재적인 문제를 찾을 수 있습니다. 이 분석기는 잠재적인 문제를 찾고 해결 방법을 제안합니다.

분석기는 코드를 작성하거나 CI 빌드의 일부와 같이 Visual Studio에서 대화형으로 실행합니다. 개발 시 가능한 빨리 분석기를 프로젝트에 추가해야 합니다. 코드의 잠재적 문제를 신속하게 발견하면 이를 쉽게 해결할 수 있습니다. 그러나 언제든지 개발 주기에서 추가할 수 있습니다. 기존 코드에 문제가 있는지 찾고 계속 개발하는 경우 새로운 문제에 대해 경고합니다.

## <a name="installing-and-configuring-the-net-framework-analyzer"></a>.NET Framework 분석기 설치 및 구성

.NET 보안 분석기를 실행하려는 모든 프로젝트에서 NuGet 패키지로 설치해야 합니다. 한 명의 개발자만이 이를 프로젝트에 추가해야 합니다. 분석기 패키지는 프로젝트에 종속된 기능이며 업데이트된 솔루션이 포함되면 모든 개발자의 컴퓨터에서 실행됩니다.

.NET Framework 분석기는 [Microsoft.NetFramework.Analyzers](https://www.nuget.org/packages/Microsoft.NetFramework.Analyzers/) NuGet 패키지에서 제공됩니다. 이 패키지는 보안 분석기를 포함하는 .NET Framework에 특정 분석기만을 제공합니다. 대부분의 경우에 [Microsoft.CodeAnalysis.FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers) NuGet 패키지가 필요합니다. FxCopAnalyzers 집계 패키지에는 다음 분석기뿐만 아니라 Framework.Analyzers 패키지에 포함된 모든 프레임워크 분석기가 포함됩니다.

- [Microsoft.CodeQuality.Analyzers](https://www.nuget.org/packages/Microsoft.CodeQuality.Analyzers): .NET 표준 API에 대한 일반 지침 및 지침을 제공합니다.
- [Microsoft.NetCore.Analyzers](https://www.nuget.org/packages/Microsoft.NetCore.Analyzers): .NET Core API에 특정된 분석기를 제공합니다.
- [Text.Analyzers](https://www.nuget.org/packages/Text.Analyzers): 주석을 비롯하여 코드로 포함된 텍스트의 지침을 제공합니다.

이를 설치하려면 프로젝트를 마우스 오른쪽 단추로 클릭하고, "종속성 관리"를 선택합니다.
NuGet 탐색기에서 "NetFramework 분석기"를 검색하거나 선호하는 경우 "Fx Cop 분석기"를 검색합니다. 솔루션의 모든 프로젝트에 안정적인 최신 버전을 설치합니다.

## <a name="using-the-net-framework-analyzer"></a>.NET Framework 분석기 사용

NuGet 패키지를 설치하면 솔루션을 빌드합니다. 분석기는 코드베이스에서 찾은 모든 문제를 보고합니다. 다음 그림에 표시된 대로 문제는 Visual Studio 오류 목록 창에 경고로 보고됩니다.

![프레임워크 분석기에서 보고한 문제](./media/framework-analyzers-2.png)

코드를 작성할 때 코드에 있는 잠재적 문제 아래에 물결선이 표시됩니다.
다음 이미지에 표시된 대로 문제를 마우스로 가리키고 문제에 대한 세부 정보 및 가능한 수정 제안 사항을 확인합니다.

![프레임워크 분석기에 의해 발견된 문제의 대화형 보고서](./media/framework-analyzers-1.png)

분석기는 솔루션에서 코드를 검사하고 이러한 문제 중 하나에 대한 경고 목록을 제공합니다.

### <a name="ca1058-types-should-not-extend-certain-base-types"></a>CA1058: 형식은 특정 기본 형식을 확장하면 안 됩니다.

.NET Framework에 직접 파생하지 않은 몇몇 형식이 있습니다. 

**범주:** 디자인

**심각도:** 경고

추가 정보: [CA:1058: 형식은 특정 기본 형식을 확장하면 안 됩니다.](/visualstudio/code-quality/ca1058-types-should-not-extend-certain-base-types)

### <a name="ca2153-do-not-catch-corrupted-state-exceptions"></a>CA2153: 손상된 상태 예외를 catch하지 마세요.

손상된 상태 예외를 catch하면 오류(예: 액세스 위반)를 마스킹할 수 있습니다. 그러면 실행의 일관성이 없는 상태가 발생하거나 공격자가 쉽게 시스템을 손상시킬 수 있습니다. 대신 구체적인 예외 형식을 catch하고 처리하거나 예외를 다시 throw합니다.

**범주:** 보안

**심각도:** 경고

추가 정보: [## CA2153: 손상된 상태 예외를 catch하지 마세요.](/visualstudio/code-quality/ca2153-avoid-handling-corrupted-state-exceptions)

### <a name="ca2229-implement-serialization-constructors"></a>CA2229: serialization 생성자를 구현하십시오.

분석기는 <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현지만 필요한 serialization 생성자를 정의하지 않는 형식을 만들 때 이 경고를 생성합니다. 이 규칙 위반 문제를 해결하려면 serialization 생성자를 구현합니다. 봉인 클래스의 경우에는 생성자를 private으로 만들고, 그 밖의 경우에는 protected로 만듭니다. Serialization 생성자에는 다음 서명이 있습니다.

```csharp
public class MyItemType
{
    // The special constructor is used to deserialize values.
    public MyItemType(SerializationInfo info, StreamingContext context)
    {
        // implementation removed.
    }
}
```

**범주:** 사용

**심각도:** 경고

추가 정보: [CA2229: serialization 생성자를 구현하십시오.](/visualstudio/code-quality/ca2229-implement-serialization-constructors)

### <a name="ca2235-mark-all-non-serializable-fields"></a>CA2235: 모두 serialize할 수 없는 필드로 표시하십시오.

serialize할 수 없는 형식의 인스턴스 필드가 serialize할 수 있는 형식에 정의되었습니다. 해당 필드를 <xref:System.NonSerializedAttribute>로 명시적으로 표시하여 이 경고를 수정해야 합니다.

**범주:** 사용

**심각도:** 경고

추가 정보: [CA2235: 모두 serialize할 수 없는 필드로 표시하십시오.](/visualstudio/code-quality/ca2235-mark-all-non-serializable-fields)

### <a name="ca2237-mark-iserializable-types-with-serializable"></a>CA2237: ISerializable 형식을 serializable로 표시하세요.

공용 언어 런타임에서 serializable로 인식되도록 하려면 형식이 <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현하여 사용자 지정 serialization 루틴을 사용하는 경우에도 <xref:System.SerializableAttribute> 특성을 사용하여 형식을 표시해야 합니다.

**범주:** 사용

**심각도:** 경고

추가 정보: [CA2237: ISerializable 형식을 serializable로 표시하세요.](/visualstudio/code-quality/ca2237-mark-iserializable-types-with-serializableattribute)

### <a name="ca3075-insecure-dtd-processing-in-xml"></a>CA3075: XML의 안전하지 않은 DTD 처리

안전하지 않은 <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A> 인스턴스를 사용하거나 외부 엔터티 소스를 참조하면 파서는 신뢰할 수 없는 입력을 허용하고 공격자에게 중요 한 정보를 공개할 수 있습니다.  

**범주:** 보안

**심각도:** 경고

추가 정보: [A3075: XML의 안전하지 않은 DTD 처리](/visualstudio/code-quality/ca2237-mark-iserializable-types-with-serializableattribute)

### <a name="ca5350-do-not-use-weak-cryptographic-algorithms"></a>CA5350: 취약한 암호화 알고리즘을 사용하지 마세요.

공격이 발전할수록 암호화 알고리즘은 시간이 지남에 따라 저하됩니다. 해당 암호화 능력이 더욱 저하되면 이 암호화 알고리즘의 형식 및 애플리케이션에 따라 공격자가 암호화된 메시지를 읽거나, 암호화된 메시지를 조작하거나, 디지털 서명을 위조하거나, 해시된 콘텐츠를 조작하거나, 이 알고리즘을 기반으로 하는 모든 암호화 시스템을 손상시킬 수 있습니다. 암호화의 경우 키 길이가 128비트 이상인 AES 알고리즘(AES-256, AES-192 및 AES-128 허용 가능함)을 사용합니다. 해시의 경우 SHA-2 512, SHA-2 384 또는 SHA-2 256 등 SHA-2 제품군의 해시 함수를 사용합니다.

**범주:** 보안

**심각도:** 경고

추가 정보: [CA5350: 취약한 암호화 알고리즘을 사용하지 마세요.](/visualstudio/code-quality/ca5350-do-not-use-weak-cryptographic-algorithms)

### <a name="ca5351-do-not-use-broken-cryptographic-algorithms"></a>CA5351: 손상된 암호화 알고리즘을 사용하지 마세요.

이 알고리즘을 중단하지 못하게 만드는 공격이 존재합니다. 이렇게 하면 제공하도록 디자인된 암호화 보장을 공격자가 무너뜨릴 수 있습니다. 그러면 이 암호화 알고리즘의 형식 및 애플리케이션에 따라 공격자가 암호화된 메시지를 읽거나, 암호화된 메시지를 조작하거나, 디지털 서명을 위조하거나, 해시된 콘텐츠를 조작하거나, 이 알고리즘을 기반으로 하는 모든 암호화 시스템을 손상시킬 수 있습니다. 암호화의 경우 키 길이가 128비트 이상인 AES 알고리즘(AES-256, AES-192 및 AES-128 허용 가능함)을 사용합니다. 해시의 경우 SHA512, SHA384 또는 SHA256 등 SHA-2 제품군의 해시 함수를 사용합니다. 디지털 서명의 경우 키 길이가 2048비트 이상인 RSA를 사용하거나 키 길이가 256비트 이상인 ECDSA를 사용합니다.

**범주:** 보안

**심각도:** 경고

추가 정보: [CA5351: 손상된 암호화 알고리즘을 사용하지 마세요.](/visualstudio/code-quality/ca5351-do-not-use-broken-cryptographic-algorithms)
