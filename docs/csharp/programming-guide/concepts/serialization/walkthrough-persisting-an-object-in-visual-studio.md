---
title: '연습: C#을 사용하여 개체 유지'
ms.date: 04/26/2018
ms.openlocfilehash: 5e3a327ca0a257c45de361e0b3734e0b127f9869
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70851046"
---
# <a name="walkthrough-persisting-an-object-using-c"></a>C\#을 사용하여 개체 유지

serialization을 사용하면 인스턴스 간에 개체의 데이터를 유지할 수 있으므로, 다음에 개체를 인스턴스화할 때 값을 저장하고 검색할 수 있습니다.

이 연습에서는 기본 `Loan` 개체를 만들고 데이터를 파일에 유지합니다. 그런 다음 개체를 다시 만들 때 파일에서 데이터를 검색합니다.

> [!IMPORTANT]
> 이 예제에서는 파일이 아직 없는 경우 새 파일을 만듭니다. 애플리케이션에서 파일을 만들어야 하는 경우 해당 애플리케이션은 폴더에 대한 `Create` 권한이 있어야 합니다. 권한은 액세스 제어 목록을 사용하여 설정됩니다. 파일이 이미 있는 경우, 애플리케이션에는 더 낮은 권한인 `Write` 권한만 필요합니다. 가능한 경우 배포하는 동안 파일을 만드는 것이 안전하며, 폴더에 대한 Create 권한 대신 단일 파일에 대해 `Read` 권한만 부여하는 것이 더 안전합니다. 또한 루트 폴더나 Program Files 폴더보다 사용자 폴더에 데이터를 쓰는 것이 더 안전합니다.

> [!IMPORTANT]
> 이 예제에서는 이진 형식 파일의 데이터를 저장합니다. 이러한 형식은 암호 또는 신용 카드 정보와 같은 중요한 데이터에 사용하면 안 됩니다.

## <a name="prerequisites"></a>전제 조건

- 빌드하고 실행하려면 [.NET Core SDK](https://dotnet.microsoft.com/download)를 설치합니다.

- 아직 없는 경우 즐겨 찾는 코드 편집기를 설치합니다.

> [!TIP]
> 코드 편집기를 설치해야 하나요? [Visual Studio](https://visualstudio.com/downloads)를 체험해 보세요.

- 예제는 C# 7.3이 필요합니다. [C# 언어 버전 선택](../../../language-reference/configure-language-version.md)을 참조하세요. 

[.NET 샘플 GitHub 리포지토리에서](https://github.com/dotnet/samples/tree/master/csharp/serialization) 온라인으로 샘플 코드를 검사할 수 있습니다.

## <a name="creating-the-loan-object"></a>Loan 개체 만들기

첫 번째 단계는 `Loan` 클래스와 이 클래스를 사용하는 콘솔 애플리케이션을 만드는 것입니다.

1. 새 애플리케이션을 만듭니다. `dotnet new console -o serialization`을 입력하여 `serialization`이라는 하위 디렉터리에서 새 콘솔 애플리케이션을 만듭니다.
1. 편집기에서 애플리케이션을 열고 `Loan.cs`라는 새 클래스를 추가합니다.
1. `Loan` 클래스에 다음 코드를 추가합니다.

[!code-csharp[Loan class definition](../../../../../samples/csharp/serialization/Loan.cs#1)]

`Loan` 클래스를 사용하는 애플리케이션도 만들어야 합니다.

## <a name="serialize-the-loan-object"></a>Loan 개체 직렬화

1. `Program.cs`를 엽니다. 다음 코드를 추가합니다.

[!code-csharp[Create a loan object](../../../../../samples/csharp/serialization/Program.cs#1)]

`PropertyChanged` 이벤트에 대한 이벤트 처리기를 추가하고 `Loan` 개체를 수정하고 변경 내용을 표시하는 몇 줄을 추가합니다. 다음 코드에서 추가된 기능을 확인할 수 있습니다.

[!code-csharp[Listening for the PropertyChanged event](../../../../../samples/csharp/serialization/Program.cs#2)]

이 시점에서 코드를 실행하고 현재 출력을 확인할 수 있습니다.

```console
New customer value: Henry Clay
7.5
7.1
```

이 애플리케이션을 반복해서 실행하면 항상 동일한 값을 씁니다. 프로그램을 실행할 때마다 새로운 Loan 개체가 생성됩니다. 현실 세계에서 금리는 주기적으로 변경되지만, 애플리케이션이 실행될 때마다 변경되는 것은 아닙니다. Serialization 코드는 애플리케이션의 인스턴스 간에 가장 최근 이자율을 유지함을 의미합니다. 다음 단계에서는 Loan 클래스에 serialization을 추가하여 이를 수행합니다.

## <a name="using-serialization-to-persist-the-object"></a>Serialization을 사용하여 개체 유지

Loan 클래스의 값을 유지하려면 먼저 클래스를 `Serializable` 속성으로 표시해야 합니다. Loan 클래스 선언 위에 다음 코드를 추가합니다.

[!code-csharp[Loan class definition](../../../../../samples/csharp/serialization/Loan.cs#2)]

<xref:System.SerializableAttribute>는 클래스의 모든 내용을 파일에 유지할 수 있음을 컴파일러에 알립니다. `PropertyChanged` 이벤트가 저장되어야 하는 개체 그래프의 일부를 나타내지 않기 때문에 직렬화되지 않아야 합니다. 그러면 해당 이벤트에 연결된 모든 개체를 직렬화합니다. `PropertyChanged` 이벤트 처리기의 필드 선언에 <xref:System.NonSerializedAttribute>를 추가할 수 있습니다.

[!code-csharp[Disable serialization for the event handler](../../../../../samples/csharp/serialization/Loan.cs#3)]

C# 7.3부터는 `field` 대상 값을 사용하여 자동 구현 속성의 지원 필드에 특성을 연결할 수 있습니다. 다음 코드에서는 `TimeLastLoaded` 속성을 추가하고 직렬화할 수 없음으로 표시합니다.

[!code-csharp[Disable serialization for an auto-implemented property](../../../../../samples/csharp/serialization/Loan.cs#4)]

다음 단계는 LoanApp 애플리케이션에 serialization 코드를 추가하는 것입니다. 클래스를 serialize하여 파일에 쓰려면 <xref:System.IO> 및 <xref:System.Runtime.Serialization.Formatters.Binary> 네임스페이스를 사용합니다. 정규화된 이름을 입력하지 않으려면 필요한 다음 코드에 표시된 대로 필요한 네임스페이스에 참조를 추가할 수 있습니다.

[!code-csharp[Adding namespaces for serialization](../../../../../samples/csharp/serialization/Program.cs#3)]

다음 단계는 개체를 만들 때 파일에서 개체를 deserialize할 코드를 추가하는 것입니다. 다음 코드에 표시된 대로 직렬화된 데이터의 파일 이름에 대한 클래스에 상수를 추가합니다.

[!code-csharp[Define the name of the saved file](../../../../../samples/csharp/serialization/Program.cs#4)]

다음으로 `TestLoan` 개체를 만든 줄 뒤에 다음 코드를 추가합니다.

[!code-csharp[Read from a file if it exists](../../../../../samples/csharp/serialization/Program.cs#5)]

먼저 파일이 있는지를 확인해야 합니다. 파일이 있으면 이진 파일을 읽는 <xref:System.IO.Stream> 클래스와 파일을 변환하는 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 클래스를 만듭니다. 또한 스트림 형식에서 Loan 개체 형식으로 변환해야 합니다.

다음으로 클래스를 직렬화하는 코드를 파일에 추가해야 합니다. `Main` 메서드에서 기존 코드 뒤에 다음 코드를 추가합니다.

[!code-csharp[Save the existing Loan object](../../../../../samples/csharp/serialization/Program.cs#6)]

이 시점에서 다시 애플리케이션을 빌드 및 실행할 수 있습니다. 처음으로 실행되면 이자율이 7.5에서 시작한 다음, 7.1로 변경됩니다. 애플리케이션을 닫았다가 다시 엽니다. 이제 애플리케이션이 저장된 파일을 읽는 메시지를 인쇄하고 이자율은 코드가 변경하기 전에도 7.1입니다.

## <a name="see-also"></a>참고 항목

- [Serialization(C#)](index.md)
- [C# 프로그래밍 가이드](../..//index.md)
