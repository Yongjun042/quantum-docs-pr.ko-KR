---
title: Q# 표준 라이브러리 - 소개 | Microsoft Docs
description: Q# 표준 라이브러리 - 소개
author: QuantumWriter
ms.author: martinro@microsoft.com
ms.date: 12/11/2017
ms.topic: article
uid: microsoft.quantum.libraries.standard.intro
ms.openlocfilehash: 547f4f6066e3ead627cd2a5970b1555999e988bb
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73056375"
---
# <a name="introduction-to-the-q-standard-libraries"></a><span data-ttu-id="e4463-103">Q# 표준 라이브러리 소개</span><span class="sxs-lookup"><span data-stu-id="e4463-103">Introduction to the Q# Standard Libraries</span></span> #

<span data-ttu-id="e4463-104">Q#은 Q# *표준 라이브러리*를 구성하는 다양한 유용한 연산, 함수 및 사용자 정의 형식에 의해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4463-104">Q# is supported by a range of different useful operations, functions, and user-defined types that comprise the Q# *standard libraries*.</span></span>
<span data-ttu-id="e4463-105">[설치 및 유효성 검사](xref:microsoft.quantum.install) 중에 설치되는 [`Microsoft.Quantum.Development.Kit` NuGet 패키지](https://www.nuget.org/packages/microsoft.quantum.development.kit)는 Q# 컴파일러 및 대상 컴퓨터에서 구현되는 표준 라이브러리의 일부를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4463-105">The [`Microsoft.Quantum.Development.Kit` NuGet package](https://www.nuget.org/packages/microsoft.quantum.development.kit) installed during [installation and validation](xref:microsoft.quantum.install) provides the Q# compiler, and parts of the standard library that are implemented by the target machines.</span></span>
<span data-ttu-id="e4463-106">[`Microsoft.Quantum.Standard` 패키지](https://www.nuget.org/packages/microsoft.quantum.standard)는 대상 컴퓨터에서 이식 가능한 Q# 표준 라이브러리의 일부를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4463-106">The [`Microsoft.Quantum.Standard` package](https://www.nuget.org/packages/microsoft.quantum.standard) provides the portion of the Q# standard libraries that are portable across target machines.</span></span>

<span data-ttu-id="e4463-107">Q# 표준 라이브러리에서 정의되는 기호는 [API 설명서](xref:microsoft.quantum.standardlibsintro)에서 훨씬 더 광범위하고 자세하게 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4463-107">The symbols defined by the Q# standard libraries are defined in much greater and more exhaustive detail in the [API documentation](xref:microsoft.quantum.standardlibsintro).</span></span>

<span data-ttu-id="e4463-108">다음 섹션에서는 각 표준 라이브러리 부분에서 가장 두드러진 몇 가지 기능을 간략하게 설명하고 각 기능을 사용하는 방법에 대한 몇 가지 컨텍스트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e4463-108">In the following sections, we will outline the most salient features of each part of the standard library and provide some context about how each feature might be used in practice.</span></span>