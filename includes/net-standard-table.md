---
ms.openlocfilehash: 9b8d28f7f5508b4ba7c46306b5e78aa3d53d95e0
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71263336"
---
| .NET Standard              | [1.0]  | [1.1]  | [1.2] | [1.3] | [1.4] | [1.5]              | [1.6]              | [2.0]               | [2.1] |
|----------------------------|--------|--------|-------|-------|-------|--------------------|--------------------|---------------------|---------------------
| .NET Core                  | 1.0    | 1.0    | 1.0   | 1.0   | 1.0   | 1.0                | 1.0                | 2.0                 | 3.0 |
| .NET Framework <sup>1</sup>| 4.5    | 4.5    | 4.5.1 | 4.6   | 4.6.1 | 4.6.1 <sup>2</sup> | 4.6.1 <sup>2</sup> | 4.6.1 <sup>2</sup>  | 해당 없음<sup>3</sup> |
| Mono                       | 4.6    | 4.6    | 4.6   | 4.6   | 4.6   | 4.6                | 4.6                | 5.4                 | 6.4 |
| Xamarin.iOS                | 10.0   | 10.0   | 10.0  | 10.0  | 10.0  | 10.0               | 10.0               | 10.14               | 12.16 |
| Xamarin.Mac                | 3.0    | 3.0    | 3.0   | 3.0   | 3.0   | 3.0                | 3.0                | 3.8                 | 5.16 |
| Xamarin.Android            | 7.0    | 7.0    | 7.0   | 7.0   | 7.0   | 7.0                | 7.0                | 8.0                 | 10.0 |
| UWP | 10.0   | 10.0   | 10.0  | 10.0  | 10.0  | 10.0.16299         | 10.0.16299         | 10.0.16299          | TBD |
| Unity                      | 2018.1 | 2018.1 | 2018.1| 2018.1| 2018.1| 2018.1             |  2018.1            | 2018.1              | TBD |

<sup>1 .NET Framework용으로 나열된 버전은 .NET Core 2.0 SDK 이상 버전의 도구에 적용됩니다. 이전 버전에서는 .NET Standard 1.5 이상에서 다른 매핑을 사용했습니다. Visual Studio 2017로 업그레이드할 수 없는 경우 [Visual Studio 2015용 .NET Core 도구를 다운로드](https://github.com/dotnet/core/blob/master/release-notes/download-archive.md)할 수 있습니다.</sup>

<sup>2 여기에 나열된 버전은 지정된 .NET Standard 라이브러리를 적용할 수 있는지 여부를 확인하기 위해 NuGet이 사용하는 규칙을 나타냅니다. NuGet에서는 .NET Framework 4.6.1을 .NET Standard 1.5에서 2.0까지 지원하는 것으로 간주하는 반면, .NET Framework 4.6.1에서 해당 버전용으로 빌드된 .NET Standard 라이브러리를 사용하는 데 몇 가지 문제가 있습니다. 이러한 라이브러리를 사용해야 하는 .NET Framework 프로젝트의 경우 .NET Framework 4.7.2 이상을 대상으로 하려면 프로젝트를 업그레이드하는 것이 좋습니다.</sup>

<sup>3 .NET Framework는 .NET Standard 2.1 이상 버전을 지원하지 않습니다. 자세한 내용은 [.NET Standard 2.1의 공지](https://devblogs.microsoft.com/dotnet/announcing-net-standard-2-1/)를 참조하세요.</sup>

- 열은 .NET 표준 버전을 나타냅니다. 각 헤더 셀은 .NET 표준의 해당 버전에 추가된 API를 보여 주는 문서의 링크입니다.
- 행은 다양한 .NET 구현을 나타냅니다.
- 각 셀의 버전 번호는 해당 .NET 표준 버전을 대상으로 지정하는 데 필요한 구현의 *최소* 버전을 나타냅니다.
- 대화형 테이블은 [.NET Standard 버전](https://dotnet.microsoft.com/platform/dotnet-standard#versions)을 참조하세요.

[1.0]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.0.md
[1.1]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.1.md
[1.2]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.2.md
[1.3]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.3.md
[1.4]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.4.md
[1.5]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.5.md
[1.6]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard1.6.md
[2.0]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.0.md
[2.1]: https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.1.md
