---
title: .NET Standard의 새로운 기능
description: 이 문서에는 .NET Standard의 각 새 버전에 있는 새로운 기능과 향상된 기능이 요약되어 있습니다.
ms.custom: updateeachrelease
ms.date: 04/12/2018
ms.technology: dotnet-standard
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 19353bd068e3b04bc3d852c1e22db9c97ebef628
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48583167"
---
# <a name="whats-new-in-the-net-standard"></a>.NET Standard의 새로운 기능

.NET Standard는 해당 버전의 표준에 부합하는 .NET 구현에서 사용할 수 있어야 하는 버전이 지정된 API 집합을 정의합니다. .NET 표준은 라이브러리 개발자에서 대상으로 지정됩니다. .NET Standard 버전을 대상으로 하는 라이브러리는 Standard의 해당 버전을 지원하는 모든 .NET Framework, .NET Core 또는 Xamarin 구현에서 사용할 수 있습니다.

.NET Standard의 최신 버전은 2.0입니다. 이 버전은 .NET Core 워크로드가 설치된 Visual Studio 2017 버전 15.3은 물론 .NET Core 2.0 SDK에 포함되어 있습니다.

## <a name="supported-net-implementations"></a>지원되는 .NET 구현

.NET Standard 2.0은 다음 .NET 구현에서 지원됩니다.

- .NET Core 2.0 이상
- .NET Framework 4.6.1 이상
- Mono 5.4 이상
- Xamarin.iOS 10.14 이상
- Xamarin.Mac 3.8 이상
- Xamarin.Android 8.0 이상
- 유니버설 Windows 플랫폼 10.0.16299 이상

## <a name="whats-new-in-the-net-standard-20"></a>.NET Standard 2.0의 새로운 기능

.NET Standard 2.0에는 다음과 같은 새로운 기능이 포함됩니다.

### <a name="a-vastly-expanded-set-of-apis"></a>매우 폭넓은 API 집합

버전 1.6을 통해 .NET Standard에는 비교적 작은 API 하위 집합이 포함되었습니다. 이들 중 .NET Framework 또는 Xamarin에서 일반적으로 사용된 많은 API가 제외되었습니다. 이로 인해 개발이 복잡해집니다. 개발자들이 여러 .NET 구현을 대상으로 하는 응용 프로그램과 라이브러리를 개발할 때 친숙한 API에 대한 적합한 대체 API를 찾아야 하기 때문입니다. .NET Standard 2.0은 이전 Standard 버전인 .NET Standard 1.6에서 제공된 것보다 20,000개 더 많은 API를 추가하여 이 제한 사항을 해결합니다. .NET Standard 2.0에 추가된 API의 목록은 [.NET Standard 2.0 및 1.6](https://raw.githubusercontent.com/dotnet/standard/master/docs/versions/netstandard2.0_diff.md)을 참조하세요.

.NET Standard 2.0에서 <xref:System> 네임스페이스에 대한 일부 추가 기능은 다음과 같습니다.

- <xref:System.AppDomain> 클래스에 대한 지원.
- <xref:System.Array> 클래스에 있는 추가 멤버의 배열을 사용하기 위한 향상된 지원.
- <xref:System.Attribute> 클래스에 있는 추가 멤버의 속성을 사용하기 위한 향상된 지원.
- <xref:System.DateTime> 값에 대한 향상된 달력 지원 및 추가 서식 옵션.
- 추가 <xref:System.Decimal> 반올림 기능.
- <xref:System.Environment> 클래스의 추가 기능.
- <xref:System.GC> 클래스를 통해 가비지 수집기 제어 강화.
- <xref:System.String> 클래스의 문자열 비교, 열거 및 정규화를 위한 향상된 지원.
- <xref:System.TimeZoneInfo.AdjustmentRule> 및 <xref:System.TimeZoneInfo.TransitionTime> 클래스의 일광 절약 조정 및 전환 시간에 대한 지원.
- <xref:System.Type> 클래스의 크게 향상된 기능.
- <xref:System.Runtime.Serialization.SerializationInfo> 및 <xref:System.Runtime.Serialization.StreamingContext> 매개 변수를 통해 예외 생성자를 추가하여 예외 개체를 deserialize하는 기능에 대한 향상된 지원.

### <a name="support-for-net-framework-libraries"></a>.NET Framework 라이브러리에 대한 지원

압도적인 다수로 라이브러리는 .NET Standard가 아닌 .NET Framework를 대상으로 합니다. 그러나 이러한 라이브러리에서 대부분의 호출은 .NET Standard 2.0에 포함된 API를 대상으로 합니다. .NET Standard 2.0부터는 [호환성 shim](https://github.com/dotnet/standard/blob/master/docs/planning/netstandard-2.0/README.md#assembly-unification)을 사용하여 .NET Standard 라이브러리에서 .NET Framework 라이브러리에 액세스할 수 있습니다. 이 호환성 레이어는 개발자에게 투명합니다. .NET Framework 라이브러리를 이용하기 위해 아무것도 할 필요가 없습니다.

하나의 요구 사항은 .NET Framework 클래스 라이브러리에서 호출하는 API가 .NET Standard 2.0에 포함되어야 합니다.

### <a name="support-for-visual-basic"></a>Visual Basic에 대한 지원

이제 Visual Basic에서 .NET Standard 라이브러리를 개발할 수 있습니다. .NET Core 워크로드가 설치된 Visual Studio 2017 버전 15.3 이상을 사용하는 Visual Basic 개발자의 경우 이제 Visual Studio에는 .NET Standard 클래스 라이브러리 템플릿이 포함됩니다. 다른 개발 도구와 환경을 사용하는 Visual Basic 개발자의 경우 [dotnet new](../../core/tools/dotnet-new.md) 명령을 사용하여 .NET Standard 라이브러리 프로젝트를 만들 수 있습니다. 자세한 내용은 [.NET Standard 라이브러리에 대한 도구 지원](#tooling-support-for-net-standard-libraries)을 참조하세요.

### <a name="tooling-support-for-net-standard-libraries"></a>.NET Standard 라이브러리에 대한 도구 지원

.NET Core 2.0 및 .NET Standard 2.0의 릴리스에서는 Visual Studio 2017 및 [.NET Core CLI(명령줄 인터페이스)](../../core/tools/index.md)에 둘 다 .NET Standard 라이브러리를 만들기 위한 도구 지원이 포함됩니다.

**.NET Core 플랫폼 간 개발** 워크로드를 통해 Visual Studio를 설치하는 경우 다음 그림과 같이 프로젝트 템플릿을 사용하여 .NET Standard 2.0 라이브러리 프로젝트를 만들 수 있습니다.

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

![새 .NET Standard 라이브러리 프로젝트 추가](./media/std-project-cs.png)

.NET Core CLI를 사용하는 경우 다음 [dotnet new](../../core/tools/dotnet-new.md) 명령은 .NET Standard 2.0을 대상으로 하는 클래스 라이브러리 프로젝트를 만듭니다.

```
dotnet new classlib
```

# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb)

![새 .NET Standard 라이브러리 프로젝트 추가](./media/std-project-vb.png)

.NET Core CLI를 사용하는 경우 다음 [dotnet new](../../core/tools/dotnet-new.md) 명령은 .NET Standard 2.0을 대상으로 하는 클래스 라이브러리 프로젝트를 만듭니다.

```
dotnet new classlib -lang vb
```

---

## <a name="see-also"></a>참고 항목

- [.NET Standard](../net-standard.md)  
- [.NET Standard 소개](https://blogs.msdn.microsoft.com/dotnet/2016/09/26/introducing-net-standard/)
