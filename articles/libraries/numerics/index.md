---
title: 양자 숫자 라이브러리 소개 | Microsoft Docs
description: 양자 숫자 라이브러리 소개
author: thomashaener
ms.author: thhaner
ms.date: 5/14/2019
ms.topic: article
uid: microsoft.quantum.numerics.intro
ms.openlocfilehash: efd1a712616534ac281433fc008f0983271881d7
ms.sourcegitcommit: aa5e6f4a2deb4271a333d3f1b1eb69b5bb9a7bad
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73442436"
---
# <a name="introduction-to-the-quantum-numerics-library"></a><span data-ttu-id="cb5c1-103">양자 숫자 라이브러리 소개</span><span class="sxs-lookup"><span data-stu-id="cb5c1-103">Introduction to the Quantum Numerics Library</span></span>

<span data-ttu-id="cb5c1-104">많은 양자 알고리즘은 입력 중첩에 대한 수학 함수를 평가하는 [오라클](xref:microsoft.quantum.concepts.oracles)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-104">Many quantum algorithms rely on [oracles](xref:microsoft.quantum.concepts.oracles) that evaluate mathematical functions on a superposition of inputs.</span></span>
<span data-ttu-id="cb5c1-105">예를 들어, Shor 알고리즘의 주요 구성 요소는 모든 $2n$비트 문자열에 대한 균일한 중첩에서 고정 $a$, $N$의 인수 및 $x$ a $2n$큐비트 정수에 대해 $f(x) = a^x\operatorname{mod} N$를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-105">The main component of Shor's algorithm, for example, evaluates $f(x) = a^x\operatorname{mod} N$ for a fixed $a$, the number to factor $N$, and $x$ a $2n$-qubit integer in a uniform superposition over all $2n$-bit strings.</span></span>

<span data-ttu-id="cb5c1-106">실제 양자 컴퓨터에서 Shor의 알고리즘을 실행하려면 대상 컴퓨터의 네이티브 연산을 기준으로 이 함수를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-106">To run Shor's algorithm on an actual quantum computer, this function has to be written in terms of the native operations of the target machine.</span></span>
<span data-ttu-id="cb5c1-107">최하위 비트에서 계산하는 $i$번째 비트를 나타내는 $x_i$로 $x$의 이진 표현을 나타낼 경우 $f(x)$는 $f(x) = a^{\sum_{i=0}^{2n-1} x_i 2^i} \operatorname{mod} N$로 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-107">Using the binary representation of $x$ with $x_i$ denoting the $i$-th bit counting from the least-significant bit, $f(x)$ can be written as $f(x) = a^{\sum_{i=0}^{2n-1} x_i 2^i} \operatorname{mod} N$.</span></span>
<span data-ttu-id="cb5c1-108">이 수식을 다시 항 $a^{2^i x_i}=(a^{2^i})^{x_i}$의 product (mod N)으로 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-108">In turn, this can be written as a product (mod N) of terms $a^{2^i x_i}=(a^{2^i})^{x_i}$.</span></span> <span data-ttu-id="cb5c1-109">따라서 함수 $f(x)$는 $x_i$가 0이 아닌 조건일 때 $2n$ (modular)를 $a^{2^i}$에 곱한 시퀀스를 사용하여 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-109">The function $f(x)$ can thus be implemented using a sequence of $2n$ (modular) multiplications by $a^{2^i}$ conditional on $x_i$ being nonzero.</span></span> <span data-ttu-id="cb5c1-110">상수 $a^{2^i}$는 알고리즘을 실행하기 전에 미리 계산하여 모듈로 N을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-110">The constants $a^{2^i}$ can be precomputed and reduced modulo N before running the algorithm.</span></span>

<span data-ttu-id="cb5c1-111">이러한 제어되는 모듈식 곱셈 시퀀스를 다음과 같이 좀 더 간단히 나타낼 수 있습니다. 각 곱셈은 $n$ 제어되는 모듈식 덧셈 시퀀스를 사용하여 수행할 수 있으며, 각 모듈식 덧셈은 일반 덧셈 및 비교 연산자에서 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-111">This sequence of controlled modular multiplications can be simplified further: Each multiplication can be performed using a sequence of $n$ controlled modular additions; and each modular addition can be built from a regular addition and a comparator.</span></span>


<span data-ttu-id="cb5c1-112">실제 구현에 도달하기 위해서 많은 단계가 필요하다는 가정할 경우, 이러한 함수를 처음부터 사용할 수 있다면 매우 유용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-112">Given that so many steps are necessary to arrive at an actual implementation, it would be extremely helpful to have such functionality available from the start.</span></span>
<span data-ttu-id="cb5c1-113">이때문에 Quantum Development Kit에서는 다양한 범위의 숫자 함수를 지원하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-113">This is why the Quantum Development Kit provides support for a wide range of numerics functionality.</span></span>


## <a name="functionality"></a><span data-ttu-id="cb5c1-114">기능</span><span class="sxs-lookup"><span data-stu-id="cb5c1-114">Functionality</span></span>

<span data-ttu-id="cb5c1-115">지금까지 언급한 정수 산술 연산 외에도, 숫자 라이브러리는 다음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-115">Besides the integer arithmetic mentioned thus far, the numerics library provides</span></span>

 - <span data-ttu-id="cb5c1-116">1~2개의 양자 정수를 입력으로 사용하는 부호 있는(없는) 정수 함수(곱하기, 제곱, 나머지 있는 나누기, 역함수, ...)</span><span class="sxs-lookup"><span data-stu-id="cb5c1-116">(Un)signed integer functionality (multiply, square, division with remainder, inversion, ...) with one or two quantum integer numbers as input</span></span>
 - <span data-ttu-id="cb5c1-117">1~2개의 양자 고정 소수점 수를 입력으로 사용하는 고정 소수점 함수(더하기/빼기, 곱하기, 제곱, 1/x, 다항식 계산)</span><span class="sxs-lookup"><span data-stu-id="cb5c1-117">Fixed-point functionality (add / subtract, multiply, square, 1/x, polynomial evaluation) with one or two quantum fixed-point numbers as input</span></span>

## <a name="getting-started"></a><span data-ttu-id="cb5c1-118">시작</span><span class="sxs-lookup"><span data-stu-id="cb5c1-118">Getting started</span></span>

<span data-ttu-id="cb5c1-119">숫자 라이브러리를 시작하려면 [설치 가이드](xref:microsoft.quantum.numerics.installation)를 확인하고 [숫자 라이브러리 사용](xref:microsoft.quantum.numerics.usage)에 대한 자세한 내용을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb5c1-119">To get started with the Numerics Library, check out the [installation guide](xref:microsoft.quantum.numerics.installation) and more information on [using the Numerics Library](xref:microsoft.quantum.numerics.usage).</span></span>