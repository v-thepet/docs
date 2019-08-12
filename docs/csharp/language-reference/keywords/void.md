---
title: "void - C# Reference"
ms.custom: seodec18

ms.date: 07/20/2015
f1_keywords: 
  - "void_CSharpKeyword"
  - "void"
helpviewer_keywords: 
  - "void keyword [C#]"
ms.assetid: 0d2d8a95-fe20-4fbd-bf5d-c1e54bce71d4
---
# void (C# Reference)

When used as the return type for a method, `void` specifies that the method doesn't return a value.

`void` isn't allowed in the parameter list of a method. A method that takes no parameters and returns no value is declared as follows:

```csharp
public void SampleMethod()
{
    // Body of the method.
}
```

`void` is also used in an unsafe context to declare a pointer to an unknown type. For more information, see [Pointer types](../../programming-guide/unsafe-code-pointers/pointer-types.md).

`void` is an alias for the .NET Framework <xref:System.Void?displayProperty=nameWithType> type.

## C# language specification

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## See also

- [C# Reference](../index.md)
- [C# Programming Guide](../../programming-guide/index.md)
- [C# Keywords](index.md)
- [Reference Types](reference-types.md)
- [Value Types](value-types.md)
- [Methods](../../programming-guide/classes-and-structs/methods.md)
- [Unsafe Code and Pointers](../../programming-guide/unsafe-code-pointers/index.md)
