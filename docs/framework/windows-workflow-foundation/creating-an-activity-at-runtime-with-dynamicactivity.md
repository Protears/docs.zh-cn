---
title: 使用 DynamicActivity 在运行时创建活动
ms.date: 03/30/2017
ms.assetid: 1af85cc6-912d-449e-90c5-c5db3eca5ace
ms.openlocfilehash: 871108fd09e9127b3f9e06174f05a47c7fd7682c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182981"
---
# <a name="creating-an-activity-at-runtime-with-dynamicactivity"></a>使用 DynamicActivity 在运行时创建活动
<xref:System.Activities.DynamicActivity> 是一个带有公共构造函数的具体的密封类。 通过使用活动 DOM，<xref:System.Activities.DynamicActivity> 可用于在运行时组合活动功能。  
  
## <a name="dynamicactivity-features"></a>DynamicActivity 功能  
 <xref:System.Activities.DynamicActivity> 有权访问执行属性、自变量和变量，但无权访问运行时服务（例如安排子活动或跟踪）。  
  
 使用工作流 <xref:System.Activities.Argument> 对象可以设置顶级属性。 在命令性代码中，使用新类型的 CLR 属性创建这些参数。 在 XAML 中，使用 `x:Class` 和 `x:Member` 标记声明这些参数。  
  
 使用 <xref:System.Activities.DynamicActivity> 构造的活动使用 <xref:System.ComponentModel.ICustomTypeDescriptor> 与设计器交互。 可以使用 <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A> 动态加载在设计器中创建的活动，如下面的过程所示。  
  
#### <a name="to-create-an-activity-at-runtime-using-imperative-code"></a>使用命令性代码在运行时创建活动  
  
1. 开放视觉工作室 2010.  
  
2. 选择**文件**，**新建**，**项目**. 在 **"项目类型"** 窗口中的 **"可视化 C#"** 下选择**工作流 4.0，** 然后选择**v2010**节点。 在**模板**窗口中选择**顺序工作流控制台应用程序**。 将新项目命名为 DynamicActivitySample。  
  
3. 右键单击 HelloActivity 项目中的工作流1.xaml，然后选择 **"删除**"。  
  
4. 打开 Program.cs。 将下面的指令添加到文件的顶部。  
  
    ```csharp  
    using System.Collections.Generic;  
    ```  
  
5. 将 `Main` 方法的内容替换为以下代码，这会创建一个包含单个 <xref:System.Activities.Statements.Sequence> 活动的 <xref:System.Activities.Statements.WriteLine> 活动，并将后者赋给新动态活动的 <xref:System.Activities.DynamicActivity.Implementation%2A> 属性。  
  
    ```csharp  
    //Define the input argument for the activity  
    var textOut = new InArgument<string>();  
    //Create the activity, property, and implementation  
                Activity dynamicWorkflow = new DynamicActivity()  
                {  
                    Properties =
                    {  
                        new DynamicActivityProperty  
                        {  
                            Name = "Text",  
                            Type = typeof(InArgument<String>),  
                            Value = textOut  
                        }  
                    },  
                    Implementation = () => new Sequence()  
                    {  
                        Activities =
                        {  
                            new WriteLine()  
                            {  
                                Text = new InArgument<string>(env => textOut.Get(env))  
                            }  
                        }  
                    }  
                };  
    //Execute the activity with a parameter dictionary  
                WorkflowInvoker.Invoke(dynamicWorkflow, new Dictionary<string, object> { { "Text", "Hello World!" } });  
                Console.ReadLine();  
    ```  
  
6. 执行应用程序。 控制台窗口，上面写着"你好世界！ 显示。  
  
#### <a name="to-create-an-activity-at-runtime-using-xaml"></a>使用 XAML 在运行时创建活动  
  
1. 开放视觉工作室 2010.  
  
2. 选择**文件**，**新建**，**项目**. 在 **"项目类型"** 窗口中的 **"可视化 C#"** 下选择**工作流 4.0，** 然后选择**v2010**节点。 在**模板**窗口中选择**工作流控制台应用程序**。 将新项目命名为 DynamicActivitySample。  
  
3. 在 HelloActivity 项目中打开 Workflow1.xaml。 单击设计器底部的 **"参数"** 选项。 创建一个 `In` 类型的新 `TextToWrite` 自变量，并将其命名为 `String`。  
  
4. 将 **"写入线"** 活动从工具箱的 **"原始"** 部分拖动到设计器曲面上。 将值`TextToWrite`分配给活动的**Text**属性。  
  
5. 打开 Program.cs。 将下面的指令添加到文件的顶部。  
  
    ```csharp  
    using System.Activities.XamlIntegration;  
    ```  
  
6. 将 `Main` 方法的内容替换为以下代码。  
  
    ```csharp  
    Activity act2 = ActivityXamlServices.Load(@"Workflow1.xaml");  
                    results = WorkflowInvoker.Invoke(act2, new Dictionary<string, object> { { "TextToWrite", "HelloWorld!" } });  
    Console.ReadLine();  
    ```  
  
7. 执行应用程序。 控制台窗口，上面写着"你好世界！  将出现。  
  
8. 右键单击**解决方案资源管理器**中的 Workflow1.xaml 文件，然后选择 **"查看代码**"。 请注意，活动类使用 `x:Class` 创建，属性使用 `x:Property` 创建。  
  
## <a name="see-also"></a>另请参阅

- [使用命令性代码创作工作流、活动和表达式](authoring-workflows-activities-and-expressions-using-imperative-code.md)
