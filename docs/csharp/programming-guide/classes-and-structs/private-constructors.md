---
title: "Private Constructors - C# Programming Guide"
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords: 
  - "C# language, private constructors"
  - "private constructors [C#]"
ms.assetid: 29eeaa7d-8d81-453c-94b9-0e2800172621
---
# Private Constructors (C# Programming Guide)
A private constructor is a special instance constructor. It is generally used in classes that contain static members only. If a class has one or more private constructors and no public constructors, other classes (except nested classes) cannot create instances of this class. For example:  
  
 [!code-csharp[csProgGuideObjects#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#11)]  
  
 The declaration of the empty constructor prevents the automatic generation of a parameterless constructor. Note that if you do not use an access modifier with the constructor it will still be private by default. However, the [private](../../../csharp/language-reference/keywords/private.md) modifier is usually used explicitly to make it clear that the class cannot be instantiated.  
  
 Private constructors are used to prevent creating instances of a class when there are no instance fields or methods, such as the <xref:System.Math> class, or when a method is called to obtain an instance of a class. If all the methods in the class are static, consider making the complete class static. For more information see [Static Classes and Static Class Members](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md).  
  
## Example  
 The following is an example of a class using a private constructor.  
  
 [!code-csharp[csProgGuideObjects#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#12)]  
  
 Notice that if you uncomment the following statement from the example, it will generate an error because the constructor is inaccessible because of its protection level:  
  
 [!code-csharp[csProgGuideObjects#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#13)]  
  
## C# Language Specification  

For more information, see [Private constructors](~/_csharplang/spec/classes.md#private-constructors) in the [C# Language Specification](../../language-reference/language-specification/index.md). The language specification is the definitive source for C# syntax and usage.
  
## See also

- [C# Programming Guide](../../../csharp/programming-guide/index.md)
- [Classes and Structs](../../../csharp/programming-guide/classes-and-structs/index.md)
- [Constructors](../../../csharp/programming-guide/classes-and-structs/constructors.md)
- [Finalizers](../../../csharp/programming-guide/classes-and-structs/destructors.md)
- [private](../../../csharp/language-reference/keywords/private.md)
- [public](../../../csharp/language-reference/keywords/public.md)
