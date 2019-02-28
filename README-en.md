# Clean Code Wollok

## Table of Contents
  1. [Introduction](#introduction)
  2. [Variables](#variables)
  3. [Functions](#functions)
  4. [Objects and Data Structures](#objects-and-data-structures)
  5. [Classes](#classes)
  6. [SOLID](#solid)
  7. [Testing](#testing)
  8. [Concurrency](#concurrency)
  9. [Error Handling](#error-handling)
  10. [Formatting](#formatting)
  11. [Comments](#comments)
  12. [Translation](#translation)

## Introduction
![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](http://www.osnews.com/images/comics/wtfm.jpg)

Software engineering principles, from Robert C. Martin's book
[*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882),
adapted for **Wollok**. This is not a style guide. It's a guide to producing
[readable, reusable, and refactorable](https://github.com/ryanmcdermott/3rs-of-software-architecture) software in **Wollok**.

Not every principle herein has to be strictly followed, and even fewer will be
universally agreed upon. These are guidelines and nothing more, but they are
ones codified over many years of collective experience by the authors of
*Clean Code*.

One more thing: knowing these won't immediately make you a better software
developer, and working with them for many years doesn't mean you won't make
mistakes. Every piece of code starts as a first draft, like wet clay getting
shaped into its final form. Finally, we chisel away the imperfections when
we review it with our peers. Don't beat yourself up for first drafts that need
improvement. Beat up the code instead!

## **Variables**
### Use meaningful and pronounceable variable names

**Bad**
```javascript
const dmyyyy = new Date(22, 2, 2019)
```

**Good**
```javascript
const actualDate = new Date(22, 2, 2019)
```

**[⬆ back to top](#table-of-contents)**

### Use the same vocabulary for the same type of variable

**Bad:**
```javascript
getUserInfo();
getClientData();
```

**Good:**
```javascript
getUser();
```
**[⬆ back to top](#table-of-contents)**

### Use searchable names
We will read more code than we will ever write. It's important that the code we
do write is readable and searchable. By *not* naming variables that end up
being meaningful for understanding our program, we hurt our readers.
Make your names searchable.

**Bad:**
```javascript
// What the heck is 1234 for?
method totalValue(quantity) = quantity * 1234
```

**Good:**
```javascript
// Declare them as capitalized named constants.
const COST = 1234

method totalValue(quantity) = quantity * COST
```
**[⬆ back to top](#table-of-contents)**

### Use explanatory variables

**Bad:**
```javascript
saveZipCode('False Address 123', 1234)
```

**Good:**
```javascript
var address = 'False Address 123'
var zipCode = 1234
saveZipCode(address, zipCode)
```
**[⬆ back to top](#table-of-contents)**

### Avoid Mental Mapping
Explicit is better than implicit.

**Bad:**
```javascript
const locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach { l => l.coordinates() }
```

**Good:**
```javascript
const locations = ['Austin', 'New York', 'San Francisco'];
locations.forEach { location => location.coordinates() }
```
**[⬆ back to top](#table-of-contents)**

### Don't add unneeded context
If your class/object name tells you something, don't repeat that in your
variable name.

**Bad:**
```javascript
class Car = {
  const property carMake = 'Honda'
  const property carModel = 'Accord'
  var property carColor =  'Blue'

  method paint(newColor) {
    this.carColor = newColor
  }
}
```

**Good:**
```javascript
class Car = {
  const property make = 'Honda'
  const property model = 'Accord'
  var property color = 'Blue'

  method paint(newColor) {
    this.color = newColor
  }
}
```

**[⬆ back to top](#table-of-contents)**