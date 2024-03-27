---
tags:
  - COSC-436
  - spring2024
---

# Basic Concepts

## Objects

**Objects** are *entities* which have <u>attributes and behavior</u>. (same as physical objects in the real world)

## State

**State** is stored in what is called generically *instance variables*. 

Behavior is ``provided`` by what are called *methods*

# Features


## Encapsulation

![[Encapsulation]]


## Inheritance

![[Inheritance]]

## Polymorphism

![[Polymorphism]]

## Early Design Methodology

### CRC Cards (1989)

- Presented at OOPSLA 1989 conference
- Simple use of index cards, putting one class on each card. Helps limit the size of classes (what can fit on a card) and they associated.
- Mostly meant as a teaching tool

Has three components:

| CLASS NAME       |     |
| ---------------- | --- |
| Responsibilities | Collaborators    |

(collaborators refers to other objects)

#### Example ATM:

| Responsibility            | Collaborators |
| ------------------------- | ------------- |
| Start up system operation | ...              |


## Refactoring


## Object-Oriented Analysis

OO Analysis is a means of determining what aspects of a given problem can be viewed as objects in an eventual object-oriented design.

OO Design includes the determination of all classes (i.e., including application object)

Thus,
- **OOA** (Object-Oriented Analysis)
	- *Find out* (Figure out what objects are needed)
- **OOD** (Object-Oriented Design)
	- *Design it* (interaction between objects)
- **OOP** (Object-Oriented Program)
	- *Program it* (write the code)


## Reusing Code

Integral aspect. You do not want to re-invent the wheel over and over. 
Components, frameworks and design patterns represent three forms of reuse

### Components

<u>Complete code</u> (reuse of *code*)

Involves the modification and reuse of executable code, just as dragging and modifying button in creating a GUI in visual programming environment.


### Frameworks

<u>Some code</u> (reuse of *"plug-in" code*)

A partial implementation that must be completed. Analogous to a motherboard and its hardware components.


### Design Patterns

<u>No code</u> (reuse of *design*)

A design pattern is a commonly occurring collection of **classes and their collaboration** that is identified and named providing for a reusable design approach that others can adopt.



