---
title: Compiler chapter 3
---
#  Lexical Analysis
## 3.1 The Role of the Lexical Analyze
1. Read input characters of the source program, group them into lexemes
2. produce a sequence of tokens for each lexeme in the source program.
3. The stream of tokens is sent to the parser for syntax analysis. 
* We can produce a lexical analyzer automatically by specifying the lexeme patterns to a lexical analyzer generator and compiling those patterns into code functions as a lexical analyzer 
*  When the lexical analyzer discovers a lexeme constituting an identifier, it needs to enter that lexeme into the symbol table 
*  ![](https://i.imgur.com/j7W6XGq.png)
* Lexical analysis: 
    * remove white space and comments
    * correlate error message generated
    * may keep track of the number of the newline characters seen, so it can associate a line number with each error message 
* Two processes of lexical analyzers 
    1. Scanning: deletion of comments and compaction of consecutive whitespace characters into one 
    2. Lexical analysis: produces the sequence of tokens as output 
### 3.1.1  Lexical Analysis Versus Parsing
1. simplicity
2. efficiency
3. portability
### 3.1.2 Tokens, Patterns, and Lexeme

### 3.1.3 Attributes for Tokens 
### 3.1.4 Lexical Errors 
## 3.2 Input Buffering 
### 3.2.1 Buffer Pairs 
### 3.2.2 Sentinels 
## 3.3 Specification of Token
### 3.3.1 Strings and Languages 
### 3.3.2 Operations on Languages 
### 3.3.3 Regular Expressions 
### 3.3.4 Regular Definitions 
### 3.3.5 Extensions of Regular Expressions
## 3.4 Recognition of Tokens 
### 3.4.1 Transition Diagrams
### 3.4.2 Recognition of Reserved Words and Identifiers
### 3.4.3 Completion of the Running Example 
### 3.4.4 Architecture of a Transition-Diagram-Based Lexical Analyzer 
## 3.5 The Lexical-Analyzer Generator Lex
### 3.5.1 Use of Lex 
### 3.5.2 Structure of Lex Programs 
### 3.5.3 Conflict Resolution in Lex
### 3.5.4 The Lookahead Operator 
##  3.6 Finite Automata 
### 3.6.1  Nondeterministic Finite Automata
### 3.6.2 Transition Tables 
### 3.6.3 Acceptance of Input Strings by Automata 
### 3.6.4 Deterministic Finite Automata 
## 3.7 From Regular Expressions to Automata 
### 3.7.1 Conversion of an NFA to a DFA
### 3.7.2 Simulation of an NF
### 3.7.3 Efficiency of NFA Simulatio
### 3.7.4 Construction of an NFA from a Regular Expression 
### 3.7.5  Efficiency of String-Processing Algorithm
## 3.8  Design of a Lexical-Analyzer Generator
### 3.8.1 The Structure of the Generated Analyzer 
### 3.8.1 The Structure of the Generated Analyzer 
### 3.8.2 Pattern Matching Based on NFA's 
### 3.8.3 DFA's for Lexical Analyzers 
### 3.8.4 Implementing the Lookahead Operato
## 3.9 Optimization of DFA-Based Pattern Matchers 
### 3.9.1 Important States of an NFA 
### 3.9.2 Functions Computed From the Syntax Tree 
### 3.9.3 Computing nullable, firstpos, and lastpos 
### 3.9.4 Computing followpo
### 3.9.5 Converting a Regular Expression Directly to a DFA
### 3.9.6 Minimizing the Number of States of a DFA 
### 3.9.7 State Minimization in Lexical Analyzers
### 3.9.8 Trading Time for Space in DFA Simulation 
# Homework
* 3.3.6
* 3.4.6
* 3.4.11
* 3.5.1(a)(b)(c)
* 3.8.1
* 3.9.4(a)
###### tags: `Compiler` `CSnote`