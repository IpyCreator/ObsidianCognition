The most important reason to define a  
model layer is to have a single source of  
truth in our program that is c]ean and we]]  
behaved and not governed by the imple  
mentation details of the application frame  
work.  
An app/ication .franzework provides in  
frastructure upon which we can build ap  
plications. In this book we use Cocoa  
more specifically, UIKit, AppKit, or Wat  
chKit, depending on the target platform  
the anni icafinn fra m ewnrk.  

  
If the model layer is kept separate from the application framework, we can use it completely outside the bounds of the ap- plication. We can easily run it in a separa- te testing harness, or we can write a new vi- ew layer using a different application fra- mework and use our model layer in the An- droid, macOS, or Windows version of the application.  

  

  
Different parts of the path between the model layer and view layer have different names. The name view action refers to the code path triggered by a view in response to a user-initiated event, such as a tapping a button or selecting a row in a table view. When a view action is sent through to the model layer, it may be converted intoa nzodeJ action (an instruction to a model ob- ject to perform an action or update). This instruction might also be called a nzessage (particularly when the model is changed using a redt£cer). The transformation of vi-  

[[Coordinator design pattern]]

**Refactoring**

Modularization

https://tech.olx.com/modular-architecture-in-ios-c1a1e3bff8e9

  

  

  

  

[[PW App Modularisation]]