---
title: 什么是模型生成器，它的工作原理是怎样的？
description: 如何使用 ML.NET 模型生成器自动训练机器学习模型
ms.date: 01/07/2020
ms.custom: overview, mlnet-tooling
ms.openlocfilehash: cff4601843ec9ca7201ea7dbdbfbcfa18f50e46e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2020
ms.locfileid: "79397805"
---
# <a name="what-is-model-builder-and-how-does-it-work"></a>什么是模型生成器，它的工作原理是怎样的？

ML.NET 模型生成器是一个直观的图形化 Visual Studio 扩展，用于生成、训练和部署自定义机器学习模型。

模型生成器使用自动化的机器学习 (AutoML) 来探索不同的机器学习算法和设置，以帮助找到最合适的方案。

使用模型生成器不需要具备机器学习的专业知识。 只需要一些数据，和确定要解决的问题。 模型生成器会生成将模型添加到 .NET 应用程序的代码。

![模型生成器 Visual Studio 扩展用户界面动画](media/ml-dotnet-model-builder.gif)

> [!NOTE]
> 模型生成器当前为预览版。

## <a name="scenarios"></a>方案

可以为模型生成器提供许多不同的方案，从而为应用程序生成一个机器学习模型。

方案就是要使用数据进行预测类型的描述。 例如：

- 根据历史销售数据预测未来的产品销量
- 根据客户评价将情绪分类为正面或负面
- 检测某项银行交易是否存在欺诈性
- 将客户反馈问题传递至公司中合适的团队

### <a name="which-machine-learning-scenario-is-right-for-me"></a>哪个机器学习方案最适合我？

在模型生成器中，你需要选择一个方案。 方案类型取决于尝试进行的预测类型。

#### <a name="predict-a-category-when-there-are-only-two-categories"></a>预测类别（只有两个类别时）

二元分类用于将数据分为两个类别（是/否；通过/失败；true/false；正面/负面）。

![显示二元分类示例（包括欺诈检测、风险环节和应用程序屏蔽）的图示](media/binary-classification-examples.png)

情绪分析可用于预测的客户反馈中的正面情绪或负面情绪。 这是一个二元分类机器学习任务的示例。

如果方案需要将数据分为两类，可以将该模板与自己的数据集配合使用。

#### <a name="predict-a-category-when-there-are-three-or-more-categories"></a>预测类别（有三个或更多个类别时）

多类分类可用于将数据分为三类或更多类。

![多类分类示例，包括文档和产品分类、支持票证路由以及客户问题优先级](media/multiclass-classification-examples.png)

问题分类可用于使用问题标题和描述对客户反馈（例如 GitHub 上的反馈）问题进行分类。 这是一个多类分类机器学习任务的示例。

如果需要将数据分为三类或更多类，可以使用问题分类模板。

#### <a name="predict-a-number"></a>预测数字

回归用于预测数字。

![显示回归示例（如价格预测、销售预测和预测性维护）的图示](media/regression-examples.png)

价格预测可以通过房屋的位置、大小等特点来预测房价。 这是一个回归机器学习任务的示例。

如果要使用自己的数据集预测数字值，可以使用价格预测模板。

#### <a name="classify-images-into-categories"></a>将图像分类为类别

此方案是多类分类的一种特殊情况，其中分类的输入数据是一组图像。

图像分类可用于标识不同类别的图像。 例如，不同类型的地形或动物或制造缺陷。

如果你有一组图像，并且想要将图像分为不同的类别，则可以使用适用于你的方案的图像分类模板。

#### <a name="custom-scenario"></a>自定义方案

使用自定义方案，可以手动选择自己的方案。

## <a name="data"></a>数据

选择方案后，模型生成器会要求你提供数据集。 这些数据用于训练、评估和选择最适合方案的的模型。

![显示模型生成器步骤的图示](media/model-builder-steps.png)

模型生成器支持 .tsv、.csv、.txt 格式以及 SQL 数据库格式的数据集。 如果你有一个 .txt 文件，则应使用 `,`、`;` 或 `/t` 分隔列，并且该文件必须具有标题行。

如果数据集由图像组成，则支持的文件类型为 `.jpg` 和 `.png`。

有关详细信息，请参阅[将训练数据加载到模型生成器](how-to-guides/load-data-model-builder.md)。

### <a name="choose-the-output-to-predict-label"></a>选择要预测的输出（标签）

数据集是一个表格，其中，行中含训练示例，列中含特性。 每一行都具有：

- 一个标签，即要预测的特性 
- 特征（为预测标签而用作输入的特性）  。

在房价预测方案中，特性可能是：

- 房屋的面积
- 卧室和卫生间的数量
- 邮政编码

标签是与其所属行（包含面积、卧室和卫生间值以及邮政编码信息）对应的历史房价。

![表显示房价数据的行和列，其中包含由大小、房间数、邮政编码和价格标签组成的特征](media/model-builder-data.png)

### <a name="example-datasets"></a>示例数据集

如果还没有自己的数据，请试用以下数据集之一：

|方案|ML 任务|数据|Label|特征|
|-|-|-|-|-|
|价格预测|回归|[出租车费数据](https://github.com/dotnet/machinelearning-samples/blob/master/datasets/taxi-fare-train.csv)|车费|行程时间、距离|
|异常情况检测|二元分类|[产品销售数据](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv)|产品销售额|月份|
|情绪分析|二元分类|[网站评论数据](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv)|标签（负面情绪为 0，正面情绪为 1）|评论、年份|
|欺诈检测|二元分类|[信用卡数据](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/BinaryClassification_CreditCardFraudDetection/CreditCardFraudDetection.Trainer/assets/input/creditcardfraud-dataset.zip)|类（存在欺诈性为 1，否则为 0）|金额，V1-V28（匿名处理后的特征）|
|文本分类|多类分类|[GitHub 问题数据](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/end-to-end-apps/MulticlassClassification-GitHubLabeler/GitHubLabeler/Data/corefx-issues-train.tsv)|区域|标题、描述|
|图像分类|多类分类|[花卉图像](http://download.tensorflow.org/example_images/flower_photos.tgz)|花卉类型：雏菊、蒲公英、玫瑰、向日葵、郁金香|图像数据本身|

## <a name="train"></a>训练

选择方案、数据和标签后，模型生成器会训练该模型。

### <a name="what-is-training"></a>什么是训练？

训练是一个自动的过程，模型生成器通过该过程教模型如何回答方案相关的问题。 训练后，模型可以对其没有见过的输入数据进行预测。 例如，在预测房价时，可以预测新上市的房屋销售价。

因为模型生成器使用自动机器学习 (AutoML)，所以在训练期间不需要任何人工输入或微调操作。

### <a name="how-long-should-i-train-for"></a>训练时长应为多长时间？

模型生成器使用 AutoML 浏览多个模型，以查找性能最佳的模型。

更长的训练周期允许 AutoML 通过更多设置来浏览更多模型。

下表汇总了在本地计算机上为一组示例数据集获取良好性能所花的平均时间。

|数据集大小|训练的平均时间|
|------------|---------------------|
|0 - 10 MB|10 秒|
|10 - 100 MB|10 分钟|
|100 - 500 MB|30 分钟|
|500 - 1 GB|60 分钟|
|1 GB 以上|3 小时以上|

这些数字仅用于指南。 训练的确切长度取决于：

- 用作模型输入的特征（列）数
- 列的类型
- ML 任务
- 用于训练的计算机的 CPU、磁盘和内存性能

## <a name="evaluate"></a>评估

评估是衡量模型品质的过程。 模型生成器使用经过训练的模型对新的测试数据进行预测，然后度量预测效果的过程。

模型生成器将训练数据拆分为训练集和测试集。 训练数据 (80%) 用于训练模型，测试数据 (20%) 用于评估模型。

### <a name="how-do-i-understand-my-model-performance"></a>如何了解模型性能？

方案映射到机器学习任务。 每个 ML 任务都有其自己的一组评估指标。

#### <a name="regression-for-example-price-prediction"></a>回归（例如，价格预测）

回归问题的默认指标为 RSquared，RSquared 值的范围介于 0 和 1 之间。 1 是可能的最大值，换句话说，RSquared 的值越接近 1，模型的性能就越好。

报告的其他指标（如绝对损失、平方损失和 RMS 损失）为附加指标，可以用来理解模型的性能，并将其与其他回归模型进行比较。

#### <a name="binary-classification-for-example-sentiment-analysis"></a>二元分类（例如情绪分析）

分类问题的默认指标是“准确性”。 准确性定义的是模型对测试数据集做出的正确预测的比例。 越接近 100% 或 1.0 越好。

报告的其他指标，如 AUC（曲线下面积），用于度量真正率和假正率之间的比例，在高于 0.50 时，才是可以接受的模型。

F1 分数等其他指标可用于控制精准率与召回率之间的平衡。

#### <a name="multi-class-classification-for-example-issue-classification-image-classification"></a>多类分类（例如，问题分类、映像分类）

多类分类问题的默认指标是微观准确性。 微观准确性越接近 100% 或 1.0 越好。

多类分类的另一个重要指标是宏观准确性，类似于微观准确性，越接近 1.0 越好。 考虑这两种准确性类型的一种好方法是：

- 微观准确性：传入票证分类给正确团队的频率如何？
- 宏观准确性：对于普通团队而言，传入票证符合其业务范围的频率如何？

### <a name="more-information-on-evaluation-metrics"></a>有关评估指标的详细信息

有关详细信息，请参阅[模型评估指标](resources/metrics.md)。

## <a name="improve"></a>改进

如果模型性能评分不符合预期，可以：

- 延长训练时间。 有了更多时间，自动机器学习引擎可以尝试更多算法和设置。

- 添加更多数据。 有时候可能是数据量不足，无法训练出高质量的机器学习模型。

- 均衡分配数据。 对于分类任务，请确保在各个类别间均匀分配训练集。 例如，若有四个类别和 100 个训练示例，前两类（标记 1 和标记 2）包含 90 个记录，而剩下两类（标记 3 和标记 4）只包含 10 个记录，这就存在数据不均衡的问题，可能会导致模型很难正确预测标记 3 或标记 4。

## <a name="code"></a>代码

完成评估阶段后，模型生成器会输出一份模型文件和代码，可以使用该代码将模型添加到应用程序。 ML.NET 模型保存为 zip 文件。 用于加载和使用模型的代码会以新项目的形式添加到解决方案中。 模型生成器还会添加一个示例控制台应用，可以运行该应用来查看工作状态下的模型。

此外，模型生成器还会输出生成模型的代码，以便你能了解生成模型所使用的步骤。 还可以通过模型训练代码使用新的数据重新训练模型。

## <a name="whats-next"></a>后续步骤

[安装](how-to-guides/install-model-builder.md)模型生成器 Visual Studio 扩展

请尝试[价格预测或任何回归方案](tutorials/predict-prices-with-model-builder.md)
