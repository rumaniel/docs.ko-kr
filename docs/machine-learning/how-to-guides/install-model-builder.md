---
title: 모델 작성기 설치 방법
description: ML.NET 모델 작성기 도구를 설치하는 방법 알아보기
author: luisquintanilla
ms.author: luquinta
ms.date: 06/21/2019
ms.custom: mvc, how-to
ms.openlocfilehash: b0d45ab7807bf84b98c58e85580d5aa04d0c5f7d
ms.sourcegitcommit: 1e72e2990220b3635cebc39586828af9deb72d8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71306321"
---
# <a name="how-to-install-mlnet-model-builder"></a>ML.NET 모델 작성기 설치 방법

ML.NET 모델 작성기를 설치하여 .NET 애플리케이션에 기계 학습을 추가하는 방법에 대해 알아봅니다.

> [!NOTE]
> 모델 작성기는 현재 미리 보기로 제공됩니다.

## <a name="pre-requisites"></a>필수 구성 요소

- Visual Studio 2017 15.9.12 이상 / Visual Studio 2019
- .NET Core 2.1 이상 SDK

## <a name="limitations"></a>제한 사항

- ML.NET 모델 작성기 확장은 현재 Windows의 Visual Studio에서만 작동합니다.
- 1GB의 학습 데이터 세트 제한
- SQL 서버에는 학습을 위한 행 수가 10만개로 제한됩니다.
- Visual Studio 2017용 Microsoft SQL Server Data Tools는 지원되지 않습니다.

## <a name="install"></a>설치

Visual Studio Marketplace를 통해 또는 Visual Studio 내에서 ML.NET 모델 작성기를 설치할 수 있습니다. 

### <a name="visual-studio-marketplace"></a>Visual Studio Marketplace

1. [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=MLNET.07)에서 다운로드
1. 프롬프트에 따라 각 Visual Studio 버전에 설치합니다.

### <a name="visual-studio-2017"></a>Visual Studio 2017

1. 메뉴 모음에서 **도구** > **확장 및 업데이트**를 선택합니다.

    ![VS2017 확장 관리자 대화 상자 열기](./media/install-model-builder/vs2017-open-extensions-manager.png)

1. *확장 및 업데이트* 프롬프트 내에서 *Online* 노드를 선택합니다.
1. 검색 창에서 *ML.NET 모델 작성기*를 검색하고 결과에서 ML.NET 모델 작성기(미리 보기)를 선택합니다.

    ![VS2017 확장 관리자 대화 상자에서 모델 작성기 확장 검색 및 설치](./media/install-model-builder/vs2017-install-model-builder.png)

1. 프롬프트에 따라 설치를 완료합니다.

### <a name="visual-studio-2019"></a>Visual Studio 2019

1. 메뉴 모음에서 **확장** > **확장 관리**를 선택합니다.

    ![VS2019 확장 관리자 대화 상자 열기](./media/install-model-builder/vs2019-open-extensions-manager.png)

1. *확장 및 업데이트* 프롬프트 내에서 *Online* 노드를 선택합니다.
1. 검색 창에 *ML.NET 모델 작성기*를 입력하고 ML.NET 모델 작성기(미리 보기)를 선택합니다.

    ![VS2019 확장 관리자 대화 상자에서 모델 작성기 확장 검색 및 설치](./media/install-model-builder/vs2019-install-model-builder.png)

1. 프롬프트에 따라 설치를 완료합니다.

## <a name="uninstall"></a>제거

### <a name="visual-studio-2017"></a>Visual Studio 2017

1. 메뉴 모음에서 **도구** > **확장 및 업데이트**를 선택합니다.

    ![VS2017 확장 관리자 대화 상자 열기](./media/install-model-builder/vs2017-open-extensions-manager.png)

1. *확장 및 업데이트* 프롬프트 내에서 *설치됨* 노드를 확장하고 *도구*를 선택합니다.
1. 도구 목록에서 ML.NET 모델 작성기(미리 보기)를 선택한 다음, *제거*를 선택합니다.

    ![VS2017 확장 관리자 대화 상자에서 모델 작성기 확장 검색 및 제거](./media/install-model-builder/vs2017-uninstall-model-builder.png)

1. 프롬프트에 따라 제거를 완료합니다.

### <a name="visual-studio-2019"></a>Visual Studio 2019

1. 메뉴 모음에서 **확장** > **확장 관리**를 선택합니다.

    ![VS2019 확장 관리자 대화 상자 열기](./media/install-model-builder/vs2019-open-extensions-manager.png)

1. *확장 및 업데이트* 프롬프트 내에서 *설치됨* 노드를 확장하고 *도구*를 선택합니다.
1. 도구 목록에서 ML.NET 모델 작성기(미리 보기)를 선택한 다음, *제거*를 선택합니다.

    ![VS2019 확장 관리자 대화 상자에서 모델 작성기 확장 검색 및 제거](./media/install-model-builder/vs2019-uninstall-model-builder.png)

1. 프롬프트에 따라 제거를 완료합니다.

## <a name="upgrade"></a>Upgrade

업그레이드 프로세스는 설치 프로세스와 유사합니다. Visual Studio Marketplace에서 최신 버전을 다운로드하거나 Visual Studio에서 확장 관리자를 사용합니다.
