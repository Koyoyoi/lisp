# enumerating tuples
+ Define a procedure, (enum-tuples list-1 list-2 .... list-k) which will generate a list of k-tuples. The tuples contains all combinations of elements from each list.
  The tuples are listed in row-major order.
## For example:
      $ scheme48
      > ,load ex11-enum-tuples-row-major.scm
      > (enum-tuples) 
      ()
      > (enum-tuples '(a b c))
      ((a) (b) (c))
      > (enum-tuples '(a b c) '(11 22))
      ((a 11) (a 22) (b 11) (b 22) (c 11) (c 22))
      > (enum-tuples '(a b) '(1 2) '(ok no))
      ((a 1 ok) (a 1 no) (a 2 ok) (a 2 no) (b 1 ok) (b 1 no) (b 2 ok) (b 2 no))
      > (enum-tuples '(a b) '(yes) '(ok no) '(aloha hi))
      ((a yes ok aloha) (a yes ok hi) (a yes no aloha) (a yes no hi) (b yes ok aloha) (b yes ok hi) (b yes no aloha) (b yes no hi))
      > ,exit
      $ 
## .scm   
```scheme
(define (proc lst f)
        (if (null? lst) '()
            (append (f (car lst)) (proc (cdr lst) f))))

(define enum-tuples
    (lambda (lst-x . lst-y)
        (cond ((null? lst-x) '())
              ((null? lst-y) (map list lst-x))
              (else (proc lst-x (lambda (x)
                                    (map (lambda (y) (cons x y))
                                             (apply enum-tuples lst-y))))))))
```
