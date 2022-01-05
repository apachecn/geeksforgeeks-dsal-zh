# Java 中的猜数字游戏

> 原文:[https://www.geeksforgeeks.org/number-guessing-game-in-java/](https://www.geeksforgeeks.org/number-guessing-game-in-java/)

任务是编写一个 [Java 程序](https://www.geeksforgeeks.org/java/)，其中用户将得到 **K** 的试验来猜测一个随机生成的数字。下面是游戏规则:

*   If the guess number is greater than the actual number, the program will respond with a message that the guess number is higher than the actual number.
*   If the number of guesses is less than the actual number, the program will respond with a message that the number of guesses is less than the actual number.
*   If the guess number is equal to the actual number, or the **k** test is exhausted, the program will end with an appropriate message.

**方法:**下面是步骤:

*   The method is to use [*math. random () method*](https://www.geeksforgeeks.org/java-math-random-method-examples/) in Java to generate a random number.
*   Now use a loop to get **k** input from the user, and print whether the number is less than or greater than the actual number for each input.
*   If the user guessed the number correctly in the **k** tryouts, the printing user won.
*   Otherwise, print what he can't guess and then print the actual numbers.

下面是上述方法的实现:

## 【爪哇】

```
// Java program for the above approach
import java.util.Scanner;

public class GFG {

    // Function that implements the
    // number guessing game
    public static void
    guessingNumberGame()
    {
        // Scanner Class
        Scanner sc = new Scanner(System.in);

        // Generate the numbers
        int number = 1 + (int)(100
                               * Math.random());

        // Given K trials
        int K = 5;

        int i, guess;

        System.out.println(
            "A number is chosen"
            + " between 1 to 100."
            + "Guess the number"
            + " within 5 trials.");

        // Iterate over K Trials
        for (i = 0; i < K; i++) {

            System.out.println(
                "Guess the number:");

            // Take input for guessing
            guess = sc.nextInt();

            // If the number is guessed
            if (number == guess) {
                System.out.println(
                    "Congratulations!"
                    + " You guessed the number.");
                break;
            }
            else if (number > guess
                     && i != K - 1) {
                System.out.println(
                    "The number is "
                    + "greater than " + guess);
            }
            else if (number < guess
                     && i != K - 1) {
                System.out.println(
                    "The number is"
                    + " less than " + guess);
            }
        }

        if (i == K) {
            System.out.println(
                "You have exhausted"
                + " K trials.");

            System.out.println(
                "The number was " + number);
        }
    }

    // Driver Code
    public static void
    main(String arg[])
    {

        // Function Call
        guessingNumberGame();
    }
}
```