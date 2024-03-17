# Parser For Lisp

## Overview
This project is a program implemented in Go. It will parse and evalueate a subset of [lisp](https://clisp.sourceforge.io/) language.

## See Also
[Software licence](https://opensource.org/license/mit)

## Setup
1. [Install Go](https://go.dev/dl/)
2. In your own Go package, import sexpr package
   ```
   import (
  	"your_path_to_package/sexpr"
    )
   ```

## Usage and Features

### Usage
To parse a lisp command, you first need to create a Parser object.
```
parser := NewParser()
```
The parser is a type Parser interface and it has a Parser() function which takes in a string as a lisp command.

### Parser Behaviors
- If the string provided is not in valid syntax, parse function throws an error.
- If the syntax is valid, it will return a **SExpr pointer**. An example is:
  ```
  var res *SExpr
  res = parser.Parse("(length 1 2 3 4)")
  ```
- A SExpr object can either be
  1. An **Atom**
  2. A list, with its **car** points to the head, and its **cdr** points to the rest of the body as another list.
- The SExpr instance can be **evaluated** by calling the eval() function.

### Evaluation
- If the instance cannot be evaluated, e.g: a list with its **car** not an function or a function with invalid number of arguments, it throws an error.
- An **ATOM** evaluats to itself.
- Functions will be processed and stores the result as another SExpr object.
- A condition function evaluates to symbol **True** or a **Nil Object** representing false.

### MiniLisp
This project only parses a subset of Lisp, and its grammar is as follows:
> \<sexpr\> ::= \<atom\> | \<pars\> | QUOTE \<sexpr\>
> 
> \<atom\> ::= NUMBER | SYMBOL
> 
> \<pars\> ::= LPAR \<dotted_list\> RPAR | LPAR \<proper_list\> RPAR
> 
> \<dotted_list\> ::= \<proper_list\> \<sexpr\> DOT \<sexpr\>
> 
> \<proper_list\> ::= \<sexpr\> \<proper_list\> | \epsilon

The functions supported are:
1. Quote
2. Basic functions
   - length
   - car
   - cdr
3. Prejudices
   - nullp
   - listp
   - zerop
   - nump
4. Mathematical operations
   - \+
   - \*
   - \-

