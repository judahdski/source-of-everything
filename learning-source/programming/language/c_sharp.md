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

### **Type Conversion (Konversi Tipe Data)**

1. **Explicit  (Manual)**
   - Dilakukan ketika ada risiko kehilangan data.
   - Harus menggunakan fungsi/method tertentu.
   - Contoh: `int("123")`, `float("3.14")`, `str(123)`, `set([1, 2, 2, 3])`.
   
2. **Implicit (Otomatis oleh Interpreter/Compiler)**
   - Terjadi saat tidak ada kehilangan data.
   - Biasanya dalam operasi aritmetika atau tipe data yang lebih besar.
   - Contoh: `int → float`, `float → complex`, `bool → int`.


#### **Urutan Type Conversion (Explicit → Implicit)**  

#### **1. Explicit Type Conversion (Type Casting)**
   - **String → Number**  
     - `int("123") → 123`
     - `float("3.14") → 3.14`
   - **Number → String**  
     - `str(123) → "123"`
   - **Float → Int (Pembulatan Otomatis)**  
     - `int(3.99) → 3` (Desimal dipotong, bukan dibulatkan)
   - **List/Tuple → Set (Menghilangkan Duplikasi)**  
     - `set([1, 2, 2, 3]) → {1, 2, 3}`
   - **Dictionary → List (Hanya Mengambil Keys atau Values)**  
     - `list({"a": 1, "b": 2}) → ["a", "b"]`
   - **Binary/Octal/Hex → Integer**  
     - `int("1010", 2) → 10` (Binary ke Decimal)
     - `int("0o12", 8) → 10` (Octal ke Decimal)
     - `int("0xA", 16) → 10` (Hex ke Decimal)


#### **2. Implicit Type Conversion (Type Promotion)**
   - **Integer → Float**  
     ```python
     a = 5
     b = 2.0
     c = a + b  # a (int) dikonversi ke float
     print(c)   # Output: 7.0
     ```
   - **Integer/Float → Complex**  
     ```python
     a = 3   # Integer
     b = 2.5 # Float
     c = a + b * 1j  # Otomatis diubah ke Complex
     print(c)  # Output: (3+2.5j)
     ```
   - **Boolean → Integer (True = 1, False = 0)**  
     ```python
     a = True + 5  # True dikonversi jadi 1
     print(a)  # Output: 6
     ```
   - **Integer → String (Operasi String Concatenation)**  
     ```python
     name = "User" + str(21)  # Harus pakai str() untuk explicit conversion
     print(name)  # Output: "User21"
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

## **Collections**

### 1. **Array**  
Array adalah struktur data yang menyimpan elemen dengan tipe data yang sama dalam satu blok memori.  

#### **Deklarasi dan Inisialisasi**  
```csharp
int[] angka = new int[5];  // Array dengan ukuran 5
int[] nilai = {1, 2, 3, 4, 5};  // Array langsung diisi nilai
```

#### **Method dan Properti Umum**
- `Length` → Mendapatkan jumlah elemen dalam array.  
- `Array.Sort(array)` → Mengurutkan array secara ascending.  
- `Array.Reverse(array)` → Membalik urutan elemen dalam array.  
- `Array.IndexOf(array, item)` → Mencari index dari item tertentu.  
- `Array.Exists(array, predicate)` → Mengecek apakah suatu elemen ada dalam array.  

**Contoh:**  
```csharp
int[] angka = {5, 3, 8, 1};
Array.Sort(angka); // {1, 3, 5, 8}
Array.Reverse(angka); // {8, 5, 3, 1}
```

---

### 2. **List (Generic List)**  
List<T> adalah koleksi yang bisa menampung banyak elemen dengan ukuran yang fleksibel.  

#### **Deklarasi dan Inisialisasi**
```csharp
List<int> listAngka = new List<int> {1, 2, 3, 4, 5};
```

#### **Method dan Properti Umum**
- `Add(item)` → Menambahkan item ke dalam list.  
- `Remove(item)` → Menghapus item dari list.  
- `RemoveAt(index)` → Menghapus item berdasarkan index.  
- `Insert(index, item)` → Menyisipkan item di posisi tertentu.  
- `Contains(item)` → Mengecek apakah item ada dalam list.  
- `IndexOf(item)` → Mencari index suatu item dalam list.  
- `Count` → Mendapatkan jumlah item dalam list.  
- `Sort()` → Mengurutkan list.  

**Contoh:**  
```csharp
List<string> buah = new List<string> { "Apel", "Jeruk", "Mangga" };
buah.Add("Pisang");  // ["Apel", "Jeruk", "Mangga", "Pisang"]
buah.Remove("Jeruk");  // ["Apel", "Mangga", "Pisang"]
buah.Sort();  // Mengurutkan list
```

---

### 3. **Dictionary**  
Dictionary<TKey, TValue> adalah koleksi pasangan **key-value**.  

#### **Deklarasi dan Inisialisasi**  
```csharp
Dictionary<int, string> mahasiswa = new Dictionary<int, string>
{
    { 101, "Andi" },
    { 102, "Budi" },
    { 103, "Citra" }
};
```

#### **Method dan Properti Umum**
- `Add(key, value)` → Menambahkan pasangan key-value.  
- `Remove(key)` → Menghapus item berdasarkan key.  
- `ContainsKey(key)` → Mengecek apakah key ada di dictionary.  
- `ContainsValue(value)` → Mengecek apakah value ada di dictionary.  
- `TryGetValue(key, out value)` → Mencari value berdasarkan key.  
- `Keys` → Mengembalikan koleksi semua key.  
- `Values` → Mengembalikan koleksi semua value.  
- `Count` → Mendapatkan jumlah item dalam dictionary.  

**Contoh:**  
```csharp
Dictionary<string, int> stock = new Dictionary<string, int>
{
    { "Laptop", 5 },
    { "Mouse", 20 },
    { "Keyboard", 10 }
};

if (stock.ContainsKey("Mouse"))
{
    Console.WriteLine($"Stock Mouse: {stock["Mouse"]}");
}
```

---

### 4. **JsonObject (Menggunakan Newtonsoft.Json)**  
JsonObject digunakan untuk memproses data JSON di C#.

#### **Instalasi**
Menggunakan library **Newtonsoft.Json**, install melalui NuGet:  
```sh
Install-Package Newtonsoft.Json
```

#### **Deklarasi dan Inisialisasi JSON**  
```csharp
using Newtonsoft.Json.Linq;

string jsonString = "{ \"nama\": \"Andi\", \"usia\": 25 }";
JObject jsonObj = JObject.Parse(jsonString);
```

#### **Method Umum**
- `Parse(jsonString)` → Mengubah string JSON menjadi JObject.  
- `ToString()` → Mengubah JObject menjadi string JSON.  
- `Add(key, value)` → Menambahkan data ke JObject.  
- `Remove(key)` → Menghapus key dari JObject.  
- `ContainsKey(key)` → Mengecek apakah key ada di JSON.  
- `SelectToken("$.path")` → Mengambil data dari path JSON.  

**Contoh:**  
```csharp
using Newtonsoft.Json.Linq;

string json = "{ \"nama\": \"Budi\", \"usia\": 30 }";
JObject obj = JObject.Parse(json);

string nama = obj["nama"].ToString();
int usia = (int)obj["usia"];

obj["usia"] = 31;  // Mengupdate nilai
obj.Add("kota", "Jakarta");  // Menambah key baru
string jsonBaru = obj.ToString();
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
