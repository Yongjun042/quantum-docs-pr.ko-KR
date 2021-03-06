---
title: Q# 프로그래밍 언어 | Microsoft Docs
description: Q# 프로그래밍 언어
author: QuantumWriter
ms.author: Alan.Geller@microsoft.com
ms.date: 12/11/2017
ms.topic: article
uid: microsoft.quantum.language.intro
ms.openlocfilehash: 560926f6f3e05c32a935f01ca5107a614e743ee2
ms.sourcegitcommit: aa5e6f4a2deb4271a333d3f1b1eb69b5bb9a7bad
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73442474"
---
# <a name="the-q-programming-language"></a>Q# 프로그래밍 언어

## <a name="introduction"></a>소개

양자 컴퓨팅의 자연 모델은 양자 컴퓨터를 GPU, FPGA 및 기타 부속 모델 프로세서에 사용되는 것과 비슷한 보조 프로세서로 처리하는 것입니다.
기본 제어 논리는 클래식 "호스트" 컴퓨터에서 클래식 코드를 실행합니다.
적절하고 필요한 경우 호스트 프로그램은 보조 모델에서 실행되는 서브루틴을 호출할 수 있습니다.
서브루틴이 완료되면 호스트 프로그램은 서브루틴의 결과에 대한 액세스 권한을 얻습니다.

Q#(Q-sharp)은 양자 알고리즘을 표현하는 데 사용되는 도메인별 프로그래밍 언어입니다.
클래식 호스트 프로그램 및 컴퓨터의 제어에 따라, 보조 양자 프로세서에서 실행되는 서브루틴을 작성하려는 경우 이 언어를 사용해야 합니다.
양자 프로세서를 광범위하게 사용할 수 있게 될 때까지, Q# 서브루틴이 시뮬레이터에서 실행됩니다.

Q#은 구조화된 새 형식을 만들기 위한 두 가지 방법(배열 및 튜플)과 함께 소규모 기본 형식 세트를 제공합니다.
루프 및 if/then 문을 사용하여 프로그램을 작성하기 위한 기본 절차 모델을 지원합니다.
Q#의 최상위 구문은 사용자 정의 형식, 연산 및 함수입니다.

이에 대해서는 다음 섹션에서 자세히 설명합니다.
- [형식 모델](xref:microsoft.quantum.language.type-model)
- [식](xref:microsoft.quantum.language.expressions)
- [문](xref:microsoft.quantum.language.statements)
- [파일 구조](xref:microsoft.quantum.language.file-structure)

## <a name="conventions"></a>규칙

모든 상황에서 일반적인 문장 부호를 일관되게 사용하기 위해 노력하고 있습니다.
이러한 표시는 항상 동일한 사항을 의미하며 동일한 개념은 항상 동일한 방식으로 표시되므로 Q#을 보다 쉽게 학습하고 읽을 수 있게 됩니다.

구체적으로 살펴보면 다음과 같습니다.

- 세미콜론(`;`)은 문이나 한 줄로 된 지시문을 종료하는 데 사용됩니다.
  다른 용도로는 사용되지 않습니다.
- 쉼표(`,`)는 시퀀스의 요소를 구분하는 데 사용됩니다. 튜플 리터럴, 배열 리터럴, 인수 목록, 튜플 정의 및 형식 목록에 사용됩니다. **이전 버전과 달리, `;`은 더 이상 배열 리터럴 구분 기호로 지원되지 않습니다.**
- 콜론(`:`)은 형식 주석을 도입하는 데 사용됩니다. 주로 호출 가능 시그니처에서 사용됩니다.
  콜론은 항상 형식 시그니처를 도입하므로 0.3에 도입된 세 부분으로 구성된 조건부 연산자는 세로 막대 `|`를 사용하여 true와 false 값을 구분합니다. 따라서 Q#은 C에서와 같이 콜론 대신 `cond ? tval | fval`을 구분 기호로 사용합니다.
  
