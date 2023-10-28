# recursive and linear iterative
efer to exercise 1.11 but the formula is changed to
>f(0) = 7
>f(1) = 3
>f(2) = 5
>f(n) = -f(n-1) + f(n-2) + f(n-3) if n ≥ 3 and n %3 == 0
>f(n) = f(n-1) - f(n-2) + f(n-3) if n ≥ 3 and n %3 == 1
>f(n) = -f(n-1) + f(n-2) - f(n-3) if n ≥ 3 and n %3 == 2
>Note that you have to write two procedures. One is written in recursive way and another in linear iterative way.
You can use (remainder n m) to compute the remainder of n divided by m.
# For example:
      \$ scheme48
      \> ,load ex4.scm
      \> (fun-rec 0)
      7
      \> (fun-rec 5)
      -3
      \> (fun-rec 10)
      51
      \> (fun-ite 10)
      51
      \> (fun-ite 100)
      84553538310603107
      \> (fun-rec 100)     <------------- take too much time to run
      ^C
      interrupt: keyboard interrupt [command-level-event-handler]
                 keyboard
      1\> ,exit
      \$ 
# .scm
```scheme
(define (fun-rec x)
    (cond ((= x 0) 7)
          ((= x 1) 3)
          ((= x 2) 5)
          ((= (modulo x 3) 0)
             (+
                  (- (fun-rec (- x 1)))
                  (fun-rec (- x 2))
                  (fun-rec (- x 3))))
          ((= (modulo x 3) 1)
             (+
                  (fun-rec (- x 1))
                  (- (fun-rec (- x 2)))
                  (fun-rec (- x 3))))
          ((= (modulo x 3) 2)
             (+
                  (- (fun-rec (- x 1)))
                  (fun-rec (- x 2))
                  (- (fun-rec (- x 3)))))))

(define (fun-ite x)
    (define (iter-sum c b a n count)
            (cond ((= count 0) c)
                  ((= (modulo n 3) 0)
                      (iter-sum (+ (- c) b a) c b (+ n 1) (- count 1)))
                  ((= (modulo n 3) 1)
                      (iter-sum (+ c (- b) a) c b (+ n 1) (- count 1)))
                  ((= (modulo n 3) 2)
                      (iter-sum (+ (- c) b (- a)) c b (+ n 1) (- count 1)))))
    (cond ((= x 0) 7)
          ((= x 1) 3)
          ((= x 2) 5)
          (else (iter-sum 5 3 7 3 (- x 2)))))

```