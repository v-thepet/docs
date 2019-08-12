---
title: "Optional parameters must specify a default value"
ms.date: 07/20/2015
f1_keywords: 
  - "vbc30812"
  - "bc30812"
helpviewer_keywords: 
  - "BC30812"
ms.assetid: 5091a250-be66-413b-98a3-2a9974c4d600
---
# Optional parameters must specify a default value
Optional parameters must provide default values that can be used if no parameter is supplied by a calling procedure.  
  
 **Error ID:** BC30812  
  
## To correct this error  
  
- Specify default values for optional parameters; for example:  
  
    ```  
    Sub Proc1(ByVal X As Integer,   
          Optional ByVal Y As String = "Default Value")  
       MsgBox("Default argument is: " & Y)  
    End Sub  
    ```  
  
## See also

- [Optional](../../../visual-basic/language-reference/modifiers/optional.md)
