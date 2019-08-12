---
title: "Using nullable types - C# Programming Guide"
ms.custom: seodec18
description: Learn how to work with C# nullable types
ms.date: 08/02/2018
helpviewer_keywords: 
  - "nullable types [C#], about nullable types"
ms.assetid: 0bacbe72-ce15-4b14-83e1-9c14e6380c28
---
# Using nullable types (C# Programming Guide)

Nullable types are types that represent all the values of an underlying value type `T`, and an additional [null](../../language-reference/keywords/null.md) value. For more information, see the [Nullable types](index.md) topic.

You can refer to a nullable type in any of the following forms: `Nullable<T>` or `T?`. These two forms are interchangeable.  
  
## Declaration and assignment

As a value type can be implicitly converted to the corresponding nullable type, you assign a value to a nullable type as you would for its underlying value type. You also can assign the `null` value.  For example:
  
[!code-csharp[declare and assign](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#1)]

## Examination of a nullable type value

Use the following readonly properties to examine an instance of a nullable type for null and retrieve a value of an underlying type:  
  
- <xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> indicates whether an instance of a nullable type has a value of its underlying type.
  
- <xref:System.Nullable%601.Value%2A?displayProperty=nameWithType> gets the value of an underlying type if <xref:System.Nullable%601.HasValue%2A> is `true`. If <xref:System.Nullable%601.HasValue%2A> is `false`, the <xref:System.Nullable%601.Value%2A> property throws an <xref:System.InvalidOperationException>.
  
The code in the following example uses the `HasValue` property to test whether the variable contains a value before displaying it:
  
[!code-csharp-interactive[use HasValue](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#2)]
  
You also can compare a nullable type variable with `null` instead of using the `HasValue` property, as the following example shows:  
  
[!code-csharp-interactive[use comparison with null](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#3)]

Beginning with C# 7.0, you can use [pattern matching](../../pattern-matching.md) to both examine and get a value of a nullable type:

[!code-csharp-interactive[use pattern matching](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#4)]

## Conversion from a nullable type to an underlying type

If you need to assign a nullable type value to a non-nullable type, use the [null-coalescing operator `??`](../../language-reference/operators/null-coalescing-operator.md) to specify the value to be assigned if a nullable type value is null (you also can use the <xref:System.Nullable%601.GetValueOrDefault(%600)?displayProperty=nameWithType> method to do that):
  
[!code-csharp-interactive[?? operator](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#5)]

Use the <xref:System.Nullable%601.GetValueOrDefault?displayProperty=nameWithType> method if the value to be used when a nullable type value is null should be the default value of the underlying value type.
  
You can explicitly cast a nullable type to a non-nullable type. For example:  
  
[!code-csharp[explicit cast](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#6)]

At run time, if the value of a nullable type is null, the explicit cast throws an <xref:System.InvalidOperationException>.

A non-nullable value type is implicitly converted to the corresponding nullable type.
  
## Operators

The predefined unary and binary operators and any user-defined operators that exist for value types may also be used by nullable types. These operators produce a null value if one or both operands are null; otherwise, the operator uses the contained values to calculate the result. For example:  
  
[!code-csharp[operators](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#7)]

> [!NOTE]
> For the `bool?` type, the predefined `&` and `|` operators don't follow the rules described in this section: the result of an operator evaluation can be non-null even if one of the operands is null. For more information, see the [Nullable Boolean logical operators](../../language-reference/operators/boolean-logical-operators.md#nullable-boolean-logical-operators) section of the [Boolean logical operators](../../language-reference/operators/boolean-logical-operators.md) article.
  
For the relational operators (`<`, `>`, `<=`, `>=`), if one or both operands are null, the result is `false`. Do not assume that because a particular comparison (for example, `<=`) returns `false`, the opposite comparison (`>`) returns `true`. The following example shows that 10 is

- neither greater than or equal to null,
- nor less than null.
  
[!code-csharp-interactive[relational and equality operators](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#8)]
  
The above example also shows that an equality comparison of two nullable types that are both null evaluates to `true`.

For more information, see the [Lifted operators](~/_csharplang/spec/expressions.md#lifted-operators) section of the [C# language specification](~/_csharplang/spec/introduction.md).

## Boxing and unboxing

A nullable value type is [boxed](../types/boxing-and-unboxing.md) by the following rules:

- If <xref:System.Nullable%601.HasValue%2A> returns `false`, the null reference is produced.  
- If <xref:System.Nullable%601.HasValue%2A> returns `true`, a value of the underlying value type `T` is boxed, not the instance of <xref:System.Nullable%601>.

You can unbox the boxed value type to the corresponding nullable type, as the following example shows:

[!code-csharp-interactive[boxing and unboxing](../../../../samples/snippets/csharp/programming-guide/nullable-types/NullableTypesUsage.cs#9)]

## See also

- [Nullable types](index.md)
- [C# Programming Guide](../../programming-guide/index.md)
- [What exactly does 'lifted' mean?](https://blogs.msdn.microsoft.com/ericlippert/2007/06/27/what-exactly-does-lifted-mean/)
