This repository contains the implementation of the PROC language discussed in Section 3.3 in EOPL3.

You can test the implementation by running `all.rkt` in DrRacket with the following test cases:
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