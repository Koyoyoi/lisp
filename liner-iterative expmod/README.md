# linear-iterative expmod
+ Write a linear-iteraitve expmod. 
* Check exercise 1.16 for how to convert 'recursive' to 'iterative'.
+ The name of your function should be named ``expmod''.
* You should define two internal procedures named, *mod, square.
## For example:
      $
      $ cat ex5.scm 
      (define (expmod b n m)
        (define (*mod a b)  . . . . )
        (define (square x)  . . . . )
        (define (iter res b n)  . . . )
        (iter 1 b n))
      $ 
      $ scheme48
      > ,load ex5.scm
      > 
      > (expmod 3 1000 123)
      42
      > (expmod 3 0 123)
      1
      > (expmod 3 101 10)
      3
      > (expmod 123232 11123232322 1123)
      256
      > ,exit
      $ 
## .scm   
```scheme
(define (expmod b n m)
    (define (*mod a b)
            (modulo a b))
    (define (square x)
            (* x x))
    (define (iter res b n)
            (cond ((= n 0)
                 res)
            ((= (*mod n 2) 0)
                 (iter res (*mod (square b) m) (/ n 2)))
            (else
                 (iter (*mod (* res b) m) b (- n 1)))))
    (iter 1 b n))
```
