#  representing a pair with a number
+ Refer to exercise 2.5.
+ Note the requirement of nonnegative is removed. Your method should accept two integers.
## For example:
      $ scheme48
      > ,load ex8-pair-int.scm
      > (define x (my-cons 2 -5))
      ; no values returned
      > (my-car x)
      2
      > (my-cdr x)
      -5
      > ,exit
      $ 
## .scm   
```scheme
(define (my-cons a b)
    (cond ((and (> a 0) (> b 0))
                (* (expt 2 a) (expt 3 b)))
          ((and (> a 0) (< b 0))
                (* (expt 5 a) (expt 7 (- b))))
          ((and (< a 0) (> b 0))
                (- (* (expt 5 (- a)) (expt 7 b))))
          ((- (* (expt 2 (- a)) (expt 3 (- b)))))))
(define (my-car n)
    (cond ((= 0 (remainder n 2))
                (if (> n 0)
                    (iter-div n 2)
                    (- (iter-div n 2))))
          ((= 0 (remainder n 5))
                (if (> n 0)
                    (iter-div n 5)
                    (- (iter-div n 5))))
          (0)))
(define (my-cdr n)
    (cond ((= 0 (remainder n 3))
                (if (> n 0)
                    (iter-div n 3)
                    (- (iter-div n 3))))
          ((= 0 (remainder n 7))
                (if (< n 0)
                    (iter-div n 7)
                    (- (iter-div n 7))))
          (0)))
(define (iter-div n divisor)
    (define (iter x divisions)
        (if (= 0 (remainder x divisor))
            (iter (/ x divisor) (+ divisions 1))
            divisions))
    (iter n 0))
```
