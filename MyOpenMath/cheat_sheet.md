# Cheat Sheet for MOM

## Variables
$var = number. Example: $a = 3
$var = calculation. Example: $a = 3*$b*$c
$var = function. Example: $a = showplot("sin(x)")
$var = randomizer. Example: $a = rand(-5,5)

A number: $a = 15. A calculation like $a = 3^2 will also result in a number
An array: $a = array(6,8,10). This is a collection of variables. You can reference the parts using an index (note that arrays are zero-indexed), so $a[0] = 6.
A string: $a = "hi there".
Boolean: $a = true

## Conditionals
Any assignment line can be followed by one of two conditional: "where" or "if".

"where" is used to repeat the previous assignment if the condition provided is not met. The "where" condition is almost exclusively used with array randomizers. Example: to select two different numbers that are not opposites:

$a,$b = diffrands(-5,5,2) where ($a+$b!=0)
"if" is used to make an assignment conditional. For example:

$a = rand(0,1)
$b = "sin(x)" if ($a==0)
$b = "cos(x)" if ($a==1)
Note the use of double equal signs (==) for testing equality. A single equal sign (=) will make an assignment (change the value of $a in this example) and return "true", which is probably not what you intended to do.

### Examples of Conditionals
To do compound conditionals, use || for "or", and && for "and". For example:

$a = nonzerorand(-9,9) where ($a!=1 && $a!=-1)
The "if" condition can also be used before or after a code block like this:

$a = rand(0,1)
if ($a==0) {
   $b = 1
   $c = 2
}
or

$a = rand(0,1)
{
   $b = 1
   $c = 2
} if ($a==0)
When "if" is used before a block of code, it can optionally be followed with "elseif" and/or an "else" statement, like this:

$a = rand(0,5)
if ($a==0) {
   $b = 1
} elseif ($a==2) {
   $b = 3
} else {
   $b = 2
}
"where" can also be applied to a block of code:

{
  $a = rand(-5,-1)
  $b = rand(1,5)
} where ($a+$b !==0)

## Loops
There are several looping macros (such as calconarray) that can meet most needs. For more general use there is a "for" loop:

for ($i=a..b) { action }
Here a and b represent whole numbers or variables. Expressions are not allowed.

Examples:

$f = 0
for ($i=1..5) { $f = $f + $i }

$a = rands(1,5,5)
$b = rands(1,5,5)
for ($i=0..4) {
  $c[$i] = $a[$i]*$b[$i]
}
Conditions can be used inside a for loop, but not outside without explicit blocking

for ($i=1..5) {$a = $a+$i if ($i>2) }     WORKS
for ($i=1..5) {$a = $a+$i} if ($a>2)     DOES NOT WORK
{for ($i=1..5) {$a = $a+$i} } if ($a>2)    WORKS

## Randomizers
Note on macros: The descriptions below explain macros available and the arguments the functions should be called with. Arguments in [square brackets] are optional arguments, and can be omitted.

For all randomizers, all bounds (min,max) are inclusive.

### Single result randomizers:

rand(min,max): Returns an integer between min and max
rrand(min,max,p): Returns a number between min and max in steps of p.
nonzerorand(min,max): Returns a nonzero integer between min and max
nonzerorrand(min,max,p): Returns a nonzero real number between min and max in steps of p
randfrom(list or array): Return an element of the list/array.
randname(),randmalename(),randfemalename(): Returns a random first name
randnamewpronouns([option]): Returns a random first name with pronouns in the order: subjective, objective, possessive (singular), possessive (plural), reflexive. Can set option to 'neutral' for they/them/their/theirs/themself pronouns. Use: $name,$heshe,$himher,$hisher,$hishers,$himherself = randnamewpronouns()

#### Examples of Single result Randomizers:
* Example: rrand(2,5,.1) might return 3.4. rrand(2,5,.01) might return 3.27. rrand(2,8,2) might return 6
* Examples of lists: "2,4,6,8", or "red,green,blue"

### Array Randomizers
* rands(min,max,n,[order]): Returns n integers between min and max. Can set order to 'inc' or 'dec' to sort the values.
* rrands(min,max,p,n,[order]): Returns n real numbers between min and max in steps of p. Can set order to 'inc' or 'dec' to sort the values.
* nonzerorands(min,max,n,[order]): Returns n nonzero integers between min and max. Can set order to 'inc' or 'dec' to sort the values.
* nonzerorrands(min,max,p,n,[order]): Returns n nonzero real numbers between min and max in steps of p. Can set order to 'inc' or 'dec' to sort the values.
* randsfrom(list/array,n,[order]): Return n elements of the list/array. Can set order to 'inc' or 'dec' to sort the values.
* jointrandfrom(list/array,list/array,[list/array,...]): Returns one element from each list, where the location used in each list is the same
* diffrands(min,max,n,[order]): Returns n different integers between min and max. Can set order to 'inc' or 'dec' to sort the values.
* diffrrands(min,max,p,n,[order]): Returns n different real numbers between min and max in steps of p. Can set order to 'inc' or 'dec' to sort the values.
* diffrandsfrom(list/array,n,[order]): Return n different elements of the list/array. Can set order to 'inc' or 'dec' to sort the values.
* nonzerodiffrands(min,max,n,[order]): Returns n different nonzero integers between min and max. Can set order to 'inc' or 'dec' to sort the values.
* nonzerodiffrrands(min,max,p,n,[order]): Returns n different nonzero real numbers between min and max in steps of p. Can set order to 'inc' or 'dec' to sort the values.
* jointshuffle(list/array1,list/array2,[n1,n2]): Shuffles two lists/arrays in a way that retains respective order. In n1 is provided, n1 elements from each shuffled array  will be returned (like a joint version of diffrandsfrom). If n2 is also provided, n1 elements of list/array1 and n2 elements of list/array2 will be returned.
* singleshuffle(list/array,[n]): returns a shuffled version of a list/array. If n is provided, it behaves identically to diffrandsfrom
* randnames(n),randmalenames(n),randfemalenames(n): Returns n random first names
* randcity([country]),randcities(n, [country]): Returns one or n random US or Canadian city names. Argument country can be set to "USA" or "Canada". The default is "USA".
* randstate([country]),randstates(n, [country]): Returns one or n random US state or Canadian province names. Argument country can be set to "USA" or "Canada". The default is "USA".
* randcountry(),randcountries(n): Returns one or n random country names
* randpythag([min,max]): Return a Pythagorean triple. min/max default to 1 to 100

#### Examples of Array Randomizers
