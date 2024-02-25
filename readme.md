# MAD - Exercise 01
## Tasks
* Watch the Kotlin Crashcourse Video in Moodle or complete the tutorials **[Introduction to programming in Kotlin](https://developer.android.com/courses/pathways/android-basics-compose-unit-1-pathway-1)** and **[Kotlin fundamentals](https://developer.android.com/courses/pathways/android-basics-compose-unit-2-pathway-1
)**.
* Answer the questions inside this Readme.md file and push it to your repository.
* Submit your coding solution of the Number Guessing Game inside the repository.
* Submit the link to your repository in Moodle.

## Questions
### Describe how Kotlin handles null safety. What are nullable types and non-null types in Kotlin? (0,5 points)

### Answer:
> 
> Kotlin's type system distinguishes between references that can or cannot hold 'null' as a value
> --> nullable and non-nullable types.
> 
> By default, every declared variable is non-nullable.
> If a variable should be able to hold 'null', it must be declared with a '?'.
> 

```kotlin
val a: String = "non-nullable" // declared as a default non-null type
a = null // will result in a compilation error
val b: String? = "nullable" // declared as a potential null-holder
b = null // ok
```

### What are lambda expressions and higher order functions in Kotlin? Why would you store a function inside a variable? (0,5 points)

### Answer:

> Lambda expressions are essentially anonymous functions, as they don't have a name unless assigned to a variable.
> They are generally more concise than regular functions, making them ideal for short operations or passing functions as arguments.
>
> I can store a function in a variable to pass it around as a parameter, to delay its execution, or to compose complex operations from simpler ones.
```kotlin
// Lambda expressions to perform two (short) mathematical operations
val isOdd: (Int) -> Boolean = { it % 2 != 0 }
val add: (Int, Int) -> Int = { a, b -> a * b }
```

> Higher-order functions take functions as parameters, or return a function.

```kotlin
// Higher-Order function that takes previous lambdas as parameters to perform their functionality on 'numbers'
fun processNumbers(
    numbers: List<Int>,
    predicate: (Int) -> Boolean,
    transform: (Int, Int) -> Int
): Int {
    return numbers.filter(predicate).map(transform).sum()
}

// Now we can combine both concepts
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    val result = processNumbers(numbers, isOdd, add)
    println("The sum of the odd numbers is: $result")
}
```




### Provide a solution for the following number guessing game inside `App.kt`. (3 points)

## Number Guessing Game in Kotlin
The game is a simple number guessing game. The task is to generate a random, max 9-digit, number. The number must **not contain repeating digits**. Valid digits are 1-9.
Ask the user to guess the max 9-digit number. The game is finished when the user guesses the correct digits in the correct order.
In each round, the user gets feedback about the number of correct digits and the number of correct digits in the correct position.
The output should be in the format "n:m", where "n" is the number of digits guessed correctly regardless of their position, 
and "m" is the number of digits guessed correctly at their correct position. Here are some examples:

This example shows the game flow with 4-digits to guess (the default argument)

Generated number: 8576
-	User input: 1234, Output: 0:0
-	User input: 5678, Output: 4:1
-	User input: 5555, Output: 1:1
-	User input: 3586, Output: 3:2
-	User input: 8576, Output: 4:4 -> user wins

Take a look into the provided code structure in `src/main/kotlin/App.kt`. Implement the following methods (lambda expressions):
- _playNumberGame(digitsToGuess: Int = 4)_ (1 point): The main game loop that handles user input and game state. Make use of _generateRandomNonRepeatingNumber_ and _checkUserInputAgainstGeneratedNumber_ here. This function also utilizes a default argument 
- _generateRandomNonRepeatingNumber_ (1 point): A lambda expression that generates a random number with non-repeating digits of a specified length.
- _checkUserInputAgainstGeneratedNumber_ (1 point): A lambda expression that compares the user's input against the generated number and provides feedback.

``CompareResult.kt`` This class is a data structure which helps with bundling the result of the comparison of the user input and the generated number. Look at the toSting() and use it in your output.

Run the project with `./gradlew run` and test your implementation with the provided tests in `src/test/kotlin/AppTest.kt` with `./gradlew test`.

# Project Structure
The project is structured into two main Kotlin files:

**App.kt**: Contains the main game logic and functions.

**AppTest.kt**: Contains unit tests for the various functions in App.kt.

