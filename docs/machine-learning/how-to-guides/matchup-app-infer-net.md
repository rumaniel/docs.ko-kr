---
title: Infer.NET 및 확률적 프로그래밍을 사용하여 게임 대전 목록 앱 만들기
description: Infer.NET과 함께 확률적 프로그래밍을 사용하여 TrueSkill의 간소화된 버전을 기반으로 게임 대전 목록 앱을 만드는 방법을 알아봅니다.
ms.date: 05/06/2019
ms.custom: mvc,how-to
ms.openlocfilehash: f6f91aecfe7fdeffb7e8913309046c7942ecbab7
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71957207"
---
# <a name="create-a-game-match-up-list-app-with-infernet-and-probabilistic-programming"></a>Infer.NET 및 확률적 프로그래밍을 사용하여 게임 대전 목록 앱 만들기

이 방법 가이드에서는 Infer.NET을 사용하는 확률적 프로그래밍을 설명합니다. 확률적 프로그래밍은 사용자 지정 모델을 컴퓨터 프로그램으로 표현하는 기계 학습 접근 방식입니다. 이를 통해 모델의 도메인 정보를 통합할 수 있고 기계 학습 시스템이 더 쉽게 해석할 수 있습니다. 새 데이터가 도착할 때 수행되는 학습 프로세스인 온라인 유추도 지원합니다. Infer.NET은 Azure, Xbox 및 Bing에서 Microsoft의 다양한 제품에 사용됩니다.

## <a name="what-is-probabilistic-programming"></a>확률적 프로그래밍이란 무엇인가요?

확률적 프로그래밍을 사용하면 실제와 같은 프로세스의 통계 모델을 만들 수 있습니다.

## <a name="prerequisites"></a>전제 조건

- 로컬 개발 환경 설정

  이 방법 가이드에서는 개발에 사용할 수 있는 머신이 있다고 예상합니다. .NET 자습서 [Hello World 10분 완성](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro)에는 macOS, Windows 또는 Linux의 로컬 개발 환경 설정에 대한 지침이 포함되어 있습니다.

## <a name="create-your-app"></a>앱 만들기

1. 새 명령 프롬프트를 열고 다음 명령을 실행합니다.

```dotnetcli
dotnet new console -o myApp
cd myApp
```

`dotnet` 명령은 `console` 형식의 `new` 애플리케이션을 만듭니다. `-o` 매개 변수는 앱이 저장되는 `myApp`이라는 디렉터리를 만들고 필요한 파일로 채웁니다. `cd myApp` 명령을 실행하면 새로 만들어진 앱 디렉터리로 이동합니다.

## <a name="install-infernet-package"></a>Infer.NET 패키지 설치

Infer.NET을 사용하려면 `Microsoft.ML.Probabilistic.Compiler` 패키지를 설치해야 합니다. 명령 프롬프트에서 다음 명령을 실행합니다.

```dotnetcli
dotnet add package Microsoft.ML.Probabilistic.Compiler
```

## <a name="design-your-model"></a>모델 디자인

예제 샘플에서는 사무실에서 진행되는 탁구 또는 테이블 축구 대전을 사용합니다. 각 대전의 참가자 및 결과가 제공됩니다.  이 데이터에서 플레이어의 기술을 유추하려고 합니다. 각 플레이어는 정상적으로 배포된 잠재 기술을 보유하고 플레이어의 특정 대전 성과는 이 기술의 정리되지 않은 버전이라고 가정하겠습니다. 데이터는 승자의 성과를 패자의 성과보다 크도록 제한합니다. 이는 팀, 그리기 및 기타 확장을 지원하는 인기 있는 [TrueSkill](https://www.microsoft.com/en-us/research/project/trueskill-ranking-system/) 모델의 간소화된 버전입니다. 이 모델의 [고급 버전](https://www.microsoft.com/en-us/research/publication/trueskill-2-improved-bayesian-skill-rating-system/)은 최대 판매 게임 타이틀인 Halo and Gears of War의 대전표 작성에 사용됩니다.

유추된 플레이어 기술을, 기술의 불확실성 측정값인 해당 차이와 함께 나열해야 합니다.

게임 결과 예제 데이터 

게임 |승자 | 패자
---------|----------|---------
 1 | 플레이어 0 | 플레이어 1
 2 | 플레이어 0 | 플레이어 3
 3 | 플레이어 0 | 플레이어 4
 4 | 플레이어 1 | 플레이어 2
 5 | 플레이어 3 | 플레이어 1
 6 | 플레이어 4 | 플레이어 2

예제 데이터를 자세히 살펴보면 플레이어 3과 플레이어 4가 둘 다 1승 1패임을 알 수 있습니다. 확률적 프로그래밍을 사용하여 순위가 어떻게 표시되는지 확인해 보겠습니다. 개발자는 사무실 대전 목록도 0부터 시작하므로 플레이어 0도 있음을 알 수 있습니다.

## <a name="write-some-code"></a>일부 코드 작성

모델을 디자인했으므로 Infer.NET 모델링 API를 사용하여 확률적 프로그램으로 표현해 보겠습니다. 원하는 텍스트 편집기에서 `Program.cs`를 열고 모든 콘텐츠를 다음 코드로 바꿉니다.

```csharp
namespace myApp

{
    using System;
    using System.Linq;
    using Microsoft.ML.Probabilistic;
    using Microsoft.ML.Probabilistic.Distributions;
    using Microsoft.ML.Probabilistic.Models;

    class Program
    {

        static void Main(string[] args)
        {
            // The winner and loser in each of 6 samples games
            var winnerData = new[] { 0, 0, 0, 1, 3, 4 };
            var loserData = new[] { 1, 3, 4, 2, 1, 2 };

            // Define the statistical model as a probabilistic program
            var game = new Range(winnerData.Length);
            var player = new Range(winnerData.Concat(loserData).Max() + 1);
            var playerSkills = Variable.Array<double>(player);
            playerSkills[player] = Variable.GaussianFromMeanAndVariance(6, 9).ForEach(player);

            var winners = Variable.Array<int>(game);
            var losers = Variable.Array<int>(game);

            using (Variable.ForEach(game))
            {
                // The player performance is a noisy version of their skill
                var winnerPerformance = Variable.GaussianFromMeanAndVariance(playerSkills[winners[game]], 1.0);
                var loserPerformance = Variable.GaussianFromMeanAndVariance(playerSkills[losers[game]], 1.0);

                // The winner performed better in this game
                Variable.ConstrainTrue(winnerPerformance > loserPerformance);
            }

            // Attach the data to the model
            winners.ObservedValue = winnerData;
            losers.ObservedValue = loserData;

            // Run inference
            var inferenceEngine = new InferenceEngine();
            var inferredSkills = inferenceEngine.Infer<Gaussian[]>(playerSkills);

            // The inferred skills are uncertain, which is captured in their variance
            var orderedPlayerSkills = inferredSkills
               .Select((s, i) => new { Player = i, Skill = s })
               .OrderByDescending(ps => ps.Skill.GetMean());

            foreach (var playerSkill in orderedPlayerSkills)
            {
                Console.WriteLine($"Player {playerSkill.Player} skill: {playerSkill.Skill}");
            }
        }
    }
}
```

## <a name="run-your-app"></a>앱 실행

명령 프롬프트에서 다음 명령을 실행합니다.

```dotnetcli
dotnet run
```

## <a name="results"></a>결과

다음과 같은 결과가 나타나야 합니다.

```console
Compiling model...done.
Iterating:
.........|.........|.........|.........|.........| 50
Player 0 skill: Gaussian(9.517, 3.926)
Player 3 skill: Gaussian(6.834, 3.892)
Player 4 skill: Gaussian(6.054, 4.731)
Player 1 skill: Gaussian(4.955, 3.503)
Player 2 skill: Gaussian(2.639, 4.288)
```

결과에서 모델에 따라 플레이어 3의 순위가 플레이어 4보다 약간 더 높음을 알 수 있습니다. 플레이어 1에 대한 플레이어 3의 승리가 플레이어 2에 대한 플레이어 4의 승리보다 더 중요합니다. 플레이어 1은 플레이어 2를 이겼기 때문입니다. 플레이어 0이 전체 챔피언입니다.

## <a name="keep-learning"></a>계속 학습

통계 모델 디자인은 훌륭한 기술입니다. Microsoft Research Cambridge 팀은 문서에 대한 가벼운 소개를 제공하는 [무료 온라인 설명서](http://mbmlbook.com/)를 작성했습니다. 이 설명서의 3장에서는 TrueSkill 모델을 더 자세히 다룹니다. 모델을 계획한 후 Infer.NET 웹 사이트에서 [광범위한 문서](https://dotnet.github.io/infer/)를 사용하여 모델을 코드로 변환할 수 있습니다.

## <a name="next-steps"></a>다음 단계

학습을 계속하고 더 많은 샘플을 찾으려면 Infer.NET GitHub 리포지토리를 체크 아웃하세요.
> [!div class="nextstepaction"]
> [dotnet/infer GitHub 리포지토리](https://github.com/dotnet/infer)
