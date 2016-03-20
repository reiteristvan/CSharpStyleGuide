# C# Style Guide

## Purpose

If you are looking for an opinionated style guide for syntax, conventions and structuring the source code of your C# based application then step right in. This article is based on my development experience and working in teams.

The purpose of this style guide is to provide guidance writing correct, reusable and most importantly developer friendly source code. I'm going to explain why I choose to use these conventions.

## Contributing

I am by all means don't know everything and of course make mistakes. If you have any suggestion or question feel free to leave them as Issues in the repository. If you find a typo create a pull request.

*By contributing to this repository you are agreeing to make your content available subject to the license of this repository*

## Table of Contents

1. [Classes](#classes)

## Classes

### Rule of 1

  - Define one class per file, recommended to be less then 500 lines of code.
  
  *Why?*: One class per file makes it easier to read and maintain the source code. Also it helps avoid conflicts in source control.

### Visibility

  - Use explicit visibility. Don't let internal classes garbaging the public interface of a library.
  
  *Why?*: Don't let developers use classes which are intended for internal use. This will make clear the purpose of the library.

### Seal

  - Classes which are not part of a hierarchy or not intended to inherit from should be marked with the *sealed* modifier.
  
  *Why?*: There are classes where it's difficult to enforce behaviors. Also we should only allow inheritance where it actually makes sense. It's hard to design classes which can be effectively extended and sometimes it is better if we don't allow it.

## Copyright

Copyright (c) 2016- Istvan Reiter

## (The MIT License)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[Back to top](#table-of-contents)**
