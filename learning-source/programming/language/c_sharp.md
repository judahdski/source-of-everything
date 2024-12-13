# **C# Basic Syntax, Data Types, and LINQ Guide**

This guide introduces the basic syntax of C#, covers the most common data types, and provides an overview of LINQ (Language Integrated Query) with best practices and examples.

## **Table of Contents**
1. [Basic Syntax of C#](#basic-syntax-of-c)
2. [Data Types in C#](#data-types-in-c)
3. [Control Flow in C#](#control-flow-in-c)
4. [Object-Oriented Programming](#object-oriented-programming)
5. [Introduction to LINQ](#introduction-to-linq)
6. [LINQ Best Practices](#linq-best-practices)

---

## **Basic Syntax of C#**

### **Hello World Example**

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

### **Variables and Types**

- Declaration: Define a variable and specify its type.
  
  ```csharp
  int age = 25;
  string name = "John";
  bool isActive = true;
  ```

- Types: C# is a strongly typed language, meaning variables need to be declared with a specific data type.

### **Type Inference**

C# allows type inference using the `var` keyword:
  
```csharp
var message = "Hello";
var number = 42;
```

The type is inferred at compile time based on the assigned value.

---

## **Data Types in C#**

C# has a wide range of data types, broadly categorized into **Value Types** and **Reference Types**.

### **Value Types**

1. **Integral Types**:
   - `int`: 32-bit signed integer
   - `long`: 64-bit signed integer
   - `byte`: 8-bit unsigned integer
   - `char`: 16-bit Unicode character

2. **Floating Point Types**:
   - `float`: 32-bit floating point
   - `double`: 64-bit floating point
   - `decimal`: 128-bit high precision decimal for financial calculations

3. **Boolean**:
   - `bool`: true/false

### **Reference Types**

1. **`string`**: Sequence of characters.
   ```csharp
   string name = "Alice";
   ```

2. **`object`**: Base type of all types.
   ```csharp
   object obj = 42;
   ```

3. **Array**: Collection of elements of the same type.
   ```csharp
   int[] numbers = new int[] { 1, 2, 3, 4 };
   ```

### **Nullable Types**

Nullable types allow you to assign `null` to value types using the `?` operator:
  
```csharp
int? nullableInt = null;
```

---

## **Control Flow in C#**

### **Conditional Statements**

#### `if-else` Statement
```csharp
int age = 18;
if (age >= 18)
{
    Console.WriteLine("Adult");
}
else
{
    Console.WriteLine("Minor");
}
```

#### `switch` Statement
```csharp
string day = "Monday";
switch (day)
{
    case "Monday":
        Console.WriteLine("Start of the week!");
        break;
    case "Friday":
        Console.WriteLine("End of the week!");
        break;
    default:
        Console.WriteLine("Mid-week");
        break;
}
```

### **Loops**

#### `for` Loop
```csharp
for (int i = 0; i < 5; i++)
{
    Console.WriteLine(i);
}
```

#### `while` Loop
```csharp
int i = 0;
while (i < 5)
{
    Console.WriteLine(i);
    i++;
}
```

---

## **Object-Oriented Programming**

C# is an object-oriented programming language. Here are key concepts:

### **Classes and Objects**

A **class** is a blueprint, and an **object** is an instance of the class.

```csharp
class Person
{
    public string Name { get; set; }
    public int Age { get; set; }

    public void SayHello()
    {
        Console.WriteLine($"Hello, my name is {Name}");
    }
}

Person person = new Person { Name = "Alice", Age = 30 };
person.SayHello();
```

### **Encapsulation**
Encapsulation ensures that a class's internal implementation details are hidden from outside interference.

```csharp
class BankAccount
{
    private decimal balance;

    public void Deposit(decimal amount)
    {
        balance += amount;
    }

    public decimal GetBalance()
    {
        return balance;
    }
}
```

---

## **Introduction to LINQ**

LINQ (Language Integrated Query) allows you to write queries directly in C# to manipulate data collections.

### **Basic LINQ Query**

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };

var evenNumbers = numbers.Where(n => n % 2 == 0);

foreach (var number in evenNumbers)
{
    Console.WriteLine(number);  // Output: 2, 4
}
```

### **Common LINQ Methods**

1. **`Where`**: Filters elements based on a condition.
   ```csharp
   var adults = people.Where(p => p.Age >= 18);
   ```

2. **`Select`**: Projects each element into a new form.
   ```csharp
   var names = people.Select(p => p.Name);
   ```

3. **`OrderBy`**: Sorts elements in ascending order.
   ```csharp
   var sortedPeople = people.OrderBy(p => p.Name);
   ```

4. **`GroupBy`**: Groups elements by a key.
   ```csharp
   var peopleByAge = people.GroupBy(p => p.Age);
   ```

5. **`First` / `FirstOrDefault`**: Returns the first element or a default value if no element is found.
   ```csharp
   var firstAdult = people.First(p => p.Age >= 18);
   ```

6. **`Any` / `All`**: Determines whether any or all elements satisfy a condition.
   ```csharp
   var hasTeenagers = people.Any(p => p.Age >= 13 && p.Age <= 19);
   var allAdults = people.All(p => p.Age >= 18);
   ```

---

## **LINQ Best Practices**

### **Do's:**

- **Use Deferred Execution**: LINQ queries are not executed until you iterate over them (e.g., with `foreach` or `ToList()`).
  
  ```csharp
  var query = numbers.Where(n => n > 10);  // Not executed yet
  var result = query.ToList();  // Executed here
  ```

- **Chain Methods for Clear Querying**: Use method chaining to create readable and concise queries.
  
  ```csharp
  var result = numbers.Where(n => n > 10)
                      .Select(n => n * 2)
                      .OrderBy(n => n);
  ```

### **Don'ts:**

- **Avoid Multiple Enumerations**: Don't iterate over a LINQ query multiple times, as it can hurt performance.
  
  ```csharp
  var query = numbers.Where(n => n > 10);
  foreach (var n in query) { /*...*/ }
  foreach (var n in query) { /*...*/ }  // Inefficient, will re-query the data
  ```

- **Don't Overuse LINQ for Critical Performance Code**: For performance-critical applications, manually looping through collections might be faster.
