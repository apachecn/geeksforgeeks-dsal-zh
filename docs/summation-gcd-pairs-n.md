# 直到 N 的所有对的 GCD 的总和

> 原文:[https://www.geeksforgeeks.org/summation-gcd-pairs-n/](https://www.geeksforgeeks.org/summation-gcd-pairs-n/)

给定一个数 N，求所有 gcd 的和，这些 gcd 可以通过选择从 1 到 N 的所有对来形成。
**示例:**

```
Input  : 4
Output : 7
Explanation: 
Numbers from 1 to 4 are: 1, 2, 3, 4
Result = gcd(1,2) + gcd(1,3) + gcd(1,4) + 
         gcd(2,3) + gcd(2,4) + gcd(3,4)
       = 1 + 1 + 1 + 1 + 2 + 1
       = 7

Input  : 12
Output : 105

Input  : 1
Output : 0

Input  : 2
Output : 1

```

一种天真的方法是运行两个循环，一个在另一个里面。逐个选择所有对，找到每对的 GCD，然后找到这些 GCD 的和。该方法的时间复杂度为 0(N<sup>2</sup>* log(N))

**高效方法**基于以下概念:

*   **[Euler’s Totient function](https://www.geeksforgeeks.org/eulers-totient-function/) ?(n)** for an input n is count of numbers in {1, 2, 3, …, n} that are relatively prime to n, i.e., the numbers whose GCD (Greatest Common Divisor) with n is 1\. For example, ?(4) = 2, ?(3) = 2 and ?(5) = 4\. There are 2 numbers smaller or equal to 4 that are relatively prime to 4, 2 numbers smaller or equal to 3 that are relatively prime to 3\. And 4 numbers smaller than or equal to 5 that are relatively prime to 5.

    其思想是将给定问题转化为欧拉全能函数的和。

    ```
    Sum of all GCDs where j is a part of
    pair is and j is greater element in pair: Sum<sub>j</sub> = ?(i=1 to j-1) gcd(i, j)
    Our final result is 
    Result = ?(j=1 to N) Sum<sub>j</sub>

    The above equation can be written as : Sum<sub>j</sub> = ? g * count(g) 
    For every possible GCD 'g' of j. Here count(g)
    represents count of pairs having GCD equals to
    g. For every such pair(i, j), we can write :
     gcd(i/g, j/g) = 1

    We can re-write our previous equation as
    Sum<sub>j</sub> = ? d * phi(j/d) 
    For every divisor d of j and phi[] is Euler
    Totient number 

    Example : j = 12 and d = 3 is one of divisor 
    of j so in order to calculate the sum of count
    of all pairs having 3 as gcd we can simple write
    it as 
    => 3*phi[12/3]  
    => 3*phi[4]
    => 3*2
    => 6

    Therefore sum of GCDs of all pairs where 12 is 
    greater part of pair and 3 is GCD.
    GCD(3, 12) + GCD(9, 12) = 6.

    Complete Example : 
    N = 4
    Sum1 = 0
    Sum2 = 1 [GCD(1, 2)]
    Sum3 = 2 [GCD(1, 3) + GCD(2, 3)]
    Sum4 = 4 [GCD(1, 4) + GCD(3, 4) + GCD(2, 4)]

    Result = Sum1 + Sum2 + Sum3 + Sum4
           = 0 + 1 + 2 + 4
           = 7

    ```

    以下是上述想法的实现。我们预先计算欧拉全能函数，并得出所有数字的最大值。实现中使用的思想基于[这个](https://www.geeksforgeeks.org/eulers-totient-function-for-all-numbers-smaller-than-or-equal-to-n/)帖子。

    ## C++

    ```
    // C++ approach of finding sum of GCD of all pairs
    #include<bits/stdc++.h>
    using namespace std;

    #define MAX 100001

    // phi[i] stores euler totient function for i
    // result[j] stores result for value j
    long long phi[MAX], result[MAX];

    // Precomputation of phi[] numbers. Refer below link
    // for details : https://goo.gl/LUqdtY
    void computeTotient()
    {
        // Refer https://goo.gl/LUqdtY
        phi[1] = 1;
        for (int i=2; i<MAX; i++)
        {
            if (!phi[i])
            {
                phi[i] = i-1;
                for (int j = (i<<1); j<MAX; j+=i)
                {
                    if (!phi[j])
                        phi[j] = j;

                    phi[j] = (phi[j]/i)*(i-1);
                }
            }
        }
    }

    // Precomputes result for all numbers till MAX
    void sumOfGcdPairs()
    {
        // Precompute all phi value
        computeTotient();

        for (int i=1; i<MAX; ++i)
        {
            // Iterate throght all the divisors
            // of i.
            for (int j=2; i*j<MAX; ++j)
                result[i*j] += i*phi[j];
        }

        // Add summation of previous calculated sum
        for (int i=2; i<MAX; i++)
            result[i] += result[i-1];
    }

    // Driver code
    int main()
    {
        // Function to calculate sum of all the GCD
        // pairs
        sumOfGcdPairs();

        int N = 4;
        cout << "Summation of " << N << " = "
             << result[N] << endl;;
        N = 12;
        cout << "Summation of " << N << " = "
            << result[N] << endl;
        N = 5000;
        cout << "Summation of " << N << " = "
            << result[N] ;

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java approach of finding 
    // sum of GCD of all pairs.
    import java.lang.*;

    class GFG {

    static final int MAX = 100001;

    // phi[i] stores euler totient function for i
    // result[j] stores result for value j
    static long phi[] = new long[MAX];
    static long result[] = new long[MAX];

    // Precomputation of phi[] numbers.
    // Refer below link for details :
    // https://goo.gl/LUqdtY
    static void computeTotient() {

        // Refer https://goo.gl/LUqdtY
        phi[1] = 1;
        for (int i = 2; i < MAX; i++) {
        if (phi[i] == 0) {
            phi[i] = i - 1;
            for (int j = (i << 1); j < MAX; j += i) {
            if (phi[j] == 0)
                phi[j] = j;

            phi[j] = (phi[j] / i) * (i - 1);
            }
        }
        }
    }

    // Precomputes result for all
    // numbers till MAX
    static void sumOfGcdPairs() {

        // Precompute all phi value
        computeTotient();

        for (int i = 1; i < MAX; ++i) {

        // Iterate throght all the 
        // divisors of i.
        for (int j = 2; i * j < MAX; ++j)
            result[i * j] += i * phi[j];
        }

        // Add summation of previous calculated sum
        for (int i = 2; i < MAX; i++)
        result[i] += result[i - 1];
    }

    // Driver code
    public static void main(String[] args) {

        // Function to calculate sum of 
        // all the GCD pairs
        sumOfGcdPairs();

        int N = 4;
        System.out.println("Summation of " + N +
                             " = " + result[N]);
        N = 12;
        System.out.println("Summation of " + N + 
                             " = " + result[N]);
        N = 5000;
        System.out.print("Summation of " + N + 
                          " = " + +result[N]);
    }
    }

    // This code is contributed by Anant Agarwal.
    ```

    ## 蟒蛇 3

    ```
    # Python approach of finding
    # sum of GCD of all pairs
    MAX = 100001

    # phi[i] stores euler 
    # totient function for 
    # i result[j] stores 
    # result for value j
    phi = [0] * MAX
    result = [0] * MAX

    # Precomputation of phi[]
    # numbers. Refer below link
    # for details : https://goo.gl/LUqdtY
    def computeTotient():

        # Refer https://goo.gl/LUqdtY
        phi[1] = 1
        for i in range(2, MAX):
            if not phi[i]:
                phi[i] = i - 1
                for j in range(i << 1, MAX, i):
                    if not phi[j]:
                        phi[j] = j
                    phi[j] = ((phi[j] // i) * 
                              (i - 1))

    # Precomputes result 
    # for all numbers 
    # till MAX
    def sumOfGcdPairs():

        # Precompute all phi value
        computeTotient()

        for i in range(MAX):

            # Iterate throght all 
            # the divisors of i.
            for j in range(2, MAX):
                if i * j >= MAX:
                    break
                result[i * j] += i * phi[j]

        # Add summation of 
        # previous calculated sum
        for i in range(2, MAX):
            result[i] += result[i - 1]

    # Driver code
    # Function to calculate 
    # sum of all the GCD pairs
    sumOfGcdPairs()

    N = 4
    print("Summation of",N,"=",result[N])
    N = 12
    print("Summation of",N,"=",result[N])
    N = 5000
    print("Summation of",N,"=",result[N])

    # This code is contributed 
    # by Sanjit_Prasad.
    ```

    ## C#

    ```
    // C# approach of finding 
    // sum of GCD of all pairs.
    using System;

    class GFG {

    static int MAX = 100001;

    // phi[i] stores euler totient
    // function for i result[j]
    // stores result for value j
    static long []phi = new long[MAX];
    static long []result = new long[MAX];

    // Precomputation of phi[] numbers.
    // Refer below link for details :
    // https://goo.gl/LUqdtY
    static void computeTotient() {

        // Refer https://goo.gl/LUqdtY
        phi[1] = 1;
        for (int i = 2; i < MAX; i++) {
        if (phi[i] == 0) {
            phi[i] = i - 1;
            for (int j = (i << 1); j < MAX; j += i) {
            if (phi[j] == 0)
                phi[j] = j;

            phi[j] = (phi[j] / i) * (i - 1);
            }
        }
        }
    }

    // Precomputes result for all
    // numbers till MAX
    static void sumOfGcdPairs() {

        // Precompute all phi value
        computeTotient();

        for (int i = 1; i < MAX; ++i) {

        // Iterate throght all the 
        // divisors of i.
        for (int j = 2; i * j < MAX; ++j)
            result[i * j] += i * phi[j];
        }

        // Add summation of previous 
        // calculated sum
        for (int i = 2; i < MAX; i++)
        result[i] += result[i - 1];
    }

    // Driver code
    public static void Main() {

        // Function to calculate sum of 
        // all the GCD pairs
        sumOfGcdPairs();

        int N = 4;
        Console.WriteLine("Summation of " + N +
                          " = " + result[N]);
        N = 12;
        Console.WriteLine("Summation of " + N + 
                          " = " + result[N]);
        N = 5000;
        Console.Write("Summation of " + N + 
                      " = " + +result[N]);
    }
    }

    // This code is contributed by Nitin Mittal.
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php
    // PHP approach of finding sum of 
    // GCD of all pairs

    $MAX = 100001;

    // phi[i] stores euler totient function for i
    // result[j] stores result for value j
    $phi = array_fill(0, $MAX, 0);
    $result = array_fill(0, $MAX, 0);

    // Precomputation of phi[] numbers. Refer 
    // link for details : https://goo.gl/LUqdtY
    function computeTotient()
    {
        global $MAX, $phi;

        // Refer https://goo.gl/LUqdtY
        $phi[1] = 1;
        for ($i = 2; $i < $MAX; $i++)
        {
            if (!$phi[$i])
            {
                $phi[$i] = $i - 1;
                for ($j = ($i << 1); $j < $MAX; $j += $i)
                {
                    if (!$phi[$j])
                        $phi[$j] = $j;

                    $phi[$j] = ($phi[$j] / $i) * ($i - 1);
                }
            }
        }
    }

    // Precomputes result for all 
    // numbers till MAX
    function sumOfGcdPairs()
    {
        global $MAX, $phi, $result;

        // Precompute all phi value
        computeTotient();

        for ($i = 1; $i < $MAX; ++$i)
        {
            // Iterate throght all the divisors
            // of i.
            for ($j = 2; $i * $j < $MAX; ++$j)
                $result[$i * $j] += $i * $phi[$j];
        }

        // Add summation of previous calculated sum
        for ($i = 2; $i < $MAX; $i++)
            $result[$i] += $result[$i - 1];
    }

    // Driver code

    // Function to calculate sum of 
    // all the GCD pairs
    sumOfGcdPairs();

    $N = 4;
    echo "Summation of " . $N . 
         " = " . $result[$N] . "\n";
    $N = 12;
    echo "Summation of " . $N . 
         " = " . $result[$N] . "\n";
    $N = 5000;
    echo "Summation of " . $N . 
         " = " . $result[$N] . "\n";

    // This code is contributed by mits
    ?>
    ```

    **输出:**

    ```
    Summation of 4 = 7
    Summation of 12 = 105
    Summation of 5000 = 61567426

    ```

    **时间复杂度:**O(MAX * log(log MAX))
    T3】辅助空间: O(MAX)

    **参考:**
    [https://www . quora . com/我如何解决问题-GCD-Extreme-on-SPOJ-SPOJ-com-Problem-GCDEX](https://www.quora.com/How-can-I-solve-the-problem-GCD-Extreme-on-SPOJ-SPOJ-com-Problem-GCDEX)

    本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。