# Question
Exercise 2.11.

# Answer
## Codes
```scheme
(define (make-interval a b)
  (cons a b))
(define (lower-bound i)
  (car i))
(define (upper-bound i)
  (cdr i))
(define (mul-interval x y)
  (let ((p1 (* (lower-bound x) (lower-bound y)))
        (p2 (* (lower-bound x) (upper-bound y)))
        (p3 (* (upper-bound x) (lower-bound y)))
        (p4 (* (upper-bound x) (upper-bound y))))
    (make-interval (min p1 p2 p3 p4)
                   (max p1 p2 p3 p4))))
(define (width i)
  (* 0.5 (- (upper-bound i) (lower-bound i))))
(define (div-interval x y)
  (if (= (width y) 0)
    (display "the width of the denominator is 0")
    (mul-interval x
                  (make-interval (/ 1.0 (upper-bound y))
                               (/ 1.0 (lower-bound y))))))
(define (make-center-width c w)
  (make-interval (- c w) (+ c w)))
(define (center i)
  (/ (+ (lower-bound i) (upper-bound i)) 2))
(define (make-center-percent c p)
  (let ((w (abs (* c p))))
    (make-interval (- c w) (+ c w))))
(define (percent i)
  (/ (width i) (center i)))

; test
(define i (make-center-percent 2 0.5))
```

## Running
```
1 ]=> i

;Value 15: (1. . 3.)

1 ]=> (center i)

;Value: 2.

1 ]=> (percent i)

;Value: .5

1 ]=> (width i)

;Value: 1.
```
