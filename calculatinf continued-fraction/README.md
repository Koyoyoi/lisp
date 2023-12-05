# calculating continued-fraction
+ Refer to exercise 1.37.
+ You have to write two procedures. One is (cont-frac n d k) and another is (root x).
+ The "cont-frac" can be implemented in linear iterative way or linear recursive way..
+ Use your "cont-frac" to write (root x).
+ The (root x) computes the root of f(y)=y^2-y-x. Assume x >= 0.
## For example:
      $ scheme48
      > ,load ex7.scm
      > (+ 1.0 (cont-frac (lambda (i) 1.0) (lambda (i) 1.0) 1000))
      1.618033988749895
      > 
      > (root 5)
      2.7912878474779195
      > (root 0)
      1.0
      > (root 1)  
      1.618033988749895
      > ,exit
      $ 
## .scm   
```scheme
(define (cont-frac n d k)
    (define (iter i result)
        (if (= i 0)
            result
            (iter (- i 1) (/ (n i) (+ (d i) result)))))
    (iter (- k 1) (/ (n k) (d k))))
(define (root x)
    (+ 1 (cont-frac (lambda (i) x) (lambda (i) 1.0) 1000)))
```
