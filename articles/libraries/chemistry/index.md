---
title: 양자 화학 패키지 소개 | Microsoft Docs
description: 양자 화학 패키지 소개
author: QuantumWriter
ms.author: Alan.Geller@microsoft.com
ms.date: 12/11/2017
ms.topic: article
uid: microsoft.quantum.chemistry.concepts.intro
ms.openlocfilehash: e5a9dd70874f1ae0baf4b781346278195a980a7e
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2019
ms.locfileid: "72960414"
---
# <a name="introduction-to-the-quantum-chemistry-library"></a>양자 화학 라이브러리 소개

물리적 시스템의 시뮬레이션은 양자 컴퓨팅에서 오랫 동안 중요한 역할을 수행해 왔습니다.  양자 동역학이 양자 컴퓨터에서 시뮬레이트하기 어려운 분야라고 널리 인식되어 왔기 때문입니다. 즉, 이 시스템의 시뮬레이트 복잡성은 양자 시스템 규모에 따라 기학급수적으로 높아집니다.  화학 및 재료 과학의 시뮬레이트 문제점은 양자 컴퓨팅의 가장 유용한 응용 분야에서도 나타나며, 이로 인해 우리의 측정 또는 시뮬레이트 능력을 벗어나는 화학 반응 메커니즘을 분석해야 할 수도 있습니다.  또한 고온의 초전도체와 같은 상호 연관된 전자 재료를 시뮬레이트해야 할 수도 있습니다. 이 우주 내에서의 응용 범주는 광범위합니다.

이 설명서는 사용자들이 우주 내에서 해밀토니안 시뮬레이션 라이브러리의 여러 측면에 수행하는 역할을 이해하도록 지원하기 위해 양자 컴퓨터의 전자 구조 문제를 시뮬레이트하는 방법을 간단히 소개합니다.  먼저 양자 메커니즘을 간략히 소개한 후, 전자 시스템이 모델링되는 방식을 살펴봅니다.  그런 다음, 양자 컴퓨터를 사용하여 이러한 양자 동역할을 에뮬레이트하는 방법을 설명합니다.  이 작업이 완료되면 양자 동역할을 기본 게이트 시퀀스로 컴파일하는 데 사용되는 다음 두 가지 방법을 설명할 것입니다. Trotter-Suzuki 분해 및 양자화
