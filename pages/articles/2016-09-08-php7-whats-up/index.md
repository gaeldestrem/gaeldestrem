---
title: PHP 7 - Scalar type and new operators 
date: "2016-09-08"
layout: post
path: "/php7"
category: "php/symfony"
description: "PHP7 is not only about performance improvements. There are a also a few cool new things that came out !"
---

PHP7 is not only about performance improvements. There are a also a few cool new things that came out !

<img src="https://i.giphy.com/3oz8xQQP4ahKiyuxHy.gif" width="500" height="500"/>

## New operators

#### Null Coalesce Operator
PHP 5.6
```
$user = isset($userName) ? $userName : "default_value";
```

PHP7
```
$user = $userName ??  "default_value";
$user = $userName ?:  "default_value";
```

Those two operators are almost the same, you can check the minor differences in this post : http://stackoverflow.com/questions/34571330/php-ternary-operator-vs-null-coalescing-operator

#### Spaceship operator


```
$compareResult = $a <=> $b
 
if $a < $b it returns “-1” to the variable “compareResult”
 
if $a = $b it returns “0” to the variable “compareResult”
 
if $a > $b it returns “1” to the variable “compareResult”
```

It is a very useful operator. The most common use of this operator will be in sorting.

## Scalar type declaration : parameters
 
PHP 7 has now added Scalar type declaration. There are two options available: non-strict (default) and strict.

 
#### Non strict 
As if you pass a string starting with a number into a float type function, it grabs the number from the start and skips everything else. Passing a float into a function that requires an int, that float will become int.

```
function getSum(float $a, float $b) {
   return $a + $b;
}
 
getSum(6, "7 week");
//returns float(13)

getSum(1.1, "2.2");
//returns float(3.3)
 
getSum(3.1, 2);
// returns float(5.1)
```

#### Strict

```
declare(strict_types=1);
function getSum(float $a, float $b) {
    return $a + $b;
}
 
getSum(3, "2 week");
// Fatal error: Uncaught TypeError: Argument 2 passed to getSum() must be of the type float, string given
 
getSum(1.8,  "4.5");
// Fatal error: Uncaught TypeError: Argument 2 passed to getSum() must be of the type float, string given
 
getSum(3.1, 2);
//returns float(5.1)
```

## Scalar type declaration : return type

#### Non strict

```
function getSum(float $a, float $b) : int {
    return $a + $b;
}

getSum(6, "7 week");
// returns int(13);
 
getSum(1.1, "2.2");
// returns int(3)
 
getSum(3.1, 2);
// returns int(5)
```

#### Strict
```
declare(strict_types=1);
 
function getSum(float $a, float $b) : int {
    return $a + $b;
}
 
getSum(3.1, 2); 
// The above statement shows Fatal error: Uncaught TypeError: Return value of getSum() must be of the type integer, float returned
```
