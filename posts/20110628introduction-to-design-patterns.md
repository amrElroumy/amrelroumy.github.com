# What are Design Patterns?
>“Each pattern describes a problem which occurs over and over in our environment, and then describes the core of the solution to that problem, in such a way that you can use this solution a million times over, without ever doing it the same way twice.”<cite>[Christopher Alexander](http://en.wikipedia.org/wiki/Christopher_Alexander)</cite>

So we can simply say, that some of the design related problems that we encounter while developing software are solved by someone else. These solutions allow us to solve our own problems and take advantage of other developer’s experience and wisdom.Design patterns are descriptions of communicating objects and classes that are customized to solve a general design problem in a particular context.  

**Important note: ** Design patterns are considered guidelines; they are powerful tools that aid developers, but they should never be regarded as rules/specifications that software should follow. That’s why it is important to understand these patterns well and know the proper situations where we could use them. Otherwise, the usage of incorrect patterns might result in unnecessary complications or maintainability issues. To avoid such inconveniences, we should always go with the simplest solution that does the job and introduce patterns only when needed.

# What are Anti-Patterns?
In a way we could say that anti-patterns tell us how to go from a problem to a bad solution. Using anti-patterns in practice, leads to counterproductive results or ineffective solutions to the problems that might face us.

# Describing Design Patterns

## A pattern has four essential elements:

* A unique pattern **name** to help us in identifying and referring to the pattern.
* **Problem** scenario.
* The proposed **solution**.
* **Consequences/tradeoffs** of applying this pattern.

## Documentation (Design Patterns Catalog)
The documentation for a design pattern describes the context, where the pattern is used, the forces within the context that the pattern seeks to resolve, and the suggested solution. There is no single, standard format for documenting design patterns. Rather, many different formats have been used by different pattern authors. One example of a commonly used documentation format is the one used by "Gang of Four" in their book [Design Patterns](http://en.wikipedia.org/wiki/Design_Patterns")

It is as follows:   

*  **Pattern Name and Classification:** A descriptive and unique name that helps in identifying and referring to the pattern.
*  **Intent:** A description of the goal behind the pattern and the reason for using it.
* **Also Known As:** Other names for the pattern. 
* **Motivation (Forces):** A scenario consisting of a problem and a context in which this pattern can be used. 
* **Applicability:** Situations in which this pattern is usable; the context for the pattern. 
* **Structure:** A graphical representation of the pattern. Class diagrams and Interaction diagrams may be used for this purpose. 
* **Participants:** A listing of the classes and objects used in the pattern and their roles in the design. 
* **Collaboration:** A description of how classes and objects used in the pattern interact with each other. 
* **Consequences:** A description of the results, side effects, and tradeoffs caused by using the pattern. 
* **Implementation:** A description of an implementation of the pattern; the solution part of the pattern. 
* **Sample Code:** An illustration of how the pattern can be used in a programming language. 
* **Known Uses:** Examples of real usages of the pattern. 
* **Related Patterns:** Other patterns that have some relationship with the pattern; discussion of the differences between the pattern and similar patterns. 
  
# Design Patterns' Classifications
* Creational Patterns
* Structural Patterns 
* Behavioral Patterns 
