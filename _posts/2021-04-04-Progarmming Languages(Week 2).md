---
layout: page
title: Programming_Languages
tags: Programming_Languages
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

<!--more-->


**week 2**

## 1. ML Variable Bindings and Expressions

using Emacs

- Creating/finding files: ```C-x C-f```
- saving files: ```C-x C-s```
- exporting files: ```C-x C-w```
- running files: ```C-c C-s```

### Bindings

```val x = 34;```

*dynamic environment : bindings we have when running a program*

*static environment : type*

when running a program, firstly check static environment then check dynamic environment

#### The sematics

*Syntax* is just how you write something

*Sematics* is what that something means

- Type-checking (before program runs) **static environment**
- Evaluation (as program runs) **dynamic environment**

 ## 2. Rules for Expressions

### Expressions

Every kind of expression has

1. Syntax
2. Type-checking rules : may lead to type error
3. Evaluation rules : produce a value after type-check

#### Different expressions:

- Variables: variable is the simplest expression

- Additions:
  - Syntax: e1+e2 where e1 and e2 are expressions
  - Type-checking: if e1 and e2 have type int, then e1 + e2 has type int.
  - Evaluation: if e1 evaluates to v1 and e2 evaluates to e2, then e1 + e2 evaluates to sum of v1 and v2.
- Values: all values are expressions, not all expressions are values, every value evaluate to itself in 0 step

#### Try myself

Syntax: e1 * e2

Type-check: e1 and e2 must have the same type like int or float

Evaluation: first evaluate e1 to a value v1, then evaluate e2 to a value v2, the whole expression's result will be the multiplication of v1 and v2

## 3. The REPL and Errors

### Pragmatics

- How do we run programs using the REPL?
- What happens when we make mistakes?

### REPL

- Read-Eval-Print-Loop
- remember to stop the REPL usint ``C+d``

### Errors

mistakes could be

- Syntax: the program you wrote doesn't match what you thought or variable names conflicts with keyword names
- Type-checking: What you wrote does not type-check
- Evaluation: It runs but produces wrong answer, or an exception, or an infinite loop

**in ML language, ~(tilde) means minus, div stands for /**

## 4. Shadowing

Definition: shadowing is when you add a variable into an environment when before it, that variable was already in the environment.

### Multiple bindings of some variable

1. Expressions in varibale bindings are evaluated "eagerly"
   - Before the variable binding "finishes"
   - Afterwards, the expression producing the value is irrelevant
2. There's no way to "assign to" a variable in ML
   - Can only shodow it in a later environment

## 5. Functions

```m
fun pow(x: int, y: int) =
    if y=0
    then 1
    else x * pow(x,y-1)
```

**A function is a value.**

### Function Calls

Syntax: check if the syntax is correct

Type-checking: 

- if e0 has type (t1 * t2 .. * tn) -> t and arguments all have their corresponding types,
- then, e0(e1, e2, ..., en) has type t

*Example: pow(x, y)* pow has type (int * int -> int), x has type int, y has type int, so pow(x,y) has type int.

Evaluation:

``e0(e1,...,en)``

1. (Under current dynamic environment) evaluate e0 to a function
2. (Under current dynamic environment) evaluate arguments to values
3. result is the evaluation of e

##  6. Pairs and other Tuples

use #x to get the xth value of the pair 

There is nesting in pairs:``val x1 = (7, (true, 9))``

## 7. Lists

different from tuple, list 

- Can have any number of elements
- but all list elements have the same type

**three ways to build lists**:

1. ``[]`` empty list
2. ``[1,2,3]`` simple list
3. ```x = [1,2,3]; 6::x; -> [6,1,2,3]``` "cons": connecting lists

**Access lists: **

1. ``null x;`` check if x is null, return bool
2. ``hd x;`` return the first element of the list
3. ``tl x;`` return the list without the first element

**type check:**

1. it's ok to nest but the elements of the list should have the same type

2. null is actually a function: ``'a list -> bool``
3. hd is a function: ``'a list ->  'a``

4. tl is a function: ``'a list -> 'a list``

## 8. List Functions

some functions that take lists as arguments or as results

functions over lists are usually recursive: only way to "get to all the elements"

- What should the answer be for the empty list?
- what should the answer be for a non-empty list?
  - typically in terms of the answer for the tail of the list

function that produces any lists is also recursive

- you create a list out of smaller lists

## 9. Let Expresssions

**Syntax:**

```
let
	xxx
in
	xxx
end
```

let creates inner environment and local variables

**type-checking:**

nothing new

**evaluation:**

Evalutate local variable first then outer levels

## 10. Nested Functions

define functions inside functions

**nested functions** is a good style to define helper functions it they are:

- Unlikely to be useful elsewhere
- likely to be misused elsewhere
- likely to be changed

*reusing code saves effort and acoids bugs,  but makes the reused code harder to change later*

## 11. Let and Efficiency

use let expressions to avoid repeated computation

```
fun bad_max (xs: int list) =
    if null xs
    then 0
    else if null (tl xs)
    then hd xs
    else if hd xs > bad_max(tl xs)
    then hd xs
    else bad_max(tl xs)
		
fun good_max (xs: int list) =
    if null xs
    then 0
    else if null (tl xs)
    then hd xs
    else
	let val tmp = good_max(tl xs)
	in
	    if hd xs > tmp
	    then hd xs
	    else tmp
	end
```

## 12. Options

an option value has either 0 or 1 thing

- NONE is a option value carrying nothing

- SOME e turns type **t** to **t option**

- isSome evaluates to false if its argument is NONE
- valOf gets the value of the argument and raise an exception for NONE

```
fun better_max (xs: int list) =  (* fn: int list -> int option *)
    if null xs
    then NONE
    else
	let val tmp = better_max(tl xs)
	in
	    if isSome tmp andalso valOf tmp > hd xs
	    then tmp
	    else SOME(hd xs)
	end
```

*too many times changing between option and normal values*

```
fun better_max2 (xs : int list) =
    if null xs
    then NONE
    else
	let
	    fun maxNonEmpty(ys : int list) =
		if null (tl ys)
		then hd ys
		else
		    let val tmp = maxNonEmpty(tl ys)
		    in
			if hd ys > tmp
			then hd ys
			else
			    tmp
		    end
	in
	    SOME(maxNonEmpty(xs))
	end
```

## 13. Booleans and Comparison Operations

```
e1 andalso e2
e1 orelse e2
not e1
```

Type-checking: e1 and e2 must have type bool

Evaluation: in the first line, if e1 is evaluated false, e2 is not going to be evaluated.

**andaslo and orelse are not functions, not is**

## 14. Benefits of No Mutation

there's no mutation in ML language, which means that once create a variable, it will not be changed.

this is the feature of functional programming.

ML makes alias instead of copy

## 15. Pieces of a Language

1. Syntax
2. Sematics: Evaluation Rules
3. Idioms
4. Libraries: file access, data structures
5. Tools: REPL, debugger (Not part of the language)























