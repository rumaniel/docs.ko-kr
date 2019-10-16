---
title: ML.NET을 통해 자동화된 기계 학습
description: 자동 모델 선택 및 학습에 대한 개요
author: natke
ms.date: 05/01/2019
ms.topic: overview
ms.custom: mvc
ms.author: nakersha
ms.openlocfilehash: da2d764e678debc78a25faeb8e48facb44fc4021
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929416"
---
# <a name="automated-machine-learning-with-mlnet"></a>ML.NET을 통해 자동화된 기계 학습

자동화된 기계 학습은 자동 모델 선택과 학습을 수행하는 ML.NET 기능입니다. 기계 학습 작업을 지정하고 데이터 세트를 제공하면 자동 ML이 최적의 메트릭이 있는 모델을 선택합니다. 다음을 출력합니다.

- 예측 애플리케이션에 로드할 수 있는 모델 파일
- 예측을 수행하는 애플리케이션 코드
- 기능 선택 및 모델 학습(모델 이해를 위해)에 사용되는 소스 코드

> [!NOTE]
> 이 기능은 현재 미리 보기로 제공되며, 자료는 변경될 수 있습니다. 

자동화된 ML은 현재 이진 분류, 다중 클래스 분류, 회귀의 기게 학습 [작업](resources/tasks.md)으로 제한됩니다. 다른 기계 학습 작업은 향후 릴리스에서 지원될 것입니다.

세 가지 방법으로 자동화된 ML을 사용할 수 있습니다.

1. 그래픽 사용자 인터페이스에서 [ML.NET 모델 작성기](automate-training-with-model-builder.md) 사용
1. 명령줄에서 [ML.NET CLI](automate-training-with-cli.md) 사용
1. 애플리케이션에서 [자동화된 ML API](how-to-guides/how-to-use-the-automl-api.md) 사용
