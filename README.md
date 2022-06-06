# Couplers

## Learning Goals

- Explain the coupler patterns

## Introduction

This family of smells happens when functionality is too tightly coupled with one
another. Tight coupling can be detected when a change somewhere requires changes
in a lot of different places.

## Feature Envy

This happens when a method accesses data from another object more than it does
its own data. This over-reliance on external data can be a sign that your
abstractions or algorithms should be restructured.

## Inappropriate Intimacy

This happens when a class is overly reliant on the private fields of another
class. As we have seen, it's possible and often desirable to make private fields
accessible to other classes through accessor methods. However, a tight
dependency between two classes' internal fields may indicate that the data
really belongs together and should be modeled differently.

## Message Chains

Message chains happen when a client class needs to use an in-between class in
order to access a third class' data or functionality:

```java
clientObject().getFirstObject().getSecondObject().doSomething();
```

As with all smells, this may be legitimate in some cases, but the presence of
this type of code should catch our attention and cause us to question whether
the functionality of `doSomething()` should be more readily available for
`clientObject()` to use. This is because we now have two classes between
`clientObject` and `doSomething()` which increases the likelihood that
additional code will have to change if/when `doSomething()` ever has to change.

## Middle Man

This is a variation of Message Chains in that the first or second class in the
example above would be responsible for nothing more than just giving access to
the next class in the chain. This creates the same complexity as before, but
without the potential benefit of additional functionality in the in-between
classes.
