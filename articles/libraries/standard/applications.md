---
title: 'Q # 표준 라이브러리-응용 프로그램 | Microsoft Docs'
description: Q# 표준 라이브러리
author: QuantumWriter
uid: microsoft.quantum.libraries.applications
ms.author: martinro@microsoft.com
ms.date: 12/11/2017
ms.topic: article
ms.openlocfilehash: 3e629e095bd2ee492496066710ef6fd4e578a543
ms.sourcegitcommit: ca5015fed409eaf0395a89c2e4bc6a890c360aa2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76868971"
---
# <a name="applications"></a>애플리케이션 #

## <a name="hamiltonian-simulation"></a>해밀토니안 시뮬레이션 ##

퀀텀 시스템의 시뮬레이션은 퀀텀 계산의 가장 흥미로운 응용 프로그램 중 하나입니다.
기존 컴퓨터에서 퀀텀 메커니즘을 시뮬레이션 하는 어려움은 일반적으로 상태-벡터 표현의 차원 $N로 확장 됩니다.
이 표현은 $n $ wbits $N = 2 ^ n $의 수를 사용 하 여 급격 하 게 증가 하 고, 차원의 [저주](xref:microsoft.quantum.concepts.multiple-qubits)라고도 알려진 특성은 클래식 하드웨어의 퀀텀 시뮬레이션 intractable입니다.

그러나이 상황은 퀀텀 하드웨어에서 매우 다를 수 있습니다. 퀀텀 시뮬레이션의 가장 일반적인 변형은 시간 독립적 Hamiltonian 시뮬레이션 문제 라고 합니다. 여기에는 시스템 Hamiltonian $H $ (Hermitian 행렬) 및 일부 초기 퀀텀 상태 $ \ket{\psi (0)} $에 대 한 설명이 제공 됩니다 .이에 대해서는 퀀텀 컴퓨터에서 $를 사용 하 여 일부 $n 기준으로 인코딩됩니다. 폐쇄 된 시스템의 퀀텀 상태는 Schrödinger 수식 $ $ \begin{align} i\frac {d \ket{\psi (t)}} {d t} & = H \ket{\psi (t)}, \end{align} $ $으로 발전 하 고 있습니다 .이 목표는 단일 시간 진화 연산자 $U (t) = e ^ {-iHt} $를 고정 된 시간에 구현 하는 것입니다 $t $ , 여기서 $ \ket{\psi (t)} = U (t) \ket{\psi (0)} $은 Schrödinger 방정식을 해결 합니다.
와 유사 시간 종속 Hamiltonian 시뮬레이션 문제는 동일한 수식을 해결 하지만 이제는 $H (t) $를 사용 하 여 시간을 계산 합니다.

Hamiltonian 시뮬레이션은 다른 여러 퀀텀 시뮬레이션 문제의 주요 구성 요소 이며 Hamiltonian 시뮬레이션 문제에 대 한 해결 방법은 synthesizing에 대 한 기본 퀀텀 게이트의 시퀀스를 설명 하는 알고리즘입니다. 오류 $\\| \tilde{U}-U (t)\\[spectral](xref:microsoft.quantum.concepts.matrix-advanced)의 \le \le $입니다. 이러한 알고리즘의 복잡성은 퀀텀 컴퓨터에서 관심 있는 Hamiltonian에 대 한 설명을 액세스 하는 방법에 매우 강력한 영향을 줍니다. 예를 들어 최악의 경우, $n $ ombits에 대해 작동 하는 $H $은 각 matrix 요소에 대해 하나씩 $2 ^ n \times 2 ^ n $ 숫자의 목록으로 제공 되어야 합니다. 즉, 데이터를 읽기만 하면 지 수 시간이 이미 필요 합니다. 최상의 경우에는 $O \ket{t}\ket{\psi (0)} = \ket{t}U (t) \ket{\psi (0)} $ 일반적으로에서 문제를 해결 하는 검정 상자에 대 한 액세스를 가정할 수 있습니다. 이러한 입력 모델은 특히 유용 하지 않습니다. 즉, 기존의 접근 방식 보다는 더 이상 유용 하지 않으며, 검은색 상자는 구현에 대 한 기본 게이트 복잡성을 숨깁니다 .이는 다양 한 기능을 지 원하는 것입니다.

### <a name="descriptions-of-hamiltonians"></a>Hamiltonians에 대 한 설명 ###

따라서 입력 형식에 대 한 추가 가정이 필요 합니다. 현실적인 물리적 시스템이 나 흥미로운 계산 문제에 대 한 설명 및 충분히 제한적인 입력 모델 등 흥미로운 Hamiltonians을 포함 하는 데 충분 한 설명이 포함 된 입력 모델 간에 미세한 균형을 맞추어야 합니다. 퀀텀 컴퓨터에서 효율적으로 구현할 수 있습니다. 이 문서의 다양 한 특수 입력 모델을 찾을 수 있으며,이는 퀀텀에서 클래식으로 범위가 달라질 수 있습니다. 

퀀텀 입력 모델의 예로 [샘플 기반 Hamiltonian 시뮬레이션](http://www.nature.com/articles/s41534-017-0013-7) 에서는 Hamiltonian $H $로 사용 되는 밀도 행렬 $ \rho $의 복사본을 생성 하는 퀀텀 작업에 대 한 블랙 박스 액세스를 가정 합니다. [단일 액세스 모델](https://arxiv.org/abs/1202.5822) 에서 Hamiltonian는 대신 unitaries $ $ \begin{align} H & = \sum ^ {d-1}\_{j = 0} a\_j \hat{U}\_j, \end{align} $ $ where ($a\_j > 0 $은 계수이 고 $ \hat{U}\_j $는 unitaries입니다. 그런 다음 원하는 $ \hat{U}\_j $를 선택 하는 단일 oracle $V = \sum ^ {d-1}\_{j = 0} \ket{j}\bra{j}\otimes \hat{U}\_j $에 대 한 블랙 박스 액세스 권한이 있다고 가정 합니다. oracle $A \ket{0}= \sum ^ {d-1}\_{j = 0} \sqrt{a\_j/\ sum ^ {d-1}\_{k = 0} \sum\_j} \ket{j} $는 이러한 계수를 만드는 퀀텀 상태를 만듭니다. [스파스 Hamiltonian 시뮬레이션](https://arxiv.org/abs/quant-ph/0301023)의 경우 Hamiltonian는 모든 행에서 0이 아닌 $d = \mathcal{O} (\Text{polylog} (N)) $0 요소만 포함 된 스파스 행렬 이라고 가정 합니다. 또한 이러한 0이 아닌 요소의 위치와 해당 값을 출력 하는 효율적인 퀀텀 회로의 존재를 가정 합니다. [Hamiltonian 시뮬레이션 알고리즘](xref:microsoft.quantum.more-information) 의 복잡성은 이러한 검은색 상자에 대 한 쿼리 수 측면에서 평가 되며, 기본 게이트 복잡성은 이러한 검은색 상자를 구현 하는 데 어려움이 매우 높습니다.

> [!NOTE]
> 큰 O 표기법은 알고리즘의 복잡성 확장을 설명 하는 데 주로 사용 됩니다. G $ 라는 두 개의 실제 함수 $f g $ $g (x) = \mathcal{O} (f (x)) $는 모든 > \le x $g $0에 대 한 $x (x) \le c f (x) $와 같은 절대 양의 상수가\_0, c\_0 $ $x 있음을 의미 합니다. 

퀀텀 컴퓨터에서 구현 되는 대부분의 실용적인 응용 프로그램에서는 이러한 검은색 상자를 효율적으로 구현 해야 합니다. 즉, $ \mathcal{O} (\text{polylog} (N)) $ primitive 퀀텀 게이트를 사용할 수 있습니다. 더 강력 하 고 효율적으로 simulable Hamiltonians에는 충분 한 스파스 기존 설명이 있어야 합니다. 이러한 공식화 중 하나에서 Hamiltonian 분해는 Hermitian parts $ $ \begin{align} H & = \sum ^ {d-1} _ {j = 0} H_j의 합계로 가정 합니다.
\end{align} $ $ 뿐만 아니라 각 Hamiltonian $H\_j $를 시뮬레이션 하는 것으로 간주 됩니다. 즉, 모든 $t 시간에 대 한 단일 $e ^ {-iH\_j t} $는 $ \mathcal{O} (1) $ primitive 퀀텀 게이트를 사용 하 여 정확 하 게 구현할 수 있습니다. 예를 들어, 각 $H\_j $가 로컬 Pauli 연산자 인 특수 한 경우에는 이러한 경우가 있습니다. 즉,이는 공간적으로 닫힌 \mathcal{O}에 적용 되는 $ (1) $ 비 id Pauli 연산자의 텐서 제품입니다. 이 모델은 용어 수가 $d = \mathcal{O} (\text{polylog} (N)) $ 이기 때문에 경계 및 로컬 상호 작용을 사용 하는 물리적 시스템에 특히 적용할 수 있으며,이는 다항식 시간에 설명 된 일반적으로를 명확 하 게 작성할 수 있습니다.

> [!TIP]
> Hamiltonians 부품의 합계로 분리 하는 경우 동적 생성기 표현 라이브러리를 사용 하 여 설명할 수 있습니다. 자세한 내용은 [데이터 구조의](xref:microsoft.quantum.libraries.data-structures)동적 생성기 표현 섹션을 참조 하세요.

### <a name="simulation-algorithms"></a>시뮬레이션 알고리즘 ###

퀀텀 시뮬레이션 알고리즘은 Hamiltonian의 지정 된 설명을 기본 퀀텀 게이트 시퀀스로 변환 합니다. 즉, Hamiltonian에 의해 전체적으로 대략적인 시간이 진화 합니다.

Hamiltonian 분해 Hermitian 부분을 합산 하는 특별 한 경우 Trotter Suzuki 분해는 Hamiltonians 구성 요소 합계를 분리 하는 Hermitian를 시뮬레이션 하는 데 특히 간단 하 고 직관적인 알고리즘입니다. 예를 들면이 패밀리의 첫 번째 주문 통합자는 $ $ \begin{align} U (t) & = \left (e ^ {-iH\_0 t/r} e ^ {-iH\_1과 근사치를 갖습니다. t/r} \c도트 e ^ {-iH\_{d-1} t/r} \left) ^ {r} + \mathcal{O} (d ^ 2 \ max_j\\| H\_j\\| ^ 2 t ^ 2/r), \end{align} $ $ $r d $ 약관의 제품을 사용 합니다. 

> [!TIP]
> Trotter-Suzuki 시뮬레이션 알고리즘의 응용 프로그램은 샘플에서 설명 합니다.
> 각 대상 컴퓨터에서 제공 되는 내장 작업만 사용 하는 Ising 모델의 경우 [ **simpleising** 샘플](https://github.com/microsoft/Quantum/blob/master/samples/simulation/ising/simple)을 참조 하세요.
> Trotter-Suzuki library 컨트롤 구조를 사용 하는 Ising 모델의 경우 [ **IsingTrotter** 샘플](https://github.com/microsoft/Quantum/tree/master/samples/simulation/ising/trotter-evolution)을 참조 하세요.
> Trotter-Suzuki library 컨트롤 구조를 사용 하는 분자 Hydrogen의 경우 [ **H2 시뮬레이션** 샘플](https://github.com/microsoft/Quantum/tree/master/samples/simulation/h2/command-line)을 참조 하세요.

대부분의 경우 시뮬레이션 알고리즘을 구현 하지만 해당 구현에 대 한 세부 정보에 관심이 없습니다. 예를 들면 두 번째 주문 통합자는 $ $ \begin{align} U (t) & = \left (e ^ {-iH\_0 t/2r} e ^ {-iH\_1 t/2r} \c도트 e ^ {-iH\_{d-1} t/2r}를 대략적으로 계산 합니다. e ^ {-iH\_{d-1} t/2r} \c도트 e ^ {-iH\_1 t/2r} e ^ {-iH\_0 t/2r} \left) ^ {r} + \mathcal{O} (d ^ 3 \ max_j\\| H\_j\\| ^ 3 t ^ 3/r ^ 2), $2rd $ 약관의 제품을 사용 하 여 $ $ \end{align}. 더 큰 주문에는 더 많은 용어가 포함 되 고, 최적화 된 변형에는 지 수에 대 한 매우 특수 한 순서 필요할 수 있습니다. 다른 고급 알고리즘은 중간 단계에서 ancilla의 사용을 포함할 수도 있습니다. 따라서 라고의 시뮬레이션 알고리즘을 사용자 정의 형식으로 패키지 합니다.

```qsharp
newtype SimulationAlgorithm = ((Double, EvolutionGenerator, Qubit[]) => Unit is Adj + Ctl);
```

첫 번째 매개 변수 `Double` 시뮬레이션의 시간입니다. [데이터 구조의](xref:microsoft.quantum.libraries.data-structures)동적 생성기 표현 섹션에서 설명 하는 두 번째 매개 변수 `EvolutionGenerator`는 퀀텀 회로에서 Hamiltonian의 각 용어를 시뮬레이션 하는 방법에 대 한 지침을 포함 하는 시간 독립적 Hamiltonian 패키지에 대 한 기존 설명입니다. 이러한 형식의 형식에는 두 번째 매개 변수 `Qubit[]`(시뮬레이션 된 시스템의 퀀텀 상태를 저장 하는 레지스터)에 $e ^ {-iHt} $가 있습니다. 시간에 따라 달라 지는 경우에도 `EvolutionSchedule` 형식으로 사용자 정의 형식을 정의 합니다 .이 형식은 시간이 종속 된 Hamiltonian에 대 한 기존 설명입니다.

```qsharp
newtype TimeDependentSimulationAlgorithm = ((Double, EvolutionSchedule, Qubit[]) => Unit : Adjoint, Controlled);
```

예를 들어, 각 지 수에서 시뮬레이션 기간을 수정 하 `trotterStepSize` 매개 변수를 사용 하 여 Trotter-Suzuki 분해를 호출 하 고 원하는 통합자의 주문에 대 한 `trotterOrder` 수 있습니다.

```qsharp
function TrotterSimulationAlgorithm(
    trotterStepSize : Double, 
    trotterOrder : Int) 
: SimulationAlgorithm {
    ...
}

function TimeDependentTrotterSimulationAlgorithm(
    trotterStepSize : Double, 
    trotterOrder : Int) 
: TimeDependentSimulationAlgorithm {
    ...
}
```

> [!TIP]
> 시뮬레이션 라이브러리의 응용 프로그램은 샘플에서 설명 합니다. `SimulationAlgorithm`를 사용 하는 Ising 모델의 단계 예측에 대해서는 [ **IsingPhaseEstimation** 샘플](https://github.com/microsoft/Quantum/tree/master/samples/simulation/ising/phase-estimation)을 참조 하세요.
> `TimeDependentSimulationAlgorithm`를 사용 하는 Ising 모델의 adiabatic 상태 준비는 [ **AdiabaticIsing** 샘플](https://github.com/microsoft/Quantum/tree/master/samples/simulation/ising/adiabatic)을 참조 하세요.


### <a name="adiabatic-state-preparation--phase-estimation"></a>Adiabatic 상태 준비 & 단계 예측 ###

Hamiltonian 시뮬레이션의 한 가지 일반적인 응용 프로그램은 adiabatic 상태 준비입니다. 여기에는 두 개의 Hamiltonians $H\_{\text{start}} $ 및 $H\_{\text{start}} $과, Hamiltonian $H\_{\text{start}} $의 그라운드 상태에 해당 하는 퀀텀 상태 $ \ket{\psi (0)} $가 제공 됩니다. 일반적 $H으로 $ \ket{\psi (0)} $는 계산 기준 상태 $ \ket{0\cdots 0} $로 쉽게 준비할 수 있도록 {\text{start}} $\_를 선택 합니다. 시간이 종속 된 시뮬레이션 문제에서 이러한 Hamiltonians을 보간 하는 경우에는\_{\text{end}} $ $H 최종 Hamiltonian의 그라운드 상태에서 확률이 높은 종료 될 수 있습니다. Hamiltonian 그라운드 상태에 대 한 좋은 근사치을 준비 하는 것은 시간에 종속 된 Hamiltonian 시뮬레이션 알고리즘에 대해 서브루틴으로 호출 하 여 이러한 방식으로 진행 될 수 있지만, 다른 개념적으로 variational 양자와 같은 다른 방법으로 eigensolver 찾기가 가능 합니다.

그러나 퀀텀 화학의 또 다른 응용 프로그램은 화학 반응의 중간 단계를 나타내는 Hamiltonians의 그라운드 상태 에너지를 추정 하는 것입니다. 예를 들어 이러한 체계는 adiabatic 상태 준비를 사용 하 여 그라운드 상태를 만든 다음, 제한 된 오류와 함께이 에너지를 추출 하는 단계 예측의 서브루틴으로 시간 독립적 Hamiltonian 시뮬레이션을 통합할 수 있습니다. 성공 확률입니다. 

시뮬레이션 알고리즘을 `SimulationAlgorithm` 사용자 정의 형식으로 추상화 하 여 기능을 더욱 정교한 퀀텀 알고리즘에 편리 하 게 통합할 수 `TimeDependentSimulationAlgorithm`. 이는 일반적으로 사용 되는 이러한 서브루틴에 대해 동일한 작업을 motivates 합니다.

따라서 편리한 함수를 정의 합니다.

```qsharp
function InterpolatedEvolution(
        interpolationTime : Double, 
        evolutionGeneratorStart : EvolutionGenerator,
        evolutionGeneratorEnd : EvolutionGenerator,
        timeDependentSimulationAlgorithm : TimeDependentSimulationAlgorithm)
: (Qubit[] => Unit is Adj + Ctl) {
        ...
}
 
```

이렇게 하면 adiabatic 상태 준비의 모든 단계를 구현 하는 단일 작업이 반환 됩니다. 첫 번째 매개 변수 `interpolatedTime`는 두 번째 매개 변수 `evolutionGeneratorStart` 설명 하는 시작 Hamiltonian와 세 번째 매개 변수 `evolutionGeneratorEnd`에서 설명 하는 end Hamiltonian 간에 선형으로 보간 하는 시간을 정의 합니다. 네 번째 매개 변수 `timeDependentSimulationAlgorithm`은 시뮬레이션 알고리즘을 선택 하는 것입니다. `interpolatedTime` 시간이 충분 한 경우 초기 접지 상태는 시간에 따라 좌우 되는 시뮬레이션 전체에 걸쳐 Hamiltonian의 순간 그라운드 상태로 유지 되므로 end Hamiltonian의 그라운드 상태로 종료 됩니다.

또한 일반적인 퀀텀 화학 실험의 모든 단계를 자동으로 수행 하는 유용한 작업을 정의 합니다. 예를 들어 다음과 같이 adiabatic 상태 준비로 생성 된 상태의 에너지 추정치를 반환 합니다.

```qsharp
operation EstimateAdiabaticStateEnergy(
    nQubits : Int,
    statePrepUnitary : (Qubit[] => Unit),
    adiabaticUnitary : (Qubit[] => Unit),
    qpeUnitary: (Qubit[] => Unit is Adj + Ctl),
    phaseEstAlgorithm : ((DiscreteOracle, Qubit[]) => Double))
: Double {
...
}
```

`nQubits`는 초기 퀀텀 상태를 인코딩하는 데 사용 되는 수 비트 수입니다. `statePrepUnitary` 계산 기준 $ \ket{0\cdots 0} $에서 시작 상태를 준비 합니다. `adiabaticUnitary`은 `InterpolatedEvolution` 함수에서 생성 된 것과 같은 adiabatic 상태 준비를 구현 하는 단일 작업입니다. `qpeUnitary`은 결과 퀀텀 상태에서 단계 예측을 수행 하는 데 사용 되는 단일 작업입니다. `phaseEstAlgorithm` 단계 추정 알고리즘을 선택 하는 것입니다.

> [!TIP]
> Adiabatic 상태 준비의 응용 프로그램은 샘플에 설명 되어 있습니다. Adiabatic 상태 준비의 수동 구현을 사용 하는 Ising 모델 및 `AdiabaticEvolution` 함수 사용에 대 한 자세한 내용은 [ **AdiabaticIsing** 샘플](https://github.com/microsoft/Quantum/tree/master/samples/simulation/ising/adiabatic)을 참조 하세요.
> Ising 모델에서 단계 예측 및 adiabatic 상태 준비는 [ **IsingPhaseEstimation** 샘플](https://github.com/microsoft/Quantum/tree/master/samples/simulation/ising/phase-estimation)을 참조 하세요.

> [!TIP]
> [분자 Hydrogen의 시뮬레이션](https://github.com/microsoft/Quantum/tree/master/samples/simulation/h2/command-line) 은 흥미로운 간단한 샘플입니다. 모델 및 실험적 결과가 [O'Malley et](https://arxiv.org/abs/1512.06860) 에 보고 되었습니다. Pauli 행렬이 필요 하 고 $ \hat H = g\_의 형식으로 사용 합니다. {0}I\_0I\_1 + g\_1 {Z\_0} + g\_2 {Z\_1} + g\_3 {Z\_0} {Z\_1} + g\_4 {Y\_0} {Y\_1} + g\_5 {X\_0} {X\_1} $입니다. 이는 두 Hydrogen 원소 사이의 거리 $R $에서 상수 $g $가 계산 되는 2 개의 비트 비트만을 필요로 하는 효과적인 Hamiltonian. 라고 함수를 사용 하 여 paulis는 unitaries로 변환 된 다음 Trotter-Suzuki 분해를 사용 하 여 짧은 기간에 걸쳐 발전 했습니다. Adiabatic 상태 준비를 사용 하지 않고 $H _2 $ 그라운드 상태에 대 한 적절 한 근사값을 만들 수 있으므로 canon의 단계 예측을 활용 하 여 직접 상태 에너지를 찾을 수 있습니다.

## <a name="shors-algorithm"></a>쇼어 알고리즘 ##
Shor의 알고리즘은 현재 일반적으로 intractable 문제를 해결 하는 데 퀀텀 컴퓨터를 사용할 수 있다는 것을 보여 주므로 퀀텀 컴퓨팅에서 가장 중요 한 개발 중 하나입니다.
Shor의 알고리즘은 퀀텀 컴퓨터를 사용 하 여 많은 수의 수를 제공 하는 빠른 방법을 제공 하며,이는 *팩터링*이라는 문제입니다.
수많은 현재 인 cryptosystems의 보안은 팩터링에 대 한 빠른 알고리즘이 없다는 가정을 기반으로 합니다.
따라서 Shor의 알고리즘은 퀀텀 전 세계의 보안을 고려 하는 방법에 큰 영향을 미칩니다.

Shor의 알고리즘은 하이브리드 알고리즘으로 간주할 수 있습니다.
퀀텀 컴퓨터는 계산 하드 태스크를 수행 하는 데 사용 됩니다.
그런 다음 기간 검색의 결과를 일반적으로 처리 하 여 요인을 예측 합니다.
다음 두 단계를 검토 합니다.

### <a name="period-finding"></a>기간 찾기 ###

퀀텀 푸리에 변환 및 단계 예측의 작동 방식에 대해 살펴보았습니다 ( [퀀텀 알고리즘](xref:microsoft.quantum.libraries.standard.algorithms)참조), 이러한 도구를 사용 하 여 *기간 찾기*라는 일반적으로 하드 계산 문제를 해결할 수 있습니다.  다음 섹션에서는 팩터링 하는 기간 찾기를 적용 하는 방법을 알아봅니다.

$ 및 $N $ $a 두 개의 정수를 지정 하는 경우 ($a < N $), order 찾기가 라고도 하는 기간 찾기를 목표로 하는 $r $ of $a $의 _주문_ $N을 찾는 것입니다. 여기서 $r $는 $a ^ r \equiv 1 \text{Mod} N $와 같이 최소 양의 정수로 정의 됩니다.  

퀀텀 컴퓨터를 사용 하 여 순서를 찾으려면 다음의 단일 연산자에 적용 되는 단계 추정 알고리즘을 사용할 수 있습니다. $U _a $: $ $ U_a \ket{x} \equiv \ket{(ax) \text{mod} N}. $ $ 고유 벡터 of $U _a $ 및 $0 \ leq s \text{r-$1 $ $ \ket{x_s} \equiv 1/\sqrt{r} \sum\_{k = 0} ^ {r-1} e ^ {\frac{-2\pi i N o} {r}} \ket{a ^ k\text {mod} N}, $ $는 $U _a $의 _eigenstates_ 입니다.
$U _a $의 고유 값는 $ $ U\_a \ket{x\_s} = e ^ {2 \ pi i s/r} \ket{x\_s}입니다. $$

따라서 단계 예측은 $e ^ {2 \ pi i s/r} $에서 고유 값를 출력 합니다. 여기서 $r $은 $s/r $의 [연속 된 분수](https://en.wikipedia.org/wiki/Continued_fraction) 를 사용 하 여 효율적으로 학습할 수 있습니다.

퀀텀 기간 찾기를 위한 회로 다이어그램은 다음과 같습니다.

![](./../../media/QPE.svg)

여기서 $2n $ \ket는 ${0}$로 초기화 되 고 $n $ 이상 비트는 $ \ket{1}$로 초기화 됩니다.
판독기는 eigenstates를 포함 하는 퀀텀 레지스터가 $ \ket{1}$로 초기화 되는 이유를 궁금할 수 있습니다.
$R $의 순서를 알 수 없으므로 $ \ket{x_s} $ 상태를 직접 준비할 수 없습니다.
다행히 $1/\ sqrt {r} \sum\_{s = 0} ^ {r-1} \ket{x\_s} = \ket{1}$로 전환 합니다.
$ \Ket{x} $!을 (를) 실제로 준비 하지 않아도 됩니다.
$ \Ket{1}$ 상태에서 $n $ 이상 비트의 퀀텀 레지스터를 준비할 수 있습니다. 

회로에는 QFT와 여러 개의 제어 된 게이트가 포함 됩니다.
QFT 게이트가 [이전](xref:microsoft.quantum.libraries.standard.algorithms)에 설명 되어 있습니다.
제어 되는 $U _a $ gate 맵은 $ \ket{x} $를 $ \ket{(ax) \text{mod} N} $로 매핑하고, 컨트롤의가 $ \ket{1}$ 이면 $ \ket{x} $를 $ \ket{x} $에 매핑합니다.

$ (A ^ nx) \text{mod} N $을 얻기 위해 일반적으로 _ {a ^ n} $를 $U 적용 하기만 하면 됩니다. 여기서는 $a ^ n \text{mod} N $를 계산 하 여 퀀텀 회로에 연결 합니다.  
이러한 모듈식 산술 연산을 수행 하기 위한 회로는 [퀀텀 산술 설명서](./algorithms.md#arithmetic)에 설명 되어 있습니다. 특히 제어 되는 $U\_{a ^ i} $ 작업을 구현 하려면 모듈식 지 수 회로가 필요 합니다.

위의 회로는 [퀀텀 단계 예측](xref:microsoft.quantum.characterization.quantumphaseestimation) 에 해당 하 고 주문 찾기를 명시적으로 사용 하도록 설정 하는 반면 필요한 것은 필요한 비트 수를 줄일 수 있습니다. [ArXiv: Beauregard/0205095v3의 8 페이지에](https://arxiv.org/pdf/quant-ph/0205095v3.pdf#page=8)설명 된 대로 주문 찾기에 대해의 방법을 따르거나, Microsoft 양자에서 사용할 수 있는 단계 예측 루틴 중 하나를 사용할 수 있습니다. 예를 들어 [강력한 단계 예측](xref:microsoft.quantum.characterization.robustphaseestimation) 은 또 하나의 추가 비트를 사용 합니다.
 
### <a name="factoring"></a>프로필과 ###
팩터링의 목표는 정수 $N $의 두 소수 요소를 확인 하는 것입니다. 여기서 $N $는 $n $ 비트 숫자입니다.  
팩터링은 아래에 설명 된 단계로 구성 됩니다. 이러한 단계는 클래식 전처리 루틴 (1-4)의 세 부분으로 나뉩니다. $a \text{mod} N $ (5)의 순서를 확인 하는 퀀텀 컴퓨팅 루틴 그리고 일반적인 후 처리 루틴은 순서 (6-9)에서 프라임 요인을 파생 시킵니다.

기존 전처리 루틴은 다음 단계로 구성 됩니다.
1. $N $가 짝수 이면 프라임 비율 $2 $를 반환 합니다.
2. $N = p ^ q $ $p \geq1 $, $q \geq1 $의 경우 소수 $p $를 반환 합니다.  이 단계는 일반적으로 수행 됩니다.
3. $1 < $a < N-$1 인 난수를 선택 합니다.
4. $ \Text{gcd} (a, N) > 1 $ 이면 프라임 요소 $ \text{gcd} (a, N) $를 반환 합니다. 이 단계는 함으로써 유클리드 알고리즘을 사용 하 여 계산 됩니다.
소수 요소가 반환 되지 않은 경우에는 퀀텀 루틴이 진행 됩니다.
5. 퀀텀 기간 찾기 알고리즘을 호출 하 여 $r $ of $a \text{mod} N $의 순서를 계산 합니다. 클래식 후 처리 루틴에서 $r $를 사용 하 여 프라임 요인을 확인 합니다.
6. $R $가 홀수 이면 전처리 단계 (3)로 돌아갑니다.
7. $R $가 짝수이 고 $a ^ {r/2} =-1 \ 텍스트 {mod} N $ 인 경우 전처리 단계 (3)로 돌아갑니다.
8. $ \Text{gcd} (a ^ {r/2} + 1, N) $이 특수 한 인수 $N $ 인 경우 $ \text{gcd} (a ^ {r/2} + 1, N) $를 반환 합니다.
9. $ \Text{gcd} (a ^ {r/2}-1, N) $이 특수 한 인수 $N $ 인 경우 $ \text{gcd} (a ^ {r/2}-1, N) $를 반환 합니다.


팩터링 알고리즘은 확률 수 있습니다. 즉, $ $r $가 짝수이 고 $a ^ {r/2} \neq-1 \neq mod} N $ 인 확률을 사용 하 여 프라임 계수를 생성 하는 것으로 표시 될 수 있습니다.  [자세한 내용은](xref:microsoft.quantum.more-information) [shor의 원래 용지](https://doi.org/10.1109/SFCS.1994.365700) 또는의 *기본 퀀텀 계산* 텍스트 중 하나를 참조 하세요.
소수 요소가 반환 되지 않는 경우에는 (1) 단계에서 알고리즘을 반복 하기만 하면 됩니다.  $ 시도를 $n 후에는 모든 시도가 실패 한 확률은 최대 $2 ^ {-n} $입니다.
따라서 알고리즘을 적은 횟수로 성공 하는 것은 거의 보장 되지 않습니다.
