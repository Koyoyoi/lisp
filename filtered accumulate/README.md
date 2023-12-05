# filtered accumulate
+ Refer to exercise 1.33.
+ Write a linear-iterative filtered-accumulate.
+ Using the above filtered-accumulate, write a procedure, named (sum-divisors n), which calculates the sum of divisors of n.
## For example:
      $ scheme48
      > ,load ex6.scm
      > 
      > (define (ok k) #t)       ;; always true
      ; no values returned
      > (define (inc x) (+ x 1))
      ; no values returned
      > (define (id x) x)
      ; no values returned
      > (filtered-accumulate ok + 0 id 1 inc 10)
      55
      > (filtered-accumulate ok * 1 id 1 inc 10)
      3628800
      > (filtered-accumulate even? + 0 id 1 inc 10)
      30
      > (sum-divisors 10)
      18
      > (sum-divisors 1)
      1
      > (sum-divisors 120)
      360
      > ,exit
      $ 
## .scm   
```scheme
(define (sum-divisors n)
    (define (divisor? x)
        (= (gcd x n) x))
    (define (id x) x)
    (define (inc x) (+ x 1))
    (define (filtered-accumulate filter combin null-value term a next b)
        (define (iter a result)
            (cond ((> a b)
                      result)
                  ((filter a)
                      (iter (next a) (combin (term a) result)))
                  (else
                      (iter (next a) result))))
        (iter a null-value))
    (filtered-accumulate divisor? + 0 id 1 inc n))
```
