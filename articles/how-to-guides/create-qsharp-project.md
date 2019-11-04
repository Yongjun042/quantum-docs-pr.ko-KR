---
title: 'QDK (퀀텀 개발 키트)를 사용 하 여 Q # 프로젝트를 만드는 방법을 알아봅니다.'
description: '선택한 개발 환경에서 QDK 및 Q #을 사용 하 여 퀀텀 개발을 위한 프로젝트를 초기화 합니다.'
author: natke
ms.author: nakersha
ms.date: 10/19/2019
ms.topic: article
ms.custom: how-to
uid: microsoft.quantum.howto.createproject
ms.openlocfilehash: b4bec5e7a174b7e2d588331dd2093c7b23a728b0
ms.sourcegitcommit: aa5e6f4a2deb4271a333d3f1b1eb69b5bb9a7bad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73444177"
---
# <a name="create-a-q-project-in-your-development-environment"></a><span data-ttu-id="6754d-103">개발 환경에서 Q # 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6754d-103">Create a Q# project in your development environment</span></span>

<span data-ttu-id="6754d-104">QDK를 사용 하 여 Q # 프로젝트를 만드는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-104">Learn how to create a Q# project with the QDK.</span></span>

<span data-ttu-id="6754d-105">Q # 프로젝트에는 퀀텀 코드를 포함 하는 Q # 파일 뿐만 아니라 퀀텀 프로그램을 실행 하는 호스트 프로그램도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-105">A Q# project contains Q# files containing quantum code, as well as a host program to run the quantum program.</span></span> <span data-ttu-id="6754d-106">호스트 프로그램은 또는 Python과 C#같은 .net 언어로 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-106">You can write the host program in .NET languages such as C#, or in Python.</span></span> <span data-ttu-id="6754d-107">또한 IQ # 커널을 사용 하 여 Jupyter 노트북에서 Q # 코드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-107">You can also run Q# code in a Jupyter notebook using the IQ# kernel.</span></span>

<span data-ttu-id="6754d-108">아래 섹션에서 개발 환경 및 언어를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-108">Choose your development environment and language from the sections below:</span></span>

* [<span data-ttu-id="6754d-109">Python</span><span class="sxs-lookup"><span data-stu-id="6754d-109">Python</span></span>](#create-a-python-project)
* [<span data-ttu-id="6754d-110">Jupyter 노트북</span><span class="sxs-lookup"><span data-stu-id="6754d-110">Jupyter notebooks</span></span>](#create-a-jupyter-notebook-project)
* [<span data-ttu-id="6754d-111">C#Visual Studio 사용</span><span class="sxs-lookup"><span data-stu-id="6754d-111">C# with Visual Studio</span></span>](#create-a-c-project-on-windows-using-visual-studio)
* [<span data-ttu-id="6754d-112">C#VS Code 사용</span><span class="sxs-lookup"><span data-stu-id="6754d-112">C# with VS Code</span></span>](#create-a-c-project-using-vs-code)
* [<span data-ttu-id="6754d-113">C#명령줄 사용</span><span class="sxs-lookup"><span data-stu-id="6754d-113">C# with the command line</span></span>](#create-a-c-project-using-the-dotnet-command-line-tool)

## <a name="create-a-python-project"></a><span data-ttu-id="6754d-114">Python 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6754d-114">Create a Python project</span></span>

1. <span data-ttu-id="6754d-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6754d-115">Pre-requisites</span></span>

     * <span data-ttu-id="6754d-116">[Python 용 퀀텀 개발 키트](xref:microsoft.quantum.install#develop-with-python)</span><span class="sxs-lookup"><span data-stu-id="6754d-116">The [Quantum Development Kit for Python](xref:microsoft.quantum.install#develop-with-python)</span></span>

1. <span data-ttu-id="6754d-117">프로젝트에 대 한 폴더를 만들고 해당 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-117">Create a folder for your project, and navigate to that folder</span></span>

1. <span data-ttu-id="6754d-118">`Operation.qs`이라는 Q # 파일을 만들고 Q # 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-118">Create a Q# file called `Operation.qs`, and add your Q# code to it.</span></span> <span data-ttu-id="6754d-119">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-119">For example:</span></span>

    ```qsharp
    namespace HelloWorld {
        open Microsoft.Quantum.Intrinsic;
        open Microsoft.Quantum.Canon;

        operation SayHello() : Result {
            Message("Hello from quantum world!");
            return Zero;
        }
    }
    ```

1. <span data-ttu-id="6754d-120">Q # 작업을 호출 하는 `host.py` 라는 python 호스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-120">Create a python host file called `host.py` to call your Q# operation.</span></span> <span data-ttu-id="6754d-121">다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-121">For example:</span></span>

    ```python
    import qsharp

    from HelloWorld import SayHello

    SayHello.simulate()
    ```

1. <span data-ttu-id="6754d-122">다음과 같이 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-122">Run the program:</span></span>

    ```bash
    python host.py
    ```

1. <span data-ttu-id="6754d-123">출력을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-123">Verify the output.</span></span> <span data-ttu-id="6754d-124">프로그램은 다음 줄을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-124">Your program should output the following lines:</span></span>

    ```bash
    Hello from quantum world!
    0
    ```

<span data-ttu-id="6754d-125">이제 퀀텀 프로그램을 계속 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-125">You can now continue to develop your quantum program.</span></span>

## <a name="create-a-jupyter-notebook-project"></a><span data-ttu-id="6754d-126">Jupyter Notebook 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6754d-126">Create a Jupyter Notebook project</span></span>

1. <span data-ttu-id="6754d-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6754d-127">Pre-requisites</span></span>

    * <span data-ttu-id="6754d-128">[Jupyter 노트북용 퀀텀 개발 키트](xref:microsoft.quantum.install#develop-with-jupyter-notebooks)</span><span class="sxs-lookup"><span data-stu-id="6754d-128">The [Quantum Development Kit for Jupyter notebooks](xref:microsoft.quantum.install#develop-with-jupyter-notebooks)</span></span>

1. <span data-ttu-id="6754d-129">다음 명령을 실행하여 Notebook 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-129">Run the following command to start the notebook server:</span></span>

    ```bash
    jupyter notebook
    ```

1. <span data-ttu-id="6754d-130">명령줄에 표시된 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-130">Browse to the URL shown on the command line.</span></span> <span data-ttu-id="6754d-131">예: [http://localhost:8888/?token=c790a52ba54f0cf77465c3c8983d776348285b0280d91b85 ]</span><span class="sxs-lookup"><span data-stu-id="6754d-131">For example: [http://localhost:8888/?token=c790a52ba54f0cf77465c3c8983d776348285b0280d91b85]</span></span>

1. <span data-ttu-id="6754d-132">브라우저에 Jupyter 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-132">A Jupyter page appears in the browser.</span></span> <span data-ttu-id="6754d-133">**파일** 탭에서 **새로** 만들기 > **q #** 를 선택 하 여 q # 커널을 사용 하 여 jupyter 노트북을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-133">On the **Files** tab, select **New** > **Q#** to create a Jupyter notebook with a Q# kernel.</span></span> <span data-ttu-id="6754d-134">첫 번째 노트북 셀에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-134">Add the following code to the first notebook cell:</span></span>

    ```qsharp
    operation SayHello() : Unit {
        Message("Hello from quantum world!");
    }
    ```

1. <span data-ttu-id="6754d-135"> > **셀** 을 선택 **하 여 노트북** 을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-135">Select **Cell** > **Run Cells** to run the notebook.</span></span> <span data-ttu-id="6754d-136">`SayHello`은 곧 셀 출력에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-136">`SayHello` will soon appear in the cell output:</span></span>

    ![Q # code를 사용 하는 jupyter 노트북 셀](~/media/install-guide-jupyter.png)

    <span data-ttu-id="6754d-138">Jupyter 노트북에서 실행 하는 경우 Q # 코드가 컴파일되고 노트북은 검색 된 작업의 이름을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-138">When running in Jupyter Notebooks, the Q# code is compiled, and the notebook outputs the name of the operation(s) that it finds.</span></span>

1. <span data-ttu-id="6754d-139">새 셀에서 `%simulate` magic을 사용 하 여 방금 만든 작업의 퀀텀 컴퓨터에서 실행을 시뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-139">In a new cell, simulate the execution in a quantum computer of the operation you just created by using the `%simulate` magic:</span></span>

    ![% 시뮬레이트 마법을 사용 하는 jupyter 노트북 셀](~/media/install-guide-jupyter-simulate.png)

    <span data-ttu-id="6754d-141">호출 된 작업 (이 경우 비어 있음)의 결과와 함께 화면에 메시지가 인쇄 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-141">You should see the message printed on the screen along with the result of the operation you invoked (in this case, empty).</span></span>

<span data-ttu-id="6754d-142">이제 다른 Q # 작업을 추가 하 여 퀀텀 개발을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-142">You can now add other Q# operations to continue your quantum development.</span></span>

## <a name="create-a-c-project-on-windows-using-visual-studio"></a><span data-ttu-id="6754d-143">Visual Studio C# 를 사용 하 여 Windows에서 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6754d-143">Create a C# project on Windows, using Visual Studio</span></span>

1. <span data-ttu-id="6754d-144">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6754d-144">Pre-requisites</span></span>

    * <span data-ttu-id="6754d-145">[Visual Studio 용 퀀텀 개발 키트](xref:microsoft.quantum.install#develop-with-c-on-windows-using-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="6754d-145">The [Quantum Development Kit for Visual Studio](xref:microsoft.quantum.install#develop-with-c-on-windows-using-visual-studio)</span></span>

1. <span data-ttu-id="6754d-146">새 Q# 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="6754d-146">Create a new Q# application</span></span>

    * <span data-ttu-id="6754d-147">**파일** -> **새로 만들기** -> **프로젝트**로 이동</span><span class="sxs-lookup"><span data-stu-id="6754d-147">Go to **File** -> **New** -> **Project**</span></span>
    * <span data-ttu-id="6754d-148">검색 상자에 `Q#` 입력</span><span class="sxs-lookup"><span data-stu-id="6754d-148">Type `Q#` in the search box</span></span>
    * <span data-ttu-id="6754d-149">**Q# 애플리케이션**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-149">Select **Q# Application**</span></span>
    * <span data-ttu-id="6754d-150">**다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-150">Select **Next**</span></span>
    * <span data-ttu-id="6754d-151">애플리케이션의 이름 및 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-151">Choose a name and location for your application</span></span>
    * <span data-ttu-id="6754d-152">**만들기**</span><span class="sxs-lookup"><span data-stu-id="6754d-152">Select **Create**</span></span>

1. <span data-ttu-id="6754d-153">프로젝트를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-153">Inspect the project</span></span>

    <span data-ttu-id="6754d-154">C# 호스트 애플리케이션에 해당하는 `Driver.cs`와 콘솔에 메시지를 출력하는 간단한 작업을 정의하는 Q# 프로그램에 해당하는 `Operation.qs`의 두 파일이 생성된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-154">You should see that two files have been created: `Driver.cs`, which is the C# host application; and `Operation.qs`, which is a Q# program that defines a simple operation to print a message to the console.</span></span>

1. <span data-ttu-id="6754d-155">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="6754d-155">Run the application</span></span>

    * <span data-ttu-id="6754d-156">**디버그** -> **디버깅하지 않고 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-156">Select **Debug** -> **Start Without Debugging**</span></span>
    * <span data-ttu-id="6754d-157">콘솔 창에 `Hello quantum world!`가 출력된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-157">You should see the text `Hello quantum world!` printed to a console window.</span></span>

<span data-ttu-id="6754d-158">이제 Visual Studio를 사용 하 여 퀀텀 개발을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-158">You can now continue your quantum development using Visual Studio</span></span>

> [!NOTE]
> * <span data-ttu-id="6754d-159">단일 Visual Studio 솔루션 내에 여러 프로젝트가 있는 경우 솔루션에 포함된 모든 프로젝트는 솔루션과 동일한 폴더 또는 해당 하위 폴더 중 하나에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-159">If you have multiple projects within one Visual Studio solution, all projects contained in the solution need to be in the same folder as the solution, or in one of its subfolders.</span></span>  

## <a name="create-a-c-project-using-vs-code"></a><span data-ttu-id="6754d-160">VS Code를 C# 사용 하 여 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6754d-160">Create a C# project, using VS Code</span></span>

1. <span data-ttu-id="6754d-161">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6754d-161">Pre-requisites</span></span>

    * <span data-ttu-id="6754d-162">[VS Code에 대 한 퀀텀 개발 키트](xref:microsoft.quantum.install#develop-with-c-using-visual-studio-code)</span><span class="sxs-lookup"><span data-stu-id="6754d-162">The [Quantum Development Kit for VS Code](xref:microsoft.quantum.install#develop-with-c-using-visual-studio-code)</span></span>

1. <span data-ttu-id="6754d-163">새 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-163">Create a new project:</span></span>

    * <span data-ttu-id="6754d-164">**보기** -> **명령 팔레트**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-164">Go to **View** -> **Command Palette**</span></span>
    * <span data-ttu-id="6754d-165">**Q #: 새 프로젝트 만들기를** 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-165">Select **Q#: Create New Project**</span></span>
    * <span data-ttu-id="6754d-166">애플리케이션을 만들려는 파일 시스템의 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-166">Navigate to the location on the file system where you would like to create the application</span></span>
    * <span data-ttu-id="6754d-167">프로젝트를 만든 후에 **새 프로젝트 열기...** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-167">Click on the **Open new project...** button, once the project has been created</span></span>

1. <span data-ttu-id="6754d-168">애플리케이션을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-168">Run the application:</span></span>

    * <span data-ttu-id="6754d-169">**디버그** -> **디버깅하지 않고 시작**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-169">Go to **Debug** -> **Start Without Debugging**</span></span>
    * <span data-ttu-id="6754d-170">출력 창에 다음 텍스트가 표시되어야 합니다. `Hello quantum world!`</span><span class="sxs-lookup"><span data-stu-id="6754d-170">You should see the following text in the output window `Hello quantum world!`</span></span>

<span data-ttu-id="6754d-171">이제 Visual Studio Code를 사용 하 여 퀀텀 개발을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-171">You can now continue your quantum development using Visual Studio Code.</span></span>

> [!NOTE]
> * <span data-ttu-id="6754d-172">여러 루트 폴더가 있는 작업 영역은 현재 Visual Studio Code 확장에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-172">Workspaces with multiple root folders are not currently supported by the Visual Studio Code extension.</span></span> <span data-ttu-id="6754d-173">단일 VS Code 작업 영역에 여러 프로젝트가 있는 경우 모든 프로젝트가 동일한 루트 폴더 내에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-173">If you have multiple projects within one VS Code workspace, all projects need to be contained within the same root folder.</span></span>

## <a name="create-a-c-project-using-the-dotnet-command-line-tool"></a><span data-ttu-id="6754d-174">`dotnet` 명령줄 C# 도구를 사용 하 여 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="6754d-174">Create a C# project, using the `dotnet` command-line tool</span></span>

1. <span data-ttu-id="6754d-175">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6754d-175">Pre-requisites</span></span>

    * <span data-ttu-id="6754d-176">[명령줄에 대 한 퀀텀 개발 키트](xref:microsoft.quantum.install#develop-with-c-using-the-dotnet-command-line-tool)</span><span class="sxs-lookup"><span data-stu-id="6754d-176">The [Quantum Development Kit for the Command Line](xref:microsoft.quantum.install#develop-with-c-using-the-dotnet-command-line-tool)</span></span>

1. <span data-ttu-id="6754d-177">새 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="6754d-177">Create a new application</span></span>

    ```bash
    dotnet new console -lang Q# -o <project name>
    ```

1. <span data-ttu-id="6754d-178">새 애플리케이션 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-178">Navigate to the new application directory</span></span>

    ```bash
    cd <project name>
    ```

    <span data-ttu-id="6754d-179">애플리케이션의 프로젝트 파일과 함께 Q# 파일(`Operation.qs`) 및 C# 호스트 파일(`Driver.cs`)의 두 파일이 생성된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-179">You should see that two files have been created, along with the project files of the application: a Q# file (`Operation.qs`) and a C# host file (`Driver.cs`).</span></span>

1. <span data-ttu-id="6754d-180">애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="6754d-180">Run the application</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="6754d-181">다음 출력이 표시됩니다. `Hello quantum world!`</span><span class="sxs-lookup"><span data-stu-id="6754d-181">You should see the following output: `Hello quantum world!`</span></span>

<span data-ttu-id="6754d-182">이제 명령줄 도구를 사용 하 여 퀀텀 개발을 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-182">You now continue your quantum development, using command line tools.</span></span>

## <a name="whats-next"></a><span data-ttu-id="6754d-183">다음은 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="6754d-183">What's next?</span></span>

<span data-ttu-id="6754d-184">이제 기본 설정 환경에서 프로젝트를 만들었으므로 퀀텀 개발을 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6754d-184">Now that you have created a project in your preferred environment, you can continue your quantum development.</span></span>