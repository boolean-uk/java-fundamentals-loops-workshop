# Java Loops

## Learning Objectives
- Understand how to use For Loops to repeat code a specific number of times
- Understand how to use For Loops to iterate over Arrays and other similar structures
- Understand how to use While Loops to loop until a given situation occurs
- Understand how Do/While and While loops differ in their behaviour
- Understand when and why infinite loops can occur and why this is sometimes a good thing

## Definite Loops - Counted

For loops allow your code to run a specific number of times before moving on. The basic code for a for loop looks like this:

```java
public void outputNumbers() {
    for (int i = 0; i < 10; i++) {
        System.out.println(i);
    }
}
```
This will output the numbers from 0 to 9. We can name the loop variable anything but common names are `i`, `x` or `n` all of which probably come from their use for similar activities in Maths.

The variable `i` is limited in scope if you try and access the value of it after the loop exits then you will get an error.

```java
public void outputNumbers() {
    for (int i = 0; i < 10; i++) {
        System.out.println(i);
    }
    System.out.println(i);
}
```

Will cause an error.

We can however do all sorts of things inside the loop. For instance if we wanted to output the even or odd numbers we could do this:

```java
public void outputEvenNumbers() {
    for (int i = 0; i < 10; i++) {
        if (i % 2 == 0) {
            System.out.println(i);
        }
    }
}

public void outputOddNumbers() {
    for (int i = 0; i < 10; i++) {
        if (i % 2 == 1) {
            System.out.println(i);
        }
    }
}
```

An alternative to the first one, is to start at 0 and then go up 2 each time.

```java
public void outputEvenNumbersAlternative() {
    for (int i = 0; i < 10; i = i + 2) {
        System.out.println(i);
    }
}
```

## Activity

- Make a function that will take in an integer as an argument and then output the times table associated with that number from 1 x the number up to 12 x the number in a nice format.
- Make another version of the function which will take two numbers as arguments, the first being the times table to output, the second the value up to which the times table should run.

## Definite Loops -  Iterate over a Collection

We can use loops to build Arrays as long as we know how big we're going to want the array to be in advance (later on we'll cover a dynamic version of an Array) for instance if we wanted to put the even numbers from 4 to 16 inclusive, into an Array we could do the following:

```java
public int[] evenNumeberedArray() {
    int[] evenNumbers = new int[7];
    for (int i = 0; i < 7; i++) {
        evenNumbers[i] = (i * 2) + 4;
    }
    return evenNumbers;
}
```

But we could equally use a `for` loop to iterate through an Array to get to its contents one at a time. This use of a for loop is very common, and works as long as we aren't going to be modifying the value at that position in the Array. The code for doing this could be in the main() method of the Main class and in this case takes the values from the Array which is returned by the evenNumberedArray method.

```java
package com.booleanuk;

public class Main {
    public static void main(String[] args) {
        Counter counter = new Counter();

        int[] myArray = counter.evenNumeberedArray();
        for (int item : myArray) {
            System.out.println(item);
        }
    }
}
```

We create a new variable called `item` in the loop, which gets the next value from the Array on each iteration until we reach the end of the Array.

If we wanted to do the same thing but modify the values as we went (we'll add 1 to the value and store it back into the Array here) then we would actually need access to the index of each item, so instead of using the above pattern we'd need to use something like the following:

```java
package com.booleanuk;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        Counter counter = new Counter();

        int[] myArray = counter.evenNumeberedArray();
        System.out.println("Array before modification: " + Arrays.toString(myArray));
        for (int i = 0; i < myArray.length; i++) {
            myArray[i] = myArray[i] + 1;
        }
        System.out.println("Array after modification: " + Arrays.toString(myArray));
    }
}
```

If we need to exit a loop early then we can use the `break` keyword. For instance if we wanted to check through all of the values in an Array using a loop and then exit if we found it we could do something like:

```java
public boolean checkForName(String theName, String[] names) {
    boolean nameFound = false;
    for (String name : names) {
        if (name.equals(theName)) {
            nameFound = true;
            break;
        }
    }
    return nameFound;
}
```

We could also achieve the same outcome in a variety of other ways, too.

## Activity

- Create a method that will take an integer Array as an argument and return the mean of the numbers (as a float or a double) in the Array.
- Create a method that will take a String Array as an argument and return the mean length of the Strings in the Array.
- Create a method that will take a String Array as an argument, which contains a poem. The first element of the Array is the title of the poem, the second element is the author's name and the rest of the Array contains the lines of the poem. The method should output a nicely formatted version of the poem which has look something like:
```
 Poem Title by Poet's Name
 =========================
 First line of poem
 Second line of poem etc
 ...
```

## Indefinite Loops

Sometimes we don't know how many times a loop will run, but we need it to run until some specific criteria is met.

- Loop until the inbox is empty.
- Loop until the maximum score is achieved

etc.

This is where an indefinite loop comes in. The most common type of indefinite loop is the `while` loop, it looks similar in some ways to an `if` statement, but this time, the contents of the `while` loop will run repeatedly until the condition is no longer true. We could build a simple Chat Bot as an example:

```java
public void simpleChatBot() {
    Scanner input = new Scanner(System.in);
    String userInput = "";
    while (!userInput.equals("q")) {
        System.out.println("Interesting, tell me more.");
        userInput = input.nextLine();
        userInput = userInput.toLowerCase();
    }
    System.out.println("Bye");
}
```

Things to note the loop does not actually exit until the test evaluates to false, so the whole rest of the loop will be run before the test is checked again and the loop exits, if we needed to exit earlier, then we would need to use a `break` to exit from the loop at that earlier point.

## Activity

Make the chatbot better by asking for the user's name and storing it for later use, also add in functionality to make the chatbot respond with one of a random selection of response strings which can be stored in an Array and chosen at random. You may need to look up how random numbers work in Java.

## Indefinite Loops - Variations

With a while loop, sometimes you may find that the loop never runs, as the test happens but fails immediately, occasionally we need a loop which is guaranteed to run at least once and then behave in the same way as a `while` loop does. This is where the `do`-`while` loop comes in.

```java
public void doItWhile() {
    int i = 100;
    do {
        System.out.println(i);
        i++;
    } while (i < 10);
}
```

If you have a `while` loop or a `do`-`while` loop in your code and you don't modify the variable that is being tested in the loop, then sometimes you may end up with an infinite loop. This is often not what you might want, but it might be.

## Infinite Loops 

In a game or an interactive system there is often some form of loop that runs effectively for ever. In reality there needs to be some way of exiting the loop (although this may only happen when the program itself exits). Even if you don't intend to exit the loop using a break statement, Java may refuse to allow you to run the program you create if you don't provide it with the opportunity to exit from an infinite loop. A modified version of our chat bot using an infinite loop might look like this:

```java
public void couldBeInfinite() {
    Scanner input = new Scanner(System.in);
    String userInput = "";
    while (true) {
        System.out.println("Interesting, tell me more.");
        userInput = input.nextLine();
        if (userInput.toLowerCase().equals("q")) {
            break;
        }
    }
    System.out.println("Bye");
}
```

## Activity

Build a menu system that allows the user to choose between three activities and quitting the menu. Use an infinite loop to do this.


## Set up instructions
- Fork this repository and clone the forked version to your machine
- Open the root directory of the project in IntelliJ
- Implement the requirements listed in comments in the `./src/main/java/com.booleanuk/core/Exercise.java` file
- When ready to test your solution, open the `./src/test/java/com.booleanuk/core/ExerciseTest.java` file and click a "Run Test" button. You can either run the entire test suite via figure 1 in the screenshot below, or run a specific test via figure 2.

![](./assets/run-a-test.PNG)

## Test Output

When you run a test, it's either going to pass or fail. When it fails, you'll be presented with a big red stream of text. This is called a stack trace and, though intimidating, does contain some useful information.

One of the core skills of a developer is debugging stack traces like this. The stack trace details in which classes & files the failure happened, and gives you a line number at the end. Most of the lines in the stack trace are irrelevant most of the time, you want to try and identify the files that you're actually working with.

In the sample screenshot below, we've tried to complete the first step of the exercise but provided an invalid value. Then we run the test associated with it and we see a big red stack trace, a test failure.

At the top, we see `expected: <32> but was: <33>`. This means the test expected the value to be 32, but the value the student provided was 33. We can see this in the code snippets at the top of the screenshot.

In the stack trace itself, we see this line: `at app//com.booleanuk.core.ExerciseTest.shouldBeAged32(ExerciseTest.java:20)`. This is helpful! This tells us the exact line in the ExerciseTest.java file (line 20) where the failure happened, as well as the method name (shouldBeAged32), helping us to identify where the issue began. This is the kind of thing you need to look for; a relevant file name, method name, class name and line number to give you a good starting point for debugging.

![](./assets/test-failure.PNG)
