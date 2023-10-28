<<<<<<< HEAD
# Sum of square two
Figure out the sum of squares of the smaller two arguments   
Write a procedure named 'sum-of-square-smaller-two' which accepts three arguments and figures out the sum of squares of the smaller two of the arguments.
#
\$ scheme48  
=======
#Figure out the sum of squares of the smaller two arguments   
Write a procedure named 'sum-of-square-smaller-two' which accepts three arguments and figures out the sum of squares of the smaller two of the arguments.
#\$ scheme48  
>>>>>>> 96cc5449db5ed39b40bcb52530f00bbce9a3a583
\> ,load ex2-sum-square-smaller-two.scm  
\>   
\> (sum-of-square-smaller-two 1 2 3)   
5   
\> (sum-of-square-smaller-two 1 2 -3)   
10  
\> (sum-of-square-smaller-two 2 2 2)  
8  
\> ,exit   
\$   
```scheme
(define (sum-of-square a b)  
  (+ (* a a) (* b b)))  
(define (sun-of-square-smaller-two x y z)  
  (cond ((and (> x y) (> x z)) (sum-of-square y z))  
        ((and (> y x) (> y z)) (sum-of-square x z))  
        (else (sum-of-square x y))))  
<<<<<<< HEAD
```
=======
```
>>>>>>> 96cc5449db5ed39b40bcb52530f00bbce9a3a583
