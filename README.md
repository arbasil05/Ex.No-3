# Ex.No:3
## RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
## Register Number: 212223040002
## Date: 15-09-2025
## AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
## PROGRAM
#### arth.l:
```l
%{
#include "arth.tab.h"   // so it knows the token names from YACC
%}

%%

"="          { printf("\n Operator is EQUAL"); return '='; }
"+"          { printf("\n Operator is PLUS"); return PLUS; }
"-"          { printf("\n Operator is MINUS"); return MINUS; }
"/"          { printf("\n Operator is DIVISION"); return DIVISION; }
"*"          { printf("\n Operator is MULTIPLICATION"); return MULTIPLICATION; }

[a-zA-Z]*[0-9]* { printf("\n Identifier is %s", yytext); return ID; }

.            { return yytext[0]; }
\n           { return 0; }

%%

int yywrap() { return 1; }

```
#### arth.y:
```y
%{
#include <stdio.h>
%}

%token ID PLUS MINUS MULTIPLICATION DIVISION

%%

statement:
    ID '=' E {
        printf("\nValid arithmetic expression");
        $$ = $3;   // semantic value (not needed here, but ok)
    }
;

E:
    E PLUS ID
  | E MINUS ID
  | E MULTIPLICATION ID
  | E DIVISION ID
  | ID
;

%%

extern FILE* yyin;

int main() {
    do {
        yyparse();
    } while (!feof(yyin));
    return 0;
}

void yyerror(char *s) {
    fprintf(stderr, "Error: %s\n", s);
}

```
## OUTPUT:

#### COMMANDS:

<img width="1205" height="504" alt="image" src="https://github.com/user-attachments/assets/5b54238e-492f-4115-b15e-ca9b8f06b6d3" />

#### VALID EXPRESSION:

<img width="488" height="280" alt="image" src="https://github.com/user-attachments/assets/185261aa-eb30-40ca-9316-5ffc87488ac0" />

#### INVALID EXPRESSION:

<img width="468" height="407" alt="image" src="https://github.com/user-attachments/assets/35495360-6c2a-4188-af38-da54b7e15656" />


## RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
