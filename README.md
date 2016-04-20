# C# Style Guide

## Purpose

If you are looking for an opinionated style guide for syntax, conventions and structuring the source code of your C# based application then step right in. This article is based on my development experience and working in teams.

The purpose of this style guide is to provide guidance writing correct, reusable and most importantly developer friendly source code. I'm going to explain why I choose to use these conventions.

## Contributing

I am by all means don't know everything and of course make mistakes. If you have any suggestion or question feel free to leave them as Issues in the repository. If you find a typo create a pull request.

*By contributing to this repository you are agreeing to make your content available subject to the license of this repository*

## Table of Contents

1. [Classes](#classes)
2. [Constructors](#constructors)
3. [Class members](#class-members)
4. [Methods and functions](#methods-and-functions)
5. [Variables](#variables)

## Classes

### Rule of 1

  - Define one class per file, recommended to be less then 500 lines of code.
  
  *Why?*: One class per file makes it easier to read and maintain the source code. Also it helps avoid conflicts in source control.

### Visibility

  - Use explicit visibility. Don't let internal classes garbaging the public interface of a library.
  
  *Why?*: Don't let developers use classes which are intended for internal use. This will make clear the purpose of the library.

### Seal

  - Classes which are not part of a hierarchy or not intended to inherit from should be marked with the *sealed* modifier.
  
  *Why?*: There are classes where it's difficult to enforce behaviors. Also we should only allow inheritance where it actually makes sense. It's hard to design classes which can be effectively extended and sometimes it is better if we don't allow it at all.

## Constructors

### One place

  - The initialization of an object happening in exactly one place: the constructor. Do not use inline initializations.
  
  *Why?*: It makes the source code readable and makes it harder to mess up something with an unwanted value. Because inline definitions run before the constructor it's actually possible to initialize a member twice.

  ```csharp
  public class Computer
  {
    /* avoid */
    private readonly HardDrive _hardDrive = new HardDrive();
    ...
    
    public class Computer()
    {
      ...
    }
  }
  
    public class Computer
  {
    /* recommended */
    private readonly HardDrive _hardDrive;
    ...
    
    public class Computer()
    {
      _hardDrive = new HardDrive();
    }
  }
  ```

### Leave it in good state

  - After the constructor executed the object should be in a "correct" state. This means there are no uninitialized members and every method call is work as intended.

  *Why?*: As a developer I expect that after the constructor called the object is ready to use.

### Less is more

  - Do not place too much logic in the constructor. The only job of the constructor is to set an initial state. After that the object is usable. A rule of thumb can be that a constructor consist of N + 5 lines where N is the number of members (not counting parameter checks).
  
  *Why?*: The constructor needs to be fast and needs to be safe. For example if your class handles database then the constructor does not need to do the database connection logic, it can be deferred to another method call. That way the developer will have complete control over the lifecycle of the object and avoid side effects.

  ```csharp
  public class DatabaseHandler
  {
    private readonly DatabaseConnection _connection;
    ...
    
    public class DatabaseHandler(string connectionString)
    {
      if(string.IsNullOrEmpty(connectionString))
      {
        throw new ArgumentException("connectionString");
      }
      
      _connection = new DatabaseConnection(connectionString);
      _connection.Start(); // avoid
    }
  }
  
  public class DatabaseHandler
  {
    private readonly DatabaseConnection _connection;
    ...
    
    public class DatabaseHandler(string connectionString)
    {
      if(string.IsNullOrEmpty(connectionString))
      {
        throw new ArgumentException("connectionString");
      }
      
      _connection = new DatabaseConnection(connectionString);
    }
    
    public void Start()
    {
      _connection.Start(); // recommended
    }
  }
  ```

## Class members

### Naming regular members
  - There are two conventions for naming private members. You should choose one and be consistent across the project.
  
  - Option 1: the name of the member is written with 'camelCase' (ie: starts with lowercase and use uppercase on subsequent words) and use 'this' when referencing it.
  - Option 2: the name of the member is starts with the underscore character '_', after that use the same format as in Option 1. Referencing does not require the 'this' keyword.
  
  *Why?* With Option 1 we have no way to make difference between variables and members, so we need to use the 'this' keyword. With Option 2 the underscore character will take care of this problem. Also, with Option 2 there is another advantage, when we hit underscore IntelliSense will display all name starting with underscore, ie all private members. With 'this' the list will include properties and methods too.

  ``` csharp
  public class Naming
  {
    private readonly string Member; // avoid
    private readonly string member; // recommended
    private readonly string _member; // recommended
    
    ...
    
    public void ThisIsAFunction()
    {
      Console.WriteLine(Member); // avoid
      Console.WriteLine(member); // avoid
      Console.WriteLine(this.member); // recommended
      Console.WriteLine(this._member); // avoid
      Console.WriteLine(_member); // recommended
    }
  }
  ```

### Naming constants and statics

  - The name of statics and constants written with 'PascalCase' (ie: starts with uppercase and use uppercase on subsequent words)
  
  ``` csharp
  public class Naming
  {
    public static string staticMember = "static"; // avoid
    public static string StaticMember = "static"; // recommended
    
    public const string constMember = "const"; // avoid
    public const string ConstMember = "const"; // recommended
  }
  ```

### Visibility

  - The visibility of class members is private or in some cases protected. If an inherited class uses the member but does not modify it create a property with only a getter. Always use the visibility keywords that way in the future all developers will know what your intention were.

### Readonly

  - Members when possible should have the readonly modifier, that way we enforce that every members get the appropriate value after the constuctor runned.

## Methods and functions

## Variables

## Copyright

Copyright (c) 2016- Istvan Reiter

## (The MIT License)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[Back to top](#table-of-contents)**
