### Implementing an interface with ASNA Visual RPG

This example shows how to implement .NET's IComparable interface in ANSA Visual RPG (AVR). The IComparable interface is generalized way to compare two objects. It is often used for sorting purposes. 

The [IComparable docs](https://docs.microsoft.com/en-us/dotnet/api/system.icomparable?view=netframework-4.7.1) shows an example of sorting a range of temperatures in C#. This example implements that code in Visual RPG. 

AVR can implement any non-generic .NET interface. That is, it can implement the [IComparable](https://docs.microsoft.com/en-us/dotnet/api/system.icomparable?view=netframework-4.7.1#methods) interface, but it cannot implement the generic [IComparable\<T>](https://docs.microsoft.com/en-us/dotnet/api/system.icomparable-1?view=netframework-4.7.1) interface. 

If you need to implement a generic interface, we recommend you make a separate C# DLL to do that work and then reference that C# DLL with AVR. 


### C# and AVR coding comparisons

#### Declaring a class

* C# uses braces to begin and end a class;  AVR uses `BegClass` and `EndClass`. 
* C# uses the `:` operator to identify a class name which this class extends and/or interfaces this class extends; AVR uses the `Extends` and `Implements` keyword to indicate those classes (respectively).
* C# uses the `public` keyword to indicate public scope; AVR uses the `Access` keyword to indicate class scope. 

**C#** 

    public class Temperature : IComparable
    {
        ...
    }


**AVR**

    BegClass Temperature Implements(IComparable) Access(*Public)
        ...
    EndClass

#### Declaring a field     

* C# can declare and assign a value on one line; AVR can do that to some degree using the `Inz` keyword as the initial value. However, `Inz` can't do some more sophisticated assignments, so it's often best in AVR to split the declaration and the assignment into separate lines. 
* C# supports block-level variables; AVR does not. Therefore, in AVR you usually always declare all of a routine's variables at the top of the routine. You can declare them inside a block, but they aren't blocked scoped--they are scoped to the routine. Declaring them inside a block may be misleading or confusing to anyone who sees that and expects block-scoped behavior. 
* C# uses the 'as' keyword as a way to cast a variable; AVR uses the `*AS` operator.

**C#**

    Temperature otherTemperature = obj as Temperature;

**AVR**

    DclFld otherTemperature Type(Temperature)

    otherTemperature = obj *As Temperature 


#### Declaring and instancing an object

* C# uses an assignment with its `new` keyword to declare and assign a new instance of a class to a variable; AVR uses its `New` keyword to do that. 

* In many cases with AVR, it may be better to declare the variable on one line and instance on a another, like this:

        DclFld rnd Type(Random) 
        rnd = *New Random()

    Note that AVR's runtime assignment of a new object uses the `*New` key word, not the `New` keyword. 


**C#** 

    Random rnd = new Random();

**AVR**

    DclFld rnd Type(Random) New()

#### `for` statement

* C# can declare and assign an initial value to its loop variable; AVR can only assign a value to its loop variable--it must be declared separately. 
* C# uses a declaration/assignment section, a test section, and an increment/decrement section delimited with semicolons; AVR uses the `Index` keyword for assignment, the `To` (or `DownTo`) keywords for incrementing and decrementing the variable, and the `By` keyword to indicate how much the variable should be changed. If `By` isn't provided 1 is assumed. 
* AVR provides special-case constants for many .NET data types. For example, AVR's `*Integer4` special value is a synonym for .NET's `System.Int32` type (which is `int` in C#). 

**C#** 

    for (int ctr = 1; ctr <= 10; ctr++) 
    {
        ...
    }

**AVR**

    DclFld ctr Type(*Integer4)

    For Index(ctr = 1) To(10)
      ...
    EndFor 


