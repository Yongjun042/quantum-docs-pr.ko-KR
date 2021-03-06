---
title: 전자 시스템용 퀀텀 모델 | Microsoft Docs
description: Electronic Systems의 퀀텀 모델 개념 문서
author: nathanwiebe2
ms.author: nawiebe@microsoft.com
ms.date: 10/09/2017
ms.topic: article-type-from-white-list
uid: microsoft.quantum.chemistry.concepts.quantummodels
ms.openlocfilehash: 45d134333c8a3c8937d206cb0a4a9cc6101a85df
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2019
ms.locfileid: "73184154"
---
# <a name="quantum-models-for-electronic-systems"></a>전자 시스템용 퀀텀 모델

전자 시스템을 시뮬레이션 하려면 먼저 위에서 설명한 정식 양자화 절차에서 찾을 수 있는 Hamiltonian를 지정 하 여 시작 해야 합니다.
특히 $N _e $ 파괴 with momenta $p _i $ (3 차원)와 mass $m _e $ 및 position 벡터 $x _i $Z를 사용 하 여 _k $y e $ at position _k $, Hamiltonian 연산자는 \begin{equation} \hat{H} = \sum\_{i = 1} ^ {N\_e} \frac{\hat{p}\_i ^ 2} {2m\_e} + \frac{1}{2}\sum\_{i\ne j} \frac{e ^ 2} {| \hat{x}\_i-\hat{x}\_j |}-\sum\_{i , k} \frac{Z\_ke ^ 2} {| \hat{x}\_i-{y}\_k |} + \frac{1}{2} \ sum_ {k\ne k '} \frac{Z\_kZ\_{k '} e ^ 2} {| y\_k-y\_k ' |}. \label{eq: Ham} \end{cation} momenta operators $ \hat{p}\_i ^ 2 $는 실제 공간에서 라플라스 operators로 볼 수 있습니다. 즉, $ \hat{p}\_i ^ 2 =-\partial\_{x\_i} ^ 2-\partial\_{y\_i} ^ 2-\partial\_{z\_i} ^ 2 $.
여기서는 nuclei가 분자에 대 한 미사용 가정을 단순화 했습니다.
이를 Steiglitz 근사값 이라고 하며, 전자 \hat{H}는 proton의 질량에 약 $1/1836 $가 있기 때문에 $ $의 저 에너지 에너지 스펙트럼에 유효한 경향이 있습니다.
이 Hamiltonian 연산자는 $N\_e $ 파괴의 시스템에 대 한 에너지를 기록 하 고 [퀀텀 Dynamics](xref:microsoft.quantum.chemistry.concepts.quantumdynamics)에 설명 된 정식 양자화 프로세스를 적용 하 여 쉽게 찾을 수 있습니다.

$E ^ {-i\hat {H} t} $에 대 한 단일 매트릭스 표현을 생성 하려면 $ \hat{H} $ 연산자를 행렬로 나타내야 합니다.
이를 위해 좌표계 또는 기준을 선택 하 여 문제를 표시 해야 합니다.
예를 들어 $ \ psi_j $이 $N _e $ 파괴에 대 한 직교 기준 함수 집합인 경우 행렬을 정의할 수 있습니다.

\begin{st} H\_{i, j} = \int\_{-\infty} ^ \infty\int\_{-\infty} ^ \infty \psi ^ {\*}\_i (x\_1) \hat{H} \psi\_j (x\_2) \dd ^ 3 x\_1 \dd ^ 3 x\_2. \ 레이블 {eq: discreteHam} \begin{equation}

원칙에 따라 $ \hat{H} $ 연산자는 제한 되지 않으며 유한 차원 공간에서 작동 하지 않습니다. 요소가 포함 된 행렬 $H\_\{i, j\}$가 있습니다.
즉, 너무 작은 기준 집합을 선택 하 여 오류가 발생 합니다. 그러나 많은 것을 선택 하는 경우에는 화학를 시뮬레이션 하는 것이 어렵습니다.
이러한 이유로 문제를 간결 하 게 나타낼 수 있는 기준을 선택 하는 것은 전자 구조 문제를 해결 하는 데 중요 합니다.

사용할 수 있는 적절 한 기본이 많이 있으며 문제에 적합 하 게 선택 하는 것은 퀀텀 연금술의 대부분입니다.
가장 간단한 이러한 기본 집합은 hydrogen 같은 atom의 Schrödinger 수식 ($ \hat{H} $의 eigenfunctions)에 대 한 (orthogonalized) 솔루션 인 Slater 형식 ()
평면-물결 또는 실제 공간 orbitals와 같은 기타 기준 집합을 사용할 수 있으며, 자세한 내용은 Helgaker에의 한 표준 텍스트 [' 분자 e-구조 이론 '](https://onlinelibrary.wiley.com/doi/book/10.1002/9781119019572) 에 대 한 자세한 정보를 참조 하세요.

위의 모델에 사용 되는 상태는 임의의 것으로 보일 수 있지만, 퀀텀 메커니즘은 특성에 따라 달라질 수 있는 상태에 제한을 둡니다.
특히 모든 유효한 전자 퀀텀 상태는 전자 레이블이 교환 되는 상태에서 대칭이 되어야 합니다.
$ \Psi (x_1, x_2) $가 두 파괴의 조인트 퀀텀 상태에 대 한 wave 함수인 경우 $ $ \psi (x_1, x_2) =-\psi (x_2, x_1)를 포함 해야 합니다.
$ $ 두 개의 파괴를 동일한 퀀텀 상태에 있는 것으로 금지 하는 Pauli 제외 원칙은 fascinatingly ($ \psi (x_1, x_1) \maps\psi와 동일한 위치에 있는 두 파괴를 교환 하는 경우 intuited 수 있습니다. $ \psi (x_1, x_1) = 0 $이 아닌 x_1, x_1) \ne-\psi (x_1, x_1) $
따라서이 대칭 대칭 속성을 준수 하기 위해 초기 상태를 선택 하 고 동시에 두 개의 파괴를 동일한 상태로 설정 하지 않아야 합니다.
이는 여러 파괴가 동일한 상태가 아닌 것을 금지 하 고, 결과적으로 퀀텀 컴퓨터에서 단일 퀀텀 비트를 사용 하 여 지정 된 퀀텀 상태의 파괴 수를 저장 하도록 허용 하기 때문에 전자 구조에 매우 중요 합니다.

이러한 상태를 분할 퀀텀 컴퓨터에서 퀀텀 메커니즘을 시뮬레이션할 수는 있지만,이 필드에서 대부분의 작업에는 상태를 저장 하는 데 많은 수의 요구가 필요 하며, 준비를 위해 복잡 한 상태 준비 절차가 필요 하기 때문에 앤티 대칭 초기 상태입니다.
그러나 다른 관점에서 시뮬레이션 문제를 확인 하 여 이러한 문제를 sidestepped 수 있습니다.
