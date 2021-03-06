---
title: Broombridge 스키마 사양
author: guanghaolow
ms.author: gulow@microsoft.com
ms.date: 05/28/2019
ms.topic: article
uid: microsoft.quantum.libraries.chemistry.schema.spec_v_0_2
ms.openlocfilehash: 2f4be96bc6f1e8e6fe21b93bc0d9ab2aa367fd53
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73185310"
---
# <a name="broombridge-specification-v02"></a>Broombridge 사양 v 0.2 #

이 문서에서 "REQUIRED", "NOT", "REQUIRED", "be", "not", "REQUIRED", "be", "REQUIRED", "be" 및 "OPTIONAL"은 [RFC 2119](https://tools.ietf.org/html/rfc2119)에 설명 된 대로 해석 됩니다.

"참고", "정보" 또는 "경고"와 같은 제목이 있는 모든 사이드바는 정보를 제공 합니다.

## <a name="introduction"></a>소개 ##

이 섹션은 정보를 제공 합니다.

Broombridge 문서는 퀀텀 시뮬레이션 및 프로그래밍 도구 체인을 사용 하 여 처리 하기 위해 퀀텀 화학의 시뮬레이션 문제를 전달 하기 위한 것입니다.

## <a name="serialization"></a>직렬화 ##

이 섹션은 규범입니다.

Broombridge 문서는 [RFC 4627](https://tools.ietf.org/html/rfc4627) 섹션 2.2에 설명 된 대로 JSON 개체를 나타내는 [yaml 1.2 문서로](http://yaml.org/spec/) serialize 되어야 합니다.
YAML로 serialize 된 개체에는 값이 `"https://raw.githubusercontent.com/Microsoft/Quantum/master/Chemistry/Schema/qchem-0.2.schema.json"`되 고 JSON 스키마 초안-06 사양 [[1](https://tools.ietf.org/html/draft-wright-json-schema-01), [2](https://tools.ietf.org/html/draft-wright-json-schema-validation-01)]에 따라 유효 해야 하는 속성 `"$schema"` 있어야 합니다.

이 사양의 나머지 부분에서는 "Broombridge 개체"가 Broombridge YAML 문서에서 deserialize 된 JSON 개체를 참조 합니다.

별도로 명시 하지 않는 한 개체에는이 문서에서 명시적으로 지정 된 속성 이외의 추가 속성을 포함 해서는 안 됩니다.

## <a name="additional-definitions"></a>추가 정의 ##

이 섹션은 규범입니다.

### <a name="quantity-objects"></a>Quantity 개체 ###

이 섹션은 규범입니다.

_Quantity 개체_ 는 JSON 개체이 고 해당 값이 표 1에 나열 된 허용 되는 값 중 하나인 속성 `units` 있어야 합니다.

Quantity 개체는 `units` 속성 외에도 `value` 단일 속성을 포함 하는 _단순 수량 개체_ 입니다.
`value` 속성의 값은 숫자 여야 합니다.

Quantity 개체는 `units` 속성 외에도 `lower` 및 `upper` 속성이 있는 경우 _제한 된 수량 개체_ 입니다.
`lower` 및 `upper` 속성의 값은 숫자 여야 합니다.
제한 된 수량 개체에는 값이 숫자 인 속성 `value` 있을 수 있습니다.

Quantity 개체는 속성 `format` 있고 속성 `values` `units` 속성 외에도 있는 경우 _스파스 배열 수량 개체_ 입니다.
`format` 값은 `sparse`문자열 이어야 합니다.
`values` 속성의 값은 배열 이어야 합니다.
`values`의 각 요소는 스파스 배열 수량의 인덱스 및 값을 나타내는 배열 이어야 합니다.

스파스 배열 수량 개체의 각 요소에 대 한 인덱스는 전체 스파스 배열 수량 개체에서 고유 해야 합니다.
`0`값이 포함 된 인덱스가 있는 경우 파서는 스파스 배열 수량 개체를 해당 인덱스가 전혀 없는 스파스 배열 수량 개체와 동일 하 게 처리 해야 합니다.


Quantity 개체는 다음 중 하나 여야 합니다.

- 단순 수량 개체
- 제한 된 수량 개체 또는
- 스파스 배열 수량 개체입니다.


### <a name="examples"></a>예시 ###

이 섹션은 정보를 제공 합니다.

$1.9844146837\,\mathrm{Ha} $를 나타내는 단순 수량입니다.

```yaml
coulomb_repulsion:
    value: 1.9844146837
    units: hartree
```

간격 $ [-7,-6]\,\mathrm{Ha} $에 대 한 균일 분포를 나타내는 제한 된 수량입니다.

```yaml
fci_energy:
    upper: -6
    lower: -7
    units: hartree
```

다음은 요소가 `hello`와 동일 `[1, 2]` 스파스 배열 수량과 `world`와 같은 요소 `[3, 4]`입니다.

```yaml
sparse_example:
    format: sparse
    units: hartree
    values:
    - [1, 2, "hello"]
    - [3, 4, "world"]
```

## <a name="format-section"></a>서식 섹션 ##

이 섹션은 규범입니다.

Broombridge 개체에는 값이 `version`라는 하나의 속성이 있는 JSON 개체인 속성 `format` 있어야 합니다.
`version` 속성에 `"0.2"`값이 있어야 합니다.

### <a name="example"></a>예제 ###

이 섹션은 정보를 제공 합니다.

```yaml
format:                        # required
    version: "0.2"             # must match exactly
```

## <a name="problem-description-section"></a>문제 설명 섹션 ##

이 섹션은 규범입니다.

Broombridge 개체에는 값이 JSON 배열인 속성 `problem_description` 있어야 합니다.
`problem_description` 속성 값의 각 항목은이 섹션의 나머지 부분에 설명 된 대로 하나의 정수 집합을 설명 하는 JSON 개체 여야 합니다.
이 섹션의 나머지 부분에서 "문제 설명 개체" 라는 용어는 Broombridge 개체의 `problem_description` 속성 값에 있는 항목을 참조 합니다.

각 문제 설명 개체에는 해당 값이 JSON 개체인 속성 `metadata` 있어야 합니다.
`metadata` 값은 빈 JSON 개체 (`{}`) 이거나 구현자에서 정의 된 추가 속성을 포함할 수 있습니다.

### <a name="hamiltonian-section"></a>Hamiltonian 섹션 ###

#### <a name="overview"></a>개요 ####

이 섹션은 정보를 제공 합니다.

각 문제 설명 개체의 `hamiltonian` 속성은 특정 퀀텀 화학 문제에 대 한 Hamiltonian에 대 한 설명으로, 한 개 및 두 개의 본문 용어를 실수의 스파스 배열로 나열 합니다.
각 문제 설명 개체에서 설명 하는 Hamiltonian 연산자는 다음 형식을 사용 합니다.

$ $ H = \sum\_\{i, j\}\sum\_{\sigma\in\\{\uparrow, \down화살표\\}} H\_\{ij\} a ^\{\aa\}\_{i , \sigma} a\_{j, \sigma} + \frac{1}{2}\sum\_\{i, j, k, l\}\sum\_{\시그마, \rho\in\\{\uparrow, \frac\\}} h\_{ijkl} a ^ \\_{i , \sigma} a ^ \dagger\_{k, \rho} a\_{l, \rho} a\_{j,, $ $

여기에서 _ {ijkl} = (ij | kl) $ in Mulliken 규칙을 $h 합니다.

명확 하 게 하기 위해 1-전자 용어는

$ $ h_ {ij} = \int {\mathrm d} x \int ^ *\_i (x) \int (\frac{1}{2}\nabla ^ 2 + \int\_{A} \frac{Z\_A} {| x-x\_A |}  \right) \right\_j (x), $ $

그리고 두 전자 단어는

$ $ h\_\{ijkl\} = \iint \{\mathrm d\}x ^ 2 \psi ^\{\*\}\_\_i (x\_1) \psi\_j (x\{1) \iint 1\}\{\|x\_1-x\_2\|\}\psi\_k ^\{\*\}(x\_2) \psi\_l (x\_2).
$$

`integral_sets` 속성의 각 요소에 대 한 [`basis_set` 속성](#basis-set-object) 에 대 한 설명에 설명 된 대로, 사용 되는 기본 함수는 실제 값 이라고 명확 하 게 가정 합니다.
이를 통해 용어 사이에 다음 symmetries를 사용 하 여 Hamiltonian 표현을 압축할 수 있습니다.

$ $ h_ {ijkl} = h_ {ijlk} = h_ {jikl} = h_ {jilk} = h_ {klij} = h_ {klji} = h_ {lkij} = h_ {lkji}.
$$


#### <a name="contents"></a>콘텐츠 ####

이 섹션은 규범입니다.

각 문제 설명 개체에는 해당 값이 JSON 개체인 속성 `hamiltonian` 있어야 합니다.
`hamiltonian` 속성의 값은 Hamiltonian 개체 라고 하며,이 섹션의 나머지 부분에 설명 된 대로 `one_electron_integrals` 및 `two_electron_integrals` 속성이 있어야 합니다.

각 문제 설명 개체에는 값이 단순 수량 개체 인 속성 `coulomb_repulsion` 있어야 합니다.
각 문제 설명 개체에는 값이 단순 수량 개체 인 속성 `energy_offet` 있어야 합니다.
> 두고 `coulomb_repulsion` 및 `energy_offet` 값을 함께 추가 하 여 Hamiltonian의 id 용어를 캡처합니다.

##### <a name="one-electron-integrals-object"></a>1-전자 정수 개체 #####

이 섹션은 규범입니다.

Hamiltonian 개체의 `one_electron_integrals` 속성은 인덱스가 두 정수이 고 해당 값이 숫자인 스파스 배열 수량 이어야 합니다.
모든 용어에는 `i >= j``[i, j]` 인덱스가 있어야 합니다.

> 두고 이는 Hamiltonian가 Hermitian 임을 나타내는 _ {ij} = h_ {ji} $ $h 하는 대칭을 반영 합니다.


###### <a name="example"></a>예제 ######

이 섹션은 정보를 제공 합니다.

다음 스파스 배열 수량은 Hamiltonian $ $ H = \left (-5.0 (a ^\{\left\}\_{1, \uparrow} a\_{1, \uparrow} + a ^\{\left\}\_{1, a\_{1입니다. , \downarrow}) + 0.17 (a ^\{\dagger\}\_{2, \uparrow} a\_{1, \uparrow} + a ^\{\dagger\}\_{1, \uparrow} a\_{2, + a ^\{\dagger\}\_{2 , \downarrow} a\_{1, \downarrow} + a ^\{\dagger\}\_{1, \downarrow} a\_{2, \downarrow}) \dagger)\\,
$$

```yaml
one_electron_integrals:     # required
    units: hartree          # required
    format: sparse          # required
    values:                 # required
        # i j f(i,j)
        - [1, 1, -5.0]
        - [2, 1,  0.17]
```
> [!NOTE]
> Broombridge는 1부터 기반으로 하는 인덱싱을 사용 합니다.


##### <a name="two-electron-integrals-object"></a>2-전자 정수 개체 #####

이 섹션은 규범입니다.

Hamiltonian 개체의 `two_electron_integrals` 속성은 `index_convention`라는 하나 이상의 추가 속성이 있는 스파스 배열 수량 이어야 합니다.
`two_electron_integrals` 값의 각 요소에는 네 개의 인덱스가 있어야 합니다.

각 `two_electron_integrals` 속성에는 `index_convention` 속성이 있어야 합니다.
`index_convention` 속성의 값은 표 1에 나열 된 허용 되는 값 중 하나 여야 합니다.
`index_convention` 값이 `mulliken`되는 경우에는 `two_electron_integrals` 스파스 배열 수량의 각 요소에 대해 Broombridge 문서를 로드 하는 파서는 두 전자 $h 연산자 (_ {i, j, k, l} a ^ \dagger_i a ^ \dagger_j a_k a_l $)와 같은 Hamiltonian 항을 인스턴스화해야 합니다. , 여기서 $i $, $j $, $k $ 및 $l $는 값의 정수 여야 하며, 여기서 $h _ {i, j, k, l} $은 스파스 배열 수량의 요소 `[i, j, k, l, h(i, j, k, l)]`입니다.

###### <a name="symmetries"></a>Symmetries ######

이 섹션은 규범입니다.

`two_electron_integrals` 개체의 `index_convention` 속성이 `mulliken`와 같으면 인덱스가 `[i, j, k, l]` 인 요소가 있는 경우 다음 인덱스는 `[i, j, k, l]`와 같지 않은 경우에는 없어야 합니다.

- `[i, j, l, k]`
- `[j, i, k, l]`
- `[j, i, l, k]`
- `[k, l, i, j]`
- `[k, l, j, i]`
- `[l, k, j, i]`

> [!NOTE]
> `index_convention` 속성이 스파스 수량 개체 이기 때문에 다른 요소에 대해 인덱스가 반복 될 수 없습니다.
> 특히 `[i, j, k, l]` 인덱스를 사용 하는 요소가 있는 경우 다른 요소는 해당 인덱스를 가질 수 없습니다.


<!-- h_{ijkl} = h_{ijlk}=h_{jikl}=h_{jilk}=h_{klij}=h_{klji}=h_{lkji}. -->

###### <a name="example"></a>예제 #######

이 섹션은 정보를 제공 합니다.

다음 개체는 Hamiltonian를 지정 합니다.

$ $ H = \frac12 \sum\_{\sum, \rho\in\\{\uparrow, \downix\\}} \sum \dagger} (1.6 a ^ {\dagger}\_{1, \rho} a ^ {\rho}\_{1, \sigma}-a\_{1, \dagger} a\_{1, 0.1 a ^ {\_{6 , \sigma} a ^ {\dagger}\_{1, \rho} a\_{3, \rho} a\_{2, \sigma}-0.1 a ^ {\dagger}\_{6, \sigma} a ^ {\dagger}\_{1, \rho} a\_{2, \rho} a\_{3 , \sigma}-0.1 a ^ {\dagger}\_{1, \sigma} a ^ {\dagger}\_{6, \rho} a\_{3, \rho} a\_{2, \sigma}-0.1 a ^ {\dagger}\_{1, \sigma} a ^ {\dagger}\_{6, \rho} a\_{2 , \rho}\_{3, \sigma} $ $ $ $-0.1 a ^ {\dagger}\_{3, \sigma} a ^ {\dagger}\_{2, \rho} a\_{6, \rho} a\_{1, \sigma}-0.1 a ^ {\dagger}\_{3, \sigma} a ^ {\dagger}\_{2 , \rho} a\_{1, \rho} a\_{6, \sigma}-0.1 a ^ {\dagger}\_{2, \sigma} a ^ {\dagger}\_{3, \rho} a\_{6, \rho} a\_{1, \sigma}-0.1 a ^ {\dagger}\_{2 , \sigma} a ^ {\dagger}\_{3, \rho} a\_{1, \rho} a\_{6, \sigma}\Biggr)\\, \textrm{Ha}.
$$

```yaml
two_electron_integrals:
    index_convention: mulliken
    units: hartree
    format: sparse
    values:
        - [1, 1, 1, 1,  1.6]
        - [6, 1, 3, 2, -0.1]
```

### <a name="initial-state-section"></a>초기 상태 섹션 ###

이 섹션은 규범입니다.

값이 JSON 배열인 `initial_state_suggestion` 개체는 지정 된 Hamiltonian에 대 한 관심의 초기 퀀텀 상태를 지정 합니다. `initial_state_suggestion` 속성 값의 각 항목은이 섹션의 나머지 부분에 설명 된 대로 하나의 퀀텀 상태를 설명 하는 JSON 개체 여야 합니다.
이 섹션의 나머지 부분에서 "상태 개체" 라는 용어는 Broombridge 개체의 `initial_state_suggestion` 속성 값에 있는 항목을 참조 합니다.

#### <a name="state-object"></a>상태 개체 ####

이 섹션은 규범입니다.

각 상태 개체에는 문자열을 포함 하는 `label` 속성이 있어야 합니다. 각 상태 개체에는 `method` 속성이 있어야 합니다. `method` 속성의 값은 표 3에 나열 된 허용 되는 값 중 하나 여야 합니다.
각 상태 개체에는 값이 단순 수량 개체 여야 하는 `energy` 속성이 있을 수 있습니다.

`method` 속성의 값이 `sparse_multi_configurational`인 경우 상태 개체에는 기본 상태 배열과 정규화 되지 않은 amplitudes을 포함 하는 `superposition` 속성이 있어야 합니다.

예를 들어 초기 상태 $ $ \ket{G0} = \ket{G1} = \ket{G2} = (a ^ {\dagger}\_{1, \uparrow}a ^ {\dagger}\_{2, \uparrow}a ^ {\dagger}\_{2, \downarrow}) \ket{0} $ $ $ $ \ket{E} = \frac{0.1 (a ^ {\dagger}\_{1) , \uparrow}a ^ {\dagger}\_{2, \uparrow}a ^ {\dagger}\_{2, \downarrow}) + 0.2 (a ^ {\dagger}\_{1, \uparrow}a ^ {\dagger}\_{3, \uparrow}a ^ {\dagger}\_{2, \downarrow})} {\sqrt{| 0.1 | ^ 2 + | 0.2 | ^ 2}} \ket{0}, $ $ where $ \ket{E} $에는 에너지 $0.987 \textrm{Ha} $가 표시 됩니다.
```yaml
initial_state_suggestions: # optional. If not provided, spin-orbitals will be filled to minimize one-body diagonal term energies.
  - label: "|G0>"
    method: sparse_multi_configurational
    superposition:
      - [1.0, "(1a)+","(2a)+","(2b)+","|vacuum>"]
  - label: "|G1>"
    method: sparse_multi_configurational
    superposition:
      - [-1.0, "(2a)+","(1a)+","(2b)+","|vacuum>"]
  - label: "|G2>"
    method: sparse_multi_configurational
    superposition:
      - [1.0, "(3a)","(1a)+","(2a)+","(3a)+","(2b)+","|vacuum>"]
  - label: "|E>"
    energy: {units: hartree, value: 0.987}
    method: sparse_multi_configurational
    superposition:
      - [0.1, "(1a)+","(2a)+","(2b)+","|vacuum>"]
      - [0.2, "(1a)+","(3a)+","(2b)+","|vacuum>"]
```

`method` 속성의 값이 `unitary_coupled_cluster`인 경우 상태 개체에는 JSON 개체인 값을 갖는 `cluster_operator` 속성이 있어야 합니다.
JSON 개체에는 값이 기본 상태 인 `reference_state` 속성이 있어야 합니다.
JSON 개체에는 값이 하나의 본문 클러스터 연산자와 해당 amplitudes 인 `one_body_amplitudes` 속성이 있을 수 있습니다.
JSON 개체에는 두 개의 본문 클러스터 연산자와 해당 amplitudes의 배열인 값을 가진 `two_body_amplitudes` 속성이 있을 수 있습니다.
기반 상태의 배열과 정규화 되지 않은 amplitudes을 포함 하는입니다.

예를 들어 상태 $ $ \ket{\text{reference}} = (a ^ {\dagger}\_{1, \uparrow}a ^ {\dagger}\_{2, \uparrow}a ^ {\dagger}\_{2, \downarrow}) \ket{0}, $ $

$ $ \ket{\text{UCCSD}} = e ^ {T-T ^ \dagger}\ket{\text{reference}}, $ $

$ $ T = 0.1 a ^ {\dagger}\_{3, \uparrow}a\_{2, \downarrow} + 0.2 a ^ {\dagger}\_{2, \uparrow}a\_{2, \downarrow}-0.3 a ^ {\dagger}\_{1, \uparrow}a ^ {\dagger}\_{3, \downarrow}a\_{3 , \uparrow}a\_{2, \downarrow} $ $는로 표시 됩니다.
```yaml
initial_state_suggestions: # optional. If not provided, spin-orbitals will be filled to minimize one-body diagonal term energies.
  - label: "UCCSD"
    method: unitary_coupled_cluster
    cluster_operator: # Initial state that cluster operator is applied to.
        reference_state: 
          [1.0, "(1a)+", "(2a)+", "(2b)+", '|vacuum>']
        one_body_amplitudes: # A one-body cluster term is t^{q}_{p} a^\dag_p a_q   
            - [0.1, "(3a)+", "(2b)"]
            - [-0.2, "(2a)+", "(2b)"]
        two_body_amplitudes: # A two-body unitary cluster term is t^{rs}_{pq} a^\dag_p a^\dag_q a_r a_s
            - [-0.3, "(1a)+", "(3b)+", "(3a)", "(2b)"]
```

#### <a name="basis-set-object"></a>기본 설정 개체 ####

이 섹션은 규범입니다.

각 문제 설명 개체에 `basis_set` 속성이 있을 수 있습니다.
`basis_set` 속성 값이 있는 경우 `type` 및 `name`라는 두 개의 속성이 있는 개체 여야 합니다.

`basis_set` 속성 값으로 식별 되는 기본 함수는 실제 값 이어야 합니다.

> [!NOTE]
> 이 사양의 이후 버전에서는 모든 기본 함수가 실제 값 이라고 가정 합니다.

## <a name="tables-and-lists"></a>테이블 및 목록 ##

### <a name="table-1-allowed-physical-units"></a>표 1. 허용 된 물리적 단위 ###

이 섹션은 규범입니다.

단위를 지정 하는 문자열은 다음 중 하나 여야 합니다.

- `hartree`
- `ev`

파서 및 생산자는 다음과 같은 단순 수량 개체를 동일 하 게 처리 해야 합니다.

```yaml
- {"units": "hartree", "value": 1}
- {"units": "ev", "value": 27.2113831301723}
```

### <a name="table-2-allowed-index-conventions"></a>표 2. 허용 되는 인덱스 규칙 ###

이 섹션은 규범입니다.

인덱스 규칙을 지정 하는 문자열은 다음 중 하나 여야 합니다.

- `mulliken`

이 섹션은 정보를 제공 합니다.

이 사양의 이후 버전에는 추가 인덱스 규칙이 도입 될 수 있습니다.

#### <a name="interpretation-of-index-conventions"></a>인덱스 규칙의 해석 ####

이 섹션은 정보를 제공 합니다.

### <a name="table-3-allowed-state-methods"></a>표 3. 허용 되는 상태 메서드 ###

이 섹션은 규범입니다.

상태 메서드를 지정 하는 문자열은 다음 중 하나 여야 합니다.

- `sparse_multi_configurational`
- `unitary_coupled_cluster`

이 섹션은 정보를 제공 합니다.

추가 상태 메서드는이 사양의 이후 버전에서 도입 될 수 있습니다.
