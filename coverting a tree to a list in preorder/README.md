# converting a tree to a list in preorder
+ A tree with a single node is like: '(a).
+ A tree with root 'a' and two children 'b' 'c' is like: '(a (b) (c)). And more examples:
            a
          / | \      ==> (a (b) (c) (d))
         b  c  d

            a
          / | \      ==> (a (b) (c (e)) (d (f) (g))) 
         b  c  d
            |  |\
            e  f g      
## For example:
      $ scheme48
      > ,load ex10-preorder.scm
      >
      > (preorder '(a  (b (c))  (e (f) (g))))
      (a b c e f g)
      >
      > (preorder '(a (b) (c) (f (g) (h))))
      (a b c f g h)
      >
      > (preorder '((hello) (b) ((baga me) (ok))))
      ((hello) b (baga me) ok)
      > ,exit
      $ 
## .scm   
```scheme
(define (preorder tree)
    (cond ((null? tree) '())
          ((pair? (car tree))
              (append (preorder (car tree))
                      (preorder (cdr tree))))
          (else
              (cons (car tree)
                    (preorder (cdr tree))))))
```
