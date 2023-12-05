# handling variable number of arguments
+ Refer to exercise 2.20.
+ Write a generalized `same-parity'. The procedure is
  (select f a x1 x2 x3 ..... xn),
  where f and a are mandatory, x1...xn are optional.
  'f' is a procedure which is called like (f a x_i). and will return a boolean value.
  The `select' will return a list consisted of x_i which makes (f a x_i) return true.
+ Write `same-parity' with the previous `select'.
+ You will need `apply' and its usage is shown below.
## For example:
      $ scheme48
      > ,load ex9-select.scm
      > (select (lambda (x y) (= x y)) 10 1 2 3 10 20 10)
      (10 10)
      > (select (lambda (x y) (even? y)) 10 1 2 3 4 5 6 7 8)
      (2 4 6 8)
      > (select (lambda (x y) (even? (+ x y))) 4 1 2 3 4 5 6 7 8 9 10 11)
      (2 4 6 8 10)
      > (same-parity 4 1 2 3 4 5 6 7 8 9 10 11)
      (4 2 4 6 8 10)
      > (select (lambda (x y) (even? (+ x y))) 3 1 2 3 4 5 6 7 8 9 10 11)
      (1 3 5 7 9 11)
      > (same-parity 3 1 2 3 4 5 6 7 8 9 10 11)
      (3 1 3 5 7 9 11)
      > (same-parity 1)
      (1)
      >
      ; 
      ; (apply f L), apply f with argument list L, 
      ;   for example: (apply + (list 7 9 11)) ==>  (+ 7 9 11)
      ; If `f' can accept variable number of arguments, `apply' is a must
      ; since it is impossible to invoke f like (f 1 2) and (f a b c d)
      ; simultaneously in a program. 
      ;
      > (apply + (list 1 2 3))                   ;  the same as (+ 1 2 3)
      6
      > (apply + (cons 1 (cons 2 (list 7 9))))   ; the same as (+ 1 2 7 9)
      19
      > (apply select                            ; the same as the first example
             (cons (lambda (x y) (= x y)) 
                   (cons 10       
                         (list 1 2 3 10 20 10))))
      (10 10)
      > ,exit
## .scm   
```scheme
(define (select f x . y)
    (define (iter f y)
      (cond ((null? y)     '())
            ((f x (car y)) (cons (car y) (iter f (cdr y))))
            (else (iter f  (cdr y)))))
    (iter f y))

(define (same-parity x . y)
    (if (null? y) (list x)
        (cons x
              (apply select (cons (lambda (a b) (even? (- a b)))
                                  (cons x y))))))
```
