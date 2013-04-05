## Pattern Name
Factory Method

## Classification
Creational Pattern

## Intent
> Define an interface for creating an object, but let subclasses decide which class to instantiate. **Factory Method** lets a class defer instantiation to subclasses.

## Also known as
Virtual Constructor

## Motivation
When we program to an implementation we risk making our code **more fragile and less flexible**. When we handle the instantiation of concrete classes explicitly, this is exactly what we are doing… By doing this, we subject our code to the severe impacts of change. One of these consequences is that we force ourselves to modify already existing code when we want to change the object creation routines or add new concrete classes, thus, breaching one of the **OOD** principles:

> “Your code should be open for extension but closed for modifications.”

A common thing to do when we have a part of the code that is likely to change is to:
> “Identify the aspects that vary and separate them from what stays the same.”

This is why we are needed to **encapsulate** the object creation and **isolate** it from the rest of the code, ensuring that any change in the object creation will remain transparent to the rest of the code. And here comes the role of the **Factory Method pattern**, as it handles the object creation and encapsulates it in a subclass. Thus, the client depends on the subclasses to handle all the object creation, so it doesn’t really know the kind of concrete product that is actually created and its code depends on an abstract product. 

### Notes:
* Factory Patterns in general focus on encapsulating the instantiation of concrete types; abstracting the product creation process, so that the type of the concrete product can be determined in the runtime.
* There are two types of **Factory Method**:
    * Parameterized: This can make more than one object based on the parameters passed to it.
    * Not parameterized: This can make only one object
* When using parameterized Factory Methods it is important to make sure that the parameters are “type safe” and ensure that errors in parameters are caught at compile time; to prevent runtime errors. E.g. we could use enumerators.
* **Factory Method** is similar to the **Abstract Factory** in that the methods of the **Abstract factory** can be implemented as **Factory Methods**. The main difference is that while abstract factory deals with an entire family of products, the **Factory Method** is only worried about a single product. Also **Factory Methods** use inheritance to get the concrete object as they delegate object creation to subclasses which implement the **Factory Method**, while **Abstract Factory** uses object composition.

# Applicability
> Use the **Factory Method** pattern when:   
>
>   * a class can't anticipate the class of objects it must create. 
>   * a class wants its subclasses to specify the objects it creates. 
>   * classes delegate responsibility to one of several helper subclasses, and you want to localize the knowledge of which helper subclass is the delegate.
> <cite>(source: GoF’s Book)</cite>

### Important Note:

Factories can only be used with a family of classes. If these classes doesn’t extend the same base or interface, then we can’t use factories with them.

## Structure
![Factory_Method](http://amrelroumy.files.wordpress.com/2011/07/factory_method2.png)

## Participants
* **CreatorBase:** If we don’t need to extend the creator and have different creators the whole factory can be implemented here. Otherwise, this base is either an interface or an abstract class; depending on the situation and if we want to add specify some simple functionality that the concrete creators inherit.
* **ConcreteCreator:** It inherits the **CreatorBase** class. It either uses the **FactoryMethod** as it is if it is implemented fully in the base class, or it overrides it with the suitable object creation code.
* **ProductBase:** This abstract class defines the type of products that the **FactoryMethod **can create.
* **ConcreteProduct:** The actual object that is created by the **FactoryMethod**.

## Consequences

#### Advantages:
* It enforces loose coupling between the Creator and the product. This is good, because it’ll allow us to add new products or change old ones without affecting our code or having to change it to fit into the new design as the code only deals with the product’s interface.
* It allows us to encapsulate all the object creation procedures and use of constructors, leaving the object type and creation to be determined at the runtime instead of being hardwired in the code.
* Using this pattern reinforces the principle of programming to an interface instead of an implementation, as we separate the object instantiation from the creators and are putting them in separate objects.
* *Provides hooks for subclasses.* Creating objects inside a class with a factory method is always more flexible than creating an object directly. Factory Method gives subclasses a hook for providing an extended version of an object. (Source: GoF’s book)

## Implementation

```csharp
abstract class ProductBase
{
}

class ConcreteProductA : ProductBase
{
}

class ConcreteProductB : ProductBase
{
}

abstract class CreatorBase
{
    public enum ProductType
    {
        TypeA,
        TypeB
    }

    public abstract ProductBase FactoryMethod(ProductType type);
}

class ConcreteCreator : CreatorBase
{
    public override ProductBase FactoryMethod(ProductType type)
    {
        if (type == ProductType.TypeA)
            return new ConcreteProductA();
        if(type == ProductType.TypeB)
            return new ConcreteProductB();
        throw new ArgumentException(“Invalid argument”, type.ToString());
    }
}
```

## References
* [Design Patterns: Elements of Reusable Object-Oriented Software](http://en.wikipedia.org/wiki/Design_Patterns) – The Gang of Four (GoF): [Erich Gamma](http://en.wikipedia.org/wiki/Erich_Gamma), Richard Helm, [Ralph Johnson](http://en.wikipedia.org/wiki/Ralph_Johnson_(computer_scientist)), [John M. Vlissides](http://en.wikipedia.org/wiki/John_Vlissides). 
* [Head First Design Patterns](http://oreilly.com/catalog/9780596007126) - [Eric T Freeman](http://www.oreillynet.com/pub/au/2003), [Elisabeth Robson](http://www.oreillynet.com/pub/au/2002), [Bert Bates](http://www.oreillynet.com/pub/au/1085), [Kathy Sierra](http://www.oreillynet.com/pub/au/1084). 
