Ananya Mathur, 2020CS50416

ML-Lex for LEXING, ML-YACC for PARSING

This folder contains while_ast.sml, while_ast.lex, while_ast.yacc, while_ast.cm, compiler.sml, glue.sml and README

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

## ACKNOWLEDGEMENTS

1. http://rogerprice.org/ug/ug.pdf : referred to pi.lex, pi.yacc, compiler.sml, datatypes,sml, pi.cm for lexing, parsing
2. https://github.com/arch1902/COL226-PL-Assignments/blob/main/A2%20-%20Lexer%20and%20Parser%20of%20Boolean%20Algebra/a2.yacc : Github repo of Senior, Referred for defining format of grammar in while_ast.yacc
