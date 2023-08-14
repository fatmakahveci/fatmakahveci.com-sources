---
title: Design Patterns in Typescript
description: Design Patterns in Typescript
summary: "Updated by Fatma, Aug 14, 2023."
date: 14-08-2023
categories:
  - "Coding"
tags:
  - "typescript"
  - "user interface"
  - "coding"
  - "framework"
  - "frontend"
  - "web development"
  - "design patterns"
comments: true
---
- A design pattern offers a widely applicable and reusable solution for addressing common problems in software design.
- It illustrates how classes or objects interact and relate to each other.
- It is programming language-independent, so it represents thinking.
- We should understand the intention and use of each pattern.

## 1. Creational patterns

- They instantiate classes using inheritance, or create objects using delegation.

### 1.1 Abstract factory

- Create entire product families without specifying their concrete classes
- It takes over the responsibility of creating objects.

```typescript
```

---

### 1.2 Factory

- Create product objects without specifying their concrete classes
- It takes over the responsibility of creating objects.

```typescript
```

---

### 1.3 Builder

- Construct complex objects step-by-step
- It manages the creation process.
- It has four parts:
  1. **Product** is the final complex object which we obtain in the end.
  2. **Builder (Interface)** abstracts the building process.
  3. **Builder (Concrete)** implements interface and builds the product. The more different products we want to send to the assembly line, the more builders we have.
  4. **Director** communicates with the client. It has a construction method that captures the right builder objects.

```typescript
```

---

### 1.4 Prototype

- Copy existing objects without making your code dependent on their classes

```typescript
```

---

### 1.5 Singleton

- Ensure that a class has only one instance, while providing a global access point to this instance

```typescript
class Flower {
    constructor(public readonly name: string, public readonly numberOfPetals: number) {
    }
}

class FlowerList {
    private flowers: Flower[] = [];

    static instance: FlowerList = new FlowerList();

    private constructor() {}

    static addFlower(flower: Flower) {
        FlowerList.instance.flowers.push(flower);
    }

    getFlowers() {
        return this.flowers;
    }
}

FlowerList.addFlower(new Flower("Rose", 20));
console.log(FlowerList.instance.getFlowers());
```

---

## 2. Structural patterns

- They create larger structures that offer additional features and capabilities by arranging different classes and objects.

### 2.1 Adapter

- Allow objects with incompatible interfaces to collaborate

```typescript
```

---

### 2.2 Bridge

- Split a large class or a set of closely related classes into two separate hierarchies-abstraction and implementation- which can be developed independently of each other

```typescript
```

---

### 2.3 Composite

- Compose objects into tree structures and then work with these structures as if they were individual objects

```typescript
```

---

### 2.4 Decorator

- Attach new behaviours to objects by placing these objects inside special wrapper objects that contain the behaviours

```typescript
```

---

### 2.5 Facade

- Provide a simplified interface to a library, a framework, or any other complex set of classes

```typescript
```

### 2.6 Flyweight

- Fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object

```typescript
```

---

### 2.7 Proxy

- Provide a substitute or placeholder for another object

```typescript
```

---

## 3. Behavioral patterns

- They recognise shared communication patterns among objects and implement them.

### 3.1 Chain of responsibility

- Pass requests along a chain of handlers

```typescript
```

---

### 3.2 Command

- Turn a request into a stand-alone object that contains all information about the request

```typescript
```

---

### 3.3 Iterator

- Traverse elements of a collection without exposing its underlying representation

```typescript
```

---

### 3.4 Mediator

- Reduce chaotic dependencies between objects
- It restricts direct communication between the objects and forces them to collaborate only via a mediator object.

```typescript
```

---

### 3.5 Memento

- Save and restore the previous state of an object without revealing the details of its implementation

```typescript
```

---

### 3.6 Observer

- Define a subscription mechanism to notify multiple objects about any events that happen to the object they're observing

```typescript
```

---

### 3.7 State

- Alter an object behaviour when its internal state changes

```typescript
```

---

### 3.8 Strategy

- Define a family of algorithms, put each of them into a separate class, and make their objects interchangeable

```typescript
```

---

### 3.9 Template

- Define the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure

```typescript
```

---

### 3.10 Visitor

- Separate algorithms from the objects on which they operate

```typescript
```

---
