---
layout: page
title: week3
tags: Programming_Languages
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

<!--more-->

**week 3**

## 1. Building Compound Types

Types: base types, compound types

*Three ways to create a compound type :*

- Each-of : int * bool contains an int and a bool
- One-of : int option contains an int or it contains no data
- Self-reference : int list contains an int and another int list or it contains no data

## 2. Records

Order of records doesn't matter

Records & Tuples : by name or by position, tuple is actually record

## 3. Tuples as Syntactic Sugar

**Syntax sugar is a great way to keep the key ideas in a programming-language small (making it easier to implement) while giving prorgammers convenient ways to write things.**

## 4. Datatype Bindings

A way to make one-of types

```
datatype mytype = TwoInts of int * int
									| Str of string
       						| Pizza
```

TwoInts is a function of type int*int -> mytype

Str is a function of type string -> mytype

pizza is a value

**Two aspects to think about: **

1. check what variant it is (what constructor made it (isStr))
2. Extract the data (getStrData)

## 5. Case Expressions

access datatype

```
fun f (x : mytype) =
    case x of
				Pizza => 3
      | Str s => 8
      | TwoInts(i1, i2) => i1+i2;
```

- Pattern matching
- Extracts data and binds to variables local to that branch
- Type-checking: all branches must have same type
- Evaluation: Evaluate between case ... of and the right branch

Pros of case: you can not forget any type or redefine twice.

## 6. Useful Datatypes

- Enumerations, including carrying other data
- Alternate ways of identifying real-world things

```
datatype exp = Constant of int
	     | Negate of exp
	     | Add of exp * exp
	     | Multiply of exp * exp;

fun eval e =
    case e of
	Constant i => i
      | Negate i  => ~ (eval i)
      | Add(e1, e2) => (eval e1) + (eval e2)
      | Multiply(e1, e2) => (eval e1) * (eval e2);
```

choose carefully between one-of and each-of

## 8. Type Synonyms

### datatype 

datatype create a new type distinct from all existing types

### type

- type synonym just create another name for a type
- the type and the name are interchangeable 

## 9. Lists and Options are Datatypes

## 10. Polymorphic Datatypes

```
datatype ('a, 'b) tree = Node of 'a * ('a, 'b) tree * ('a, 'b) tree
												| Leaf of 'b
```

## 11. Each of Pattern Matching / Truth about Functions

- In ML, every function takes exactly one argument

## 12. Type Inference

This version needs an explicit type on the argument:

```
fun sum_triple (triple : int * int * int) = #1 triple + #2 triple + #3 triple
```

## 13. Polymorphic and Equality Types

A type like ''a can only have an equality type substituted for it

```
fun same_thing(x,y) = if x=y then "yes" else "no" (* has type ’’a * ’’a -> string *)
```

## 14. Nested Patterns

```
fun len xs = 
		case xs of 
				[] => 0
			|	x::xs' => 1 + len xs'
```

## 15. Exceptions

just like **datatype**

````
exception myexception => 3
````

Catch exception

```
exception MyUndesirableCondition;

fun maxlist (xs, ex) = (* int list * exn -> int *)
    case xs of
	[] => raise ex
      | x::[] => x
      | x::xs' => Int.max(x, maxlist(xs', ex));
      
val z = maxlist ([], MyUndesirableCondition)
		handle MyUndesirableCondition => 42
```

## 16. Tail Recursion

### Call stacks

While a program runs, there is a **call stack** of function calls that have started but not yet returned

- calling a function *f* pushes an instance of *f* on the stack
- when a call to *f* finished, it is popped from the stack

These stack-frames store information like the value of local variables and "what is left to do" in the function

tail recursion means there is nothing to do after the call is done (no other computing)

```
fun rev xs =
    let fun aux(xs, acc) =
	    if xs = []
	    then acc
	    else
          let
              val x = hd xs
              val xs' = tl xs
          in
              aux(xs', x::acc)
          end
    in
			aux(xs, [])
    end;	
```













