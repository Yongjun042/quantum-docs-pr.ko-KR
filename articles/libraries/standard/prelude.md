---
title: 'Q # 표준 라이브러리-prelude | Microsoft Docs'
description: 'Q # 표준 라이브러리-prelude'
author: QuantumWriter
uid: microsoft.quantum.libraries.standard.prelude
ms.author: martinro@microsoft.com
ms.date: 12/11/2017
ms.topic: article
ms.openlocfilehash: dddb3d4a5ebcdca16da41a5ae5520d98ea900a7f
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73183236"
---
# <a name="the-prelude"></a><span data-ttu-id="b9f21-103">Prelude</span><span class="sxs-lookup"><span data-stu-id="b9f21-103">The Prelude</span></span> #

<span data-ttu-id="b9f21-104">Q # 컴파일러 및 퀀텀 개발 키트에 포함 된 대상 컴퓨터는 Q #에서 퀀텀 프로그램을 작성할 때 사용할 수 있는 내장 함수 및 작업 집합을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-104">The Q# compiler and the target machines included with the Quantum Development Kit provide a set of intrinsic functions and operations that can be used when writing quantum programs in Q#.</span></span>

## <a name="intrinsic-operations-and-functions"></a><span data-ttu-id="b9f21-105">내장 작업 및 함수</span><span class="sxs-lookup"><span data-stu-id="b9f21-105">Intrinsic Operations and Functions</span></span> ##

<span data-ttu-id="b9f21-106">표준 라이브러리에 정의 된 기본 작업은 다음과 같은 몇 가지 범주 중 하나에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-106">The intrinsic operations defined in the standard library roughly fall into one of several categories:</span></span>

- <span data-ttu-id="b9f21-107"><xref:microsoft.quantum.core> 네임 스페이스에 수집 된 필수 클래식 함수</span><span class="sxs-lookup"><span data-stu-id="b9f21-107">Essential classical functions, collected in the <xref:microsoft.quantum.core> namespace.</span></span>
- <span data-ttu-id="b9f21-108">[Clifford 및 $T $ 게이트](xref:microsoft.quantum.concepts.qubit)로 구성 된 unitaries를 나타내는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-108">Operations representing unitaries composed of [Clifford and $T$ gates](xref:microsoft.quantum.concepts.qubit).</span></span>
- <span data-ttu-id="b9f21-109">다양 한 연산자에 대 한 회전을 나타내는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-109">Operations representing rotations about various operators.</span></span>
- <span data-ttu-id="b9f21-110">측정을 구현 하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-110">Operations implementing measurements.</span></span>

<span data-ttu-id="b9f21-111">Clifford + $T $ gate 집합은 퀀텀 컴퓨팅을 위한 [유니버설](xref:microsoft.quantum.concepts.multiple-qubits) 이므로 negligibly 작은 오류 내에서 임의 퀀텀 알고리즘을 구현 하는 데에는 충분 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-111">Since the Clifford + $T$ gate set is [universal](xref:microsoft.quantum.concepts.multiple-qubits) for quantum computing, these operations suffice to approximately implement any quantum algorithm within negligibly small error.</span></span>
<span data-ttu-id="b9f21-112">Q #은 회전도 제공 하 여 프로그래머는 단일의 단일 기능 및 CNOT gate 라이브러리 내에서 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-112">By providing rotations as well, Q# allows the programmer to work within the single qubit unitary and CNOT gate library.</span></span> <span data-ttu-id="b9f21-113">이 라이브러리는 프로그래머가 Clifford + $T $ 분해를 직접 표현할 필요가 없으며, 단일 highbit unitaries를 Clifford 및 $T $ 게이트로 컴파일하기 위한 매우 효율적인 메서드가 필요 하지 않기 때문에 훨씬 더 쉽습니다. ( [여기](xref:microsoft.quantum.more-information) 참조 추가 정보).</span><span class="sxs-lookup"><span data-stu-id="b9f21-113">This library is much easier to think about because it does not  require the programmer to directly express the Clifford + $T$ decomposition and because highly efficient methods exist for compiling single qubit unitaries into Clifford and $T$ gates (see [here](xref:microsoft.quantum.more-information) for more information).</span></span>

<span data-ttu-id="b9f21-114">가능 하면, prelude에서 정의 된 작업을 수행 하 여 대상 컴퓨터에서 적절 한 분해를 수행 하는 등의 작업을 수행할 `Controlled` 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-114">Where possible, the operations defined in the prelude which act on qubits allow for applying the `Controlled` variant, such that the target machine will perform the appropriate decomposition.</span></span>

<span data-ttu-id="b9f21-115">Prelude의이 부분에 정의 된 대부분의 함수 및 작업은 @"microsoft.quantum.intrinsic" 네임 스페이스에 있습니다. 즉, 대부분의 Q # 소스 파일은 초기 네임 스페이스 선언 바로 뒤에 `open Microsoft.Quantum.Intrinsic;` 지시문을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-115">Many of the functions and operations defined in this portion of the prelude are in the @"microsoft.quantum.intrinsic" namespace, such that most Q# source files will have an `open Microsoft.Quantum.Intrinsic;` directive immediately following the initial namespace declaration.</span></span>
<span data-ttu-id="b9f21-116"><xref:microsoft.quantum.core> 네임 스페이스는 자동으로 열리므로 <xref:microsoft.quantum.core.length>와 같은 함수를 `open` 문 없이 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-116">The <xref:microsoft.quantum.core> namespace is automatically opened, so that functions such as <xref:microsoft.quantum.core.length> can be used without an `open` statement at all.</span></span>

### <a name="common-single-qubit-unitary-operations"></a><span data-ttu-id="b9f21-117">일반적인 단일 기능 비트 단일 작업</span><span class="sxs-lookup"><span data-stu-id="b9f21-117">Common Single-Qubit Unitary Operations</span></span> ###

<span data-ttu-id="b9f21-118">또한 prelude는 여러 일반적인 [단일 기능 비트 작업](xref:microsoft.quantum.concepts.qubit#single-qubit-operations)을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-118">The prelude also defines many common [single-qubit operations](xref:microsoft.quantum.concepts.qubit#single-qubit-operations).</span></span>
<span data-ttu-id="b9f21-119">이러한 모든 작업은 `Controlled` 및 `Adjoint` 함수를 모두 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-119">All of these operations allow both the `Controlled` and `Adjoint` functors.</span></span>

#### <a name="pauli-operators"></a><span data-ttu-id="b9f21-120">Pauli 연산자</span><span class="sxs-lookup"><span data-stu-id="b9f21-120">Pauli Operators</span></span> ####

<span data-ttu-id="b9f21-121"><xref:microsoft.quantum.intrinsic.x> 작업은 Pauli $X $ 연산자를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-121">The <xref:microsoft.quantum.intrinsic.x> operation implements the Pauli $X$ operator.</span></span>
<span data-ttu-id="b9f21-122">이를 `NOT` 게이트 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-122">This is sometimes also known as the `NOT` gate.</span></span>
<span data-ttu-id="b9f21-123">`(Qubit => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-123">It has signature `(Qubit => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-124">단일 기능에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-124">It corresponds to the single-qubit unitary:</span></span>

<span data-ttu-id="b9f21-125">\begin{equation} \begin{bmatrix} 0 & 1 \\\\% FIXME: 현재는 quadwhack hack를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-125">\begin{equation} \begin{bmatrix} 0 & 1 \\\\ % FIXME: this currently uses the quadwhack hack.</span></span>
<span data-ttu-id="b9f21-126">1 & 0 \end{bmatrix} \end{ation}</span><span class="sxs-lookup"><span data-stu-id="b9f21-126">1 & 0 \end{bmatrix} \end{equation}</span></span>

<span data-ttu-id="b9f21-127"><xref:microsoft.quantum.intrinsic.y> 작업은 Pauli $Y $ 연산자를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-127">The <xref:microsoft.quantum.intrinsic.y> operation implements the Pauli $Y$ operator.</span></span>
<span data-ttu-id="b9f21-128">`(Qubit => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-128">It has signature `(Qubit => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-129">단일 기능에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-129">It corresponds to the single-qubit unitary:</span></span>

<span data-ttu-id="b9f21-130">\begin{equation} \begin{bmatrix} 0 &-i \\\\% FIXME: 현재는 quadwhack hack를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-130">\begin{equation} \begin{bmatrix} 0 & -i \\\\ % FIXME: this currently uses the quadwhack hack.</span></span>
<span data-ttu-id="b9f21-131">i & 0 \end{bmatrix} \end{ation}</span><span class="sxs-lookup"><span data-stu-id="b9f21-131">i & 0 \end{bmatrix} \end{equation}</span></span>

<span data-ttu-id="b9f21-132"><xref:microsoft.quantum.intrinsic.z> 작업은 Pauli $Z $ 연산자를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-132">The <xref:microsoft.quantum.intrinsic.z> operation implements the Pauli $Z$ operator.</span></span>
<span data-ttu-id="b9f21-133">`(Qubit => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-133">It has signature `(Qubit => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-134">단일 기능에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-134">It corresponds to the single-qubit unitary:</span></span>

<span data-ttu-id="b9f21-135">\begin{equation} \begin{bmatrix} 1 & 0 \\\\% FIXME: 현재는 quadwhack hack를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-135">\begin{equation} \begin{bmatrix} 1 & 0 \\\\ % FIXME: this currently uses the quadwhack hack.</span></span>
<span data-ttu-id="b9f21-136">0 &-1 \end{bmatrix} \end{ation}</span><span class="sxs-lookup"><span data-stu-id="b9f21-136">0 & -1 \end{bmatrix} \end{equation}</span></span>

<span data-ttu-id="b9f21-137">아래에는 [Bloch 구에](xref:microsoft.quantum.concepts.qubit#visualizing-qubits-and-transformations-using-the-bloch-sphere) 매핑되는 이러한 변환이 표시 됩니다 (각 사례의 회전 축은 빨간색으로 강조 표시 됨).</span><span class="sxs-lookup"><span data-stu-id="b9f21-137">Below we see these transformations mapped to the [Bloch sphere](xref:microsoft.quantum.concepts.qubit#visualizing-qubits-and-transformations-using-the-bloch-sphere) (the rotation axis in each case is highlighted red):</span></span>

![Bloch 구에 매핑된 pauli 작업](~/media/prelude_pauliBloch.png)

<span data-ttu-id="b9f21-139">동일한 이상 비트에 동일한 Pauli 게이트를 두 번 적용 하면 작업을 취소 합니다. 이제 Bloch 구에 대 한 2π (360 °)의 전체 회전을 수행 했으므로 시작 지점에서 다시 도착 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-139">It is important to note that applying the same Pauli gate twice to the same qubit cancels out the operation (because you have now performed a full rotation of 2π (360°) over the surface to the Bloch Sphere, thus arriving back at the starting point).</span></span> <span data-ttu-id="b9f21-140">그러면 다음 id가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-140">This brings us to the following identity:</span></span>

<span data-ttu-id="b9f21-141">$ $ X ^ 2 = Y ^ 2 = Z ^ 2 = \boldone $ $</span><span class="sxs-lookup"><span data-stu-id="b9f21-141">$$ X^2=Y^2=Z^2=\boldone $$</span></span>

<span data-ttu-id="b9f21-142">Bloch 구에 visualised 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-142">This can be visualised on the Bloch sphere:</span></span>

![XX = I](~/media/prelude_blochIdentity.png)

#### <a name="other-single-qubit-cliffords"></a><span data-ttu-id="b9f21-144">다른 단일 수준 비트 Cliffords</span><span class="sxs-lookup"><span data-stu-id="b9f21-144">Other Single-Qubit Cliffords</span></span> ####

<span data-ttu-id="b9f21-145"><xref:microsoft.quantum.intrinsic.h> 작업은 Hadamard gate를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-145">The <xref:microsoft.quantum.intrinsic.h> operation implements the Hadamard gate.</span></span>
<span data-ttu-id="b9f21-146">이는 \ket{0} = \ket{+} \mathrel{: =} (\ket{0} + \ket{1})/\sqrt{2}$ 및 $H \ket{+} = \ket{0}$와 $H 같은 대상의 Pauli $X $ 및 $Z $ 축을 교환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-146">This interchanges the Pauli $X$ and $Z$ axes of the target qubit, such that $H\ket{0} = \ket{+} \mathrel{:=} (\ket{0} + \ket{1}) / \sqrt{2}$ and $H\ket{+} = \ket{0}$.</span></span>
<span data-ttu-id="b9f21-147">이 파일에는 `(Qubit => Unit is Adj + Ctl)`시그니처와 해당 하는 단일 고 비트에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-147">It has signature `(Qubit => Unit is Adj + Ctl)`, and corresponds to the single-qubit unitary:</span></span>

<span data-ttu-id="b9f21-148">\begin{equation} \frac{1}{\sqrt{2}} \begin{bmatrix} 1 & 1 \\\\% FIXME: 현재 quadwhack 해킹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-148">\begin{equation} \frac{1}{\sqrt{2}} \begin{bmatrix} 1 & 1 \\\\ % FIXME: this currently uses the quadwhack hack.</span></span>
<span data-ttu-id="b9f21-149">1 &-1 \end{bmatrix} \end{ation}</span><span class="sxs-lookup"><span data-stu-id="b9f21-149">1 & -1 \end{bmatrix} \end{equation}</span></span>

<span data-ttu-id="b9f21-150">Hadamard gate는 $ \ket{0}$ 및 $ \ket{1}$ states의 superposition를 만드는 데 사용할 수 있으므로 특히 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-150">The Hadamard gate is particularly important as it can be used to create a superposition of the $\ket{0}$ and $\ket{1}$ states.</span></span> <span data-ttu-id="b9f21-151">Bloch 구의 표현은 $ \pi $ radians ($ 180 ^ \pi $)에 의해 x 축 주위에 $ \ket{\psi} $를 회전 하 고, $ \ pi/2 $ radians ($ 90 ^ \pi $)로 y 축을 중심으로 (시계 방향) 회전으로 생각 하는 것이 가장 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-151">In the Bloch sphere representation, it is easiest to think of this as a rotation of $\ket{\psi}$ around the x-axis by $\pi$ radians ($180^\circ$) followed by a (clockwise) rotation around the y-axis by $\pi/2$ radians ($90^\circ$):</span></span>

![Bloch 구에 매핑된 Hadamard 작업](~/media/prelude_hadamardBloch.png)

<span data-ttu-id="b9f21-153"><xref:microsoft.quantum.intrinsic.s> 작업은 단계 게이트 $S $을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-153">The <xref:microsoft.quantum.intrinsic.s> operation implements the phase gate $S$.</span></span>
<span data-ttu-id="b9f21-154">이는 Pauli $Z $ operation의 매트릭스 제곱근입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-154">This is the matrix square root of the Pauli $Z$ operation.</span></span>
<span data-ttu-id="b9f21-155">즉, $S ^ 2 = Z $입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-155">That is, $S^2 = Z$.</span></span>
<span data-ttu-id="b9f21-156">이 파일에는 `(Qubit => Unit is Adj + Ctl)`시그니처와 해당 하는 단일 고 비트에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-156">It has signature `(Qubit => Unit is Adj + Ctl)`, and corresponds to the single-qubit unitary:</span></span>

<span data-ttu-id="b9f21-157">\begin{equation} \begin{bmatrix} 1 & 0 \\\\% FIXME: 현재는 quadwhack hack를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-157">\begin{equation} \begin{bmatrix} 1 & 0 \\\\ % FIXME: this currently uses the quadwhack hack.</span></span>
<span data-ttu-id="b9f21-158">0 & i \end{bmatrix} \end{ation}</span><span class="sxs-lookup"><span data-stu-id="b9f21-158">0 & i \end{bmatrix} \end{equation}</span></span>

#### <a name="rotations"></a><span data-ttu-id="b9f21-159">회전</span><span class="sxs-lookup"><span data-stu-id="b9f21-159">Rotations</span></span> ####

<span data-ttu-id="b9f21-160">위의 Pauli 및 Clifford 작업 외에도 Q # prelude는 회전을 표현 하는 다양 한 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-160">In addition to the Pauli and Clifford operations above, the Q# prelude provides a variety of ways of expressing rotations.</span></span>
<span data-ttu-id="b9f21-161">[단일 기능 비트 작업](xref:microsoft.quantum.concepts.qubit#single-qubit-operations)에 설명 된 대로,이를 회전 하는 기능은 퀀텀 알고리즘에 매우 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-161">As described in [single-qubit operations](xref:microsoft.quantum.concepts.qubit#single-qubit-operations), the ability to rotate is critical to quantum algorithms.</span></span>

<span data-ttu-id="b9f21-162">먼저 $H $ 및 $T $ 게이트를 사용 하 여 단일 기능 비트 작업을 표현할 수 있습니다. 여기서 $H $은 Hadamard 연산이 고, 여기서 \begin{equation} T \mathrel{: =} \begin{bmatrix} 1 & 0 \\\\% FIXME: 현재는 쿼드 back을 사용 합니다. whack hack.</span><span class="sxs-lookup"><span data-stu-id="b9f21-162">We start by recalling that we can express any single-qubit operation using the $H$ and $T$ gates, where $H$ is the Hadamard operation, and where \begin{equation} T \mathrel{:=} \begin{bmatrix} 1 & 0 \\\\ % FIXME: this currently uses the quad back whack hack.</span></span>
<span data-ttu-id="b9f21-163">0 & e ^ {i \pi/4} \end{bmatrix} \end{cation}이는 $T ^ 2 = S $와 같이 <xref:microsoft.quantum.intrinsic.s> 작업의 제곱근입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-163">0 & e^{i \pi / 4} \end{bmatrix} \end{equation} This is the square root of the <xref:microsoft.quantum.intrinsic.s> operation, such that $T^2 = S$.</span></span>
<span data-ttu-id="b9f21-164">$T $ gate는 <xref:microsoft.quantum.intrinsic.t> 작업에 의해 구현 되 고, `(Qubit => Unit is Adj + Ctl)`시그니처를 포함 하 여 단일의 단일 작업 임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-164">The $T$ gate is in turn implemented by the <xref:microsoft.quantum.intrinsic.t> operation, and has signature `(Qubit => Unit is Adj + Ctl)`, indicating that it is a unitary operation on a single-qubit.</span></span>

<span data-ttu-id="b9f21-165">이 경우 임의의 단일 기능 비트 작업을 설명 하는 데에는 충분 하지만, prelude에는 다양 한 방법이 포함 되어 있기 때문에 다른 대상 컴퓨터에서 Pauli 연산자에 대 한 회전을 보다 효율적으로 표현할 수 있습니다. 이러한 회전을 표현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-165">Even though this is in principle sufficient to describe any arbitrary single-qubit operation, different target machines may have more efficient representations for rotations about Pauli operators, such that the prelude includes a variety of ways to convienently express such rotations.</span></span>
<span data-ttu-id="b9f21-166">이러한 작업의 가장 기본적인 <xref:microsoft.quantum.intrinsic.r> 작업입니다. 지정 된 Pauli 축을 중심으로 하는 회전을 구현 하는 것입니다. \begin{equation} R (\시그마, \\as) \mathrel{: =} \exp (-i \\a\aa\시그마/2), \begin{equation} 여기서 $ \b\시그마 $은 \exp $는 행렬 지 수를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-166">The most basic of these is the <xref:microsoft.quantum.intrinsic.r> operation, which implements a rotation around a specified Pauli axis, \begin{equation} R(\sigma, \phi) \mathrel{:=} \exp(-i \phi \sigma / 2), \end{equation} where $\sigma$ is a Pauli operator, $\phi$ is an angle, and where $\exp$ represents the matrix exponential.</span></span>
<span data-ttu-id="b9f21-167">이 클래스에는 서명 `((Pauli, Double, Qubit) => Unit is Adj + Ctl)`있습니다. 여기서 입력의 처음 두 부분은 n\시그마 $ 및 $ \\\\\\\\\\\\a>를 $R 지정 하는 데 필요한 기존 인수인 $ \sigma $ 및 $ \\? $를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-167">It has signature `((Pauli, Double, Qubit) => Unit is Adj + Ctl)`, where the first two parts of the input represent the classical arguments $\sigma$ and $\phi$ needed to specify the unitary operator $R(\sigma, \phi)$.</span></span>
<span data-ttu-id="b9f21-168">$ \Sigma $ 및 $ \\s$를 부분적으로 적용 하 여 해당 형식이 단일의 단일 비트를 포함 하는 작업을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-168">We can partially apply $\sigma$ and $\phi$ to obtain an operation whose type is that of a single-qubit unitary.</span></span>
<span data-ttu-id="b9f21-169">예를 들어 `R(PauliZ, PI() / 4, _)`에는 `(Qubit => Unit is Adj + Ctl)`형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-169">For example, `R(PauliZ, PI() / 4, _)` has type `(Qubit => Unit is Adj + Ctl)`.</span></span>

> [!NOTE]
> <span data-ttu-id="b9f21-170"><xref:microsoft.quantum.intrinsic.r> 연산은 입력 각도를 2로 나누고-1을 곱합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-170">The <xref:microsoft.quantum.intrinsic.r> operation divides the input angle by 2 and multiplies it by -1.</span></span>
> <span data-ttu-id="b9f21-171">$Z $ 회전의 경우 $ \ket{0}$ eigenstate가 $-\\a/$2에 의해 회전 되 고 $ \ket{1}$ eigenstate가 $ \\a/$2에 의해 회전 되며 $ \ket{0}$ eigenstate에 상대적인 $ \\an$에서 $ \ket{1}$ eigenstate가 회전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-171">For $Z$ rotations, this means that the $\ket{0}$ eigenstate is rotated by $-\phi / 2$ and the $\ket{1}$ eigenstate is rotated by $\phi / 2$, so that the $\ket{1}$ eigenstate is rotated by $\phi$ relative to the $\ket{0}$ eigenstate.</span></span>
>
> <span data-ttu-id="b9f21-172">특히 `T`와 `R(PauliZ, PI() / 8, _)`는 관련이 없는 [전역 단계](xref:microsoft.quantum.glossary#global-phase)에 의해서만 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-172">In particular, this means that `T` and `R(PauliZ, PI() / 8, _)` differ only by an irrelevant [global phase](xref:microsoft.quantum.glossary#global-phase).</span></span>
> <span data-ttu-id="b9f21-173">따라서 $ \frac{\pi}{8}$-gate 라고도 하는 $T $를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-173">For this reason, $T$ is sometimes known as the $\frac{\pi}{8}$-gate.</span></span>
>
> <span data-ttu-id="b9f21-174">또한 `PauliI`을 순환 하는 것은 $ \\a/$2의 글로벌 단계를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-174">Note also that rotating around `PauliI` simply applies a global phase of $\phi / 2$.</span></span> <span data-ttu-id="b9f21-175">이러한 단계는 [개념 문서](xref:microsoft.quantum.concepts.qubit)에서 주장해와는 관련이 없지만 제어 되는 `PauliI` 회전과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-175">While such phases are irrelevant, as argued in [the conceptual documents](xref:microsoft.quantum.concepts.qubit), they are relevant for controlled `PauliI` rotations.</span></span>

<span data-ttu-id="b9f21-176">퀀텀 알고리즘 내에서 dyadic로 회전을 표현 하는 것이 유용한 경우가 종종 있습니다. 예를 들어 \mathbb{Z} $ 및 $n \bin \mathbb{N} $의 일부 $k \phi = \phi k/2 ^ n $입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-176">Within quantum algorithms, it is often useful to express rotations as dyadic fractions, such that $\phi = \pi k / 2^n$ for some $k \in \mathbb{Z}$ and $n \in \mathbb{N}$.</span></span>
<span data-ttu-id="b9f21-177"><xref:microsoft.quantum.intrinsic.rfrac> 연산은이 규칙을 사용 하 여 지정 된 Pauli 축을 중심으로 회전을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-177">The <xref:microsoft.quantum.intrinsic.rfrac> operation implements a rotation around a specified Pauli axis using this convention.</span></span>
<span data-ttu-id="b9f21-178">회전 각도가 dyadic 분수로 해석 된 `Int`형식의 두 입력으로 지정 된다는 점에서 <xref:microsoft.quantum.intrinsic.r>와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-178">It differs from <xref:microsoft.quantum.intrinsic.r> in that the rotation angle is specified as two inputs of type `Int`, interpreted as a dyadic fraction.</span></span>
<span data-ttu-id="b9f21-179">따라서 `RFrac`에는 `((Pauli, Int, Int, Qubit) => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-179">Thus, `RFrac` has signature `((Pauli, Int, Int, Qubit) => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-180">단일 기능을 구현 합니다. 여기서 $ \b\시그마 $는 첫 번째 인수에 해당 하는 Pauli 매트릭스이 고 $k $은 두 번째 인수 이며 $n $는 세 번째 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-180">It implements the single-qubit unitary $\exp(i \pi k \sigma / 2^n)$, where $\sigma$ is the Pauli matrix corresponding to the first argument, $k$ is the second argument, and $n$ is the third argument.</span></span>
<span data-ttu-id="b9f21-181">`RFrac(_,k,n,_)`은 `R(_,-πk/2^n,_)`와 동일 합니다. 각도는 분수의 *음수* 입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-181">`RFrac(_,k,n,_)` is the same as `R(_,-πk/2^n,_)`; note that the angle is the *negative* of the fraction.</span></span>

<span data-ttu-id="b9f21-182"><xref:microsoft.quantum.intrinsic.rx> 연산은 Pauli $X $ axis를 중심으로 회전을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-182">The <xref:microsoft.quantum.intrinsic.rx> operation implements a rotation around the Pauli $X$ axis.</span></span>
<span data-ttu-id="b9f21-183">`((Double, Qubit) => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-183">It has signature `((Double, Qubit) => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-184">`Rx(_, _)`은 `R(PauliX, _, _)`와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-184">`Rx(_, _)` is the same as `R(PauliX, _, _)`.</span></span>

<span data-ttu-id="b9f21-185"><xref:microsoft.quantum.intrinsic.ry> 연산은 Pauli $Y $ axis를 중심으로 회전을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-185">The <xref:microsoft.quantum.intrinsic.ry> operation implements a rotation around the Pauli $Y$ axis.</span></span>
<span data-ttu-id="b9f21-186">`((Double, Qubit) => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-186">It has signature `((Double, Qubit) => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-187">`Ry(_, _)`은 `R(PauliY,_ , _)`와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-187">`Ry(_, _)` is the same as `R(PauliY,_ , _)`.</span></span>

<span data-ttu-id="b9f21-188"><xref:microsoft.quantum.intrinsic.rz> 연산은 Pauli $Z $ axis를 중심으로 회전을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-188">The <xref:microsoft.quantum.intrinsic.rz> operation implements a rotation around the Pauli $Z$ axis.</span></span>
<span data-ttu-id="b9f21-189">`((Double, Qubit) => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-189">It has signature `((Double, Qubit) => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-190">`Rz(_, _)`은 `R(PauliZ, _, _)`와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-190">`Rz(_, _)` is the same as `R(PauliZ, _, _)`.</span></span>

<span data-ttu-id="b9f21-191"><xref:microsoft.quantum.intrinsic.r1> 연산은 $ \ket{1}$ ($Z $의 $-$1 eigenstate)를 기준으로 지정 된 양만큼 회전을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-191">The <xref:microsoft.quantum.intrinsic.r1> operation implements a rotation by the given amount around $\ket{1}$, the $-1$ eigenstate of $Z$.</span></span>
<span data-ttu-id="b9f21-192">`((Double, Qubit) => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-192">It has signature `((Double, Qubit) => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-193">`R1(phi,_)`은 `R(PauliZ,phi,_)`와 동일 하며 `R(PauliI,-phi,_)`.</span><span class="sxs-lookup"><span data-stu-id="b9f21-193">`R1(phi,_)` is the same as `R(PauliZ,phi,_)` followed by `R(PauliI,-phi,_)`.</span></span>

<span data-ttu-id="b9f21-194"><xref:microsoft.quantum.intrinsic.r1frac> 연산은 Z = 1 eigenstate를 기준으로 지정 된 양만큼 소수 순환을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-194">The <xref:microsoft.quantum.intrinsic.r1frac> operation implements a fractional rotation by the given amount around the Z=1 eigenstate.</span></span>
<span data-ttu-id="b9f21-195">`((Int,Int, Qubit) => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-195">It has signature `((Int,Int, Qubit) => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-196">`R1Frac(k,n,_)`은 `RFrac(PauliZ,-k.n+1,_)`와 동일 하며 `RFrac(PauliI,k,n+1,_)`.</span><span class="sxs-lookup"><span data-stu-id="b9f21-196">`R1Frac(k,n,_)` is the same as `RFrac(PauliZ,-k.n+1,_)` followed by `RFrac(PauliI,k,n+1,_)`.</span></span>

<span data-ttu-id="b9f21-197">Bloch 구에 매핑된이 인스턴스에서 Pauli $Z $ 축에 대 한 회전 작업의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-197">An example of a rotation operation (around the Pauli $Z$ axis, in this instance) mapped onto the Bloch sphere is shown below:</span></span>

![회전 작업이 Bloch 구에 매핑됨](~/media/prelude_rotationBloch.png)

#### <a name="multi-qubit-operations"></a><span data-ttu-id="b9f21-199">다중 기능 비트 작업</span><span class="sxs-lookup"><span data-stu-id="b9f21-199">Multi-Qubit Operations</span></span> ####

<span data-ttu-id="b9f21-200">Prelude는 위의 단일 비트 작업 외에도 여러 가지 다중 기능 비트 작업을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-200">In addition to the single-qubit operations above, the prelude also defines several multi-qubit operations.</span></span>

<span data-ttu-id="b9f21-201">먼저 <xref:microsoft.quantum.intrinsic.cnot> 작업에서 표준 제어-`NOT` 게이트를 수행 합니다. \begin{equation} \operatorname{CNOT} \mathrel{: =} \begin{bmatrix} 1 & 0 & 0 & 0 \\\\ 0 & 1 & 0 & 0 \\\\ 0 & 0 & 0 & 1 \\\\ 0 & 0 & 1 & 0 \end{bmatrix}.</span><span class="sxs-lookup"><span data-stu-id="b9f21-201">First, the <xref:microsoft.quantum.intrinsic.cnot> operation performs a standard controlled-`NOT` gate, \begin{equation} \operatorname{CNOT} \mathrel{:=} \begin{bmatrix} 1 & 0 & 0 & 0 \\\\ 0 & 1 & 0 & 0 \\\\ 0 & 0 & 0 & 1 \\\\ 0 & 0 & 1 & 0 \end{bmatrix}.</span></span>
<span data-ttu-id="b9f21-202">\end{equation} \operatorname{CNOT} $ unitarily이 두 개의 개별 비트에서 작동 함을 나타내는 시그니처 `((Qubit, Qubit) => Unit is Adj + Ctl)`있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-202">\end{equation} It has signature `((Qubit, Qubit) => Unit is Adj + Ctl)`, representing that $\operatorname{CNOT}$ acts unitarily on two individual qubits.</span></span>
<span data-ttu-id="b9f21-203">`CNOT(q1, q2)`은 `(Controlled X)([q1], q2)`와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-203">`CNOT(q1, q2)` is the same as `(Controlled X)([q1], q2)`.</span></span>
<span data-ttu-id="b9f21-204">`Controlled` 함수를 사용 하 여 레지스터를 제어할 수 있으므로 `[q1]` 배열 리터럴을 사용 하 여 한 개의 컨트롤을 사용 한다고 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-204">Since the `Controlled` functor allows for controlling on a register, we use the array literal `[q1]` to indicate that we want only the one control.</span></span>

<span data-ttu-id="b9f21-205"><xref:microsoft.quantum.intrinsic.ccnot> 작업은 Toffoli 게이트가 라고도 하는 이중 제어 되지 않는 게이트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-205">The <xref:microsoft.quantum.intrinsic.ccnot> operation performs doubly-controlled NOT gate, sometimes also known as the Toffoli gate.</span></span>
<span data-ttu-id="b9f21-206">`((Qubit, Qubit, Qubit) => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-206">It has signature `((Qubit, Qubit, Qubit) => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-207">`CCNOT(q1, q2, q3)`은 `(Controlled X)([q1, q2], q3)`와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-207">`CCNOT(q1, q2, q3)` is the same as `(Controlled X)([q1, q2], q3)`.</span></span>

<span data-ttu-id="b9f21-208"><xref:microsoft.quantum.intrinsic.swap> 작업은 두 가지 비트의 퀀텀 상태를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-208">The <xref:microsoft.quantum.intrinsic.swap> operation swaps the quantum states of two qubits.</span></span>
<span data-ttu-id="b9f21-209">즉, 단일 행렬을 구현 합니다. \begin{equation} \operatorname{SWAP} \mathrel{: =} \begin{bmatrix} 1 & 0 & 0 & 0 \\\\ 0 & 0 & 1 & 0 \\\\ 0 & 1 & 0 & 0 \\\\ 0 & 0 & 0 & 1 \end{bmatrix}.</span><span class="sxs-lookup"><span data-stu-id="b9f21-209">That is, it implements the unitary matrix \begin{equation} \operatorname{SWAP} \mathrel{:=} \begin{bmatrix} 1 & 0 & 0 & 0 \\\\ 0 & 0 & 1 & 0 \\\\ 0 & 1 & 0 & 0 \\\\ 0 & 0 & 0 & 1 \end{bmatrix}.</span></span>
<span data-ttu-id="b9f21-210">\end{equation} `((Qubit, Qubit) => Unit is Adj + Ctl)`시그니처를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-210">\end{equation} It has signature `((Qubit, Qubit) => Unit is Adj + Ctl)`.</span></span>
<span data-ttu-id="b9f21-211">`SWAP(q1,q2)`은 `CNOT(q1, q2)`와 같으며 `CNOT(q2, q1)` 다음에 `CNOT(q1, q2)`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-211">`SWAP(q1,q2)` is equivalent to `CNOT(q1, q2)` followed by `CNOT(q2, q1)` and then `CNOT(q1, q2)`.</span></span>

> [!NOTE]
> <span data-ttu-id="b9f21-212">스왑 게이트는 `Qubit[]`형식의 변수 요소를 다시 정렬 하는 것 *과는 다릅니다* .</span><span class="sxs-lookup"><span data-stu-id="b9f21-212">The SWAP gate is *not* the same as rearranging the elements of a variable with type `Qubit[]`.</span></span>
> <span data-ttu-id="b9f21-213">`SWAP(q1, q2)`를 적용 하면 `q1` 및 `q2`에서 참조 하는 원하는 비트의 상태가 변경 됩니다. 반면 `let swappedRegister = [q2, q1];`은 이러한 것이 해당 하는 비트를 참조 하는 방법에만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-213">Applying `SWAP(q1, q2)` causes a change to the state of the qubits referred to by `q1` and `q2`, while `let swappedRegister = [q2, q1];` only affects how we refer to those qubits.</span></span>
> <span data-ttu-id="b9f21-214">또한 `(Controlled SWAP)([q0], (q1, q2))`를 사용 하면 요소를 다시 정렬 하 여 나타낼 수 없는 세 번째 조건 화 된의 상태를 `SWAP` 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-214">Moreover, `(Controlled SWAP)([q0], (q1, q2))` allows for `SWAP` to be conditioned on the state of a third qubit, which we cannot represent by rearranging elements.</span></span>
> <span data-ttu-id="b9f21-215">Fredkin gate 라고도 하는 제어 교환 게이트는 모든 클래식 계산을 포함 하기에 충분히 강력한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-215">The controlled-SWAP gate, also known as the Fredkin gate, is powerful enough to include all classical computation.</span></span>

<span data-ttu-id="b9f21-216">마지막으로 prelude는 여러 가지 지 수 연산자를 나타내는 두 가지 작업을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-216">Finally, the prelude provides two operations for representing exponentials of multi-qubit Pauli operators.</span></span>
<span data-ttu-id="b9f21-217"><xref:microsoft.quantum.intrinsic.exp> 작업은 여러 \operatorname{Exp} (\vec{\sigma}, \a\mathrel{): =} \a\left (i \\a\sigma_0 \otime \sigma_1 \os)로 표현 된 Pauli 행렬의 텐서 제품을 기반으로 하는 회전을 수행 합니다. cdots \otimes \sigma_n \right), \end{-ation} (여기서 $ \vec{\sigma} = (\sigma_0, \sigma_1, \도트, \sigma_n) $은 단일 = (,, \</span><span class="sxs-lookup"><span data-stu-id="b9f21-217">The <xref:microsoft.quantum.intrinsic.exp> operation performs a rotation based on a tensor product of Pauli matrices, as represented by the multi-qubit unitary \begin{equation} \operatorname{Exp}(\vec{\sigma}, \phi) \mathrel{:=} \exp\left(i \phi \sigma_0 \otimes \sigma_1 \otimes \cdots \otimes \sigma_n \right), \end{equation} where $\vec{\sigma} = (\sigma_0, \sigma_1, \dots, \sigma_n)$ is a sequence of single-qubit Pauli operators, and where $\phi$ is an angle.</span></span>
<span data-ttu-id="b9f21-218">`Exp` 회전은 $ \vec{\sigma} $를 `Pauli` 요소의 배열로 나타내며이를 통해 시그니처 `((Pauli[], Double, Qubit[]) => Unit is Adj + Ctl)`을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-218">The `Exp` rotation represents $\vec{\sigma}$ as an array of `Pauli` elements, such that it has signature `((Pauli[], Double, Qubit[]) => Unit is Adj + Ctl)`.</span></span>

<span data-ttu-id="b9f21-219"><xref:microsoft.quantum.intrinsic.expfrac> 작업은 위에서 설명한 dyadic 분수 표기법을 사용 하 여 동일한 회전을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-219">The <xref:microsoft.quantum.intrinsic.expfrac> operation performs the same rotation, using the dyadic fraction notation discussed above.</span></span>
<span data-ttu-id="b9f21-220">`((Pauli[], Int, Int, Qubit[]) => Unit is Adj + Ctl)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-220">It has signature `((Pauli[], Int, Int, Qubit[]) => Unit is Adj + Ctl)`.</span></span>

> [!WARNING]
> <span data-ttu-id="b9f21-221">Pauli 연산자의 텐서 제품 지 수은 Pauli 연산자 지 수의 텐서 제품과 동일 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-221">Exponentials of the tensor product of Pauli operators are not the same as tensor products of the exponentials of Pauli operators.</span></span>
> <span data-ttu-id="b9f21-222">즉, $e ^ {i (Z \otimes Z)는 \phi} \ne e ^ {i Z \phi} \otimes e ^ {i Z \phi} $입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-222">That is, $e^{i (Z \otimes Z) \phi} \ne e^{i Z \phi} \otimes e^{i Z \phi}$.</span></span>

### <a name="measurements"></a><span data-ttu-id="b9f21-223">측정값</span><span class="sxs-lookup"><span data-stu-id="b9f21-223">Measurements</span></span> ###

<span data-ttu-id="b9f21-224">측정할 때 측정 되는 연산자의 + 1 eigenvalue는 `Zero` 결과에 해당 하 고-1 eigenvalue는 `One` 결과에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-224">When measuring, the +1 eigenvalue of the operator being measured corresponds to a `Zero` result, and the -1 eigenvalue to a `One` result.</span></span>

> [!NOTE]
> <span data-ttu-id="b9f21-225">이 규칙은 이상한 것 처럼 보일 수 있지만 두 가지 매우 좋은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-225">While this convention might seem odd, it has two very nice advantages.</span></span>
> <span data-ttu-id="b9f21-226">첫째, $ \ket{0}$ 결과를 관찰 하는 것은 `Result` 값 `Zero`으로 표시 되 고 $ \ket{1}$은 `One`에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-226">First, observing the outcome $\ket{0}$ is represented by the `Result` value `Zero`, while observing $\ket{1}$ corresponds to `One`.</span></span>
> <span data-ttu-id="b9f21-227">둘째, $ \lambda = (-1) ^ r $ $r 결과에 해당 하는 eigenvalue $ \lambda $를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-227">Second, we can write out that the eigenvalue $\lambda$ corresponding to a result $r$ is $\lambda = (-1)^r$.</span></span>

<span data-ttu-id="b9f21-228">측정 연산은 `Adjoint`와 `Controlled` 함수를 모두 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-228">Measurement operations support neither the `Adjoint` nor the `Controlled` functor.</span></span>

<span data-ttu-id="b9f21-229"><xref:microsoft.quantum.intrinsic.measure> 작업은 지정 된 Pauli 연산자 제품에서 하나 이상의에 대 한 공동 측정을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-229">The <xref:microsoft.quantum.intrinsic.measure> operation performs a joint measurement of one or more qubits in the specified product of Pauli operators.</span></span>
<span data-ttu-id="b9f21-230">Pauli 배열 및 원하는 비트 배열의 길이가 다른 경우 작업이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-230">If the Pauli array and qubit array are different lengths, then the operation fails.</span></span>
<span data-ttu-id="b9f21-231">`Measure`에 `((Pauli[], Qubit[]) => Result)`시그니처가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-231">`Measure` has signature `((Pauli[], Qubit[]) => Result)`.</span></span>

<span data-ttu-id="b9f21-232">조인트 측정은 각 비트를 개별적으로 측정 하는 것과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-232">Note that a joint measurement is not the same as measuring each qubit individually.</span></span>
<span data-ttu-id="b9f21-233">예를 들어 $ \ket{11} = \ket{1} \otimes \ket{1} = X\otimes X \ket{00}$ 상태를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-233">For example, consider the state $\ket{11} = \ket{1} \otimes \ket{1} = X\otimes X \ket{00}$.</span></span>
<span data-ttu-id="b9f21-234">$Z _0 $ 및 $Z _1 $를 개별적으로 측정 하 여 _0 = $1 및 $r _1 = $1 $r 결과를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-234">Measuring $Z_0$ and $Z_1$ each individually, we get the results $r_0 = 1$ and $r_1 = 1$.</span></span>
<span data-ttu-id="b9f21-235">$Z _0 Z_1 $을 측정 $r _ {\textrm{joint}} = $0의 단일 결과는 $ \ket{11}$의 pairity가 양수인 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-235">Measuring $Z_0 Z_1$, however, we get the single result $r_{\textrm{joint}} = 0$, representing that the pairity of $\ket{11}$ is positive.</span></span>
<span data-ttu-id="b9f21-236">다른 방법으로 $ (-1) ^ {r_0 + r_1} = (-1) ^ r_ {\textrm{joint}}) $를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-236">Put differently, $(-1)^{r_0 + r_1} = (-1)^r_{\textrm{joint}})$.</span></span>
<span data-ttu-id="b9f21-237">이 측정을 통해 패리티 *를 알아보는 것* 이기 때문에 superposition에서 긍정 패리티 2 2-\ket{00}$ 및 $ \ket{11}$와 같은에 표시 되는 퀀텀 정보는 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-237">Critically, since we *only* learn the parity from this measurement, any quantum information represented in the superposition between the two two-qubit states of positive parity, $\ket{00}$ and $\ket{11}$, is preserved.</span></span>
<span data-ttu-id="b9f21-238">오류 수정에 대해 설명 하는 것 처럼이 속성은 나중에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-238">This property will be essential later, as we discuss error correction.</span></span>

<span data-ttu-id="b9f21-239">편의를 위해 prelude는 두 가지 다른 작업을 제공 하 여이를 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-239">For convenience, the prelude also provides two other operations for measuring qubits.</span></span>
<span data-ttu-id="b9f21-240">첫째, 단일 수준 측정을 수행 하는 것이 매우 일반적 이기 때문에 prelude은이 경우의 약어를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-240">First, since performing single-qubit measurements is quite common, the prelude defines a shorthand for this case.</span></span>
<span data-ttu-id="b9f21-241"><xref:microsoft.quantum.intrinsic.m> 작업은 단일의 비트에서 Pauli $Z $ 연산자를 측정 하 고 시그니처 `(Qubit => Result)`를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-241">The <xref:microsoft.quantum.intrinsic.m> operation measures the Pauli $Z$ operator on a single qubit, and has signature `(Qubit => Result)`.</span></span>
<span data-ttu-id="b9f21-242">`M(q)`은 `Measure([PauliZ], [q])`와 동등합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-242">`M(q)` is equivalent to `Measure([PauliZ], [q])`.</span></span>

<span data-ttu-id="b9f21-243"><xref:microsoft.quantum.measurement.multim>는 각 고 비트에 대해 얻은 `Result` 값의 *배열을* 반환 하 여 각 값의 배열에 대해 Pauli $Z $ 연산자를 *별도로* 측정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-243">The <xref:microsoft.quantum.measurement.multim> measures the Pauli $Z$ operator *separately* on each of an array of qubits, returning the *array* of `Result` values obtained for each qubit.</span></span>
<span data-ttu-id="b9f21-244">일부 경우에는이를 최적화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-244">In some cases this can be optimized.</span></span> <span data-ttu-id="b9f21-245">서명 (`Qubit[] => Result[])`)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-245">It has signature (`Qubit[] => Result[])`.</span></span>
<span data-ttu-id="b9f21-246">`MultiM(qs)`는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-246">`MultiM(qs)` is equivalent to:</span></span>

```qsharp
mutable rs = new Result[Length(qs)];
for (index in 0..Length(qs)-1)
{
    set rs[index] = M(qs[index]);
}
return rs;
```

## <a name="extension-functions-and-operations"></a><span data-ttu-id="b9f21-247">확장 함수 및 작업</span><span class="sxs-lookup"><span data-stu-id="b9f21-247">Extension Functions and Operations</span></span> ##

<span data-ttu-id="b9f21-248">또한 prelude는 Q # 코드 내에서 사용 하기 위해 .NET 수준에서 다양 한 수학적 및 형식 변환 함수 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-248">In addition, the prelude defines a rich set of mathematical and type conversion functions at the .NET level for use within Q# code.</span></span>
<span data-ttu-id="b9f21-249">예를 들어 <xref:microsoft.quantum.extensions.math> 네임 스페이스는 <xref:microsoft.quantum.extensions.math.sin> 및 <xref:microsoft.quantum.extensions.math.log>와 같은 유용한 작업을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-249">For instance, the <xref:microsoft.quantum.extensions.math> namespace defines useful operations such as <xref:microsoft.quantum.extensions.math.sin> and <xref:microsoft.quantum.extensions.math.log>.</span></span>
<span data-ttu-id="b9f21-250">퀀텀 개발 키트에서 제공 하는 구현에서는 기존 .NET 기본 클래스 라이브러리를 사용 하므로 퀀텀 프로그램 및 해당 클래식 드라이버 사이에 추가 통신 왕복이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-250">The implementation provided by the Quantum Development Kit uses the classical .NET base class library, and thus may involve an additional communications round trip between quantum programs and their classical drivers.</span></span>
<span data-ttu-id="b9f21-251">이는 로컬 시뮬레이터에 대 한 문제를 제공 하지 않지만 원격 시뮬레이터 또는 실제 하드웨어를 대상 컴퓨터로 사용 하는 경우 성능 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-251">While this does not present a problem for a local simulator, this can be a performance issue when using a remote simulator or actual hardware as a target machine.</span></span>
<span data-ttu-id="b9f21-252">즉, 개별 대상 컴퓨터는 특정 시스템에 보다 효율적인 버전으로 이러한 작업을 재정의 하 여 이러한 성능 영향을 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-252">That said, an individual target machine may mitigate this performance impact by overriding these operations with versions that are more efficient for that particular system.</span></span>

### <a name="math"></a><span data-ttu-id="b9f21-253">산</span><span class="sxs-lookup"><span data-stu-id="b9f21-253">Math</span></span> ###

<span data-ttu-id="b9f21-254"><xref:microsoft.quantum.extensions.math> 네임 스페이스는 .NET 기본 클래스 라이브러리의 [`System.Math` 클래스](https://docs.microsoft.com/dotnet/api/system.math?view=netframework-4.7.1)에서 많은 유용한 함수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-254">The <xref:microsoft.quantum.extensions.math> namespace provides many useful functions from the .NET base class library's [`System.Math` class](https://docs.microsoft.com/dotnet/api/system.math?view=netframework-4.7.1).</span></span>
<span data-ttu-id="b9f21-255">이러한 함수는 다른 Q # 함수와 동일한 방식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-255">These functions can be used in the same manner as any other Q# functions:</span></span>

```qsharp
open Microsoft.Quantum.Math;
// ...
let y = Sin(theta);
```

<span data-ttu-id="b9f21-256">.NET 정적 메서드가 인수의 형식에 따라 오버 로드 된 경우 해당 하는 Q # 함수는 해당 입력의 형식을 나타내는 접미사로 주석을 답니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-256">Where a .NET static method has been overloaded based on the type of its arguments, the corresponding Q# function is annotated with a suffix indicating the type of its input:</span></span>

```qsharp
let x = AbsI(-3); // x : Int = 3
let y = AbsD(-PI()); // y : Double = 3.1415...
```


### <a name="bitwise-operations"></a><span data-ttu-id="b9f21-257">비트 연산</span><span class="sxs-lookup"><span data-stu-id="b9f21-257">Bitwise Operations</span></span> ###

<span data-ttu-id="b9f21-258">마지막으로, <xref:microsoft.quantum.extensions.bitwise> 네임 스페이스는 비트 연산자를 통해 정수 조작을 위한 몇 가지 유용한 함수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-258">Finally, the <xref:microsoft.quantum.extensions.bitwise> namespace provides several useful functions for manipulating integers through bitwise operators.</span></span>
<span data-ttu-id="b9f21-259">예를 들어 <xref:microsoft.quantum.extensions.bitwise.parity>은 정수의 비트 패리티를 다른 정수로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f21-259">For instance, <xref:microsoft.quantum.extensions.bitwise.parity> returns the bitwise parity of an integer as another integer.</span></span>