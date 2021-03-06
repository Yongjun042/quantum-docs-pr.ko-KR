---
title: 퀀텀 oracles | Microsoft Docs
description: 퀀텀 oracles
author: cgranade
uid: microsoft.quantum.concepts.oracles
ms.author: Christopher.Granade@microsoft.com
ms.date: 07/11/2018
ms.topic: article
ms.openlocfilehash: 96949b371a3a5a1135d624690933a48ea0214a2e
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2019
ms.locfileid: "73184715"
---
# <a name="quantum-oracles"></a>퀀텀 Oracles

Oracle $O $은 다른 알고리즘에 대 한 입력으로 사용 되는 "블랙 박스" 작업입니다.
이러한 작업은 $f 기존 함수를 사용 하 여 정의 되는 경우가 많습니다. \\{0, 1\\} ^ n \ \\{0, 1\\} ^ m $은 $n $ 비트 이진 입력을 사용 하 고 $m $ bit 이진 출력을 생성 합니다.
이렇게 하려면 특정 이진 입력 $x = (x_{0}, x_{1}, \dots, x_ {n-1}) $를 고려 합니다.
\Ket{\vec{x}} = \ket{x_{0}} \otimes \ket{x_{1}} \otimes \cst\otimes \ket{x_{n-1}} $로 stbit 상태에 레이블을 지정할 수 있습니다.

먼저 $O $를 $O \ket{x} = \ket{f (x)} $로 정의 하려고 할 수 있지만, 여기에는 몇 가지 문제가 있습니다.
첫째, $f $에는 다른 크기의 입력 및 출력 ($n \ne m $)이 있을 수 있습니다 .이 경우 $O $을 적용 하면 레지스터의 원하는 비트 수가 변경 됩니다.
둘째, $n = m $ 인 경우에도 함수를 반전할 수 없습니다. 일부 $x \ne y $로 $f (x) = f (y) $를 입력 하는 경우에는 \ket{x} = O\ket {y} $ 이지만 $O ^ \dagger O\ket {x} \ne O ^ \Dagger {y} $를 $O 누릅니다.
즉, adjoint 작업 $O ^ \dagger $에 생성할 수 없으며,이에 대해 adjoint가 정의 되어 있어야 합니다.

## <a name="defining-an-oracle-by-its-effect-on-computational-basis-states"></a>계산 기준 상태에 영향을 미치는 oracle 정의
이러한 두 가지 문제를 해결할 수 있습니다. 이러한 문제는 답변을 보유 하기 위해 $ $ $m의 두 번째 레지스터를 도입 하는 것입니다.
그런 다음 모든 계산 기준에 대 한 oracle의 효과를 정의 합니다. 모든 $x \in \\{0, 1\\} ^ n $ 및 \\{0, 1\\} ^ m $의 $y \in

$ $ \begin{align} O (\ket{x} \otimes \ket{y}) = \ket{x} \otimes \ket{y \otimes f (x)}.
\end{align} $ $

이제 생성에의 한 $O = O ^ \aate$를 생성 했으므로 이전 문제를 모두 해결 했습니다.

> [!TIP]
> $O = O ^ {\dagger} $에 대 한 자세한 내용은 $a \oplus b\oplus b = a $ for all $a, b \bin \{0, 1\}$ 이므로 ^ 2 = \boldone $ $O.
> 결과적으로 \ket{x} \ket{y \oplus f (x)} = \ket{x} \ket{y \oplus f (x) \oplus f (x)} = \ket{x} \ket{y} $를 $O 합니다.

중요 한 것은 각 계산 기준 상태 $ \ket{x}\ket{y} $에 대해 oracle을 정의 하 $O는 것은 다른 모든 상태에 대해 $가 작동 하는 방법을 정의 합니다.
이는 모든 퀀텀 작업과 마찬가지로 $O $가 작동 하는 상태에서 선형 이라는 사실을 즉시 따릅니다.
예를 들어 $H \ket{0} = \ket{+} $ 및 $H \ket{1} = \ket{-}$에 의해 정의 된 Hadamard 작업을 고려 합니다.
$ \Ket{+} $에서 $H $가 작동 하는 방법을 알고 싶으면 $ is linear $H를 사용할 수 있습니다.

$ $ \begin{align} H\ket {+} & = \frac{1}{\sqrt{2}} H (\ket{0} + \ket{1}) = \frac{1}{\sqrt{2}} (H\ket{0} + H\ket{1}) \\\\ & = \frac{1}{\sqrt{2}} (\ k {+} + \ket{-}) = \frac12 (\ket{0} + \ket{1} + \ket{0}-\ket{1}) = \ket{0}.
\end{align} $ $

Oracle $O $를 정의 하는 경우와 비슷한 방법으로 $ \ket{\psi} $ on $n + m $를 사용할 수 있습니다.

$ $ \begin{align} \ket{\psi} & = \sum_{x \in \\{0, 1\\} ^ n, y \in \\{0, 1\\} ^ m} \alpha (x, y) \ket{x} \ket{y} \end{align} $ $

여기서 $ \alpha: \\{0, 1\\} ^ n \alpha \\{0, 1\\} ^ m \alpha $ \mathbb{C} $는 state $ $의 계수를 나타냅니다. 따라서

$ $ \begin{align} O \ket{\psi} & = O \sum_{x \in \\{0, 1\\} ^ n, y \in \\{0, 1\\} ^ m} \alpha (x, y) \ket{x} \ket{y} \\\\ & = \sum_{x \in \\{0 , 1\\} ^ n, y \ \\{0, 1\\} ^ m} \in (x, y) O \ket{x} \ket{y} \\\\ & = \sum_{x \in \\{0, 1\\} ^ n, y \in \\{0 , 1\\} ^ m} \alpha (x, y) \ket{x} \ket{y \oplus f (x)}.
\end{align} $ $

## <a name="phase-oracles"></a>Oracles 단계
또는 $O $에 대 한 입력에 따라 _단계_ 를 적용 하 여 $ $f $를 oracle $O $로 인코딩할 수 있습니다.
예를 들어 $ $ \begin{align} O \ket{x} = (-1) ^ {f (x)} \ket{x}.와 같은 $를 $O 정의할 수 있습니다.
\end{align} $ $ 단계 oracle이 초기에 계산 기준 상태 $ \ket{x} $로 작동 하는 경우이 단계는 글로벌 단계 이므로 관찰 가능 하지 않습니다.
그러나 이러한 oracle은 superposition에 적용 되거나 제어 된 작업으로 적용 되는 경우 매우 강력한 리소스가 될 수 있습니다.
예를 들어, _f $에 대 한 단계 orcale $O $는 단일의 비트 함수 $f $입니다.
그런 다음 $ $ \begin{align} O_f \ket{+} & = O_f (\ket{0} + \ket{1})/\sqrt{2} \\\\ &{0} = ((-1) ^ {f (0)} \ket{1}+ (-1) ^ {f (1)} \ket{2})/\sqrt \\\\ & = (-1) ^ {f ( 0)} (\ket{0} + (-1) ^ {f (1)-f (0)} \ket{1})/\sqrt{2} \\\\ & = (-1) ^ {f (0)} Z ^ {f (0)-f (1)} \ket{+}.
\end{align} $ $

보다 일반적으로는 oracles의 두 뷰를 넓혔습니다 하 여 단일 비트만이 아닌 실수를 반환 하는 클래식 함수를 나타낼 수 있습니다.

Oracle을 구현 하는 가장 좋은 방법은 지정 된 알고리즘 내에서이 oracle을 사용 하는 방법에 따라 크게 달라 집니다.
예를 들어 [Deutsch-Jozsa 알고리즘](https://en.wikipedia.org/wiki/Deutsch%E2%80%93Jozsa_algorithm) 은 첫 번째 방법으로 구현 된 oracle을 사용 하는 반면 [Grover의 알고리즘](https://en.wikipedia.org/wiki/Grover's_algorithm) 은 두 번째 방법으로 구현 된 oracle에 의존 합니다.


자세한 내용은 [Gilyén *et al*. 1711.00465](https://arxiv.org/abs/1711.00465)에 설명 되어 있습니다.
