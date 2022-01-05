# 检查 N 是否为同心六边形数的程序

> 原文:[https://www . geesforgeks . org/program-to-check-if-n-is-a-同心圆-六边形-number/](https://www.geeksforgeeks.org/program-to-check-if-n-is-a-concentric-hexagonal-number/)

给定一个整数 **N** ，任务是检查 **N** 是否为[同心六角数字](https://www.geeksforgeeks.org/concentric-hexagonal-numbers/)。如果编号 **N** 是同心六边形编号，则打印**“是”**否则打印**“否”**。

> [同心六边形数字](https://www.geeksforgeeks.org/concentric-hexagonal-numbers/)是用同心六边形构成图案的数字序列，数字表示图案第 N 阶段后所需的点数。前几个同心六边形数字是 0，1，6，13，24，37，54，73，96，121 …

**示例:**

> **输入:** N = 6
> **输出:**是
> **说明:**
> 第三个同心六边形数为 6。
> 
> **输入:**N = 20
> T3】输出:否

**进场:**

1.  同心六边形编号的第**K**项给出为:

    > 第 K 项= (3 * K * K) / 2

2.  因为我们必须检查给定的数是否可以表示为同心六边形数。这可以勾选为:

    > 这里，第 K 项= N
    > =>(3 * K * K)/2 = N
    > =>3 * K * K–2 * N = 0
    > 这个方程的正根是:
    > K = sqrt((2 * N )/3)

3.  如果用上述公式计算的 **K** 的值是一个整数，那么 **N** 就是一个同心六边形数。
4.  Else the number **N** is not a ConcentricHexagonal Number.

    以下是上述方法的实现:

    ## C++

    ```
    // C++ program to check if N is a
    // Concentric Hexagonal Number

    #include <bits/stdc++.h>
    using namespace std;

    // Function to check if the
    // number is a Concentric hexagonal number
    bool isConcentrichexagonal(int N)
    {
        float n = sqrt((2 * N) / 3);

        // Condition to check if the
        // number is a Concentric 
        // hexagonal number
        return (n - (int)n) == 0;
    }

    // Driver Code
    int main()
    {
        int N = 6;

        // Function call
        if (isConcentrichexagonal(N)) {
            cout << "Yes";
        }
        else {
            cout << "No";
        }
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to check if N is a
    // Concentric Hexagonal Number
    class GFG{

    // Function to check if the
    // number is a Concentric hexagonal number
    static boolean isConcentrichexagonal(int N)
    {
        float n = (float) Math.sqrt((2 * N) / 3);

        // Condition to check if the
        // number is a Concentric 
        // hexagonal number
        return (n - (int)n) == 0;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 6;

        // Function call
        if (isConcentrichexagonal(N)) 
        {
            System.out.print("Yes");
        }
        else 
        {
            System.out.print("No");
        }
    }
    }

    // This code is contributed by PrinciRaj1992
    ```

    ## 蟒蛇 3

    ```
    # Python3 program to check if N is a 
    # concentric hexagonal number 
    import math

    # Function to check if the number
    # is a concentric hexagonal number 
    def isConcentrichexagonal(N):

        n = math.sqrt((2 * N) / 3)

        # Condition to check if the 
        # number is a concentric 
        # hexagonal number
        return (n - int(n)) == 0

    # Driver code
    N = 6

    if isConcentrichexagonal(N):
        print("Yes")
    else:
        print("No")

    # This code is contributed by divyeshrabadiya07
    ```

    ## C#

    ```
    // C# program to check if N is a
    // concentric hexagonal number
    using System;

    class GFG{

    // Function to check if the number 
    // is a concentric hexagonal number
    static bool isConcentrichexagonal(int N)
    {
        float n = (float) Math.Sqrt((2 * N) / 3);

        // Condition to check if the
        // number is a concentric 
        // hexagonal number
        return (n - (int)n) == 0;
    }

    // Driver Code
    public static void Main()
    {
        int N = 6;

        // Function call
        if (isConcentrichexagonal(N)) 
        {
            Console.Write("Yes");
        }
        else
        {
            Console.Write("No");
        }
    }
    }

    // This code is contributed by Code_Mech
    ```

    **Output:**

    ```
    Yes

    ```