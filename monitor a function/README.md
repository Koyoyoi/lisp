# monitor a function
+ Refer to exercise 3.2.
+The "f" may take any number of arguments. See the examples below. You may have to use "apply".
## For example:
      $ scheme48
      > ,open random
      > (define a (make-random 1024))
      ; no values returned
      > (a)
      150946159
      > (a)
      44350967
      > ,load ex13-monitor.scm
      > (define f (make-monitored a))
      ; no values returned
      > (f)
      88941411
      > (f)
      154130900
      > (f 'how-many-calls?)
      2
      > (f) 
      1024
      > (f)
      159857230
      > (f)
      53732961
      > (f 'how-many-calls?)
      5
      > (f 'reset-count)
      0
      > (f)
      10059006
      > (f 'how-many-calls?)
      1
      > (define plus (make-monitored +))
      ; no values returned
      > (plus)
      0
      > (plus 1 2 3 4 5)
      15
      > (plus 'how-many-calls?)
      2
      > (plus 'reset-count)
      0
      > (plus 1 2)
      3
      > (plus 'how-many-calls?)
      1
      > ,exit
      $  
## .scm   
```scheme
(define (make-monitored f)
   (let ((count 0))
     (define (mf . msg)
       (cond ((and (number? (f)) (NULL? msg))
                 (begin (set! count (+ count 1))
                        (f)))
             ((eq? (car msg) 'how-many-calls?) count)
             ((eq? (car msg) 'reset-count) (begin (set! count 0)
                                              count))
             (else (begin (set! count (+ count 1))
                          (apply f (cons 0 msg))))))
     mf))
```
