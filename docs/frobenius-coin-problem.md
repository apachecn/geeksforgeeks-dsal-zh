# 弗罗贝尼乌斯硬币问题

> 原文:[https://www.geeksforgeeks.org/frobenius-coin-problem/](https://www.geeksforgeeks.org/frobenius-coin-problem/)

分别给定面值为“X”和“Y”的两枚硬币，找出使用这两枚硬币无法获得的最大金额(假设硬币无限供应)，然后是此类无法获得的金额的总数，如果不存在此类价值，则打印“NA”。

**示例:**

```
Input : X=2, Y=5  
Output: Largest amount = 3
        Total count  = 2
We cannot represent 1 and 3 from infinite supply
of given two coins. The largest among these 2 is 3.
We can represent all other amounts for example 13
can be represented 2*4 + 5.

Input : X=5, Y=10
Output: NA
There are infinite number of amounts that cannot
be represented by these two coins.

```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/frobenius-coin-problem5532/1)

一个重要的观察是，如果 X 和 Y 的 GCD 不是一，那么给定两个硬币能形成的所有值都是 GCD 的倍数。例如，如果 X = 4，Y = 6。那么所有的值都是 2 的倍数。所以所有不是 2 的倍数的值，都不能由 X 和 y 构成，这样就有无限多的值不能由 4 和 6 构成，我们的答案就变成了“NA”。

n 个硬币的一般问题被称为经典的福本纽斯硬币问题。

```
When the number of coins is two, there is 
explicit formula if GCD is not 1\. The formula
is:
  Largest amount A = (X * Y) - (X + Y)
  Total amount = (X -1) * (Y - 1) /2 

```

因此，我们现在可以通过以下步骤轻松回答上述问题:

1.  计算 X 和 Y 的 GCD
2.  如果 GCD 为 1，则所需的最大金额为(X*Y)-(X+Y)，总计数为(X-1)*(Y-1)/2
3.  Else print “NA”

    下面是一个基于相同的程序。

    ## C++

    ```
    // C++ program to find the largest number that
    // cannot be formed from given two coins
    #include <bits/stdc++.h>
    using namespace std;

    // Utility function to find gcd
    int gcd(int a, int b)
    {
        int c;
        while (a != 0)
        {
            c = a;
            a = b%a;
            b = c;
        }
        return b;
    }

    // Function to print the desired output
    void forbenius(int X,int Y)
    {
        // Solution doesn't exist 
        // if GCD is not 1
        if (gcd(X,Y) != 1)
        {
            cout << "NA\n";
            return;
        }

        // Else apply the formula
        int A = (X*Y)-(X+Y);
        int N = (X-1)*(Y-1)/2;

        cout << "Largest Amount = " << A << endl;
        cout << "Total Count = " << N << endl;
    }

    // Driver Code
    int main()
    {
        int X = 2,Y = 5;
        forbenius(X,Y);

        X = 5, Y = 10;
        cout << endl;
        forbenius(X,Y);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to find the largest
    // number that cannot be formed 
    // from given two coins
    import java.io.*;

    class GFG
    {
    // Utility function to find gcd
        static int gcd(int a, int b)
        {
            int c;
            while (a != 0)
            {
                c = a;
                a = b % a;
                b = c;
            }
            return b;
        }

        // Function to print the
        // desired output
        static void forbenius(int X, 
                              int Y)
        {
            // Solution doesn't exist 
            // if GCD is not 1
            if (gcd(X, Y) != 1)
            {
                System.out.println( "NA");
                return;
            }

            // Else apply the formula
            int A = (X * Y) - (X + Y);
            int N = (X - 1) * (Y - 1) / 2;

            System.out.println("Largest Amount = " + A );
            System.out.println("Total Count = " + N );
        }

        // Driver Code
        public static void main(String[] args)
        {
            int X = 2,Y = 5;
            forbenius(X, Y);
            X = 5;
            Y = 10;
            System.out.println();
            forbenius(X, Y);

        }
    }

    // This code is contributed by Sam007
    ```

    ## 蟒蛇 3

    ```
    # Python3 program to find the largest 
    # number that cannot be formed
    # from given two coins

    # Utility function to find gcd
    def gcd(a, b):
        while (a != 0):
            c = a;
            a = b % a;
            b = c;

        return b;

    # Function to print the desired output
    def forbenius(X, Y):

        # Solution doesn't exist 
        # if GCD is not 1
        if (gcd(X, Y) != 1):
            print("NA");
            return;

        # Else apply the formula
        A = (X * Y) - (X + Y);
        N = (X - 1) * (Y - 1) // 2;

        print("Largest Amount =", A);
        print("Total Count =", N);

    # Driver Code
    X = 2; 
    Y = 5;
    forbenius(X, Y);

    X = 5; 
    Y = 10;
    print("");
    forbenius(X, Y);

    # This code is contributed by mits
    ```

    ## C#

    ```
    // C# program to find the largest
    //  number that cannot be formed 
    // from given two coins
    using System;

    class GFG
    {
    // Utility function to find gcd
        static int gcd(int a, int b)
        {
            int c;
            while (a != 0)
            {
                c = a;
                a = b%a;
                b = c;
            }
            return b;
        }

        // Function to print the
        // desired output
        static void forbenius(int X, int Y)
        {
            // Solution doesn't exist 
            // if GCD is not 1
            if (gcd(X,Y) != 1)
            {
                Console.WriteLine( "NA");
                return;
            }

            // Else apply the formula
            int A = (X * Y) - (X + Y);
            int N = (X - 1) * (Y - 1) / 2;

            Console.WriteLine("Largest Amount = " + A );
            Console.WriteLine("Total Count = " + N );
        }

        // Driver Code
        public static void Main()
        {
            int X = 2,Y = 5;
            forbenius(X,Y);
            X = 5;
            Y = 10;
            Console.WriteLine();
            forbenius(X,Y);

        }
    }

    // This code is contributed by Sam007
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php
    // php program to find the largest 
    // number that cannot be formed
    // from given two coins

    // Utility function to find gcd
    function gcd($a, $b)
    {
        $c;
        while ($a != 0)
        {
            $c = $a;
            $a = $b % $a;
            $b = $c;
        }

        return $b;
    }

    // Function to print the desired output
    function forbenius($X, $Y)
    {
        // Solution doesn't exist 
        // if GCD is not 1
        if (gcd($X, $Y) != 1)
        {
            echo "NA\n";
            return;
        }

        // Else apply the formula
        $A = ($X * $Y) - ($X + $Y);
        $N = ($X - 1) * ($Y - 1) / 2;

        echo "Largest Amount = ", $A, "\n";
        echo "Total Count = ", $N, "\n";
    }

    // Driver Code

        $X = 2; $Y = 5;
        forbenius($X, $Y);

        $X = 5; $Y = 10;
        echo "\n";
        forbenius($X, $Y);

    // This code is contributed by ajit.
    ?>
    ```

    **Output :**

    ```
    Largest Amount = 3
    Total Count = 2

    NA

    ```

    **参考资料:**
    [https://en . Wikipedia . org/wiki/corner _ problem](https://en.wikipedia.org/wiki/Coin_problem)

    本文由[阿舒托什·库马尔](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile)供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论