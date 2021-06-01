---
title: Compiler chapter 1
---
# CH1 Introduction
## 1.1 Language Processors
* a compiler is a program that can read a program in one language - the source language - and translate it into an equivalent program in another language - the target language
### Compiler
* Source program $\rightarrow$ Compiler $\rightarrow$ Target program
### Target program
* If the target program is an executable machine-language program, it can then be called by the user to process inputs and produce outputs;
* input $\rightarrow$ Target program $\rightarrow$ output
### Interpreter
* Instead of producing a target program as a translation, an interpreter appears to directly execute the operations specified in the source program on inputs supplied by the use
* ![](https://i.imgur.com/pxPuSY6.png)
## 1.2 The structure of a compiler
![](https://i.imgur.com/9EelKU3.png)
* 96,100 , 101 考畫上圖
* 下面使用範例 position = initial + rate * 60 
* symbol table

| 1| position  |float |
| -------- | ---------- | -------- |
| 2         |   inital     |    float      |
| 3     | rate       | float   |

### 1.2.1 Lexical Analyzer
* The first phase of a compiler is called lexical analysis or scanning. The lex- ical analyzer reads the stream of characters making up the source program and groups the characters into meaningful sequences called lexemes. 
* For each lexeme, the lexical analyzer produces as output a token of the form 
$(token-name, attribute-value)$
![](https://i.imgur.com/0l9dPoj.png)
### 1.2.2 Syntax Analysis
* The second phase of the compiler is syntax analysis or parsing. The parser uses the first components of the tokens produced by the lexical analyzer to create a tree-like intermediate representation that depicts the grammatical structure of the token stream. A typical representation is a syntax tree in which each interior node represents an operation and the children of the node represent the arguments of the operation. 
![](https://i.imgur.com/aaegVjc.png)

### 1.2.3 Semantic Analysis
* Uses the syntax tree and the information in the symbol table to check the source program for semantic consistency with the language definition. 
* Gathers type information and saves it in either the syntax tree or the symbol table, for subsequent use during intermediate-code generation. 
* An important part of semantic analysis is type checking
![](https://i.imgur.com/mnWpJiM.png)
### 1.2.4 Intermediate Code Generation2
* An explicit low-level or machine like intermediate representation
* intermediate representation should have two important properties: 
    1. easy to produce
    2. easy to translate to into the target machine
* Three-address code: consists of a sequence of assembly-like instructions with three operands per instruction
![](https://i.imgur.com/dT5lsKp.png)
### 1.2.5 Code Optimization 
* Attempts to improve the intermediate code
    1. faster
    2. shorter code
    3. consumes less power
![](https://i.imgur.com/RtgzX5v.png)
### 1.2.6 Code Generation 
* takes intermediate representation of the source program as input and maps it into the target language
* If the target language is machine code, registers or memory locations are selected for each of the variables used by the program. Then, the intermediate instructions are translated into sequences of machine instructions that perform the same task
![](https://i.imgur.com/G46AYrG.png)
### 1.2.7 Symbol-Table Management 
* The symbol table is a data structure containing a record for each variable name, with fields for the attributes of the name
![](https://i.imgur.com/SiSrHp4.png)
#### Extra example
![](https://i.imgur.com/BvP12wv.jpg)
### 1.2.8 The Grouping of Phases into Passes 
* Activities from several phases may be grouped together into a pass that reads an input file and writes an output file
* We can produce compilers for different machines, by combining a front end with back ends for different target machines
### 1.2.9 Compiler-Construction Tools
* Parser generators
* Scanner generators
* Syntax-directed translation engines
* Code-generator generators
* Data-flow analysis engine
* Compiler-construction toolkits
## 1.3 The Evolution of Programming Languages 
### 1.3.1 The Move to Higher-level Languages 
#### Generations
* 1st machine languages
* 2nd assembly languages
* 3rd high level languages
* 4th languages designed for specific applications. e.g. NOMAD, SQL
* 5th logic and constraint-based languages. e.g. Prolog, OPS5
#### Types
* Imperative: Program specifies how a computation is to be done. Uses statements that change a program's state. e.g. c, c++, c#, Java
* Declarative: Program specifies what a computation is to be done. That expresses the logic of a computation without describing its control flow. e.g. SQL
* Functional: constructed by applying and composing functions. e.g. Lisp, scheme
* Object-oriented: one that supports object-oriented programming e.g. c++
* von Neumann language: computational model is based on the von Neumann computer archi- tecture. 
* Scripting languages: Interpreted languages with high-level operators designed for “gluing together” computations. e.g. Lisp, Lua, Bash
### 1.3.2 Impacts on Compilers 
*  a computer system is dependent on compiler technology 
*  compilers are used as a tool in evaluating architectural concepts before a computer is 
* Compiler writing is challenging
* compiler must translate correctly the potentially finite set of programs that could be written in the source language
## 1.4 The Science of Building a Compiler 
### 1.4.1 Modeling in Compiler Design and Implementation
* The study of compilers is mainly a study of how we design the right mathematical models and choose the right algorithms, while balancing the need for generality and power against simplicity and efficiency.
* Finite-state machines and regular expressions are useful for describing the lexical units of programs
* Context-free grammars are used to describe the syntactic structure of programming languages
### 1.4.2 The Science of Code Optimization
* The term "optimization" in compiler design refers to the attempts that a compiler makes to produce code that is more efficient than the obvious code.
* Processor architectures have become more complex, yielding more opportunities to improve the way code executes
* All compilers will have to face the problem of taking advantage of multiprocessor machines
#### Objectives
* optimization must be correct, that is, preserve the meaning of the compiled program
* optimization must improve the performance of many programs
* compilation time must be kept reasonable
* engineering effort required must be manageable
## 1.5 Applications of Compiler Technology
* Implementation of high-level programming languages 
* Optimizations for computer architectures 
* Design of new computer architectures
* Program translations  Software productivity tools
###### tags: `Compiler` `CSnote`

