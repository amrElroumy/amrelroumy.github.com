# Pattern Name
Decorator Pattern

# Classification
Structural Pattern

# Intent
> The Decorator Pattern attaches additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

# Also known as
Wrapper

# Motivation
You might find yourself while working on a project and in the need of adding/modifying responsibilities or behaviors to objects of a certain type. One way of approaching this problem is that we extend this type using inheritance and add the new behavior to it in its children. But what would happen when we want to add more than one responsibility for some objects while keeping others with only a single new responsibility? Then, we would have to implement all the combinations of these responsibilities and ending up with what can be called as a **class explosion**; as you’ll end up with a lot of classes, more time to debug and a lot of those long & lonely nights of maintenance.

An answer to this problem would be to **extend** **the behavior without using inheritance**. This can be achieved by using **composition** to wrap the components by the decorator and add new behavior/properties or modify already existing ones in the runtime. Using this approach we can avoid having to use inheritance and constrain ourselves with static (compile-time) extending to the objects and use instead **dynamic (runtime)** extending of those specific objects. Also it allows us to add the needed behavior according to the specific conditions that occur during the runtime; meaning that objects of the same type can end up being decorated differently and that the same object can be wrapped in more than one decorator.

### Design principles behind this pattern:
* **Open-Closed Principle** from SOLID Principles Classes should be **open** **for extension**, but **closed for modification**. One reason why this principle is important is that it prevents us from introducing bugs into code that has already been tested and debugged.

### Important Notes:
* The decorator pattern is used to extend behavior of objects during the runtime not classes.
* You can't apply the **Open-Closed Principle** to every part of your design, because it'll add complexity to the code and it'll take time and effort. You need to identify—comes with experience—the parts of the code that are most likely to change and apply the principle on them.
* Using decorators with code that relies on the component's **concrete** type will break that code. But if we only use them with code that depends on the **abstract** component's type, then the decorators will remain **transparent** to the client of the component.

# Applicability (from GoF’s Book)
* To add responsibilities to individual objects dynamically and transparently, that is, without affecting other objects. 
* For responsibilities that can be withdrawn. 
* When extension by subclassing is impractical. Sometimes a large number of independent extensions are possible and would produce an explosion of subclasses to support every combination. Or a class definition may be hidden or otherwise unavailable for subclassing. 

# Structure
![Decorator Pattern Structure](http://amrelroumy.files.wordpress.com/2011/07/decorator_pattern1.png)

You might ask yourself if the decorator pattern teaches us to favor composition over inheritance, then why does the **DecoratorBase** class extends the Object's super class? The answer is that the decorator is extending this class to gain the same interface as the object it will wrap, not to gain the behavior. Thus we extend the base class to get the interface but we're getting the behavior through composition of decorators with the base components as other decorators.

# Participants
* **ComponentBase: **Defines the basic behaviors/properties that would be implemented by the components that will be decorated. If we don’t want to define any actual functionality in it, you can use an interface instead of an abstract class.
* **DecoratorBase: **It is the abstract class for all the decorators. It inherits the basic interface of the components from the **ConcreteBase**, to allow the decorators to be used in place of the components. You’ll notice that it adds a constructor that accepts a **Component** of type **ComponentBase; **this is the Component to be wrapped.
* **ConcreteComponent: **The actual components that will be wrapped.
* **ConcreteDecoratorA/****ConcreteDecoratorA: **The decorators that wrap Components. They can introduce new behavior/properties like **ConcreteDecoratorA **or modify already existing ones like **ConcretDecoratorB**.

# Properties of decorators:
* They have the same supertype as the objects they decorate.
* You can use one or more decorators to wrap an object.
* The decorator adds its own behavior either before and/or after delegating to the object it decorates to do the rest of the job.
* Objects can be decorated at runtime.
 

# Consequences

### Advantages of using the decorator pattern:

* It allows us to add new behavior to existing code without the need to modify it (Following the Open-Closed Principle) or without having to use inheritance, thus avoiding inheritance’s rigidity and adding more flexibility to the code.
* Avoids having classes with complicated and complex responsibilities high up in the class hierarchy. Instead we use simple classes that are customizable and whose responsibilities can be added during the runtime.

### One of the shortcomings of using the Decorator Pattern:

* Using this pattern in your design, you'll end up with a relatively large number of small objects that differ in the way they are assembled. This can be overwhelming to a developer trying to use the Decorator-based API, but is easy to those who understand them and are familiar with this design pattern.
* Using this pattern can complicate the process of instantiating objects, that's why this pattern is used alongside the Factory and Builder patterns

# Implementation

```csharp
public abstract class ComponentBase
{
    public abstract void Operation();
}

public class ConcreteComponent : ComponentBase
{
    public override void Operation()
    {
        // Implementation of component's behavior
    }
}

public abstract class DecoratorBase : ComponentBase
{
    private ComponentBase _componentObject; // The one to be extended

    public DecoratorBase(ComponentBase componentObject)
    {
       _componentObject = componentObject;
    }

    public override void Operation()
    {
       _componentObject.Operation();
    }
}

public class ConcreteDecorator : DecoratorBase
{
    public ConcreteDecorator(ComponentBase componentObject) : base(componentObject)
    { }

    public override void Operation()
    {
       // Implementation of new behavior
       base.Operation();
       // Implementation of new behavior
    }
}
```

# Related Patterns (from GoF’s book)

* **Adapter** : A decorator is different from an adapter in that a decorator only changes an object's responsibilities, not its interface; an adapter will give an object a completely new interface.
* **Composite** : A decorator can be viewed as a degenerate composite with only one component. However, a decorator adds additional responsibilities—it isn't intended for object aggregation.
* **Strategy **: A decorator lets you change the skin of an object; a strategy lets you change the guts. These are two alternative ways of changing an object.
