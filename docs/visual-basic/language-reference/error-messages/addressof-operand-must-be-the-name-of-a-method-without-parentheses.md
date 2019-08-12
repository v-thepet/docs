---
title: "'AddressOf' operand must be the name of a method (without parentheses)"
ms.date: 07/20/2015
f1_keywords: 
  - "vbc30577"
  - "bc30577"
helpviewer_keywords: 
  - "BC30577"
ms.assetid: c2c55640-5c61-4e66-97a4-4322020c6001
---
# 'AddressOf' operand must be the name of a method (without parentheses)
The `AddressOf` operator creates a procedure delegate instance that references a specific procedure. The syntax is as follows.  
  
 `AddressOf` `procedurename`  
  
 You inserted parentheses around the argument following `AddressOf`, where none are needed.  
  
 **Error ID:** BC30577  
  
## To correct this error  
  
1. Remove the parentheses around the argument following `AddressOf`.  
  
2. Make sure the argument is a method name.  
  
## See also

- [AddressOf Operator](../../../visual-basic/language-reference/operators/addressof-operator.md)
- [Delegates](../../../visual-basic/programming-guide/language-features/delegates/index.md)
