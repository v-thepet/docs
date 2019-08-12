---
title: "<permission> - C# Programming Guide"
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords: 
  - "permission"
  - "<permission>"
helpviewer_keywords: 
  - "<permission> C# XML tag"
  - "permission C# XML tag"
ms.assetid: 769e93fe-8404-443f-bf99-577aa42b6a49
---
# \<permission> (C# Programming Guide)
## Syntax  
  
```xml  
<permission cref="member">description</permission>  
```  
  
## Parameters  
 cref = " `member`"  
 A reference to a member or field that is available to be called from the current compilation environment. The compiler checks that the given code element exists and translates `member` to the canonical element name in the output XML. *member* must appear within double quotation marks (" ").  
  
 For information on how to create a cref reference to a generic type, see [\<see>](../../../csharp/programming-guide/xmldoc/see.md).  
  
 `description`  
 A description of the access to the member.  
  
## Remarks  
 The \<permission> tag lets you document the access of a member. The <xref:System.Security.PermissionSet> class lets you specify access to a member.  
  
 Compile with [/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) to process documentation comments to a file.  
  
## Example  
 [!code-csharp[csProgGuideDocComments#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#8)]  
  
## See also

- [C# Programming Guide](../../../csharp/programming-guide/index.md)
- [Recommended Tags for Documentation Comments](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)
