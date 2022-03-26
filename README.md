Ananya Mathur, 2020CS50416

ML-Lex for LEXING, ML-YACC for PARSING

This folder contains while_ast.sml, while_ast.lex, while_ast.yacc, while_ast.cm, compiler.sml, glue.sml, vmc.sml and README

## AST DATATYPE DEFINITION

**Program** = PROG of IDEN * Block

**Type** = INT, BOOL

**Block** = BLK of DeclarationSequence * CommandSequence

**Exp** = IEXP of int , BEXP of bool , BINEXP of BinaryOp * Exp * Exp , UNEXP of UnaryOp * Exp , CONDEXP of RelOp * Exp * Exp

**Declaration** = DECL of Variable * VariableList * Type

**DeclarationSequence** = DECLSEQ1 of Declaration, DECLSEQ2 of Declaration * DeclarationSequence

**CommandSequence** = CMDSEQ1 of Command, CMDSEQ2 of Command*CommandSequence

**VariableList** = VARLIST1 of Variable, VARLIST2 of Variable*VariableList

**Command** = SET of Variable * Exp , ITE of Exp * CommandSequence * CommandSequence , WH of Exp * CommandSequence 

**UnaryOp** = NOT , NEG

**BinaryOp** = PLUS , MINUS , TIMES , DIV , MOD , AND , OR

**RelOp** = EQ of Exp * Exp , NEQ of Exp * Exp , LT of Exp * Exp , LEQ of Exp * Exp , GT of Exp * Exp , GEQ of Exp * Exp

**Variable** = VAR of IDEN

## CONTEXT FREE GRAMMAR
START ::=  Program

Program ::=  PROG IDEN SEQ Block

Type ::=  INT |BOOL

Block ::=  DeclarationSequence CommandSequence 

Declaration ::=  VAR VariableList COLON Type SEMICOLON

DeclarationSequence ::=  Declaration | Declaration DeclarationSequence

CommandSequence ::=  LCUR CommandSequence1 RCUR

VariableList ::=  Variable |Variable SEMICOLON VariableList

CommandSequence1 ::=  Command SEMICOLON | Command SEMICOLON CommandSequence1

Command ::=  Variable SET Expression | READ Variable | WRITE Expression | IF Expression THEN CommandSequence ELSE CommandSequence ENDIF | 
WHILE Expression DO CommandSequence ENDWH 

Expression ::=  Expression PLUS Expression | Expression MINUS Expression | Expression OR Expression | Expression GT Expression | Expression GEQ Expression |Expression LT Expression|
Expression LEQ Expression | Expression EQ Expression | Expression NEQ Expression | Expression TIMES Expression | Expression DIV Expression | Expression MOD Expression | Expression AND Expression | 
NOT Expression 

Variable ::= IDEN

## FunStack IMPLEMENTATION

Implemented a general-purpose functional stack structure as mentioned in the assignment with all required Stack functions in vmc.sml. 

## Memory M

Allocated space for variables as an Array.array in vmc.sml.

## Vmc structure

I have defined type VMC = 'a Stack * Array.array * 'a Stack in vmc.sml.

## Semantic Rules

Implemented semantic rules using the function rules which takes VMC as input (one configuration) and using pattern matching applies the relevant semantic rule (using stack operations) to output a VMC configuration in vmc.sml.

## postfix function

This is a recursive function which returns postfix of a program (as a' list) given as input in the form of an AST. It is present in while_ast.sml .

## execute function

execute function takes postfix of a program as list as input and outputs a VMC (final configuration). It calls a function f, which recursively calls itself after application of rules on the current VMC configuration.
 

## ACKNOWLEDGEMENTS

1. http://rogerprice.org/ug/ug.pdf : referred to pi.lex, pi.yacc, compiler.sml, datatypes,sml, pi.cm for lexing, parsing
2. https://github.com/arch1902/COL226-PL-Assignments/blob/main/A2%20-%20Lexer%20and%20Parser%20of%20Boolean%20Algebra/a2.yacc : Github repo of Senior, Referred for defining format of grammar in while_ast.yacc
3. http://www.cs.cornell.edu/courses/cs312/2005sp/lectures/rec07.html https://smlfamily.github.io/Basis/list.html#SIG:LIST.mapPartial:VAL https://www.cs.cornell.edu/courses/cs312/2008sp/recitations/rec05.html https://condor.depaul.edu/ichu/csc447/notes/wk8/ml.html : Implementation of Stack functions
