Download Link: https://assignmentchef.com/product/solved-cs3723-asg6-lisp-macros
<br>
Code the two macros listed below and use the specified test cases.Notes:• You can only use the functions/macros we discussed in the LISP notes. You may use part 1 (+=) in part 2 (iterate).• Your code must be executed on a fox/hen server using the specified test cases. To load your code, use:(load “HW6_solution.lisp” :echo T :print T).• To run the test cases, use:(load “HW6_testcases.lisp” :echo T :print T)• Turn in a zip file named LastNameFirstName.zip (no spaces) containing:o Your source LISP code, named HW6_solution.lisp.o Your log of the session. This should be called HW6_out.txt. You can also use the dribble function mentioned in the notes.o Do not have any directories within your zip file.

1. Code the macro, +=, which is passed a variable which it increments and assigns the new value. The function value returned by += should be the new value of numericVariable.

You must verify that the variable is changed. It is NOT sufficient to see that it printed the correct number.

(+= numericVariable incrementValue)

Example:&gt; (setf x 1)1&gt; (+= x 5)6&gt; x6

CLISP sometimes gave an error like the following when you LOAD a file with that macro definition:#&lt;PACKAGE COMMON-LISP&gt; is lockedif you continue (by typing ‘continue’): Ignore the lock and proceedTo ignore that message, simply typeCONTINUE

2. Code the macro, iterate, which is based on the following:(iterate controlVariable beginValueExpr endValueExpr incrExpr bodyexpr1 bodyexpr2 … bodyexprN)• iterate is passed a controlVariable which is used to count from beginValueExpr to endValueExpr (inclusive) by the specified increment.• For each iteration, it evaluates each of the one or more body expressions.• Since beginValueExpr, endValueExpr, and incrExpr are expressions, they must be evaluated.• The endValueExpr and incrExpr are evaluated before processing the rest of the macro. This means the code within the user’s use of the macro cannot alter the termination condition or the increment; however, it can change the value of the controlVariable.• The functional return value of iterate macro doesn’t matter, and will probably be T.• You can create an intermediate variable named endValue for the endValueExpr. You can create an intermediate variable named incValue for the incrExpr. For 5 bonus points, use gensym to generate the name of those two variables.• The “T” printed at the end of each of these is irrelevant. Yours can print “NIL”, doesn’t matter.

Examples:1. &gt; (iterate i 1 5 1(print (list ‘one i)))(one 1)(one 2)(one 3)(one 4)(one 5)T

2. &gt; (setf n 5)5&gt; (iterate i 1 n 1(print (list ‘two i n))(+= i 1))(two 1 5)(two 3 5)(two 5 5)T

3. &gt; (setf n 5)5&gt; (iterate i 1 n 1(print (list ‘three i n))(+= n 1))(three 1 5)(three 2 6)(three 3 7)(three 4 8)(three 5 9)T4. &gt; (setf n 5)5&gt; (setf inc 2)2&gt; (iterate i 1 n inc(print (list ‘three i n inc))(+= inc 1))(three 1 5 2)(three 3 5 3)(three 5 5 4)T

Test cases:




;; test +=(setf x 10)(+= x 5)(print x)




;; iterate(iterate i 1 5 1(print (list ‘one i) ))




(setf n 5)

(iterate i 1 n 1(print (list ‘two i n))(+= i 1))




(setf n 5)

(iterate i 1 n 1(print (list ‘three i n))(+= n 1))




(setf n 5)(setf inc 2)

(iterate i 1 n inc(print (list ‘three i n inc))(+= inc 1))

(setf n 5)(setf inc 2)(iterate i 1 (+ n 2) inc(print (list ‘four i n inc))(+= n 1)(+= i 1)(+= inc 1))


