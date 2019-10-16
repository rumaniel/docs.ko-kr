---
title: 데이터 변경 및 변경 내용 전송
ms.date: 03/30/2017
ms.assetid: d68c2dc3-99b3-49ab-b547-2ca5b386429a
ms.openlocfilehash: 18468c9a2018a28e85d87155d98b0853854013fd
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792970"
---
# <a name="making-and-submitting-data-changes"></a>데이터 변경 및 변경 내용 전송

이 단원의 항목에서는 데이터베이스에 변경 내용을 만들고 전송하는 방법과 낙관적 동시성 충돌을 처리하는 방법에 대해 설명합니다.

> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], `Insert` 및 `Update` 데이터베이스 작업에 대한 `Delete` 기본 메서드를 재정의할 수 있습니다. 자세한 내용은 [삽입, 업데이트 및 삭제 작업 사용자 지정](customizing-insert-update-and-delete-operations.md)을 참조 하세요.
>
> Visual Studio를 사용 하는 개발자는 개체 관계형 디자이너을 사용 하 여 동일한 목적으로 저장 프로시저를 개발할 수 있습니다.

## <a name="in-this-section"></a>섹션 내용

[방법: 데이터베이스에 행 삽입](how-to-insert-rows-into-the-database.md) \
개체 모델에 개체를 추가하여 데이터베이스에 행을 삽입하는 방법에 대해 설명합니다.

[방법: 데이터베이스의 행 업데이트](how-to-update-rows-in-the-database.md) \
개체 모델에 개체를 업데이트하여 데이터베이스에 행을 업데이트하는 방법에 대해 설명합니다.

[방법: 데이터베이스에서 행 삭제](how-to-delete-rows-from-the-database.md) \
개체 모델에서 개체를 삭제하여 데이터베이스의 행을 삭제하는 방법에 대해 설명합니다.

[방법: 데이터베이스에 변경 내용 전송](how-to-submit-changes-to-the-database.md) \
데이터베이스에 개체 모델 변경 내용을 보내는 방법에 대해 설명합니다.

[방법: 트랜잭션을 사용 하 여 대괄호 데이터 전송](how-to-bracket-data-submissions-by-using-transactions.md) \
트랜젝션에 작업을 포함시키는 방법에 대해 설명합니다.

[방법: 동적으로 데이터베이스 만들기](how-to-dynamically-create-a-database.md) \
동적으로 데이터베이스를 생성하고 이 방법에 대한 일반적인 시나리오에 대해 설명합니다.

[방법: 변경 내용 충돌 관리](how-to-manage-change-conflicts.md) \
낙관적 동시성 문제를 해결하는 기술에 대해 설명합니다.
