---
title: 'Q # 기술-테스트 및 디버깅 | Microsoft Docs'
description: 'Q # 기술-테스트 및 디버깅'
author: tcNickolas
ms.author: mamykhai@microsoft.com
uid: microsoft.quantum.techniques.testing-and-debugging
ms.date: 12/11/2017
ms.topic: article
ms.openlocfilehash: 25679331f1bed9f98b86c6eb20f511c891bac1af
ms.sourcegitcommit: 8becfb03eb60ba205c670a634ff4daa8071bcd06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2019
ms.locfileid: "73183491"
---
# <a name="testing-and-debugging"></a><span data-ttu-id="ae0f3-103">테스트 및 디버깅</span><span class="sxs-lookup"><span data-stu-id="ae0f3-103">Testing and Debugging</span></span>

<span data-ttu-id="ae0f3-104">기존 프로그래밍과 마찬가지로 퀀텀 프로그램이 의도 한 대로 작동 하는지 확인 하 고 잘못 된 퀀텀 프로그램을 진단할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-104">As with classical programming, it is essential to be able to check that quantum programs act as intended, and to be able to diagnose a quantum program that is incorrect.</span></span>
<span data-ttu-id="ae0f3-105">이 섹션에서는 퀀텀 프로그램 테스트 및 디버깅을 위해 Q #에서 제공 하는 도구를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-105">In this section, we cover the tools offered by Q# for testing and debugging quantum programs.</span></span>

## <a name="unit-tests"></a><span data-ttu-id="ae0f3-106">단위 테스트</span><span class="sxs-lookup"><span data-stu-id="ae0f3-106">Unit Tests</span></span>

<span data-ttu-id="ae0f3-107">클래식 프로그램을 테스트 하는 일반적인 방법 중 하나는 라이브러리에서 코드를 실행 하 고 해당 출력을 예상 출력과 비교 하는 *단위 테스트* 라는 작은 프로그램을 작성 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-107">One common approach to testing classical programs is to write small programs called *unit tests* which run code in a library and compare its output to some expected output.</span></span>
<span data-ttu-id="ae0f3-108">예를 들어 $2 ^ 2 = $4 *apriori* 을 알고 있으므로 `Square(2)`에서 `4`를 반환 하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-108">For instance, we may want to ensure that `Square(2)` returns `4`, since we know *a priori* that $2^2 = 4$.</span></span>

<span data-ttu-id="ae0f3-109">Q #은 퀀텀 프로그램에 대 한 단위 테스트 만들기를 지원 하 고 [Xunit](https://xunit.github.io/) 단위 테스트 프레임 워크 내에서 테스트로 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-109">Q# supports creating unit tests for quantum programs, and which can be executed as tests within the [xUnit](https://xunit.github.io/) unit testing framework.</span></span>

### <a name="creating-a-test-project"></a><span data-ttu-id="ae0f3-110">테스트 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ae0f3-110">Creating a Test Project</span></span>

#### <a name="visual-studio-2019tabtabid-vs2019"></a>[<span data-ttu-id="ae0f3-111">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="ae0f3-111">Visual Studio 2019</span></span>](#tab/tabid-vs2019)

<span data-ttu-id="ae0f3-112">Visual Studio 2019를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-112">Open Visual Studio 2019.</span></span> <span data-ttu-id="ae0f3-113">`File` 메뉴로 이동 하 여 `New` > `Project...`를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-113">Go to the `File` menu and select `New` > `Project...`.</span></span>
<span data-ttu-id="ae0f3-114">프로젝트 템플릿 탐색기의 `Installed` > `Visual C#`에서 `Q# Test Project` 템플릿을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-114">In the project template explorer, under `Installed` > `Visual C#`, select the `Q# Test Project` template.</span></span>

#### <a name="command-line--visual-studio-codetabtabid-vscode"></a>[<span data-ttu-id="ae0f3-115">명령줄/Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ae0f3-115">Command Line / Visual Studio Code</span></span>](#tab/tabid-vscode)

<span data-ttu-id="ae0f3-116">선호 하는 명령줄에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-116">From your favorite command line, run the following command:</span></span>
```bash
$ dotnet new xunit -lang Q# -o Tests
$ cd Tests
$ code . # To open in Visual Studio Code
```

****

<span data-ttu-id="ae0f3-117">두 경우 모두 새 프로젝트에는 두 개의 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-117">In either case, your new project will have two files open.</span></span>
<span data-ttu-id="ae0f3-118">첫 번째 파일인 `Tests.qs`는 새 Q # 단위 테스트를 정의 하는 편리한 장소를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-118">The first file, `Tests.qs`, provides a convenient place to define new Q# unit tests.</span></span>
<span data-ttu-id="ae0f3-119">처음에이 파일에는 새로 할당 된 \ket가 ${0}$ 상태에 있는지 확인 하 고 메시지를 인쇄 하는 하나의 샘플 단위 테스트 `AllocateQubitTest` 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-119">Initially this file contains one sample unit test `AllocateQubitTest` which checks that a newly allocated qubit is in the $\ket{0}$ state and prints a message:</span></span>

```qsharp
    operation AllocateQubitTest () : Unit {
        using (q = Qubit()) {
            Assert([PauliZ], [q], Zero, "Newly allocated qubit must be in the |0⟩ state.");
        }
        
        Message("Test passed");
    }
```

<span data-ttu-id="ae0f3-120">`(Unit -> Unit)`과 호환 되는 형식 `(Unit => Unit)` 또는 함수와 호환 되는 모든 Q # 작업을 단위 테스트로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-120">Any Q# operation compatible with the type `(Unit => Unit)` or function compatible with `(Unit -> Unit)` can be executed as a unit test.</span></span> 

<span data-ttu-id="ae0f3-121">두 번째 파일인 `TestSuiteRunner.cs`에는 Q # 단위 테스트를 검색 하 고 실행 하는 메서드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-121">The second file, `TestSuiteRunner.cs` contains a method that discovers and runs Q# unit tests.</span></span> <span data-ttu-id="ae0f3-122">`OperationDriver` 특성으로 주석이 지정 된 `TestTarget` 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-122">This is the method `TestTarget` annotated with `OperationDriver` attribute.</span></span>
<span data-ttu-id="ae0f3-123">`OperationDriver` 특성은 Xunit 확장 라이브러리의 일부입니다. x x x. x x x.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-123">The `OperationDriver` attribute is a part of the Xunit extension library Microsoft.Quantum.Simulation.Xunit.</span></span>
<span data-ttu-id="ae0f3-124">단위 테스트 프레임 워크는 검색 된 모든 Q # 단위 테스트에 대 한 `TestTarget` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-124">The unit testing framework calls `TestTarget` method for every Q# unit test it has discovered.</span></span>
<span data-ttu-id="ae0f3-125">프레임 워크는 `op` 인수를 통해 단위 테스트 설명을 메서드에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-125">The framework passes the unit test description to the method through `op` argument.</span></span> <span data-ttu-id="ae0f3-126">다음 코드 줄:</span><span class="sxs-lookup"><span data-stu-id="ae0f3-126">The following line of code:</span></span>
```csharp
op.TestOperationRunner(sim);
```
<span data-ttu-id="ae0f3-127">`QuantumSimulator`에서 단위 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-127">executes the unit test on `QuantumSimulator`.</span></span>

<span data-ttu-id="ae0f3-128">기본적으로 단위 테스트 검색 메커니즘은 다음 속성을 충족 하는 모든 Q # 함수 또는 호환 되는 형식의 작업을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-128">By default, the unit test discovery mechanism looks for all Q# functions or operations of compatible type that satisfy the following properties:</span></span>
* <span data-ttu-id="ae0f3-129">`OperationDriver` 특성으로 주석이 지정 된 메서드와 동일한 어셈블리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-129">Located in the same assembly as the method annotated with the `OperationDriver` attribute.</span></span>
* <span data-ttu-id="ae0f3-130">`OperationDriver` 특성으로 주석이 지정 된 메서드와 동일한 네임 스페이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-130">Located in the same namespace as the method annotated with the `OperationDriver` attribute.</span></span>
* <span data-ttu-id="ae0f3-131">이름이 `Test`로 끝나는 경우</span><span class="sxs-lookup"><span data-stu-id="ae0f3-131">Has a name ending with `Test`.</span></span>

<span data-ttu-id="ae0f3-132">어셈블리, 네임 스페이스 및 단위 테스트 함수 및 작업에 대 한 접미사는 `OperationDriver` 특성의 선택적 매개 변수를 사용 하 여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-132">An assembly, a namespace, and a suffix for unit test functions and operations can be set using optional parameters of the `OperationDriver` attribute:</span></span>
* <span data-ttu-id="ae0f3-133">`AssemblyName` 매개 변수는 테스트를 위해 검색 중인 어셈블리의 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-133">`AssemblyName` parameter sets the name of the assembly which is being searched for tests.</span></span>
* <span data-ttu-id="ae0f3-134">`TestNamespace` 매개 변수는 테스트를 위해 검색 중인 네임 스페이스의 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-134">`TestNamespace` parameter sets the name of the namespace which is being searched for tests.</span></span>
* <span data-ttu-id="ae0f3-135">`Suffix`는 단위 테스트로 간주 되는 작업 또는 함수 이름의 접미사를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-135">`Suffix` sets the suffix of operation or function names that are considered to be unit tests.</span></span>

<span data-ttu-id="ae0f3-136">또한 선택적 매개 변수 `TestCasePrefix` 사용 하 여 테스트 사례의 이름에 대 한 접두사를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-136">In addition, the `TestCasePrefix` optional parameter lets you set a prefix for the name of the test case.</span></span> <span data-ttu-id="ae0f3-137">작업 이름 앞에 있는 접두사는 테스트 사례 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-137">The prefix in front of the operation name will appear in the list of test cases.</span></span> <span data-ttu-id="ae0f3-138">예를 들어 `TestCasePrefix = "QSim:"`는 검색 된 테스트 목록에서 `AllocateQubitTest`을 `QSim:AllocateQubitTest`으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-138">For example, `TestCasePrefix = "QSim:"` will cause `AllocateQubitTest` to appear as `QSim:AllocateQubitTest` in the list of found tests.</span></span> <span data-ttu-id="ae0f3-139">이는 예를 들어 테스트를 실행 하는 데 사용 되는 시뮬레이터를 표시 하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-139">This can be useful to indicate, for instance, which simulator is used to run a test.</span></span>

### <a name="running-q-unit-tests"></a><span data-ttu-id="ae0f3-140">Q # 단위 테스트 실행</span><span class="sxs-lookup"><span data-stu-id="ae0f3-140">Running Q# Unit Tests</span></span>

#### <a name="visual-studio-2019tabtabid-vs2019"></a>[<span data-ttu-id="ae0f3-141">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="ae0f3-141">Visual Studio 2019</span></span>](#tab/tabid-vs2019)

<span data-ttu-id="ae0f3-142">솔루션 당 일회성 설치로 `Test` 메뉴로 이동 하 여 `Test Settings` > `Default Processor Architecture` > `X64`를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-142">As a one-time per-solution setup, go to `Test` menu and select `Test Settings` > `Default Processor Architecture` > `X64`.</span></span>

> [!TIP]
> <span data-ttu-id="ae0f3-143">Visual Studio의 기본 프로세서 아키텍처 설정은 각 솔루션에 대 한 솔루션 옵션 (`.suo`) 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-143">The default processor architecture setting for Visual Studio is stored in the solution options (`.suo`) file for each solution.</span></span>
> <span data-ttu-id="ae0f3-144">이 파일을 삭제 하는 경우 프로세서 아키텍처로 `X64`을 다시 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-144">If you delete this file, then you will need to select `X64` as your processor architecture again.</span></span>

<span data-ttu-id="ae0f3-145">프로젝트를 빌드하고 `Test` 메뉴로 이동 하 여 `Windows` > `Test Explorer`를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-145">Build the project, go to the `Test` menu and select `Windows` > `Test Explorer`.</span></span> <span data-ttu-id="ae0f3-146">`AllocateQubitTest` `Not Run Tests` 그룹의 테스트 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-146">`AllocateQubitTest` will show up in the list of tests in the `Not Run Tests` group.</span></span> <span data-ttu-id="ae0f3-147">`Run All`를 선택 하거나이 개별 테스트를 실행 하 고 통과 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-147">Select `Run All` or run this individual test, and it should pass!</span></span>

#### <a name="command-line--visual-studio-codetabtabid-vscode"></a>[<span data-ttu-id="ae0f3-148">명령줄/Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ae0f3-148">Command Line / Visual Studio Code</span></span>](#tab/tabid-vscode)

<span data-ttu-id="ae0f3-149">테스트를 실행 하려면 프로젝트 폴더 (`Tests.csproj`포함 된 폴더)로 이동 하 고 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-149">To run tests, navigate to the project folder (the folder which contains `Tests.csproj`), and execute the command:</span></span>

```bash
$ dotnet restore
$ dotnet test
```

<span data-ttu-id="ae0f3-150">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-150">You should get output similar to the following:</span></span>

```
Build started, please wait...
Build completed.

Test run for C:\Users\chgranad.REDMOND\tmp\Tests\bin\Debug\netcoreapp2.0\Tests.dll(.NETCoreApp,Version=v2.0)
Microsoft (R) Test Execution Command Line Tool Version 15.3.0-preview-20170628-02
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
[xUnit.net 00:00:00.5864002]   Discovering: Tests
[xUnit.net 00:00:00.7073844]   Discovered:  Tests
[xUnit.net 00:00:00.7453826]   Starting:    Tests
[xUnit.net 00:00:00.9590439]   Finished:    Tests

Total tests: 1. Passed: 1. Failed: 0. Skipped: 0.
Test Run Successful.
Test execution time: 1.9607 Seconds
```

***

## <a name="logging-and-assertions"></a><span data-ttu-id="ae0f3-151">로깅 및 어설션</span><span class="sxs-lookup"><span data-stu-id="ae0f3-151">Logging and Assertions</span></span>

<span data-ttu-id="ae0f3-152">Q #의 함수는 의도 하지 않은 동작의 한 가지 중요 한 결과 이며, 출력 형식이 빈 튜플 인 함수를 실행 하는 경우에는 Q # 프로그램 내에서 관찰 하지 못할 수 `()`.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-152">One important consequence of the fact that functions in Q# have no side effects is that any effects of executing a function whose output type is the empty tuple `()` can never be observed from within a Q# program.</span></span>
<span data-ttu-id="ae0f3-153">즉, 대상 컴퓨터는 이러한 누락으로 인 한 `()` 반환 하는 함수를 실행 하지 않도록 선택할 수 있습니다 .이는 다음 Q # 코드의 동작을 수정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-153">That is, a target machine can choose not to execute any function which returns `()` with the guarantee that this omission will not modify the behavior of any following Q# code.</span></span>
<span data-ttu-id="ae0f3-154">이를 통해 함수는 어설션 및 디버깅 논리를 Q # 프로그램에 포함 하는 데 유용한 도구를 `()` 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-154">This makes functions returning `()` a useful tool for embedding assertions and debugging logic into Q# programs.</span></span> 

### <a name="logging"></a><span data-ttu-id="ae0f3-155">로깅</span><span class="sxs-lookup"><span data-stu-id="ae0f3-155">Logging</span></span>

<span data-ttu-id="ae0f3-156">내장 함수 <xref:microsoft.quantum.intrinsic.message>에는 `(String -> Unit)` 형식이 있으며 진단 메시지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-156">The intrinsic function <xref:microsoft.quantum.intrinsic.message> has type `(String -> Unit)` and enables the creation of diagnostic messages.</span></span>

<span data-ttu-id="ae0f3-157">`QuantumSimulator`의 `onLog` 작업을 사용 하 여 Q # 코드에서 `Message`를 호출할 때 수행 되는 작업을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-157">The `onLog` action of `QuantumSimulator` can be used to define actions performed when Q# code calls `Message`.</span></span> <span data-ttu-id="ae0f3-158">기본적으로 기록 된 메시지는 표준 출력으로 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-158">By default logged messages are printed to standard output.</span></span>

<span data-ttu-id="ae0f3-159">단위 테스트 도구 모음을 정의 하는 경우 기록 된 메시지를 테스트 출력으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-159">When defining a unit test suite, the logged messages can be directed to the test output.</span></span> <span data-ttu-id="ae0f3-160">Q # 테스트 프로젝트 템플릿에서 프로젝트를 만든 경우이 리디렉션은 도구 모음에 대해 미리 구성 되며 기본적으로 다음과 같이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-160">When a project is created from Q# Test Project template, this redirection is pre-configured for the suite and created by default as follows:</span></span>

```qsharp
using (var sim = new QuantumSimulator())
{
    // OnLog defines action(s) performed when Q# test calls operation Message
    sim.OnLog += (msg) => { output.WriteLine(msg); };
    op.TestOperationRunner(sim);
}
```

#### <a name="visual-studio-2019tabtabid-vs2019"></a>[<span data-ttu-id="ae0f3-161">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="ae0f3-161">Visual Studio 2019</span></span>](#tab/tabid-vs2019)

<span data-ttu-id="ae0f3-162">테스트 탐색기에서 테스트를 실행 하 고 테스트를 클릭 하면 테스트 실행: 성공/실패 상태, 경과 시간 및 "출력" 링크에 대 한 정보가 포함 된 패널이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-162">After you execute a test in Test Explorer and click on the test, a panel will appear with information about test execution: Passed/Failed status, elapsed time and an "Output" link.</span></span> <span data-ttu-id="ae0f3-163">"출력" 링크를 클릭 하면 테스트 출력이 새 창에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-163">If you click the "Output" link, test output will open in a new window.</span></span>

![테스트 출력](~/media/unit-test-output.png)

#### <a name="command-line--visual-studio-codetabtabid-vscode"></a>[<span data-ttu-id="ae0f3-165">명령줄/Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ae0f3-165">Command Line / Visual Studio Code</span></span>](#tab/tabid-vscode)

<span data-ttu-id="ae0f3-166">각 테스트에 대 한 통과/실패 상태는 `dotnet test`하 여 콘솔에 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-166">The pass/fail status for each test is printed to the console by `dotnet test`.</span></span>
<span data-ttu-id="ae0f3-167">실패 한 테스트의 경우 위의 `output.WriteLine(msg)` 호출 결과로 기록 된 출력도 콘솔에 출력 되어 오류를 진단 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-167">For failing tests, the outputs logged as a result of the `output.WriteLine(msg)` call above are also printed to the console to help diagnose the failure.</span></span>

***

### <a name="assertions"></a><span data-ttu-id="ae0f3-168">어설션을</span><span class="sxs-lookup"><span data-stu-id="ae0f3-168">Assertions</span></span>

<span data-ttu-id="ae0f3-169">동일한 논리를 적용 하 여 어설션을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-169">The same logic can be applied to implementing assertions.</span></span> <span data-ttu-id="ae0f3-170">간단한 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-170">Let's consider a simple example:</span></span>

```qsharp
function AssertPositive(value : Double) : Unit 
{
    if (value <= 0) 
    {
        fail "Expected a positive number.";
    }
}
```

<span data-ttu-id="ae0f3-171">여기서 키워드 `fail`는 계산이 진행 되지 않아야 함을 나타냅니다. Q # 프로그램을 실행 하는 대상 컴퓨터에서 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-171">Here, the keyword `fail` indicates that the computation should not proceed, raising an exception in the target machine running the Q# program.</span></span>
<span data-ttu-id="ae0f3-172">정의에 따라 Q # 내에서 이러한 종류의 오류를 확인할 수 없습니다. `fail` 문에 도달한 후에 추가 Q # 코드가 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-172">By definition, a failure of this kind cannot be observed from within Q#, as no further Q# code is run after a `fail` statement is reached.</span></span>
<span data-ttu-id="ae0f3-173">따라서 `AssertPositive`에 대 한 호출을 계속 진행 하는 경우 해당 입력이 양수가 되도록 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-173">Thus, if we proceed past a call to `AssertPositive`, we can be assured by that its input was positive.</span></span>

<span data-ttu-id="ae0f3-174">이러한 아이디어를 기반으로 하 [는 prelude는](xref:microsoft.quantum.libraries.standard.prelude) <xref:microsoft.quantum.intrinsic.assert> <xref:microsoft.quantum.intrinsic.assertprob> `()`에 대 한 작업으로 모델링 된 두 가지 특히 유용한 어설션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-174">Building on these ideas, [the prelude](xref:microsoft.quantum.libraries.standard.prelude) offers two especially useful assertions, <xref:microsoft.quantum.intrinsic.assert> and <xref:microsoft.quantum.intrinsic.assertprob> both modeled as operations onto `()`.</span></span> <span data-ttu-id="ae0f3-175">이러한 어설션은 각각 특정 측정값을 설명 하는 Pauli 연산자, 측정을 수행 해야 하는 퀀텀 레지스터 및 가상 결과를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-175">These assertions each take a Pauli operator describing a particular measurement of interest, a quantum register on which a measurement is to be performed, and a hypothetical outcome.</span></span>
<span data-ttu-id="ae0f3-176">시뮬레이션을 통해 작동 하는 대상 컴퓨터에서는 [복제 안 함 정리](https://en.wikipedia.org/wiki/No-cloning_theorem)바인딩되지 않으며 이러한 어설션에 전달 된 레지스터를 방해 하지 않고 이러한 측정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-176">On target machines which work by simulation, we are not bound by [the no-cloning theorem](https://en.wikipedia.org/wiki/No-cloning_theorem), and can perform such measurements without disturbing the register passed to such assertions.</span></span>
<span data-ttu-id="ae0f3-177">그런 다음 시뮬레이터는 위의 `AssertPositive` 함수와 마찬가지로 가상 결과가 실제로 관찰 되지 않는 경우 계산을 중단 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-177">A simulator can then, similar to the `AssertPositive` function above, abort computation if the hypothetical outcome would not be observed in practice:</span></span>

```qsharp
using (register = Qubit()) 
{
    H(register);
    Assert([PauliX], [register], Zero);
    // Even though we do not have access to states in Q#,
    // we know by the anthropic principle that the state
    // of register at this point is |+〉.
}
```

<span data-ttu-id="ae0f3-178">복제 안 함 정리에서 퀀텀 상태를 검사 하는 것을 방지 하는 실제 퀀텀 하드웨어에서는 `Assert` 및 `AssertProb` 작업이 다른 효과 없이 `()` 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-178">On physical quantum hardware, where the no-cloning theorem prevents examination of quantum state, the `Assert` and `AssertProb` operations simply return `()` with no other effect.</span></span>

<span data-ttu-id="ae0f3-179"><xref:microsoft.quantum.diagnostics> 네임 스페이스는 더 많은 고급 조건을 확인할 수 있도록 하는 `Assert` 패밀리의 여러 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-179">The <xref:microsoft.quantum.diagnostics> namespace provides several more functions of the `Assert` family which allow us to check more advanced conditions.</span></span> 

## <a name="dump-functions"></a><span data-ttu-id="ae0f3-180">덤프 함수</span><span class="sxs-lookup"><span data-stu-id="ae0f3-180">Dump Functions</span></span>

<span data-ttu-id="ae0f3-181">퀀텀 프로그램의 문제를 해결 하는 데 도움이 되도록 <xref:microsoft.quantum.diagnostics> 네임 스페이스는 대상 컴퓨터의 현재 상태 (<xref:microsoft.quantum.diagnostics.dumpmachine> 및 <xref:microsoft.quantum.diagnostics.dumpregister>)를 파일에 덤프할 수 있는 두 가지 함수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-181">To help troubleshooting quantum programs, the <xref:microsoft.quantum.diagnostics> namespace offers two functions that can dump into a file the current status of the target machine: <xref:microsoft.quantum.diagnostics.dumpmachine> and <xref:microsoft.quantum.diagnostics.dumpregister>.</span></span> <span data-ttu-id="ae0f3-182">각각의 생성 된 출력은 대상 컴퓨터에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-182">The generated output of each depends on the target machine.</span></span>

### <a name="dumpmachine"></a><span data-ttu-id="ae0f3-183">컴퓨터 \ 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ae0f3-183">DumpMachine</span></span>

<span data-ttu-id="ae0f3-184">퀀텀 개발 키트의 일부로 배포 되는 전체 상태 퀀텀 시뮬레이터는 전체 퀀텀 시스템의 [wave 함수](https://en.wikipedia.org/wiki/Wave_function) 를 파일에 기록 하 고, 각 요소가 해당 값의 진폭을 나타내는 복소수의 1 차원 배열입니다. 계산 기준 상태 $ \ket{n} $를 측정할 확률 (where $ \ket{n} = \ket{b_{n-1}...) b_1b_0} $ for bits $\{b_i\}$.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-184">The full-state quantum simulator distributed as part of the Quantum Development Kit writes into the file the [wave function](https://en.wikipedia.org/wiki/Wave_function) of the entire quantum system, as a one-dimensional array of complex numbers, in which each element represents the amplitude of the probability of measuring the computational basis state $\ket{n}$, where $\ket{n} = \ket{b_{n-1}...b_1b_0}$ for bits $\{b_i\}$.</span></span> <span data-ttu-id="ae0f3-185">예를 들어, 두 개의 om비트만 할당 된 컴퓨터에서 및 퀀텀 상태 $ $ \begin{align} \ket{\psi} = \frac{1}{\sqrt{2}} \ket{00}-\frac{(1 + i)}{2} \ket{10}, \end{align} $ $ 호출 <xref:microsoft.quantum.diagnostics.dumpmachine>이 출력을 생성 합니다. :</span><span class="sxs-lookup"><span data-stu-id="ae0f3-185">For example, on a machine with only two qubits allocated and in the quantum state $$ \begin{align} \ket{\psi} = \frac{1}{\sqrt{2}} \ket{00} - \frac{(1 + i)}{2} \ket{10}, \end{align} $$ calling <xref:microsoft.quantum.diagnostics.dumpmachine> generates this output:</span></span>

```
# wave function for qubits with ids (least to most significant): 0;1
∣0❭:     0.707107 +  0.000000 i  ==     **********           [ 0.500000 ]     --- [  0.00000 rad ]
∣1❭:     0.000000 +  0.000000 i  ==                          [ 0.000000 ]                   
∣2❭:    -0.500000 + -0.500000 i  ==     **********           [ 0.500000 ]   /     [ -2.35619 rad ]
∣3❭:     0.000000 +  0.000000 i  ==                          [ 0.000000 ]                   
```

<span data-ttu-id="ae0f3-186">첫 번째 행은 중요 한 순서 대로 해당 하는의 Id를 사용 하 여 주석을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-186">The first row provides a comment with the IDs of the corresponding qubits in their significant order.</span></span>
<span data-ttu-id="ae0f3-187">나머지 행은 데카르트 및 극좌표 형식의 기본 상태 vector $ \ket{n} $를 측정 하는 확률 진폭을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-187">The rest of the rows describe the probability amplitude of measuring the basis state vector $\ket{n}$ in both Cartesian and polar formats.</span></span> <span data-ttu-id="ae0f3-188">첫 번째 행에 대해 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-188">In detail for the first row:</span></span>

* <span data-ttu-id="ae0f3-189">이 행 **`∣0❭:`** `0` 계산 기준 상태에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-189">**`∣0❭:`** this row corresponds to the `0` computational basis state</span></span>
* <span data-ttu-id="ae0f3-190">**`0.707107 +  0.000000 i`** : 데카르트 형식의 확률 진폭입니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-190">**`0.707107 +  0.000000 i`**: the probability amplitude in Cartesian format.</span></span>
* <span data-ttu-id="ae0f3-191">**` == `** : `equal` seperates 부호와 동일 하 게 표현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-191">**` == `**: the `equal` sign seperates both equivalent representations.</span></span>
* <span data-ttu-id="ae0f3-192">**`**********  `** : 크기의 그래픽 표현으로, `*` 수는이 상태 벡터를 측정할 확률에 비례 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-192">**`**********  `**: A graphical representation of the magnitude, the number of `*` is proportionate to the probability of measuring this state vector.</span></span>
* <span data-ttu-id="ae0f3-193">**`[ 0.500000 ]`** : 크기의 숫자 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-193">**`[ 0.500000 ]`**: the numeric value of the magnitude</span></span>
* <span data-ttu-id="ae0f3-194">**`    ---`** : 진폭의 단계 (아래 참조)에 대 한 그래픽 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-194">**`    ---`**: A graphical representation of the amplitude's phase (see below).</span></span>
* <span data-ttu-id="ae0f3-195">**`[ 0.0000 rad ]`** : 단계의 숫자 값 (라디안 단위)입니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-195">**`[ 0.0000 rad ]`**: the numeric value of the phase (in radians).</span></span>

<span data-ttu-id="ae0f3-196">크기와 단계가 모두 그래픽 표현으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-196">Both the magnitude and the phase are displayed with a graphical representation.</span></span> <span data-ttu-id="ae0f3-197">크기 표현은 간단 하 게 표시 됩니다 .이는 `*`막대를 표시 하 고 막대의 클수록 표시 되는 확률이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-197">The magnitude representation is straight-forward: it shows a bar of `*`, the bigger the probability the bigger the bar will be.</span></span> <span data-ttu-id="ae0f3-198">단계에서는 범위에 따라 각도를 나타내기 위해 다음 기호를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-198">For the phase, we show the following symbols to represent the angle based on ranges:</span></span>

```
[ -π/16,   π/16)       ---
[  π/16,  3π/16)        /-
[ 3π/16,  5π/16)        / 
[ 5π/16,  7π/16)       +/ 
[ 7π/16,  9π/16)      ↑   
[ 8π/16, 11π/16)    \-    
[ 7π/16, 13π/16)    \     
[ 7π/16, 15π/16)   +\     
[15π/16, 19π/16)   ---    
[17π/16, 19π/16)   -/     
[19π/16, 21π/16)    /     
[21π/16, 23π/16)    /+    
[23π/16, 25π/16)      ↓   
[25π/16, 27π/16)       -\ 
[27π/16, 29π/16)        \ 
[29π/16, 31π/16)        \+
[31π/16,   π/16)       ---
```

<span data-ttu-id="ae0f3-199">다음 예에서는 몇 가지 일반적인 상태에 대 한 `DumpMachine` 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-199">The following examples show `DumpMachine` for some common states:</span></span>

### `∣0❭`

```
# wave function for qubits with ids (least to most significant): 0
∣0❭:     1.000000 +  0.000000 i  ==     ******************** [ 1.000000 ]     --- [  0.00000 rad ]
∣1❭:     0.000000 +  0.000000 i  ==                          [ 0.000000 ]                   
```

### `∣1❭`

```
# wave function for qubits with ids (least to most significant): 0
∣0❭:     0.000000 +  0.000000 i  ==                          [ 0.000000 ]                   
∣1❭:     1.000000 +  0.000000 i  ==     ******************** [ 1.000000 ]     --- [  0.00000 rad ]
```

### `∣+❭`

```
# wave function for qubits with ids (least to most significant): 0
∣0❭:     0.707107 +  0.000000 i  ==     **********           [ 0.500000 ]      --- [  0.00000 rad ]
∣1❭:     0.707107 +  0.000000 i  ==     **********           [ 0.500000 ]      --- [  0.00000 rad ]
```

### `∣-❭`

```
# wave function for qubits with ids (least to most significant): 0
∣0❭:     0.707107 +  0.000000 i  ==     **********           [ 0.500000 ]      --- [  0.00000 rad ]
∣1❭:    -0.707107 +  0.000000 i  ==     **********           [ 0.500000 ]  ---     [  3.14159 rad ]
```


  > [!NOTE]
  > <span data-ttu-id="ae0f3-200">의 id는 런타임에 할당 되며,이는 해당 비트를 할당 하는 순서 또는이를 사용 하는 순서에 따라 결정 되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-200">The id of a qubit is assigned at runtime and it's not necessarily aligned with the order in which the qubit was allocated or its position within a qubit register.</span></span>


#### <a name="visual-studio-2019tabtabid-vs2019"></a>[<span data-ttu-id="ae0f3-201">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="ae0f3-201">Visual Studio 2019</span></span>](#tab/tabid-vs2019)

  > [!TIP]
  > <span data-ttu-id="ae0f3-202">코드에 중단점을 배치 하 고 다음과 같이 다음과 같이 Visual Studio에서 사용자 비트 id를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-202">You can figure out a qubit id in Visual Studio by putting a breakpoint in your code and inspecting the value of a qubit variable, for example:</span></span>
  > 
  > ![Visual Studio에서 이상 비트 id 표시](~/media/qubit_id.png)
  >
  > <span data-ttu-id="ae0f3-204">`register2`에서 index가 `0` 인 이상 비트에는 id =`3`, 인덱스 `1`의 고 비트는 id =`2`입니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-204">the qubit with index `0` on `register2` has id=`3`, the qubit with index `1` has id=`2`.</span></span>

#### <a name="command-line--visual-studio-codetabtabid-vscode"></a>[<span data-ttu-id="ae0f3-205">명령줄/Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ae0f3-205">Command Line / Visual Studio Code</span></span>](#tab/tabid-vscode)

  > [!TIP]
  > <span data-ttu-id="ae0f3-206"><xref:microsoft.quantum.intrinsic.message> 함수를 사용 하 고 다음과 같이 메시지에 다음과 같은 기능을 전달 하 여이에 대 한 비트 id를 알아낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-206">You can figure out a qubit id by using the <xref:microsoft.quantum.intrinsic.message> function and passing the qubit variable in the message, for example:</span></span>
  >
  > ```qsharp
  > Message($"0={register2[0]}; 1={register2[1]}");
  > ```
  > 
  > <span data-ttu-id="ae0f3-207">다음 출력이 생성 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-207">which could generate this output:</span></span>
  >```
  > 0=q:3; 1=q:2
  >```
  > <span data-ttu-id="ae0f3-208">즉, 인덱스를 사용 하 여 `register2`에서 `0` 하는 것이 id =`3`이며 인덱스 `1`의 이상 비트는 id =`2`입니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-208">which means that the qubit with index `0` on `register2` has id=`3`, the qubit with index `1` has id=`2`.</span></span>


***

<span data-ttu-id="ae0f3-209"><xref:microsoft.quantum.diagnostics.dumpmachine> <xref:microsoft.quantum.diagnostics> 네임 스페이스에 포함 되어 있으므로이를 사용 하려면 `open` 문을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-209"><xref:microsoft.quantum.diagnostics.dumpmachine> is part of the  <xref:microsoft.quantum.diagnostics> namespace, so in order to use it you must add an `open` statement:</span></span>

```qsharp
namespace Samples {
    open Microsoft.Quantum.Intrinsic;
    open Microsoft.Quantum.Diagnostics;

    operation Operation () : Unit {
        using (qubits = Qubit[2]) {
            H(qubits[1]);
            DumpMachine("dump.txt");
        }
    }
}
```


### <a name="dumpregister"></a><span data-ttu-id="ae0f3-210">DumpRegister</span><span class="sxs-lookup"><span data-stu-id="ae0f3-210">DumpRegister</span></span>

<span data-ttu-id="ae0f3-211"><xref:microsoft.quantum.diagnostics.dumpregister>은 (는) <xref:microsoft.quantum.diagnostics.dumpmachine>와 같이 작동 합니다. 단,이는 해당 하는 것과 관련 된 정보만으로 정보의 양을 제한 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-211"><xref:microsoft.quantum.diagnostics.dumpregister> works like <xref:microsoft.quantum.diagnostics.dumpmachine>, except it also takes an array of qubits to limit the amount of information to only that relevant to the corresponding qubits.</span></span>

<span data-ttu-id="ae0f3-212"><xref:microsoft.quantum.diagnostics.dumpmachine>와 마찬가지로 <xref:microsoft.quantum.diagnostics.dumpregister>에 의해 생성 되는 정보는 대상 컴퓨터에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-212">As with <xref:microsoft.quantum.diagnostics.dumpmachine>, the information generated by <xref:microsoft.quantum.diagnostics.dumpregister> depends on the target machine.</span></span> <span data-ttu-id="ae0f3-213">전체 상태 퀀텀 시뮬레이터에 대해 wave 함수를 파일에 기록 합니다 .이 함수는 <xref:microsoft.quantum.diagnostics.dumpmachine>와 동일한 형식으로 제공 된이를 통해 생성 된 퀀텀 하위 시스템의 전역 단계까지 파일에 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-213">For the full-state quantum simulator it writes into the file the wave function up to a global phase of the quantum sub-system generated by the provided qubits in the same format as <xref:microsoft.quantum.diagnostics.dumpmachine>.</span></span>  <span data-ttu-id="ae0f3-214">예를 들어 두 개의 기능이 할당 된 컴퓨터를 다시 사용 하 고 퀀텀 상태 $ $ \begin{align} \ket{\psi} = \frac{1}{\sqrt{2}} \ket{00}-\frac{(1 + i)}{2} \ket{10} =-e ^ {-i \ pi/4} ((\frac{1}{\sqrt{2}} \ k{0}-\frac{(1 + i)}{2} \ket{1}) \otimes \frac{-(1 + i)} {\sqrt{2}} \ket{0}), \end{align} $ $ <xref:microsoft.quantum.diagnostics.dumpregister>에 대 한 호출 `qubit[0]`이 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-214">For example, take again a machine with only two qubits allocated and in the quantum state $$ \begin{align} \ket{\psi} = \frac{1}{\sqrt{2}} \ket{00} - \frac{(1 + i)}{2} \ket{10} = - e^{-i\pi/4} ( (\frac{1}{\sqrt{2}} \ket{0} - \frac{(1 + i)}{2} \ket{1} ) \otimes \frac{-(1 + i)}{\sqrt{2}} \ket{0} ) , \end{align} $$ calling <xref:microsoft.quantum.diagnostics.dumpregister> for `qubit[0]` generates this output:</span></span>

```
# wave function for qubits with ids (least to most significant): 0
∣0❭:    -0.707107 + -0.707107 i  ==     ******************** [ 1.000000 ]  /      [ -2.35619 rad ]
∣1❭:     0.000000 +  0.000000 i  ==                          [ 0.000000 ]                   
```

<span data-ttu-id="ae0f3-215">`qubit[1]`에 대 한 <xref:microsoft.quantum.diagnostics.dumpregister>를 호출 하면 다음 출력이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-215">and calling <xref:microsoft.quantum.diagnostics.dumpregister> for `qubit[1]` generates this output:</span></span>

```
# wave function for qubits with ids (least to most significant): 1
∣0❭:     0.707107 +  0.000000 i  ==     ***********          [ 0.500000 ]     --- [  0.00000 rad ]
∣1❭:    -0.500000 + -0.500000 i  ==     ***********          [ 0.500000 ]  /      [ -2.35619 rad ]
```

<span data-ttu-id="ae0f3-216">일반적으로 다른 레지스터와 함께 사용 되는 레지스터의 상태는 순수 상태가 아닌 혼합 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-216">In general, the state of a register that is entangled with another register is a mixed state rather than a pure state.</span></span> <span data-ttu-id="ae0f3-217">이 경우 <xref:microsoft.quantum.diagnostics.dumpregister>는 다음과 같은 메시지를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-217">In this case, <xref:microsoft.quantum.diagnostics.dumpregister> outputs the following message:</span></span>

```
Qubits provided (0;) are entangled with some other qubit.
```

<span data-ttu-id="ae0f3-218">다음 예제에서는 Q # 코드에서 <xref:microsoft.quantum.diagnostics.dumpregister>와 <xref:microsoft.quantum.diagnostics.dumpmachine>를 모두 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-218">The following example shows you how you can use both <xref:microsoft.quantum.diagnostics.dumpregister> and <xref:microsoft.quantum.diagnostics.dumpmachine> in your Q# code:</span></span>

```qsharp
namespace app
{
    open Microsoft.Quantum.Intrinsic;
    open Microsoft.Quantum.Diagnostics;

    operation Operation () : Unit {

        using (qubits = Qubit[2]) {
            X(qubits[1]);
            H(qubits[1]);
            R1Frac(1, 2, qubits[1]);
            
            DumpMachine("dump.txt");
            DumpRegister("q0.txt", qubits[0..0]);
            DumpRegister("q1.txt", qubits[1..1]);

            ResetAll(qubits);
        }
    }
}
```

## <a name="debugging"></a><span data-ttu-id="ae0f3-219">디버깅</span><span class="sxs-lookup"><span data-stu-id="ae0f3-219">Debugging</span></span>

<span data-ttu-id="ae0f3-220">`Assert` 및 `Dump` 함수 및 작업을 기반으로 하는 Q #은 표준 Visual Studio 디버깅 기능의 하위 집합을 지원 합니다. [줄 중단점 설정](https://docs.microsoft.com/visualstudio/debugger/using-breakpoints), F10 키를 [사용 하 여 코드 단계별 실행](https://docs.microsoft.com/visualstudio/debugger/navigating-through-code-with-the-debugger) 및 [클래식 변수의 값 검사 ](https://docs.microsoft.com/visualstudio/debugger/autos-and-locals-windows)시뮬레이터에서 코드를 실행 하는 동안 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-220">On top of `Assert` and `Dump` functions and operations, Q# supports a subset of standard Visual Studio debugging capabilities: [setting line breakpoints](https://docs.microsoft.com/visualstudio/debugger/using-breakpoints), [stepping through code using F10](https://docs.microsoft.com/visualstudio/debugger/navigating-through-code-with-the-debugger) and [inspecting values of classic variables](https://docs.microsoft.com/visualstudio/debugger/autos-and-locals-windows) are all possible during code execution on the simulator.</span></span>

<span data-ttu-id="ae0f3-221">Visual Studio Code 디버깅은 아직 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae0f3-221">Debugging in Visual Studio Code is not yet supported.</span></span>
