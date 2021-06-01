---
title: Compiler Midterm
---

# Chapter 1
## Compiler structure(15%)
* 必考
* Please draw the phases of a compiler.
* Please write down the sequence of phases of a typical compiler.
96, 100, 101 考畫圖
![](https://i.imgur.com/9EelKU3.png)
## Translate the assignment statement(20%)
* 必考
### 步驟
* 下面使用範例 position = initial + rate * 60 
#### 1.2.1 Lexical Analyzer
* The first phase of a compiler is called lexical analysis or scanning. The lex- ical analyzer reads the stream of characters making up the source program and groups the characters into meaningful sequences called lexemes. 
* For each lexeme, the lexical analyzer produces as output a token of the form 
$(token-name, attribute-value)$
![](https://i.imgur.com/0l9dPoj.png)
#### 1.2.2 Syntax Analysis
* The second phase of the compiler is syntax analysis or parsing. The parser uses the first components of the tokens produced by the lexical analyzer to create a tree-like intermediate representation that depicts the grammatical structure of the token stream. A typical representation is a syntax tree in which each interior node represents an operation and the children of t

#### 1.2.3 Semantic Analysis
* Uses the syntax tree and the information in the symbol table to check the source program for semantic consistency with the language definition. 
* Gathers type information and saves it in either the syntax tree or the symbol table, for subsequent use during intermediate-code generation. 
* An important part of semantic analysis is type checking
![](https://i.imgur.com/mnWpJiM.png)
#### 1.2.4 Intermediate Code Generation2
* An explicit low-level or machine like intermediate representation
* intermediate representation should have two important properties: 
    1. easy to produce
    2. easy to translate to into the target machine
* Three-address code: consists of a sequence of assembly-like instructions with three operands per instruction
![](https://i.imgur.com/dT5lsKp.png)
#### 1.2.5 Code Optimization 
* Attempts to improve the intermediate code
    1. faster
    2. shorter code
    3. consumes less power
![](https://i.imgur.com/RtgzX5v.png)
#### 1.2.6 Code Generation 
* takes intermediate representation of the source program as input and maps it into the target language
* If the target language is machine code, registers or memory locations are selected for each of the variables used by the program. Then, the intermediate instructions are translated into sequences of machine instructions that perform the same task
![](https://i.imgur.com/G46AYrG.png)
#### 1.2.7 Symbol-Table Management 
* The symbol table is a data structure containing a record for each variable name, with fields for the attributes of the name
![](https://i.imgur.com/SiSrHp4.png)
#### Extra example
![](https://i.imgur.com/BvP12wv.jpg)
### 歷屆
#### 100
* Please translate the assignment statement: $c = (f-32)*5/9$;into assembly codes, where c and f are all floats. Please refer to Fig. 1.7 to write down the translation process.
#### 101
* Please translate the assignment statement: $f = 32+c*9/5$;into assembly codes, where c and f are all floats. Please refer to Fig. 1.7 to write down the translation process.
## Block structure
* 96(10%)
### 寫法
* Block Bx:
    * Declarations: Scope
        * A $B_x-B_y$
        * B $B_x$
        * C $B_x$
        * D $B_x$
* Block By:
    * Declarations: Scope
        * A $B_y$
# Chapter 2
## Construct syntax-directed translation scheme(7.5%)
* Construct a syntax-directed translation scheme that translates arithmetic expressions from Postfix notation into prefix notation
    * (96)
* Construct a syntax-directed translation scheme that translates arithmetic expressions from Prefix notation into infix notation
    * (100,101)
### Productions
#### infix
```
expr-> expr + term 
     | expr - term 
     | term        
term-> term * factor
     | term / factor
     | factor
factor-> digit | (expr)
```
#### Postfix
```
expr-> expr term +
     | expr term -
     | term        
term-> term factor *
     | term factor \
     | factor
factor-> digit | (expr)
```
#### Prefix
* Change operator to the front
### translation
####  infix to prefix
```
expr -> {print("+")} expr + term
      | {print("-")} expr - term
      | term
term -> {print("*")} term * factor
      | {print("/")} term / factor
      | factor
factor -> digit {print(digit)}
        | (expr)
```
### conclusion
* Production should be the original notation, insert Print operator at the targeted notation
## Give annotated parse tree(7.5%)
1. With each grammar symbol, a set of attributes, and
2. With each production, a set of semantic rules for computing the values ofthe attributes associated with the symbols appearing in the production.
* Postfix 63+52-/(96)
* Prefix 8-62(100)
* (3+2)*(8-5)(101)
#### example
![](https://i.imgur.com/5k881oP.png)
## recursive-descent parsers(10%)
* 100, 101
* Construct a recursive-descent parsers, starting with the following grammars:
    * $S\rightarrow Sab|ba$
    * $S\rightarrow S+A|S-A|c,  A\rightarrow a|b$
### answer
* always add this in answer
```
void match(terminal t) {
    if ( lookahead == t ) lookahead = nextTerminal;
    else report ("syntax error");
}
```
*  S -> + S S | - S S | a
```
 void S(){
  switch(lookahead){
    case "+":
      match("+"); S(); S();
      break;
    case "-":
      match("-"); S(); S();
      break;
    case "a":
      match("a");
      break;
    default:
      throw new SyntaxException();
  }
}
```
*  S -> S ( S ) S | ε
```
void S(){
  if(lookahead == "("){
    match("("); S(); match(")"); S();
  }
}
```
*  S -> 0 S 1 | 0 1
```
void S(){
  switch(lookahead){
    case "0":
      match("0"); S(); match("1");
      break;
    case "1":
      // match(epsilon);
      break;
    default:
      throw new SyntaxException();
  }
}
```
* $S\rightarrow S+A|S-A|c,  A\rightarrow a|b$
```
void S(){
  switch(lookahead){
    case "0":
      S(); match("+"); A(); 
      break;
    case "1":
      S(); match("-"); A();
      break;
    case "2":
      match("c");
      break;
    default:
      throw new SyntaxException();
  }
}

void A(){
  switch(lookahead){
  case "0":
      match("a");
      break;
    case "2":
      match("b");
      break;
    default:
      throw new SyntaxException();
  }
}
```
## Define a class for statement(10-15%)
* For-statements in C have the form:
    * 96. do statement while(expr)
    * 100,101. $if(exp_1)stmt_1\ else\ stmt_2$

### Example
* if(expr) statement
* ![](https://i.imgur.com/1hKy1qO.png)
* ![](https://i.imgur.com/qVkB6JL.png)
#### for
```
class For extends Stmt {
  Expr E1;
  Expr E2;
  Expr E3;
  Stmt S;
  public For(Expr expr1, Expr expr2, Expr expr3, Stmt stmt){
    E1 = expr1;
    E2 = expr2;
    E3 = expr3;
    S = stmt;
  }
  public void gen(){
    E1.gen();
    Label start = new Label();
    Label end = new Label();
    emit("ifEqualZero " + E.rvalue().toString() + " goto " + after);
    S.gen();
    E3.gen();
    emit("goto " + start);
    emit(end + ":")
  }
}
```
# Chapter 3
## Construct the tries(12-15%)
* Construct the tries and compute the failure function for the following sets of keywords:
    * person, peter, peseant(92)
    * all, fall, fatal(100)
    * all, fall, tall(101)
### 解法
#### trie
* There is one state for every string that is a prefix (not necessarily proper) of any keyword. The parent of a state corresponding to string $b_1b_2 ... b_k$ is the state that corresponds to $b1b2 ... b_{k-1}$
* 不同字，但prefix同樣的地方共用同一個state，開始不同的點形成分支
#### failure function
* The failure function for the general trie is defined as follows. Suppose $s$ is the state that corresponds to string $b_1b_2 ... b_n$. Then $f (s)$ is the state that corresponds to the longest proper suffix of $b_1b_2 ... b_n$ that is also a prefix of some keyword.
* 本身最長的suffix是別人的Prefix
### example
*![](https://i.imgur.com/9wHEQ7I.png)

![](https://i.imgur.com/goHOvd9.png)
## modify lex program(10%)
* Describe how to make the following modifications to the Lex program
### fig
```
%{
/* definitions of manifest constants
LT, LE, EQ, NE, GT, GE,
IF, THEN, ELSE, ID, NUMBER, RELOP */
%}

/* regular definitions */
delim [ \t\n]
ws {delim}+
letter [A-Za-z]
digit [0-9]
id {letter}({letter}|{digit})*
number {digit}+(\.{digit}+)?(E[+-]?{digit}+)?
%%
{ws} {/* no action and no return */}
if {return(IF);}
then {return(THEN);}
else {return(ELSE);}
{id} {yylval = (int) installID(); return(ID);}
{number} {yylval = (int) installNum(); return(NUMBER);}
"<" {yylval = LT; return(RELOP);}
"<=" {yylval = LE; return(RELOP);}
"=" {yylval = EQ; return(RELOP);}
"<>" {yylval = NE; return(RELOP);}
">" {yylval = GT; return(RELOP);}
">=" {yylval = GE; return(RELOP);}
%%
int installID() {/* function to install the lexeme, whose
first character is pointed to by yytext,
and whose length is yyleng, into the
symbol table and return a pointer
thereto */
}
int installNum() {/* similar to installID, but puts numerical constants into a separate table */
}
```
### 解法
* 符號（如：數字）加在regular definitions
* realative operation要在manifest constants中加入，並且仿照大於小於有ｙｙｖａｌ的
* Arithmatic operation 仿照ＲＥＬＯＰ
## NFA
![](https://i.imgur.com/8SH0h3P.png)
![](https://i.imgur.com/XR1KvoC.png)

## DFA(12-15%)
* (ba)*bb(a|b)* (96)
* (a|b)ab(a|b)* (100)
* (a|b)*ab(a|b)(101)
### NFA to DFA
![](https://i.imgur.com/6W8ULVr.png)
![](https://i.imgur.com/h7OrgyB.png)
### DFA
* regular expression to DFA
#### Syntax tree
![](https://i.imgur.com/0PtJJwo.png)
* $*$: Star node. set of all strings of letters, including $\epsilon$, the empty string.
* $\circ$: Cat node.
* $|$: Or node.
#### Method
* METHOD:
1. Construct a syntax tree T from the augmented regular expression (r)#.
2. Compute nullable, firstpos, lastpos, and fol lowpos for T 
3. Construct Dstates, the set of states of DFA D, and Dtran, the transition function for D, by the procedure of Fig. 3.62. The states of D are sets of positions in T . Initially, each state is "unmarked," and a state becomes "marked" just before we consider its out-transitions. The start state of D is firstpos(n0), where node n0 is the root of T . The accepting statesare those containing the position for the endmarker symbol #.

##### Fig 3.62
![](https://i.imgur.com/FESJ87g.png)
#### pos
![](https://i.imgur.com/Gk5CL8Z.png)
* follow pose
![](https://i.imgur.com/Sr9DzJr.png)
#### Minimize
![](https://i.imgur.com/FHc3Dp0.png)

###### tags: `Compiler` `CSnote`