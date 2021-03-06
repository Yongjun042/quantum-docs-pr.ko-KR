---
title: Q# Style Guide | Microsoft Docs
description: Q# Style Guide
author: cgranade
ms.author: chgranad
ms.date: 10/12/2018
ms.topic: article
uid: microsoft.quantum.contributing.style
ms.openlocfilehash: 4050e2ee9e516aed7a8ba1398792562926808ee0
ms.sourcegitcommit: c93fea5980d1d46fbda1e7c7153831b9337134bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73463314"
---
# <a name="q-style-guide"></a>Q# Style Guide #
## <a name="general-conventions"></a>General Conventions ##

The conventions suggested in this guide are intended to help make programs and libraries written in Q# easier to read and understand.

## <a name="guidance"></a>인도

다음을 권장 합니다.

- Never disregard a convention unless you’re doing so intentionally in order to provide more readable and understandable code for your users.

## <a name="naming-conventions"></a>Naming Conventions ##

In offering the Quantum Development Kit, we strive for function and operation names that help quantum developers write programs that are easy to read and that minimize surprise.
An important part of that is that when we choose names for functions, operations, and types, we are establishing the *vocabulary* that programmers use to express quantum concepts; with our choices, we either help or hinder them in their effort to clearly communicate.
This places a responsibility on us to make sure that the names we introduce offer clarity rather than obscurity.
이 섹션에서는 Q # 개발 커뮤니티에서 가장 잘 활용 하는 데 도움이 되는 명시적 지침을 기준으로이 의무를 어떻게 충족 하는지 자세히 설명 합니다.

### <a name="operations-and-functions"></a>작업 및 함수 ###

이름을 설정 해야 하는 첫 번째 작업 중 하나는 지정 된 기호가 함수 또는 작업을 나타내는지 여부입니다.
함수 및 작업 간의 차이점은 코드 블록이 동작 하는 방식을 이해 하는 데 중요 합니다.
함수와 작업을 사용자에 게 구분 하기 위해이 질문에는 의도 하지 않은 결과를 사용 하 여 퀀텀 작업을 모델링 하는 데 사용 됩니다.
즉, 작업은 어떤 작업을 *수행* 합니다.

이와 대조적으로 함수는 데이터 간의 수학적 관계를 설명 합니다.
식 `Sin(PI() / 2.0)` `1.0`*되* 고 프로그램 또는 해당 비트의 상태에 대해 아무 것도 의미 하지 않습니다.

요약 하면 함수는 작업을 수행 합니다.
이러한 구분은 작업을 명사로 서 동사와 함수로 이름을 지정할 것을 제안 합니다.

> [!NOTE]
> 사용자 정의 형식이 선언 되 면 해당 형식의 인스턴스를 생성 하는 새 함수가 암시적으로 동시에 정의 됩니다.
> 이러한 관점에서 사용자 정의 형식은 형식 자체와 생성자 함수에 일관 된 이름을 갖도록 명사로 이름을 지정 해야 합니다.

적절 한 경우 작업 이름이 작업에서 수행한 효과를 명확 하 게 나타내는 동사로 시작 되는지 확인 합니다.
다음은 그 예입니다.

- `MeasureInteger`
- `EstimateEnergy`
- `SampleInt`

특별 한 언급할 만한 사례는 작업이 다른 작업을 입력으로 사용 하 고 호출 하는 경우입니다.
이러한 경우에는 외부 작업이 정의 될 때 입력 작업에서 수행 하는 동작이 명확 하지 않으므로 오른쪽 동사가 명확 하지 않습니다.
`ApplyIf`, `ApplyToEach`및 `ApplyToFirst`같이 동사 `Apply`를 권장 합니다.
다른 동사는이 경우에도 `IterateThroughCartesianPower`에 유용할 수 있습니다.

| 동사 | 예상 효과 |
| ---- | ------ |
| 신청 | 입력으로 제공 된 작업을 라고 합니다. |
| Assert | 가능한 퀀텀 측정의 결과에 대 한 가설은 시뮬레이터에 의해 확인 됩니다. |
| 견적 | 하나 이상의 측정값 으로부터 그려진 추정치를 나타내는 고전 값이 반환 됩니다. |
| 측정값 | 퀀텀 측정이 수행 되며 결과가 사용자에 게 반환 됩니다. |
| 준비 | 지정 된 비트 레지스터가 특정 상태로 초기화 됩니다. |
| 샘플 | 일부 분포에서 무작위로 값이 반환 됩니다. |

함수의 경우 일반적인 명사를 선호 하는 동사를 사용 하지 않는 것이 좋습니다 (아래의 적절 한 명사에 대 한 지침 참조).

- `ConstantArray`
- `Head`
- `LookupFunction`

특히 거의 모든 경우에, 함수 이름이 퀀텀 프로그램의 다른 위치에 있는 작업 또는 부작용에 강력 하 게 연결 되어 있음을 나타내기 위해 해당 하는 경우 과거 participles를 사용 하는 것이 좋습니다.
예를 들어, `ControlledOnInt`는 동사 "control"의 part 분사 폼을 사용 하 여 함수가 인수를 수정 하는 형용사로 작용 함을 표시 합니다.
이 이름에는 아래에서 설명한 대로 기본 제공 `Controlled` 함수에 대 한 의미 체계와 일치 하는 추가적인 이점도 있습니다.
마찬가지로, `Encode`와 강력 하 게 연결 된 UDT에 대 한 `Encoder` 이름의 경우 처럼 _에이전트 명사_ 를 사용 하 여 작업 이름에서 함수와 UDT 이름을 생성할 수 있습니다.

# <a name="guidancetabguidance"></a>[지침](#tab/guidance)

다음을 권장 합니다.

- 작업 이름에 대 한 동사를 사용 합니다.
- 함수 이름에 명사 또는 형용사를 사용 합니다.
- 사용자 정의 형식 및 특성에는 명사를 사용 합니다.
- 모든 호출 가능 이름의 경우 `pascalCase`, `snake_case`또는 `ANGRY_CASE`에 대 한 강력한 기본 설정 `CamelCase` 사용 합니다. 특히 호출 가능 이름이 대문자로 시작 하는지 확인 합니다.
- 모든 지역 변수에 대해 강력한 기본 설정의 `pascalCase`를 사용 하 여 `CamelCase`, `snake_case`또는 `ANGRY_CASE`합니다. 특히 지역 변수가 소문자로 시작 하는지 확인 합니다.
- 함수 및 작업 이름에 밑줄 `_` 사용 하지 않습니다. 계층의 추가 수준이 필요한 경우 네임 스페이스 및 네임 스페이스 별칭을 사용 합니다.

# <a name="examplestabexamples"></a>[예](#tab/examples)

|   | name | 설명 |
|---|------|-------------|
| ☑ | `operation ReflectAboutStart` | 작업의 효과를 나타내려면 동사 ("반사")를 사용 하지 않습니다. |
| ☒ | <s>`operation XRotation`</s> | 명사구를 사용 하는 것은 연산이 아니라 함수를 제안 합니다. |
| ☒ | <s>`operation search_oracle`</s> | `snake_case` contravenes Q # 표기법을 사용 합니다. |
| ☒ | <s>`operation Search_Oracle`</s> | 작업 이름 contravenes Q # notation 내부에 밑줄을 사용 합니다. |
| ☑ | `function StatePreparationOracle` | 명사구를 사용 하면 함수가 연산을 반환 하는 것을 의미 합니다. |
| ☑ | `function EqualityFact` | 명사 ("fact")를 명확 하 게 사용 하 여 함수가 함수 임을 나타내야 합니다. |
| ☒ | <s>`function GetRotationAngles`</s> | 동사 ("get")를 사용 하는 것은 이것이 작업 임을 나타냅니다. |
| ☑ | `newtype GeneratorTerm` | 명사 구를 사용 하면 UDT 생성자 호출 결과를 명확 하 게 참조할 수 있습니다. |
| ☒ | <s>`@Attribute() newtype RunOnce()`</s> | 동사 구를 사용 하면 UDT 생성자가 연산이 됩니다. |
| ☑ | `@Attribute() newtype Deprecated(Reason : String)` | 명사구를 사용 하면 특성의 사용이 전달 됩니다. |

***

### <a name="shorthand-and-abbreviations"></a>약어 및 약어 ###

위의 충고도 불구는 퀀텀 컴퓨팅에서 공통적이 고 널리 사용 되는 여러 가지 형태의 축약형입니다.
특히 대상 컴퓨터의 작업에 내장 된 작업의 경우 기존 및 일반적인 약어를 사용 하는 것이 좋습니다.
예를 들어 `ApplyX`대신 `X` 이름을 선택 하 고 `RotateAboutZ`대신 `Rz` 합니다.
이러한 약어를 사용 하는 경우 작업 이름은 모두 대문자 여야 합니다 (예: `MAJ`).

일반적으로 사용 되는 머리글자어의 경우에는 "퀀텀 푸리에 변환"의 경우 "QFT"와 같은의 두문자어 정의에이 규칙을 적용할 때 주의 해야 합니다.
전체 이름에 머리글자어 및의 두문자어 정의를 사용 하는 데 일반적인 .NET 규칙을 사용 하는 것이 좋습니다 .이에 대 한 자세한 내용은 다음과 같습니다.

- 두 문자로 된 머리글자어와의 두문자어 정의는 대문자로 명명 됩니다 (예 `BE`: "빅 endian"의 경우).
- 모든 긴 머리글자어 및의 두문자어 정의는 `CamelCase` (예: "퀀텀 푸리에 변환"의 `Qft`)로 이름이 지정 됩니다.

따라서 QFT를 구현 하는 작업을 약어로 `QFT` 호출 하거나 `ApplyQft`으로 작성할 수 있습니다.

특히 일반적으로 사용 되는 작업 및 함수에 대해 더 긴 형식의 _별칭_ 으로 약식 이름을 제공 하는 것이 좋을 수 있습니다.

```qsharp
operation CCNOT(control0 : Qubit, control1 : Qubit, target : Qubit)
is Adj + Ctl {
    Controlled X([control0, control1], target);
}
```

# <a name="guidancetabguidance"></a>[지침](#tab/guidance)

다음을 권장 합니다.

- 적절 한 경우 일반적으로 허용 되 고 널리 사용 되는 약식 이름을 고려 합니다.
- 약어에 대문자를 사용 합니다.
- Short (2 자) 머리글자어 및의 두문자어 정의에 대문자를 사용 합니다.
- 더 긴 (3 자 이상) 머리글자어 및의 두문자어 정의에 대 한 `CamelCase`를 사용 합니다.

# <a name="examplestabexamples"></a>[예](#tab/examples)

|   | name | 설명 |
|---|------|-------------|
| ☑ | `X` | "$X $ 변환 적용"의 이해 하기 쉬운 약어 |
| ☑ | `CNOT` | "제어-없음"에 대 한 이해 하기 쉬운 약어 |
| ☒ | <s>`Cnot`</s> | 약어는 `CamelCase`하지 않아야 합니다. |
| ☑ | `ApplyQft` | 일반적인 initialism "QFT"는 긴 형식 이름의 일부로 표시 됩니다. |
| ☑ | `QFT` | 일반적인 initialism "QFT"는 약식 이름의 일부로 표시 됩니다. |



***


### <a name="proper-nouns-in-names"></a>이름에 적절 한 명사 ###

물리학에는 첫 번째 사람이 게시 한 후 이름을 변경 하는 것이 일반적 이지만 대부분의 비 physicists은 모든 사용자의 이름 및 모든 기록에 대해 잘 알고 있지 않습니다.
다른 배경의 사용자는 일반적인 작업 및 개념을 사용 하기 위해 많은 수의 불투명 한 이름을 알아야 하므로, 물리의 명명 규칙에 너무 많이 의존 하는 것은 매우 중요 한 항목입니다.
<!-- An important part of the task of reducing confusion is to make code more accessible.
Especially in a field such as quantum computing that is rich with domain expertise, we must at all times be cognizant of the demands we place on that expertise as we design quantum software.
In naming code symbols, one way that this cognizance expresses itself is as an awareness of the convention from physics of adopting as the names of algorithms and operations the names of their original publishers.
While we must maintain the history and intellectual provenance of concepts in quantum computing, demanding that all users be versed in this history to use even the most basic of functions and operations places a barrier to entry that is in most cases severe enough to even present an ethical compromise. -->
따라서 개념을 설명 하는 적절 한 일반적인 명사를 개념의 게시 기록을 설명 하는 적절 한 명사에 적용 하는 것이 좋습니다.
특정 한 예로, 단일 제어 된 교환 및 이중 제어 되지 않는 작업을 교육용 자료에서 "Fredkin" 및 "Toffoli" 작업 이라고 하지만 Q #에서는 주로 `CSWAP` 및 `CCNOT`로 식별 됩니다.
두 경우 모두 적절 한 명사와 함께 적절 한 명사를 기반으로 하는 동의어 이름을 제공 합니다.

이 기본 설정은 특히 적절 한 명사를 사용 하는 경우에 특히 중요 합니다. Q #은 다양 한 기존 언어에 의해 설정 된 전통을을 따르고, 예를 들어, 부울 논리에 대 한 참조의 `Bool` 형식을 참조 하며,이는 그대로 사용 됩니다. George Boole.
이와 비슷한 몇 가지 퀀텀 개념은 비슷한 방식으로 이름이 지정 됩니다 (Q # 언어에 기본 제공 되는 `Pauli` 형식 포함).
이러한 사용법이 필수적이 지 않은 적절 한 명사 사용을 최소화 하면 적절 한 명사를 피할 수 없는 영향을 줄일 수 있습니다.

# <a name="guidancetabguidance"></a>[지침](#tab/guidance) 

다음을 권장 합니다.

- 이름에 적절 한 명사를 사용 하지 마십시오.

# <a name="examplestabexamples"></a>[예](#tab/examples)

***

### <a name="type-conversions"></a>형식 변환 ###

Q #은 강력 하 고 staticly 지정 된 언어 이기 때문에 형식 변환 함수에 대 한 명시적 호출을 사용 하 여 한 형식의 값을 다른 형식의 값 으로만 사용할 수 있습니다.
이는 값이 암시적으로 (예: 유형 프로 모션) 형식을 변경 하거나 캐스팅을 통해 변경할 수 있는 언어와는 대조적입니다.
따라서 형식 변환 함수는 Q # 라이브러리 개발에서 중요 한 역할을 수행 하 고 명명에 대 한 보다 일반적으로 발생 하는 사항 중 하나를 구성 합니다.
그러나 형식 변환은 항상 _결정적_이므로 함수로 작성 될 수 있으므로 위의 권장 사항 아래에 있습니다.
특히 형식 변환 함수에는 동사 (예: `ConvertToX`) 또는 부사 prepositional 문구 (`ToX`)로 이름을 지정 하지 않는 것이 좋지만, 원본 및 대상 유형을 나타내는 형용사 prepositional 구로 명명 되어야 합니다 (`XAsY`).
형식 변환 함수 이름에 배열 형식을 나열할 때 줄임 `Arr`를 권장 합니다.
예외적인 상황을 방지 하기 위해 `As`를 사용 하 여 모든 형식 변환 함수 이름을 지정 하 여 신속 하 게 식별할 수 있도록 하는 것이 좋습니다.

# <a name="guidancetabguidance"></a>[지침](#tab/guidance)

다음을 권장 합니다.

- 함수가 `X` 형식의 값을 `Y`형식의 값으로 변환 하는 경우 이름 `AsY` 또는 `XAsY`를 사용 합니다.

# <a name="examplestabexamples"></a>[예](#tab/examples)

|   | name | 설명 |
|---|------|-------------|
| ☒ | <s>`ToDouble`</s> | 전치사 "to"는 동사가 아닌 연산을 나타내는 동사 구를 생성 합니다. |
| ☒ | <s>`AsDouble`</s> | 입력 형식이 함수 이름에서 명확 하지 않습니다. |
| ☒ | <s>`PauliArrFromBoolArr`</s> | 입력 및 출력 형식이 잘못 된 순서로 나타납니다. |
| ☑ | `ResultArrAsBoolArr` | 입력 형식과 출력 형식은 모두 명확 하지 않습니다. |

***

### <a name="private-or-internal-names"></a>개인 또는 내부 이름 ###

대부분의 경우 이름은 라이브러리 또는 프로젝트 내부에서 사용 하기 위한 것 이며 라이브러리에서 제공 하는 API의 보장 된 부분이 아닙니다.
내부 전용 코드에 대 한 실수로 종속성이 명확 하 게 적용 되도록 함수 및 작업의 이름을 지정 하는 경우이를 명확 하 게 표시 하는 것이 좋습니다.
작업 또는 함수가 직접 사용 하기 위한 것이 아니며, 부분 응용 프로그램에서 작동 하는 일치 하는 호출 가능에서 사용 해야 하는 경우에는 부분적으로 적용 되는 호출 가능에 대해 `_` 시작 하는 이름을 사용 하는 것이 좋습니다.

# <a name="guidancetabguidance"></a>[지침](#tab/guidance)

다음을 권장 합니다.

- 함수, 작업 또는 사용자 정의 형식이 Q # 라이브러리 또는 프로그램에 대 한 공용 API의 일부가 아니면 이름이 선행 밑줄 (`_`)로 시작 하는지 확인 합니다.

# <a name="examplestabexamples"></a>[예](#tab/examples)

|   | name | 설명 |
|---|------|-------------|
| ☒ | <s>`ApplyDecomposedOperation_`</s> | 밑줄 `_` 이름의 끝에 표시 되어서는 안 됩니다. |
| ☑ | `_ApplyDecomposedOperation` | 처음에 `_` 밑줄은이 작업이 내부용 으로만 사용 됨을 나타냅니다. |

***

### <a name="variants"></a>변종 ###

이후 버전의 Q #에서는이 제한 사항이 유지 되지 않을 수 있지만, 현재는 해당 입력을 함수 하는 것과 관련 된 작업 또는 함수의 그룹이 나 구체적으로 해당 인수의 그룹이 있는 경우가 많습니다.
이러한 그룹은 동일한 루트 이름과 해당 변형을 나타내는 하나 또는 두 개의 문자를 사용 하 여 구분할 수 있습니다.

| 접미사 | 의미 |
|--------|---------|
| `A` | 입력이 `Adjoint` 지원 되어야 합니다. |
| `C` | 입력이 `Controlled` 지원 되어야 합니다. |
| `CA` | 입력이 `Controlled` 및 `Adjoint`를 지원 해야 합니다. |
| `I` | 입력 또는 입력은 형식 `Int` |
| `D` | 입력 또는 입력은 형식 `Double` |
| `L` | 입력 또는 입력은 형식 `BigInt` |

# <a name="guidancetabguidance"></a>[지침](#tab/guidance)

다음을 권장 합니다.

- 함수 또는 작업이 해당 입력의 유형 및 함수 지원에 의해 유사한 함수 또는 작업과 관련이 없는 경우에는 접미사를 사용 하지 마십시오.
- 함수 또는 작업이 해당 입력의 유형 및 함수 지원에 의해 유사한 함수 또는 작업과 관련 된 경우에는 위의 표에서와 같이 접미사를 사용 하 여 변형을 구분 합니다.

# <a name="examplestabexamples"></a>[예](#tab/examples)

***

### <a name="arguments-and-variables"></a>인수 및 변수 ###

함수 또는 작업에 대 한 Q # 코드의 핵심 목표는 쉽게 읽고 이해할 수 있도록 하는 것입니다.
마찬가지로 입력 및 형식 인수의 이름은 제공 된 후 함수 또는 인수가 사용 되는 방식에 대해 통신 해야 합니다.


# <a name="guidancetabguidance"></a>[지침](#tab/guidance)

다음을 권장 합니다.

- 모든 변수 및 입력 이름에 대해 강력한 기본 설정 `pascalCase` 사용 하 여 `CamelCase`, `snake_case`또는 `ANGRY_CASE`합니다.
- 입력 이름은 설명적 이어야 합니다. 가능 하면 하나 또는 두 개의 문자 이름을 사용 하지 마십시오.
- 정확히 하나의 형식 인수를 허용 하는 작업 및 함수는 해당 역할이 명확 하면 `T` 해당 형식 인수를 나타냅니다.
- 함수나 연산이 여러 형식 인수를 사용 하거나 단일 형식 인수의 역할이 명확 하지 않은 경우 각 형식에 대해 `T` (예: `TOutput`)로 앞에 오는 짧은 대문자 단어를 사용 하는 것이 좋습니다.
- 인수 및 변수 이름에 형식 이름을 포함 하지 마십시오. 이 정보는 개발 환경에서 제공 해야 합니다.
- 리터럴 이름 (`flagQubit`)과 배열 형식 (`measResults`)으로 스칼라 형식을 나타냅니다.
  구체적 비트 배열의 경우에는 이름이 특정 방식으로 밀접 하 게 관련 된 다양 한 비트 시퀀스를 참조 하는 `Register` 하 여 이러한 형식을 나타내는 것이 좋습니다.
- 배열로 인덱스로 사용 되는 변수는 `idx` 시작 해야 하며 단수형 (예: `things[idxThing]`) 이어야 합니다.
  특히 단일 문자 변수 이름을 인덱스로 사용 하지 않는 것이 좋습니다. 최소한 `idx`를 사용 하는 것이 좋습니다.
- 배열의 길이를 포함 하는 데 사용 되는 변수는 `n` 시작 해야 하며 복수화 (예: `nThings`) 이어야 합니다.

# <a name="examplestabexamples"></a>[예](#tab/examples)

***

### <a name="user-defined-type-named-items"></a>사용자 정의 형식 항목 ###

사용자 정의 형식의 명명 된 항목은 UDT 생성자에 대 한 입력에도 `CamelCase`으로 이름이 지정 되어야 합니다.
이를 통해 접근자 표기법 (예: `callable::Apply`) 또는 복사 및 업데이트 표기법 (`set arr w/= Data <- newData`)을 사용할 때 명명 된 항목을 지역 범위 변수에 대 한 참조에서 명확 하 게 구분할 수 있습니다.

# <a name="guidancetabguidance"></a>[지침](#tab/guidance)

다음을 권장 합니다.

- UDT 생성자의 명명 된 항목 이름은 `CamelCase`로 지정 해야 합니다. 즉, 초기 대문자로 시작 해야 합니다.
- 작업으로 확인 되는 명명 된 항목은 동사 단계로 명명 되어야 합니다.
- 작업을 확인 하지 않는 명명 된 항목은 명사 구로 명명 되어야 합니다.
- 작업을 래핑하는 Udt의 경우 `Apply` 라는 단일 명명 된 항목을 정의 해야 합니다.

# <a name="examplestabexamples"></a>[예](#tab/examples)

|   | 살펴보겠습니다 | 설명 |
|---|---------|-------------|
| ☑ | `newtype Oracle = (Apply : Qubit[] => Unit is Adj + Ctl)` | 이름 `Apply`은 `CamelCase`형식의 동사 구로, 명명 된 항목이 작업 임을 제안 합니다. |
| ☒ | <s>`newtype Oracle = (apply : Qubit[] => Unit is Adj + Ctl) `</s> | 명명 된 항목은 초기 대문자로 시작 해야 합니다. |
| ☒ | <s>`newtype Collection = (Length : Int, Get : Int -> (Qubit => Unit)) `</s> | 함수를 확인 하는 명명 된 항목은 동사 구가 아닌 명사 구로 명명 되어야 합니다. |

***

## <a name="input-conventions"></a>입력 규칙 ##

개발자가 작업 또는 함수를 호출 하는 경우 해당 작업 또는 함수에 대 한 다양 한 입력을 특정 순서로 지정 하 여 개발자가 라이브러리를 사용 하기 위해 직면 하 게 되는 인지 부하를 늘려야 합니다.
특히 입력 순서 기억 하는 작업은 일반적으로 퀀텀 알고리즘의 구현 프로그래밍의 작업에서 혼란 스 러가 됩니다.
풍부한 IDE 지원으로 인해이를 매우 광범위 하 게 완화할 수 있지만 일반적인 규칙을 잘 설계 하 고 준수 하는 것은 API에 의해 적용 되는 인지 부하를 최소화 하는 데도 도움이 될 수 있습니다.

가능 하면 작업이 나 함수에 필요한 입력 수를 줄이는 것이 도움이 될 수 있습니다. 그러면 각 입력의 역할이 해당 작업 또는 함수를 호출 하는 개발자와 나중에 해당 코드를 읽는 개발자에 게 더 즉각적으로 표시 됩니다.
특히 작업이 나 함수에 대 한 인수 수를 줄이는 것이 불가능 하거나 적절 하지 않은 경우 입력 순서를 예측할 때 사용자가 직면 하는 갑작스러운 요소를 최소화 하는 일관 된 순서를 지정 하는 것이 중요 합니다.

Currying f (x, y) ≡ f (x) (y)의 일반화로 부분 응용 프로그램의 생각에서 주로 파생 되는 입력 순서 지정 규칙을 권장 합니다.
따라서 첫 번째 인수를 부분적으로 적용 하면 적절 한 경우 항상 적절 한 권한으로 사용할 수 있는 호출 가능이 발생 합니다.
이 원칙에 따라 다음과 같은 인수 순서를 사용 하는 것이 좋습니다.

- 각도, 거듭제곱 벡터 등의 호출 가능 하지 않은 클래식 인수
- 호출 가능 인수 (함수 및 인수)
  함수와 연산이 모두 인수로 사용 되는 경우 함수 뒤에 작업을 배치 하는 것이 좋습니다.
- `Map`, `Iter`, `Enumerate`및 `Fold`와 비슷한 방식으로 호출 가능 인수에 의해 처리 된 컬렉션입니다.
- 컨트롤로 사용 되는 인수입니다.
- 대상으로 사용 되는 인수입니다.

각도와 oracle을 사용 하는 단계 추정에서 사용 하기 위해 `ApplyPhaseEstimationIteration` 하 고, 다른 배율 인수 배열에 의해 수정 된 `Rz` 각도를 전달 하 고, oracle의 응용 프로그램을 제어 하는 작업을 고려 합니다.
`ApplyPhaseEstimationIteration`에 대 한 입력은 다음과 같은 방식으로 정렬 됩니다.

```qsharp
operation ApplyPhaseEstimationIteration(
    angle : Double,
    callable : (Qubit => () is Ctl),
    scaleFactors : Double[],
    controlQubit : Qubit,
    targetQubits : Qubit[]
)
: Unit
...
```
갑작스러운 문제를 최소화 하는 특별 한 경우에는 일부 함수 및 작업이 기본 제공 함수 `Adjoint` 및 `Controlled`의 동작을 모방 합니다.
예를 들어 `ControlledOnInt<'T>`에는 `Controlled` 함수 처럼 작동 하지만 컨트롤 레지스터가 상태 $ \ket{5} = \ket{101}$를 나타내는 조건에서 `ControlledOnInt<Qubit[]>(5, _)` `(Int, ('T => Unit is Adj + Ctl)) => ((Qubit[], 'T) => Unit is Adj + Ctl)`형식이 있습니다.
따라서 개발자는 `ControlledOnInt`에 대 한 입력이 마지막으로 변환 되는 호출을 수행 하 고, 결과 작업에서 `Controlled` 함수의 출력과 동일한 순서를---하는 입력 `(Qubit[], 'T)`으로 간주 합니다.

# <a name="guidancetabguidance"></a>[지침](#tab/guidance)

다음을 권장 합니다.

- 부분 응용 프로그램을 사용 하는 경우 입력 순서 일치를 사용 합니다.
- 기본 제공 함수와 일치 하는 입력 순서을 사용 합니다.
- 모든 기존 입력을 퀀텀 입력 앞에 저장 합니다.

# <a name="examplestabexamples"></a>[예](#tab/examples)

***

## <a name="documentation-conventions"></a>설명서 규칙 ##

Q # 언어를 사용 하면 특수 형식의 문서 주석을 사용 하 여 작업, 함수 및 사용자 정의 형식에 대 한 설명서를 첨부할 수 있습니다.
삼중 슬래시 (`///`)로 표시 되는 이러한 설명서 주석은 각 작업, 함수 및 사용자 정의 형식, 각 작업의 용도를 설명 하는 데 사용할 수 있는 작은 [Docfx-Flavored Markdown](https://dotnet.github.io/docfx/spec/docfx_flavored_markdown.html) 문서입니다.
퀀텀 개발 키트와 함께 제공 되는 컴파일러는 이러한 주석을 추출 하 고이를 사용 하 여 https://docs.microsoft.com/quantum 와 비슷한 설명서를 조판 합니다.
마찬가지로, 퀀텀 개발 키트와 함께 제공 되는 언어 서버는 이러한 주석을 사용 하 여 사용자가 Q # 코드에서 기호를 마우스로 가리킬 때 사용자에 게 도움을 제공 합니다.
따라서 문서 주석을 사용 하면이 문서의 다른 규칙을 사용 하 여 쉽게 표현 되지 않는 세부 정보에 대 한 유용한 참조를 제공 하 여 사용자가 코드를 이해 하는 데 도움이 될 수 있습니다.

<div class="nextstepaction">
    [문서 주석 구문 참조](xref:microsoft.quantum.language.statements#documentation-comments)
</div>

이 기능을 효과적으로 사용 하 여 사용자를 돕기 위해 문서 주석을 작성할 때 몇 가지 사항을 염두에 두어야 합니다.

# <a name="guidancetabguidance"></a>[지침](#tab/guidance)

다음을 권장 합니다.

- 각 public 함수, 작업 및 사용자 정의 형식은 문서 주석 바로 앞에와 야 합니다.
- 최소한 각 문서 주석에는 다음 섹션이 포함 되어 있어야 합니다.
    - 요약
    - 입력
    - 출력 (해당 하는 경우)
- 모든 요약이 두 문장 이내 인지 확인 합니다. 더 많은 공간이 필요한 경우 전체 세부 정보를 `# Summary` 바로 다음에 `# Description` 섹션을 제공 하세요.
- 모든 클라이언트에서 요약에 TeX 표기법을 지 원하는 것이 아니라 적절 한 경우 요약에 수학을 포함 하지 마세요. Prose 문서를 작성 하는 경우 (예: TeX 또는 Markdown) 더 긴 줄 길이를 사용 하는 것이 더 적합할 수 있습니다.
- `# Description` 섹션에서 관련 된 모든 수학 식을 제공 합니다.
- 입력을 설명할 때 컴파일러에서 유추할 수 있는 각 입력의 형식과 불일치를 발생 하는 위험을 반복 해 서는 안 됩니다.
- 각각의 `# Example` 섹션에서 적절 한 예제를 제공 합니다.
- 코드를 나열 하기 전에 각 예제를 간략하게 설명 합니다.
- `# References` 섹션에서 관련 된 모든 교육 기관 게시 (예: 용지, proceedings of the, 블로그 게시물 및 대체 구현)를 링크의 글머리 기호 목록으로 인용 합니다.
- 가능 하면 모든 인용 링크가 영구적이 고 변경할 수 없는 식별자 (DOIs 또는 버전이 지정 된 arXiv 번호)에 해당 하는지 확인 합니다.
- 작업 또는 함수가 함수 변형의 다른 작업 또는 함수와 관련 된 경우 `# See Also` 섹션에서 다른 변형을 글머리 기호로 나열 합니다.
- 수준-1 (`/// #`) 섹션 사이에 빈 주석 줄을 그대로 두고 수준 2 (`/// ##`) 섹션 사이에 빈 줄을 남겨 두지 않습니다.

# <a name="examplestabexamples"></a>[예](#tab/examples)

#### <a name=""></a>☑ ####

```
/// # Summary
/// Applies a rotation about the X-axis by a given angle.
///
///
/// # Description
/// This operation rotates a single qubit by the unitary operation
/// \begin{align}
///     R_x(\theta) \mathrel{:=} e^{-i \theta \sigma_x / 2}.
/// \end{align}
///
/// # Input
/// ## theta
/// Angle about which the qubit is to be rotated.
/// ## qubit
/// Qubit to which the gate should be applied.
///
/// # Remarks
/// Equivalent to:
/// ```qsharp
/// R(PauliX, theta, qubit);
/// ```
///
/// # See Also
/// - Ry
/// - Rz
operation Rx(theta : Double, qubit : Qubit) : Unit
is Adj + Ctl {
    body (...) { R(PauliX, theta, qubit); }
    adjoint (...) { R(PauliX, -theta, qubit); }
}
```

***

## <a name="formatting-conventions"></a>서식 지정 규칙 ##

앞의 제안 사항 외에도 일관 된 서식 지정 규칙을 사용 하는 코드를 가능한 한 이해 하기 쉽게 만드는 데 도움이 됩니다.
이러한 서식 지정 규칙은 본질적으로 임의로 임의적 이며 개인용 미관에 게 매우 강력 합니다.
그럼에도 불구 하 고 작업자 그룹 내에 일관 된 형식 지정 규칙 집합을 유지 하는 것이 좋습니다. 특히 퀀텀 개발 키트와 같은 초대형 Q # 프로젝트의 경우에는 특히 그렇습니다.
이러한 규칙은 Q # 컴파일러와 통합 된 서식 도구를 사용 하 여 자동으로 적용할 수 있습니다.

# <a name="guidancetabguidance"></a>[지침](#tab/guidance) 

다음을 권장 합니다.

- 이식성을 위해 탭 대신 4 개의 공백을 사용 합니다.
  예를 들어 VS Code에서 다음을 수행 합니다.
  ```json
    "editor.insertSpaces": true,
    "editor.tabSize": 4
  ```
- 줄 바꿈이 적당 한 79 문자입니다.
- 이항 연산자 주위의 공백을 사용 합니다.
- 형식 주석에 사용 되는 콜론의 양쪽에 공백을 사용 합니다.
- 배열 및 튜플 리터럴 (예: 함수 및 작업에 대 한 입력)에서 쉼표 뒤에 사용 되는 단일 공백을 사용 합니다.
- 함수, 작업 또는 UDT 이름 뒤에 공백을 사용 하거나 특성 선언에서 `@` 뒤에 공백을 사용 하지 마십시오.
- 각 특성 선언은 별도의 줄에 있어야 합니다.

# <a name="examplestabexamples"></a>[예](#tab/examples)

|   | 살펴보겠습니다 | 설명 |
|---|---------|-------------|
| ☒ | <s>`2+3`</s> | 이항 연산자 주위의 공백을 사용 합니다. |
| ☒ | <s>`target:Qubit`</s> | 형식 주석 콜론 앞뒤에 공백을 사용 합니다. |
| ☑ | `Example(a, b, c)` | 입력 튜플의 항목은 가독성을 위해 정확 하 게 배치 됩니다. |
| ☒ | <s>`Example (a, b, c)`</s> | 함수, 작업 또는 UDT 이름 뒤에는 공백을 표시 하지 않아야 합니다. |

***

