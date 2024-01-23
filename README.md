<h1 align="center">
  SOLID Principles in PHP
</h1>

<p align="center">
  <a href="https://github.com/ramazancetinkaya/solid-principles-for-php">
    <img src="https://rijsat.com/wp-content/uploads/2023/11/image-3.png" alt="Logo">
  </a>

  <p align="center">
    In software engineering, SOLID is a mnemonic acronym for five design principles intended to make object-oriented designs more understandable, flexible, and maintainable.
  </p>
</p>

## Introduction

SOLID principles are a set of five design principles that aim to make software design more understandable, flexible, and maintainable. These principles were introduced by Robert C. Martin and have become fundamental guidelines for object-oriented design. In this guide, we'll explore each SOLID principle and demonstrate how to apply them in PHP with clear and detailed examples.

## SOLID Principles

* Single Responsibility Principle (SRP)
* Open/Closed Principle (OCP)
* Liskov Substitution Principle (LSP)
* Interface Segregation Principle (ISP)
* Dependency Inversion Principle (DIP)

### SOLID Principles Overview

1) **Single Responsibility Principle (SRP):**

    A class should have only one reason to change, meaning it should have only one responsibility.

2) **Open/Closed Principle (OCP):**

    Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.

3) **Liskov Substitution Principle (LSP):**

    Subtypes must be substitutable for their base types without altering the correctness of the program.

4) **Interface Segregation Principle (ISP):**

    Clients should not be forced to depend on interfaces they do not use.

5) **Dependency Inversion Principle (DIP):**

    High-level modules should not depend on low-level modules; both should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions.

## Single Responsibility Principle (SRP) in PHP

The Single Responsibility Principle suggests that a class should only have one reason to change.

Let's consider a simple example:

```php
// Before SRP

class Report {
    public function generate() {
        // Code to generate report
    }

    public function saveToFile() {
        // Code to save report to a file
    }
}
```

In this example, the Report class has both report generation and file-saving responsibilities. Let's refactor this to adhere to SRP:

```php
// After SRP

class Report {
    public function generate() {
        // Code to generate report
    }
}

class ReportSaver {
    public function saveToFile(Report $report) {
        // Code to save report to a file
    }
}
```

Now, we have two classes, each with a single responsibility: Report for generating reports and ReportSaver for saving reports to a file.

## Open/Closed Principle (OCP) in PHP

The Open/Closed Principle encourages entities to be open for extension but closed for modification.

Let's consider an example:

```php
// Before OCP

class Circle {
    public function calculateArea($radius) {
        return 3.14 * $radius * $radius;
    }
}
```

To adhere to OCP, we can introduce an interface and create a class that extends it:

```php
// After OCP

interface Shape {
    public function calculateArea();
}

class Circle implements Shape {
    private $radius;

    public function __construct($radius) {
        $this->radius = $radius;
    }

    public function calculateArea() {
        return 3.14 * $this->radius * $this->radius;
    }
}
```

Now, if we want to add more shapes, we can create new classes implementing the Shape interface without modifying the existing code.

## Liskov Substitution Principle (LSP) in PHP

The Liskov Substitution Principle ensures that objects of a base class can be replaced with objects of a derived class without affecting the correctness of the program.

Consider the following example:

```php
// Before LSP

class Bird {
    public function fly() {
        // Code for flying
    }
}

class Penguin extends Bird {
    public function fly() {
        // Penguins can't fly, but this method is inherited
    }
}
```

To adhere to LSP, we can create a separate interface:

```php
// After LSP

interface Flyable {
    public function fly();
}

class Bird implements Flyable {
    public function fly() {
        // Code for flying
    }
}

class Penguin implements Flyable {
    public function fly() {
        // Penguins can't fly, but this method is overridden
        throw new Exception("Penguins can't fly");
    }
}
```

Now, both Bird and Penguin implement the Flyable interface, ensuring correct substitution.

## Interface Segregation Principle (ISP) in PHP

The Interface Segregation Principle suggests that a class should not be forced to depend on interfaces it does not use.

Consider the following example:

```php
// Before ISP

interface Worker {
    public function work();
    public function eat();
}
```

If a class doesn't need the eat method, it is forced to implement it. Let's refactor using ISP:

```php
// After ISP

interface Workable {
    public function work();
}

interface Eatable {
    public function eat();
}

class Robot implements Workable {
    public function work() {
        // Code for working
    }
}

class Human implements Workable, Eatable {
    public function work() {
        // Code for working
    }

    public function eat() {
        // Code for eating
    }
}
```

Now, classes can implement only the interfaces they need.

## Dependency Inversion Principle (DIP) in PHP

The Dependency Inversion Principle states that high-level modules should not depend on low-level modules.

Let's consider the following example:

```php
// Before DIP

class LightBulb {
    public function turnOn() {
        // Code to turn on the light bulb
    }
}

class Switch {
    private $bulb;

    public function __construct(LightBulb $bulb) {
        $this->bulb = $bulb;
    }

    public function operate() {
        // Code to operate the switch
        $this->bulb->turnOn();
    }
}
```

To adhere to DIP, we can introduce an interface:

```php
// After DIP

interface Switchable {
    public function turnOn();
}

class LightBulb implements Switchable {
    public function turnOn() {
        // Code to turn on the light bulb
    }
}

class Switch {
    private $device;

    public function __construct(Switchable $device) {
        $this->device = $device;
    }

    public function operate() {
        // Code to operate the switch
        $this->device->turnOn();
    }
}
```

Now, Switch depends on the abstraction Switchable, allowing for greater flexibility in the future.

## Conclusion
In this guide, we've explored the SOLID principles and demonstrated how to apply them in PHP through clear and practical examples.

By following these principles, you can create more maintainable, scalable, and robust software systems.

Always strive to write code that is not only functional but also follows sound design principles for long-term success in your projects.

## Contact

For any inquiries or feedback, feel free to reach out to us via email.

📧 Email: [ramazancetinkayadev@outlook.com](mailto:ramazancetinkayadev@outlook.com)

## Credits

This guide was made possible by the following awesome contributors:

- **Ramazan Çetinkaya** - [@ramazancetinkaya](https://github.com/ramazancetinkaya)
  - Lead Developer

Special thanks to the following resources:

- [Wikipedia](https://en.wikipedia.org/wiki/SOLID)

If you've contributed to this guide and your name is not listed, please let us know, and we'll add you!

Thank you to everyone who has helped make this guide better!
