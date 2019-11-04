---
title: 퀀텀 회로 | Microsoft Docs
description: 퀀텀 회로
author: QuantumWriter
uid: microsoft.quantum.concepts.circuits
ms.author: nawiebe@microsoft.com
ms.date: 12/11/2017
ms.topic: article
ms.openlocfilehash: 7c2afa58fd70d893529cf794ae07df480466aaec
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2019
ms.locfileid: "73210697"
---
# <a name="quantum-circuits"></a><span data-ttu-id="b6bf7-103">퀀텀 회로</span><span class="sxs-lookup"><span data-stu-id="b6bf7-103">Quantum Circuits</span></span>
<span data-ttu-id="b6bf7-104">그 순간에는 단일 변환 $ \text{CNOT} _{01}(H\otimes 1) $를 고려 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-104">Consider for a moment the unitary transformation $\text{ CNOT}_{01}(H\otimes 1)$.</span></span>
<span data-ttu-id="b6bf7-105">이 게이트 시퀀스는 최대 entangled의 2 상 비트 상태를 만들기 때문에 퀀텀 컴퓨팅에 대 한 근본적인 중요 한 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-105">This gate sequence is of fundamental significance to quantum computing because it creates a maximally entangled two-qubit state:</span></span>

<span data-ttu-id="b6bf7-106">$ $ \mathrm{CNOT}_{01}(H\otimes 1) \ket{00} = \frac{1}{\sqrt{2}} \left (\ket{00} + \ket{11} \right), $ $</span><span class="sxs-lookup"><span data-stu-id="b6bf7-106">$$\mathrm{CNOT}_{01}(H\otimes 1)\ket{00} = \frac{1}{\sqrt{2}} \left(\ket{00} + \ket{11} \right),$$</span></span>

<span data-ttu-id="b6bf7-107">이러한 복잡성을 포함 하는 작업은 퀀텀 알고리즘과 퀀텀 오류 수정에서 사용할 수 있으므로 *퀀텀 회로 다이어그램*이라고 하는 시각화에 대 한 간단한 메서드가 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-107">Operations with this or greater complexity are ubiquitous in quantum algorithms and quantum error correction, so it should come as a great relief that there is a simple method for their visualization called a *quantum circuit diagram*.</span></span>
<span data-ttu-id="b6bf7-108">이 최대 entangled 퀀텀 상태를 준비 하기 위한 회로 다이어그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-108">The circuit diagram for preparing this maximally entangled quantum state is:</span></span>

<!--- ![](.\media\1.svg) --->
<!-- Can't find a way to easily center this... probably an extension needed:  -->
![](~/media/Concepts1.png)

## <a name="quantum-circuit-diagram-conventions"></a><span data-ttu-id="b6bf7-109">퀀텀 회로 다이어그램 규칙</span><span class="sxs-lookup"><span data-stu-id="b6bf7-109">Quantum circuit diagram conventions</span></span>
<span data-ttu-id="b6bf7-110">퀀텀 작업의 시각적 언어는 퀀텀 회로를 표현 하는 규칙을 이해 하 고 나면 동등한 행렬을 작성 하는 것 보다 훨씬 더 쉽게 좋게 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-110">This visual language for quantum operations can be more readily digestible than writing down its equivalent matrix once you understand the conventions for expressing a quantum circuit.</span></span>
<span data-ttu-id="b6bf7-111">아래에서 이러한 규칙을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-111">We review these conventions below.</span></span>

<span data-ttu-id="b6bf7-112">회로 다이어그램에서 각 실선은 보다 일반적으로는 이상 비트 레지스터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-112">In a circuit diagram, each solid line depicts a qubit or more generally a qubit register.</span></span>
<span data-ttu-id="b6bf7-113">규칙에 따라 맨 위 줄은 고 비트 레지스터 $0 $ 이며 나머지는 순차적으로 레이블이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-113">By convention, the top line is qubit register $0$ and the remainder are labeled sequentially.</span></span> <span data-ttu-id="b6bf7-114">위의 예제 회로는 두 개의 비트에서 작동 하는 것으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-114">The above example circuit is depicted as acting on two qubits (or equivalently two registers consisting of one qubit).</span></span>
<span data-ttu-id="b6bf7-115">하나 이상의 이상 비트 레지스터에서 동작 하는 게이트가 상자로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-115">Gates acting on one or more qubit registers are denoted as a box.</span></span>
<span data-ttu-id="b6bf7-116">예: 기호</span><span class="sxs-lookup"><span data-stu-id="b6bf7-116">For example, the symbol</span></span>

<!--- ![](.\media\2.svg) --->
<!-- Can't find a way to easily center this... probably an extension needed:  -->
![](~/media/concepts_2.png)

<span data-ttu-id="b6bf7-117">[Hadamard](xref:microsoft.quantum.primitive.h) gate는 단일의 비트 레지스터에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-117">is the [Hadamard](xref:microsoft.quantum.primitive.h) gate acting on a single-qubit register.</span></span>

<span data-ttu-id="b6bf7-118">퀀텀 게이트는 처음에는 관문을 중심으로 가장 왼쪽의 게이트가 있는 시간순으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-118">Quantum gates are ordered in chronological order with the left-most gate as the gate first applied to the qubits.</span></span>
<span data-ttu-id="b6bf7-119">즉, 퀀텀을 퀀텀 상태를 유지 하는 경우 와이어는 다이어그램의 각 게이트를 통해 퀀텀 상태를 왼쪽에서 오른쪽으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-119">In other words, if you picture the wires as holding the quantum state, the wires bring the quantum state through each of the gates in the diagram from left to right.</span></span>
<span data-ttu-id="b6bf7-120">예를 들면</span><span class="sxs-lookup"><span data-stu-id="b6bf7-120">That is to say</span></span> 

<!--- ![](.\media\3.svg) --->
<!-- Can't find a way to easily center this... probably an extension needed:  -->
![](~/media/concepts_3.png)

<span data-ttu-id="b6bf7-121">는 단일 행렬 $CBA $입니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-121">is the unitary matrix $CBA$.</span></span>
<span data-ttu-id="b6bf7-122">행렬 곱셈은 반대 규칙을 따르는 합니다. 가장 오른쪽의 행렬이 먼저 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-122">Matrix multiplication obeys the opposite convention: the right-most matrix is applied first.</span></span> <span data-ttu-id="b6bf7-123">그러나 퀀텀 회로 다이어그램에서 가장 왼쪽의 게이트가 먼저 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-123">In quantum circuit diagrams, however, the left-most gate is applied first.</span></span>
<span data-ttu-id="b6bf7-124">이러한 차이는 때때로 혼란 스 러 울 수 있으므로 선형 대 수 표기법과 퀀텀 회로 다이어그램 간의 상당한 차이를 확인 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-124">This difference can at times lead to confusion, so it is important to note this significant difference between the linear algebraic notation and quantum circuit diagrams.</span></span>

## <a name="inputs-and-outputs-of-quantum-circuits"></a><span data-ttu-id="b6bf7-125">퀀텀 회로의 입/출력</span><span class="sxs-lookup"><span data-stu-id="b6bf7-125">Inputs and outputs of quantum circuits</span></span>
<span data-ttu-id="b6bf7-126">지정 된 앞의 모든 예제에는 퀀텀 게이트의 와이어 수와 동일한 수의 와이어 (는)를 퀀텀 게이트에 정확 하 게 입력 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-126">All previous examples given have had precisely the same number of wires (qubits) input to a quantum gate as the number of wires out from the quantum gate.</span></span>
<span data-ttu-id="b6bf7-127">처음에는 퀀텀 회로가 일반적으로 입력 하는 것 보다 더 많거나 적을 수 있다는 것이 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-127">It may at first seem reasonable that quantum circuits could have more, or fewer, outputs than inputs in general.</span></span>
<span data-ttu-id="b6bf7-128">그러나 모든 퀀텀 작업을 저장 하는 것은 단일 작업 이므로 해독 가능 하기 때문에 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-128">This is impossible, however, because all quantum operations, save measurement, are unitary and hence reversible.</span></span>
<span data-ttu-id="b6bf7-129">입력과 동일한 수의 출력을 포함 하지 않은 경우에는 해독 하지 않고 일치 하지 않는 단일 사용자가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-129">If they did not have the same number of outputs as inputs they would not be reversible and hence not unitary, which is a contradiction.</span></span>
<span data-ttu-id="b6bf7-130">이러한 이유로 회로 다이어그램에 그려진 상자는 종료 하는 것과 정확히 동일한 수의 와이어로 입력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-130">For this reason any box drawn in a circuit diagram must have precisely the same number of wires entering it as exiting it.</span></span>

<span data-ttu-id="b6bf7-131">다중 기능 비트 회로 다이어그램은 유사한 규칙에 따라 단일 비트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-131">Multi-qubit circuit diagrams follow similar conventions to single-qubit ones.</span></span>
<span data-ttu-id="b6bf7-132">명확 하 게 예를 들면 $ (H somtimes X) $ to $ (H ssttimes X) $로 두 개의 ubit 단일 $B 작업을 정의 하 고 회로를 같은 것으로 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-132">As a clarifying example, we can define a two-qubit unitary operation $B$ to be $(H S\otimes X)$ and express the circuit equivalently as</span></span>

<!--- ![](.\media\4.svg) --->
<!-- Can't find a way to easily center this... probably an extension needed:  -->
![](~/media/concepts_4.png)

<span data-ttu-id="b6bf7-133">회로를 사용 하는 컨텍스트에 따라 2 1-가 비트 레지스터가 아닌 단일 2-가 비트 레지스터에서 작업을 수행 하는 것으로 $B $를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-133">We can also view $B$ as having an action on a single two-qubit register rather than two one-qubit registers depending on the context in which the circuit is used.</span></span> <span data-ttu-id="b6bf7-134">이러한 추상 회로 다이어그램의 가장 유용한 속성은 기본 게이트로 컴파일하지 않고도 복잡 한 퀀텀 알고리즘을 높은 수준으로 설명할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-134">Perhaps the most useful property of such abstract circuit diagrams is that they allow complicated quantum algorithms to be described at a high level without having to compile them down to fundamental gates.</span></span>
<span data-ttu-id="b6bf7-135">즉, 알고리즘 내의 각 서브루틴이 작동 하는 방식에 대 한 모든 세부 정보를 이해 하지 않고도 대량 퀀텀 알고리즘에 대 한 데이터 흐름에 대 한 intuition를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-135">This means that you can get an intuition about the data flow for a large quantum algorithm without needing to understand all the details of how each of the subroutines within the algorithm work.</span></span>

## <a name="controlled-gates"></a><span data-ttu-id="b6bf7-136">제어 된 게이트</span><span class="sxs-lookup"><span data-stu-id="b6bf7-136">Controlled gates</span></span>
<span data-ttu-id="b6bf7-137">Multi-factor bit 퀀텀 회로 다이어그램에 기본 제공 되는 다른 구문은 제어입니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-137">The other construct that is built into multi-qubit quantum circuit diagrams is control.</span></span>
<span data-ttu-id="b6bf7-138">$ \Lambda (G) $ $G로 표시 되는 퀀텀 단일 제어 되는 게이트의 작업은 제품 상태 입력 $ \Lambda (G) (\lambda \ket{0} + \lambda \ket의 다음 예제를 확인 하 여이를 이해할 수 있습니다{1}) \ket{\psi} = \alpha \ket{0} \ket{\psi} + \alpha \ket{1} G\ket {\ psi} $.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-138">The action of a quantum singly controlled gate, denoted $\Lambda(G)$, where a single qubit's value controls the application of $G$, can be understood by looking at the following example of a product state input $\Lambda(G) (\alpha \ket{0} + \beta \ket{1}) \ket{\psi} = \alpha \ket{0} \ket{\psi} + \beta \ket{1} G\ket{\psi}$.</span></span>
<span data-ttu-id="b6bf7-139">즉, 제어 되는 게이트는 $ \psi $를 포함 하는 레지스터에 $G $을 적용 합니다 .이 경우 컨트롤의 값이 $1 $ 인 경우에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-139">That is to say, the controlled gate applies $G$ to the register containing $\psi$ if and only if the control qubit takes the value $1$.</span></span>
<span data-ttu-id="b6bf7-140">일반적으로 회로 다이어그램에서 이와 같이 제어 되는 작업을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-140">In general, we describe such controlled operations in circuit diagrams as</span></span>

<!--- ![](.\media\5.svg) --->
<!-- Can't find a way to easily center this... probably an extension needed:  -->
![](~/media/concepts_5.png)

<span data-ttu-id="b6bf7-141">여기서 검정 원은 게이트가 제어 되는 퀀텀 비트를 나타내며, 세로는 컨트롤의 값이 $1 $ 인 경우 적용 되는 단일를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-141">Here the black circle denotes the quantum bit on which the gate is controlled and a vertical wire denotes the unitary that is applied when the control qubit takes the value $1$.</span></span>
<span data-ttu-id="b6bf7-142">$G = X $ 및 $G = Z $와 같은 특수 한 경우에는 제어 되는 게이트 버전을 설명 하는 다음과 같은 표기법이 제공 됩니다 (제어 된 X 게이트는 [$CNOT $ gate](xref:microsoft.quantum.primitive.cnot)임을 유의).</span><span class="sxs-lookup"><span data-stu-id="b6bf7-142">For the special cases where $G=X$ and $G=Z$ we introduce the following notation to describe the controlled version of the gates (note that the controlled-X gate is the [$CNOT$ gate](xref:microsoft.quantum.primitive.cnot)):</span></span>

<!--- ![](.\media\6.svg) --->
<!-- Can't find a way to easily center this... probably an extension needed:  -->
![](~/media/concepts_6.png)

<span data-ttu-id="b6bf7-143">Q #은 작업의 제어 된 버전을 자동으로 생성 하는 메서드를 제공 합니다. 그러면 프로그래머가 이러한 작업을 직접 코딩할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-143">Q# provides methods to automatically generate the controlled version of an operation, which saves the programmer from having to hand code these operations.</span></span> <span data-ttu-id="b6bf7-144">이에 대 한 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-144">An example of this is shown below:</span></span>

```qsharp
operation PrepareSuperposition(qubit : Qubit) : Unit
is Ctl { // Auto-generate the controlled specialization of the operation
    H(qubit);
}
```

## <a name="measurement-operator"></a><span data-ttu-id="b6bf7-145">측정 연산자</span><span class="sxs-lookup"><span data-stu-id="b6bf7-145">Measurement operator</span></span>
<span data-ttu-id="b6bf7-146">회로 다이어그램에서 시각화 하는 나머지 작업은 측정입니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-146">The remaining operation to visualize in circuit diagrams is measurement.</span></span>
<span data-ttu-id="b6bf7-147">측정은 더 많은 비트 레지스터를 사용 하 여 측정 하 고 결과를 기존 정보로 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-147">Measurement takes a qubit register, measures it, and outputs the result as classical information.</span></span>
<span data-ttu-id="b6bf7-148">측정 연산은 미터 기호로 표시 되 고 항상 (실선으로 표시 됨)에 대 한 입력으로 사용 되며, 이중 줄로 표시 되는 고전적인 정보를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-148">A measurement operation is denoted by a meter symbol and always takes as input a qubit register (denoted by a solid line) and outputs classical information (denoted by a double line).</span></span>
<span data-ttu-id="b6bf7-149">특히 이러한 subcircuit는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-149">Specifically, such a subcircuit looks like:</span></span>

<!--- ![](.\media\7.svg) ---->
<!-- Can't find a way to easily center this... probably an extension needed:  -->
<span data-ttu-id="b6bf7-150">![측정 회로](~/media/concepts_7.png)</span><span class="sxs-lookup"><span data-stu-id="b6bf7-150">![Measurement circuit](~/media/concepts_7.png)</span></span>

<span data-ttu-id="b6bf7-151">Q #에서는이 목적을 위해 [측정값 연산자](xref:microsoft.quantum.primitive.measure) 를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-151">Q# implements a [Measure operator](xref:microsoft.quantum.primitive.measure) for this purpose.</span></span>
<span data-ttu-id="b6bf7-152">자세한 내용은 [측정에](xref:microsoft.quantum.libraries.standard.prelude#measurements) 대 한 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-152">See the [section on measurements](xref:microsoft.quantum.libraries.standard.prelude#measurements) for more information.</span></span>

<span data-ttu-id="b6bf7-153">마찬가지로 subcircuit</span><span class="sxs-lookup"><span data-stu-id="b6bf7-153">Similarly, the subcircuit</span></span>

<!--- ![](.\media\8.svg) --->
<!-- Can't find a way to easily center this... probably an extension needed:  -->
![](~/media/concepts_8.png)

<span data-ttu-id="b6bf7-154">일반적으로 제어 되는 게이트를 제공 합니다. 여기서 $G $은 클래식 컨트롤 비트에 조건 화 된 $1 $ 값이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-154">gives a classically controlled gate, where $G$ is applied conditioned on the classical control bit being value $1$.</span></span>

## <a name="teleportation-circuit-diagram"></a><span data-ttu-id="b6bf7-155">Teleportation 회로 다이어그램</span><span class="sxs-lookup"><span data-stu-id="b6bf7-155">Teleportation circuit diagram</span></span>
<span data-ttu-id="b6bf7-156">[퀀텀 teleportation](xref:microsoft.quantum.techniques.puttingittogether) 는 이러한 구성 요소를 보여 주는 최상의 퀀텀 알고리즘이 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-156">[Quantum teleportation](xref:microsoft.quantum.techniques.puttingittogether) is perhaps the best quantum algorithm for illustrating these components.</span></span>
<span data-ttu-id="b6bf7-157">퀀텀 teleportation는 되거나 얽 히 및 측정을 사용 하 여 퀀텀 컴퓨터 (또는 퀀텀 네트워크의 먼 퀀텀 컴퓨터 사이) 내에서 데이터를 이동 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-157">Quantum teleportation is a method for moving data within a quantum computer (or even between distant quantum computers in a quantum network) through the use of entanglement and measurement.</span></span>
<span data-ttu-id="b6bf7-158">흥미롭게도, 실제 값을 알고 있는 것이 아니라, 지정 된의 값을 한 가지 이상에서 다른 값으로 이동 하는 것은 사실입니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-158">Interestingly, it is actually capable of moving a quantum state, say the value in a given qubit, from one qubit to another, without even knowing what the qubit's value is!</span></span>
<span data-ttu-id="b6bf7-159">이는 프로토콜이 퀀텀 메커니즘의 법에 따라 작동 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-159">This is necessary for the protocol to work according to the laws of quantum mechanics.</span></span>
<span data-ttu-id="b6bf7-160">퀀텀 teleportation 회로는 아래에 제공 됩니다. 또한 퀀텀 회로를 읽는 방법을 보여 주기 위해 주석이 추가 된 회로 버전을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6bf7-160">The quantum teleportation circuit is given below; we also provide an annotated version of the circuit to illustrate how to read the quantum circuit.</span></span>

<!--- ![](.\media\tp2.svg){ width=50% } --->
![](~/media/concepts_tp2.png)