---
title: "<list> - C# Programming Guide"
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords: 
  - "list"
  - "<list>"
helpviewer_keywords: 
  - "list C# XML tag"
  - "listheader C# XML tag"
  - "<listheader> C# XML tag"
  - "item C# XML tag"
  - "<item> C# XML tag"
  - "<list> C# XML tag"
ms.assetid: c9620b1b-c2e6-43f1-ab88-8ab47308ffec
---
# \<list> (C# Programming Guide)
## Syntax  
  
```xml  
<list type="bullet" | "number" | "table">  
    <listheader>  
        <term>term</term>  
        <description>description</description>  
    </listheader>  
    <item>  
        <term>term</term>  
        <description>description</description>  
    </item>  
</list>  
```  
  
## Parameters  
 `term`  
 A term to define, which will be defined in `description`.  
  
 `description`  
 Either an item in a bullet or numbered list or the definition of a `term`.  
  
## Remarks  
 The \<listheader> block is used to define the heading row of either a table or definition list. When defining a table, you only need to supply an entry for term in the heading.  
  
 Each item in the list is specified with an \<item> block. When creating a definition list, you will need to specify both `term` and `description`. However, for a table, bulleted list, or numbered list, you only need to supply an entry for `description`.  
  
 A list or table can have as many \<item> blocks as needed.  
  
 Compile with [/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) to process documentation comments to a file.  
  
## Example  
 [!code-csharp[csProgGuideDocComments#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#6)]  
  
## See also

- [C# Programming Guide](../../../csharp/programming-guide/index.md)
- [Recommended Tags for Documentation Comments](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)
