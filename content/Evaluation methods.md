There are two approaches to evaluating compound expressions.

-  “fully expand and then reduce” evaluation method is known as **normal-order evaluation**, 
-  “evaluate the arguments and then apply” method that the interpreter actually uses, which is called **applicative-order evaluation**. 
 
Given a program
```
 (define (square x) (* x x))
 
(square 21)
 441
 
 (define (sum-of-squares x y)
	 (+ (square x) (square y)))
	 
 (sum-of-squares 3 4)
 25
 
 (define (f a)
	 (sum-of-squares (+ a 1) (* a 2)))
	 
 (f 5)
 136
```
Solve `(f 5)` using 
- Normal-order evaluation
```
(sum-of-squares (+ 5 1) (* 5 2))
(+ (square (+ 5 1)) (square (* 5 2)) ) 
(+ (* (+ 5 1) (+ 5 1)) (* (* 5 2) (* 5 2)))

followed by the reductions
(+ (* 6 6) (* 10 10))
(+ 36  100)
	 136
```
- Applicative-order evaluation
```
(f 5)
(sum-of-squares (+ a 1) (* a 2))
(sum-of-squares (+ 5 1) (* 5 2))
(+ (square 6) (square 10))
(+ (* 6 6) (* 10 10))
(+ 36 100)
136
```

It can be shown that, for procedure applications that can be modeled using substitution and that yield legitimate values, normal-order and applicative-order evaluation produce the same value. (See instance of an “illegit imate” value where normal-order and applicative-order evaluation do not give the same result.)