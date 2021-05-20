### Implementing an interface with ASNA Visual RPG

This example shows how to implement .NET's IComparable interface in ANSA Visual RPG (AVR). The IComparable interface is generalized way to compare two objects. It is often used for sorting purposes. 

The [IComparable docs](https://docs.microsoft.com/en-us/dotnet/api/system.icomparable?view=netframework-4.7.1) shows an example of sorting a range of temperatures in C#. This example implements that code in Visual RPG. 

AVR can implement any non-generic .NET interface. That is, it can implement the [IComparable](https://docs.microsoft.com/en-us/dotnet/api/system.icomparable?view=netframework-4.7.1#methods) interface, but it cannot implement the generic [IComparable\<T>](https://docs.microsoft.com/en-us/dotnet/api/system.icomparable-1?view=netframework-4.7.1) interface. 

If you need to implement a generic interface, we recommend you make a separate C# DLL to do that work and then reference that C# DLL with AVR. 



