---
title: 创建 dotnet new 项目模板
description: 了解如何创建 dotnet new 命令的项目模板。
author: thraka
ms.date: 06/25/2019
ms.topic: tutorial
ms.author: adegeo
ms.openlocfilehash: 31a6189c0126d6dff000bb84978c1527dbe4e2ae
ms.sourcegitcommit: 6472349821dbe202d01182bc2cfe9d7176eaaa6c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67870616"
---
# <a name="tutorial-create-a-project-template"></a><span data-ttu-id="2ba6a-103">教程：创建项目模板</span><span class="sxs-lookup"><span data-stu-id="2ba6a-103">Tutorial: Create a project template</span></span>

<span data-ttu-id="2ba6a-104">使用 .NET Core，可以创建和部署可生成项目、文件甚至资源的模板。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-104">With .NET Core, you can create and deploy templates that generate projects, files, even resources.</span></span> <span data-ttu-id="2ba6a-105">本教程是系列教程的第二部分，介绍如何创建、安装和卸载用于 `dotnet new` 命令的模板。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-105">This tutorial is part two of a series that teaches you how to create, install, and uninstall, templates for use with the `dotnet new` command.</span></span>

<span data-ttu-id="2ba6a-106">在本系列的这一部分中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="2ba6a-106">In this part of the series you'll learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2ba6a-107">创建项目模板的资源</span><span class="sxs-lookup"><span data-stu-id="2ba6a-107">Create the resources of a project template</span></span>
> * <span data-ttu-id="2ba6a-108">创建模板配置文件夹和文件</span><span class="sxs-lookup"><span data-stu-id="2ba6a-108">Create the template config folder and file</span></span>
> * <span data-ttu-id="2ba6a-109">从文件路径安装模板</span><span class="sxs-lookup"><span data-stu-id="2ba6a-109">Install a template from a file path</span></span>
> * <span data-ttu-id="2ba6a-110">测试项模板</span><span class="sxs-lookup"><span data-stu-id="2ba6a-110">Test an item template</span></span>
> * <span data-ttu-id="2ba6a-111">卸载项模板</span><span class="sxs-lookup"><span data-stu-id="2ba6a-111">Uninstall an item template</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ba6a-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="2ba6a-112">Prerequisites</span></span>

* <span data-ttu-id="2ba6a-113">完成本系列教程的[第 1 部分](cli-templates-create-item-template.md)。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-113">Complete [part 1](cli-templates-create-item-template.md) of this tutorial series.</span></span>
* <span data-ttu-id="2ba6a-114">打开终端并导航到 working\templates\\  文件夹。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-114">Open a terminal and navigate to the _working\templates\\_ folder.</span></span>

## <a name="create-a-project-template"></a><span data-ttu-id="2ba6a-115">创建项目模板</span><span class="sxs-lookup"><span data-stu-id="2ba6a-115">Create a project template</span></span>

<span data-ttu-id="2ba6a-116">项目模板生成可立即运行的项目，使用户可以轻松地使用一组有效的代码。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-116">Project templates produce ready-to-run projects that make it easy for users to start with a working set of code.</span></span> <span data-ttu-id="2ba6a-117">.NET Core 包含一些项目模板，例如控制台应用程序或类库。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-117">.NET Core includes a few project templates such as a console application or a class library.</span></span> <span data-ttu-id="2ba6a-118">在本例中，你将创建一个新的控制台项目，该项目启用 C# 8.0 并生成 `async main` 入口点。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-118">In this example, you'll create a new console project that enables C# 8.0 and produces an `async main` entry point.</span></span>

<span data-ttu-id="2ba6a-119">在终端中，导航到 working\templates\\  文件夹，并创建一个名为“consoleasync”  的新子文件夹。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-119">In your terminal, navigate to the _working\templates\\_ folder and create a new subfolder named _consoleasync_.</span></span> <span data-ttu-id="2ba6a-120">进入子文件夹，并运行 `dotnet new console` 以生成标准控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-120">Enter the subfolder and run `dotnet new console` to generate the standard console application.</span></span> <span data-ttu-id="2ba6a-121">将编辑此模板生成的文件以创建新模板。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-121">You'll be editing the files produced by this template to create a new template.</span></span>

```console
working
└───templates
    └───consoleasync
            consoleasync.csproj
            Program.cs
```

## <a name="modify-programcs"></a><span data-ttu-id="2ba6a-122">修改 Program.cs</span><span class="sxs-lookup"><span data-stu-id="2ba6a-122">Modify Program.cs</span></span>

<span data-ttu-id="2ba6a-123">打开 program.cs  文件。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-123">Open up the _program.cs_ file.</span></span> <span data-ttu-id="2ba6a-124">控制台项目不使用异步入口点，我们来添加它。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-124">The console project doesn't use an asynchronous entry point, so let's add that.</span></span> <span data-ttu-id="2ba6a-125">将代码更改为以下内容并保存文件：</span><span class="sxs-lookup"><span data-stu-id="2ba6a-125">Change your code to the following and save the file:</span></span>

```csharp
using System;
using System.Threading.Tasks;

namespace consoleasync
{
    class Program
    {
        static async Task Main(string[] args)
        {
            await Console.Out.WriteAsync("Hello World with C# 8.0!");
        }
    }
}
```

## <a name="modify-consoleasynccsproj"></a><span data-ttu-id="2ba6a-126">修改 consoleasync.csproj</span><span class="sxs-lookup"><span data-stu-id="2ba6a-126">Modify consoleasync.csproj</span></span>

<span data-ttu-id="2ba6a-127">将项目使用的 C# 语言版本更新到 8.0 版。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-127">Let's update the C# language version the project uses to version 8.0.</span></span> <span data-ttu-id="2ba6a-128">编辑 consoleasync.csproj  文件并将 `<LangVersion>` 设置添加到`<PropertyGroup>` 节点。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-128">Edit the _consoleasync.csproj_ file and add the `<LangVersion>` setting to a `<PropertyGroup>` node.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.2</TargetFramework>

    <LangVersion>8.0</LangVersion>

  </PropertyGroup>
  
</Project>
```

## <a name="build-the-project"></a><span data-ttu-id="2ba6a-129">生成项目</span><span class="sxs-lookup"><span data-stu-id="2ba6a-129">Build the project</span></span>

<span data-ttu-id="2ba6a-130">在完成项目模板之前，应对其进行测试，确保它能够正确编译和运行。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-130">Before you complete a project template, you should test it to make sure it compiles and runs correctly.</span></span> <span data-ttu-id="2ba6a-131">在终端中，运行 `dotnet run` 命令，应能看到以下输出：</span><span class="sxs-lookup"><span data-stu-id="2ba6a-131">In your terminal, run the `dotnet run` command and you should see the following output:</span></span>

```console
C:\working\templates\consoleasync> dotnet run
Hello World with C# 8.0!
```

<span data-ttu-id="2ba6a-132">可以使用 `dotnet run` 删除已创建的 obj  和 bin  文件夹。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-132">You can delete the _obj_ and _bin_ folders created by using `dotnet run`.</span></span> <span data-ttu-id="2ba6a-133">删除这些文件可确保你的模板仅包含与模板相关的文件，而不包含生成操作产生的任何文件。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-133">Deleting these files ensures your template only includes the files related to your template and not any files that result of a build action.</span></span>

<span data-ttu-id="2ba6a-134">现在你已经创建了模板的内容，需要在模板的根文件夹中创建模板配置。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-134">Now that you have the content of the template created, you need to create the template config at the root folder of the template.</span></span>

## <a name="create-the-template-config"></a><span data-ttu-id="2ba6a-135">创建模板配置</span><span class="sxs-lookup"><span data-stu-id="2ba6a-135">Create the template config</span></span>

<span data-ttu-id="2ba6a-136">模板在 .NET Core 中通过模板根目录中的特殊文件夹和配置文件进行识别。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-136">Templates are recognized in .NET Core by a special folder and config file that exist at the root of your template.</span></span> <span data-ttu-id="2ba6a-137">在本教程中，你的模板文件夹位于 working\templates\consoleasync\\  。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-137">In this tutorial, your template folder is located at _working\templates\consoleasync\\_.</span></span>

<span data-ttu-id="2ba6a-138">创建模板时，除特殊配置文件夹外，模板文件夹中的所有文件和文件夹都作为模板的一部分包含在内。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-138">When you create a template, all files and folders in the template folder are included as part of the template except for the special config folder.</span></span> <span data-ttu-id="2ba6a-139">此配置文件夹名为“.template.config”  。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-139">This config folder is named _.template.config_.</span></span>

<span data-ttu-id="2ba6a-140">首先，创建一个名为“.template.config”  的新子文件夹，然后进入该文件夹。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-140">First, create a new subfolder named _.template.config_, enter it.</span></span> <span data-ttu-id="2ba6a-141">然后，创建一个名为“template.json”  的新文件。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-141">Then, create a new file named _template.json_.</span></span> <span data-ttu-id="2ba6a-142">文件夹结构应如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ba6a-142">Your folder structure should look like this:</span></span>

```console
working
└───templates
    └───consoleasync
        └───.template.config
                template.json
```

<span data-ttu-id="2ba6a-143">使用你喜爱的文本编辑器打开 template.json  并粘贴以下 json 代码，然后保存：</span><span class="sxs-lookup"><span data-stu-id="2ba6a-143">Open the _template.json_ with your favorite text editor and paste in the following json code and save it:</span></span>

```json
{
  "$schema": "http://json.schemastore.org/template",
  "author": "Me",
  "classifications": [ "Common", "Console", "C#8" ],
  "identity": "ExampleTemplate.AsyncProject",
  "name": "Example templates: async project",
  "shortName": "consoleasync",
  "tags": {
    "language": "C#",
    "type": "project"
  }
}
```

<span data-ttu-id="2ba6a-144">此配置文件包含模板的所有设置。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-144">This config file contains all of the settings for your template.</span></span> <span data-ttu-id="2ba6a-145">可以看到基本设置，例如 `name` 和 `shortName`，除此之外，还有一个设置为 `project` 的 `tags/type` 值。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-145">You can see the basic settings such as `name` and `shortName` but also there's a `tags/type` value that's set to `project`.</span></span> <span data-ttu-id="2ba6a-146">这会将模板指定为项目模板。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-146">This designates your template as a project template.</span></span> <span data-ttu-id="2ba6a-147">你创建的模板类型不存在限制。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-147">There's no restriction on the type of template you create.</span></span> <span data-ttu-id="2ba6a-148">`item` 和 `project` 值是 .NET Core 建议使用的通用名称，便于用户轻松筛选正在搜索的模板类型。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-148">The `item` and `project` values are common names that .NET Core recommends so that users can easily filter the type of template they're searching for.</span></span>

<span data-ttu-id="2ba6a-149">`classifications` 项表示你在运行 `dotnet new` 并获取模板列表时看到的“标记”  列。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-149">The `classifications` item represents the **tags** column you see when you run `dotnet new` and get a list of templates.</span></span> <span data-ttu-id="2ba6a-150">用户还可以根据分类标记进行搜索。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-150">Users can also search based on classification tags.</span></span> <span data-ttu-id="2ba6a-151">不要将 json 文件中的 `tags` 属性与 `classifications` 标记列表混淆。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-151">Don't confuse the `tags` property in the json file with the `classifications` tags list.</span></span> <span data-ttu-id="2ba6a-152">它们虽然具有类似的名称，但截然不同。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-152">They're two different things unfortunately named similarly.</span></span> <span data-ttu-id="2ba6a-153">template.json  文件的完整架构位于 [JSON 架构存储](http://json.schemastore.org/template)。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-153">The full schema for the *template.json* file is found at the [JSON Schema Store](http://json.schemastore.org/template).</span></span> <span data-ttu-id="2ba6a-154">有关 template.json  文件的详细信息，请参阅 [dotnet 创建模板 wiki](https://github.com/dotnet/templating/wiki)。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-154">For more information about the *template.json* file, see the [dotnet templating wiki](https://github.com/dotnet/templating/wiki).</span></span>

<span data-ttu-id="2ba6a-155">现在你已有一个有效的 .template.config/template.json  文件，可以安装模板了。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-155">Now that you have a valid _.template.config/template.json_ file, your template is ready to be installed.</span></span> <span data-ttu-id="2ba6a-156">在安装模板之前，请务必删除无需在模板中包含的任何额外文件夹和文件，例如 bin  或 obj  文件夹。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-156">Before you install the template, make sure that you delete any extra files folders and files you don't want included in your template, like the _bin_ or _obj_ folders.</span></span> <span data-ttu-id="2ba6a-157">在终端中，导航到 consoleasync  文件夹，并运行 `dotnet new -i .\` 以安装位于当前文件夹的模板。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-157">In your terminal, navigate to the _consoleasync_ folder and run `dotnet new -i .\` to install the template located at the current folder.</span></span> <span data-ttu-id="2ba6a-158">如果使用的是 Linux 或 MacOS 操作系统，请使用正斜杠：`dotnet new -i ./`。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-158">If you're using a Linux or MacOS operating system, use a forward slash: `dotnet new -i ./`.</span></span>

<span data-ttu-id="2ba6a-159">此命令输出安装的模板列表，其中应包括你的模板。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-159">This command outputs the list of templates installed, which should include yours.</span></span>

```console
C:\working\templates\consoleasync> dotnet new -i .\
Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.

... cut to save space ...

Templates                                         Short Name            Language          Tags
-------------------------------------------------------------------------------------------------------------------------------
Console Application                               console               [C#], F#, VB      Common/Console
Example templates: async project                  consoleasync          [C#]              Common/Console/C#8
Class library                                     classlib              [C#], F#, VB      Common/Library
WPF Application                                   wpf                   [C#], VB          Common/WPF
Windows Forms (WinForms) Application              winforms              [C#], VB          Common/WinForms
Worker Service                                    worker                [C#]              Common/Worker/Web
```

### <a name="test-the-project-template"></a><span data-ttu-id="2ba6a-160">测试项目模板</span><span class="sxs-lookup"><span data-stu-id="2ba6a-160">Test the project template</span></span>

<span data-ttu-id="2ba6a-161">现在你已安装了项模板，可对其进行测试。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-161">Now that you have an item template installed, test it.</span></span> <span data-ttu-id="2ba6a-162">导航到 test  文件夹，使用 `dotnet new console` 创建新的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-162">Navigate to the _test_ folder and create a new console application with `dotnet new console`.</span></span> <span data-ttu-id="2ba6a-163">这将生成一个可以使用 `dotnet run` 命令轻松测试的工作项目。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-163">This generates a working project you can easily test with the `dotnet run` command.</span></span>

```console
C:\test> dotnet new consoleasync
The template "Example templates: async project" was created successfully.
```

```console
C:\test> dotnet run
Hello World with C# 8.0!
```

<span data-ttu-id="2ba6a-164">祝贺你！</span><span class="sxs-lookup"><span data-stu-id="2ba6a-164">Congratulations!</span></span> <span data-ttu-id="2ba6a-165">你已使用 .NET Core 创建并部署了项目模板。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-165">You created and deployed a project template with .NET Core.</span></span> <span data-ttu-id="2ba6a-166">为准备学习本系列教程的下一部分，必须卸载已创建的模板。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-166">In preparation for the next part of this tutorial series, you must uninstall the template you created.</span></span> <span data-ttu-id="2ba6a-167">确保同时删除 test  文件夹中的所有文件。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-167">Make sure to delete all files from the _test_ folder too.</span></span> <span data-ttu-id="2ba6a-168">这将回到干净状态，为本教程的下一个主要部分做好准备。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-168">This will get you back to a clean state ready for the next major section of this tutorial.</span></span>

### <a name="uninstall-the-template"></a><span data-ttu-id="2ba6a-169">卸载模板</span><span class="sxs-lookup"><span data-stu-id="2ba6a-169">Uninstall the template</span></span>

<span data-ttu-id="2ba6a-170">由于模板是使用文件路径安装的，因此，必须使用绝对  文件路径将其卸载。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-170">Because you installed the template by using a file path, you must uninstall it with the **absolute** file path.</span></span> <span data-ttu-id="2ba6a-171">可以通过运行 `dotnet new -u` 命令看到已安装的模板列表。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-171">You can see a list of templates installed by running the `dotnet new -u` command.</span></span> <span data-ttu-id="2ba6a-172">你的模板应列在最后。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-172">Your template should be listed last.</span></span> <span data-ttu-id="2ba6a-173">使用列出的路径，通过执行 `dotnet new -u <ABSOLUTE PATH TO TEMPLATE DIRECTORY>` 命令卸载模板。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-173">Use the path listed to uninstall your template with the `dotnet new -u <ABSOLUTE PATH TO TEMPLATE DIRECTORY>` command.</span></span>

```console
C:\working> dotnet new -u
Template Instantiation Commands for .NET Core CLI

Currently installed items:
  Microsoft.DotNet.Common.ItemTemplates
    Templates:
      dotnet gitignore file (gitignore)
      global.json file (globaljson)
      NuGet Config (nugetconfig)
      Solution File (sln)
      Dotnet local tool manifest file (tool-manifest)
      Web Config (webconfig)

... cut to save space ...

  NUnit3.DotNetNew.Template
    Templates:
      NUnit 3 Test Project (nunit) C#
      NUnit 3 Test Item (nunit-test) C#
      NUnit 3 Test Project (nunit) F#
      NUnit 3 Test Item (nunit-test) F#
      NUnit 3 Test Project (nunit) VB
      NUnit 3 Test Item (nunit-test) VB
  C:\working\templates\consoleasync
    Templates:
      Example templates: async project (consoleasync) C#
```

```console
C:\working> dotnet new -u C:\working\templates\consoleasync
```

## <a name="next-steps"></a><span data-ttu-id="2ba6a-174">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2ba6a-174">Next steps</span></span>

<span data-ttu-id="2ba6a-175">在本教程中，你创建了一个项目模板。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-175">In this tutorial, you created a project template.</span></span> <span data-ttu-id="2ba6a-176">若要了解如何将项模板和项目模板打包为易于使用的文件，请继续学习本教程系列。</span><span class="sxs-lookup"><span data-stu-id="2ba6a-176">To learn how to package both the item and project templates into an easy-to-use file, continue this tutorial series.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ba6a-177">创建模板包</span><span class="sxs-lookup"><span data-stu-id="2ba6a-177">Create a template pack</span></span>](cli-templates-create-template-pack.md)