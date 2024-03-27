
Creational design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance.

Solves two problems at the same time:
- Ensure that a class has just a single instance
- Why?
	- You need to control access to some shared resource, for example, a database or a file.
	- Provide a global access point to that instance.
- Provide a global access point to that instance

```java
// Singleton
static getInstance()
...
```

Defines the unique instance of the class as a static variable, and defines a static method getInstance() for clients to access the unique instance.

```java
public class Singleton
{
	private static Singleton instance_A = new Singleton();
	public static Singleton getInstance()
	{
		return instance_A
	}
	private Singleton()
	{
		// init instance variables
	}
	// other methods and fields
}
```


Design pattern

- how many problems does it solve?
- code examples
- pros and cons
- other ways to prepare