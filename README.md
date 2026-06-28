# cloxInterpreter
Interpreter in C for Lox language based on craftinginterpreters.com

## How to use
1. Ensure you have a C compiler installed (e.g., `gcc` or `clang`).
2. Clone this repository: `git clone https://github.com/allan-brunner/cloxInterpreter.git`
3. Compile the interpreter:
    **Using raw GCC** (adjust the path based on your folder structure): `gcc -o clox *.c`
    **Using Make** (if you have a Makefile configured): `make`
4. Run the program:  
4.1. Runs the CLI interpreters: `./clox`  
4.2. Interprets a script: `./clox script.lox`

## Grammar
```
program        → declaration* EOF ;

declaration    → classDecl
               | funDecl
               | varDecl
               | statement ;

classDecl      → "class" IDENTIFIER ( "<" IDENTIFIER )?
                 "{" function* "}" ;

funDecl        → "fun" function ;
function       → IDENTIFIER "(" parameters? ")" block ;
parameters     → IDENTIFIER ( "," IDENTIFIER )* ;

varDecl        → "var" IDENTIFIER ( "=" expression )? ";" ;
statement      → exprStmt
               | forStmt
               | ifStmt
               | printStmt
               | returnStmt
               | whileStmt
               | block ;

returnStmt     → "return" expression? ";" ;

forStmt        → "for" "(" ( varDecl | exprStmt | ";" )
                 expression? ";"
                 expression? ")" statement ;

whileStmt      → "while" "(" expression ")" statement ;

ifStmt         → "if" "(" expression ")" statement
               ( "else" statement )? ;
block          → "{" declaration* "}" ;

exprStmt       → expression ";" ;
printStmt      → "print" expression ";" ;

expression     → assignment ;
assignment     → ( call "." )? IDENTIFIER "=" assignment
               | logic_or ;
logic_or       → logic_and ( "or" logic_and )* ;
logic_and      → equality ( "and" equality )* ;
equality       → comparison ( ( "!=" | "==" ) comparison )* ;
comparison     → term ( ( ">" | ">=" | "<" | "<=" ) term )* ;
term           → factor ( ( "-" | "+" ) factor )* ;
factor         → unary ( ( "/" | "*" ) unary )* ;
unary          → ( "!" | "-" ) unary | call ;
call           → primary ( "(" arguments? ")" | "." IDENTIFIER )* ;

arguments      → expression ( "," expression )* ;

primary        → NUMBER | STRING | "true" | "false" | "nil" | "this"
               | "(" expression ")" ;
               | IDENTIFIER | "super" "." IDENTIFIER ;```
