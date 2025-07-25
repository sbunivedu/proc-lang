This repository contains the implementation of the PROC language discussed in Section 3.3 in EOPL3.

## Syntax
The concrete syntax for the LET language is as follows (`[]` denotes abstract syntax):
```
Program     ::= Expression
                [a-program (exp1)]
Expression  ::= Number
                [const-exp (num)]
            ::= - (Expression , Expression)
                [diff-exp (exp1 exp2)]
            ::= zero? (Expression)
                [zero?-exp (exp1)]
            ::= if Expression then Expression else Expression
                [if-exp (exp1 exp2 exp3)]
            ::= identifier
                [var-exp (var)]
            ::= let identifier = Expression in Expression
                [let-exp (var exp1 body)]
            ::= proc (identifier) Expression
                [proc-exp (var body)]
            ::= (Expression Expression)
                [call-exp (rator rand)]
```

You can test the implementation by running `all.rkt` in DrRacket with the following test cases.

* step 1: load `all.rkt` in DrRacket and click on "Run" to execute the definitions.
* step 2: copy and paste the following commands one at a time into DrRacket's REPL/console.
```
> (run "(proc(x) -(x,1)  30)")
#(struct:num-val 29)
> (run "let f = proc (x) -(x,1) in (f 30)")
#(struct:num-val 29)
> (run "(proc(f)(f 30)  proc(x)-(x,1))")
#(struct:num-val 29)
> (run "((proc (x) proc (y) -(x,y)  5) 6)")
#(struct:num-val -1)
> (run "let f = proc(x) proc (y) -(x,y) in ((f -(10,5)) 6)")
#(struct:num-val -1)
> (run  "
let fix =  proc (f)
            let d = proc (x) proc (z) ((f (x x)) z)
            in proc (n) ((f (d d)) n)
in let
    t4m = proc (f) proc(x) if zero?(x) then 0 else -((f -(x,1)),-4)
in let times4 = (fix t4m)
   in (times4 3)")
#(struct:num-val 12)
```