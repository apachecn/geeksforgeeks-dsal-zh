# 计算一个数的幂的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序计算数的幂/](https://www.geeksforgeeks.org/java-program-to-calculate-power-of-a-number/)

给定一个数 N 和一个幂 P，任务是求这个数上升到给定幂的指数，即 **N <sup>P</sup>** 。

**示例:**

```
Input: N = 5, P = 2
Output: 25

Input: N = 2, P = 5
Output: 32

```

以下是找到 N <sup>P</sup> 的各种方法:

*   **方法一:使用递归**

    ```
    // Java program to find the power of a number
    // using Recursion

    class GFG {

        // Function to calculate N raised to the power P
        static int power(int N, int P)
        {
            if (P == 0)
                return 1;
            else
                return N * power(N, P - 1);
        }

        // Driver code
        public static void main(String[] args)
        {
            int N = 2;
            int P = 3;

            System.out.println(power(N, P));
        }
    }
    ```

    **输出:**

    ```
    8

    ```

*   **方法二:借助 Loop**

    ```
    // Java program to find the power of a number
    // with the help of loop

    class GFG {

        // Function to calculate N raised to the power P
        static int power(int N, int P)
        {
            int pow = 1;
            for (int i = 1; i <= P; i++)
                pow *= N;
            return pow;
        }

        // Driver code
        public static void main(String[] args)
        {
            int N = 2;
            int P = 3;

            System.out.println(power(N, P));
        }
    }
    ```

    **输出:**

    ```
    8

    ```

*   **方法三:使用 [Math.pow()](https://www.geeksforgeeks.org/math-pow-method-in-java-with-example/) 方法**

    ```
    // Java program to find the power of a number
    // using Math.pow() method

    import java.lang.Math;

    class GFG {

        // Function to calculate N raised to the power P
        static double power(int N, int P)
        {
            return Math.pow(N, P);
        }

        // Driver code
        public static void main(String[] args)
        {
            int N = 2;
            int P = 3;

            System.out.println(power(N, P));
        }
    }
    ```

    **输出:**

    ```
    8.0

    ```