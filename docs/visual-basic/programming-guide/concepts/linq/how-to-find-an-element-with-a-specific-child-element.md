---
title: 如何：查找具有特定子元素的元素
ms.date: 07/20/2015
ms.assetid: b0d0a463-6a85-46c3-8453-ad25b0ecf93c
ms.openlocfilehash: a00ca238c67e2edf4e2e68a46fbd7e2cb480ba15
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/22/2019
ms.locfileid: "74352923"
---
# <a name="how-to-find-an-element-with-a-specific-child-element-visual-basic"></a>如何：查找具有特定子元素的元素（Visual Basic）
本主题演示如何查找特定元素，该特定元素包含具有特定值的子元素。  
  
## <a name="example"></a>示例  
 示例查找 `Test` 元素，该元素包含具有值为“Examp2.EXE”的 `CommandLine` 子元素。  
  
 本示例使用以下 XML 文档：[示例 XML 文件：测试配置 (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-test-configuration-linq-to-xml.md)。  
  
```vb  
Dim root As XElement = XElement.Load("TestConfig.xml")  
Dim tests As IEnumerable(Of XElement) = _  
    From el In root.<Test> _  
    Where el.<CommandLine>.Value = "Examp2.EXE" _  
    Select el  
For Each el as XElement In tests  
    Console.WriteLine(el.@TestId)  
Next  
```  
  
 此代码生成以下输出：  
  
```console  
0002  
0006  
```  
  
 请注意，此示例使用[Xml 子轴属性](../../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)、 [xml 属性轴属性](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)和[xml 值属性](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示如何对命名空间中的 XML 进行同样的查询。 有关详细信息，请参阅[命名空间概述（LINQ to XML）（Visual Basic）](namespaces-overview-linq-to-xml.md)。  
  
 本示例使用以下 XML 文档：[示例 XML 文件：命名空间中的测试配置](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-test-configuration-in-a-namespace.md)。  
  
```vb  
Imports <xmlns='http://www.adatum.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = XElement.Load("TestConfigInNamespace.xml")  
        Dim tests As IEnumerable(Of XElement) = _  
            From el In root.<Test> _  
            Where el.<CommandLine>.Value = "Examp2.EXE" _  
            Select el  
        For Each el As XElement In tests  
            Console.WriteLine(el.@TestId)  
        Next  
    End Sub  
End Module  
```  
  
 此代码生成以下输出：  
  
```console  
0002  
0006  
```  
  
## <a name="see-also"></a>另请参阅

- <xref:System.Xml.Linq.XElement.Attribute%2A>
- <xref:System.Xml.Linq.XContainer.Elements%2A>
- [基本查询（LINQ to XML）（Visual Basic）](../../../../visual-basic/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)
- [标准查询运算符概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [投影操作（Visual Basic）](../../../../visual-basic/programming-guide/concepts/linq/projection-operations.md)
