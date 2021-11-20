# CNG - Countdown Numbers Game
How to solve the countdown numbers game!
I have developed an ability to solve most numbers of the countdown numbers game (even the ones that don't follow the rules - Смотрю на тебя, бабушка)

Most of the time, I simply read the question and my brain provides an answer.
If not, this is what I do.

Algorithm
---------

This is a calculation strategy that is called reverse Polish notation (RPN).
Doing maths in a  way doesn't need parenthesis. You build up a stack of values
and operations like this:

    5 + 4 * 2

The `+` adds the `5` and `4` and leaves a `9` on the stack:

    9 * 2

So now the `9` and `2` are multiplied which leaves:

    18

This is useful because it is an easy way to express these mathematical
operations just in an array of values and operations. If the number of possible
values are limited you know the maximum size of the array in advance:

    number_of_values * 2 - 1

However, since we don't just want to calculate an expression using RPN, but
want to actually remember what the expression was so we can know it if it
matches the target we don't pop off anything from the operation stack when
pushing on operations. Instead we track the calculated intermediate values
on a separate stack. We need a separate stack for that since we don't know
where on the operation stack the operations before the current one end without
searching through it in reverse.

So now the search for a solution just works as follows:

* call [solve numbers](#solve-numbers)

### Solve Numbers

* for all unused numbers
  * pop the number on the operation and value stacks
  * call [check solution](#check-solution)
  * call [solve operations](#solve-operations)
  * call [solve numbers](#solve-numbers)
  * pop the number from the operations and value stack

### Check Solution

* if only one value is on the value stack and it is the target
  * print the operations stack

### Solve Operations

* if more than one values are on the value stack:
  * for all operations
    * push the operation on the operation stack
    * push the result of the operation on the value stack
    * call [check solution](#check-solution)
    * call [solve operations](#solve-operations)
    * call [solve numbers](#solve-numbers)
    * pop the operation from operation stack
    * pop the value from the value stack



Hope it helps you :)

Btw, the reason I can do it so fast is because I have [Hypercalculia](https://en.wikipedia.org/wiki/Hypercalculia)
