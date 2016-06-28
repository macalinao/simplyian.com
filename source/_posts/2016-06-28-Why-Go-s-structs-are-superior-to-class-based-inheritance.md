title: Why Go's structs are superior to class-based inheritance
date: 2016-06-28 15:25:29
tags:
- software
- Go
---

Go is unique from a lot of object-oriented languages in that it doesn't have classes. Instead, Go has two awesome features that make its model of polymorphism way more powerful than classical inheritance: interfaces and struct embedding.

## Interfaces

Interfaces in Go are very different from, say, Java interfaces. You don't explicitly say a data type implements an interface; rather, your data types must implement all of the methods that the interface defines, and the compiler checks to see if assignments to variables of the interface type are valid.

For example, let's define an Animal interface as so:

```go
type Animal interface {
    Name() string
}
```

The following type satisfies the Animal interface since it has all the methods Animal implements:

```go
type Dog struct {}

func (d *Dog) Name() string {
    return "Dog"
}

func (d *Dog) Bark() {
    fmt.Println("Woof!")
}
```

Thus, the following code is valid:

```go
func main() {
    var animal Animal
    animal = &Dog{}  // returns a pointer to a new Dog
    fmt.Println(animal.Name())  // Dog
}
```

However, the following does not work:

```go
func main() {
    var animal Animal
    animal = Dog{}  // compile error!
}
```

since `*Dog`, not `Dog`, satisfies the interface.

You can also compose interfaces like this:

```go
type PartyAnimal interface {
    Animal
    Party()
}
```

This defines an interface `PartyAnimal` which must satisfy all methods of Animal on top of satisfying `Party()`, thus the following is equivalent:

```go
type PartyAnimal interface {
    Name() string
    Party()
}
```

## Struct embedding

Let's say we want to create a type that does everything a Dog does, but more. Let's call it a GuideDog, and give it a method `Help(h *Human)`. We can do that like so:

```go
type GuideDog struct {
    *Dog
}

func (gd *GuideDog) Help(h *Human) {
    fmt.Printf("Hey human, grab %s's leash!\n", gd.Name())
}

func main() {
    gd := &GuideDog{}
    gd.Help(nil)  // prints "Hey human, grab Dog's leash!"
}
```

This calls the `Name` method on the embedded `*Dog` to do this.

Side note: even though we didn't initialize the `\*Dog`, we won't get a null pointer exception here. This is because `\*Dog#name` doesn't access any struct attributes. Nifty, huh?

Now what if we do something like this:

```go
type Cat struct {}

func (c *Cat) Name() string {
    return "Cat"
}

type CatDog struct {
    *Cat
    *Dog
}

func main() {
    cd := &CatDog{}
    fmt.Printf("My favorite animal is the %s!\n", cd.Name())
}
```

This doesn't compile! `cd.Name()` is an ambiguous call. To fix this, we must add this method:

```go
func (cd *CatDog) Name() string {
    return fmt.Sprintf("%s%s", cd.Cat.Name(), cd.Dog.Name())
}
```

Now the program will print the following message:

```
My favorite animal is the CatDog!
```

This seems kind of tricky, but in the following sections I'll cover why this is so awesome.

## Go polymorphism

Go polymorphism involves creating many different data types that satisfy a common interface. This is different from Java in that Java polymorphism also allows satisfying a common base class, which can lead to many problems.

## The fragile base class problem

Wikipedia defines the fragile base class problem as the following:

> The fragile base class problem is a fundamental architectural problem of object-oriented programming systems where base classes (superclasses) are considered "fragile" because seemingly safe modifications to a base class, when inherited by the derived classes, may cause the derived classes to malfunction. The programmer cannot determine whether a base class change is safe simply by examining in isolation the methods of the base class.


Basically, classes are the tightest form of coupling in object-oriented programming, and this is a bad thing. Changing a base class can cause unwanted side effects all over a code base.

For example, let's say I am building a game called MyCraft and I need to create some items, which are all derived from the Item base class. Let's say a lot of these items are Blocks, which are derived from Item. I create two blocks, a Sponge and a Brick. But what if Brick requires a change from the Item class, e.g. it needs to handle different burn behavior, and I cannot isolate the change to the Brick class? I make my change to Item and everything but Brick breaks. These kinds of mistakes are common in class-based inheritance.

You need to inherit all behavior from base classes in a class based inheritance model, but often times you don't want everything.

## Favor composition over inheritance

There is a famous statement in object oriented programming to [favor composition over inheritance](https://en.wikipedia.org/wiki/Composition_over_inheritance). Making complex, multi-tiered class inheritance structures is a bad idea in general, as it makes your code more resistance to change.

With composition, you can pick different features rather than classes. You can compose your Brick of Block and Unburnable rather than making changes to a rigid class hierarchy. Class inheritance forces you to use an existing structure that may not be the best for your use case.

## Conclusion

Go's struct embedding is amazing. It disguises composition as inheritance and allows easily changing implementation details via its powerful interfaces. It is much more powerful than a class-based inheritance model, as it allows a much greater degree of flexibility.
