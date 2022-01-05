# 子集差异之和

> 原文:[https://www.geeksforgeeks.org/sum-subset-differences/](https://www.geeksforgeeks.org/sum-subset-differences/)

给定一个由 n 个数字组成的集合 S，求每个子集的最后一个元素和第一个元素之差的和。我们通过保持它们在输入集 s 中出现的顺序相同来找到每个子集的第一个和最后一个元素。

即 sumSetDiff(S) = ∑(最后一个(S)–第一个(S))，
其中 sum 覆盖 S 的所有子集 S

**注意:**子集中的元素应与集合 s 中的元素顺序相同。

示例:

```
S = {5, 2, 9, 6}, n = 4

Subsets are:
{5}, last(s)-first(s) = 0.
{2}, last(s)-first(s) = 0.
{9}, last(s)-first(s) = 0.
{6}, last(s)-first(s) = 0.
{5,2}, last(s)-first(s) = -3.
{5,9}, last(s)-first(s) = 4.
{5,6}, last(s)-first(s) = 1.
{2,9}, last(s)-first(s) = 7.
{2,6}, last(s)-first(s) = 4.
{9,6}, last(s)-first(s) = -3.
{5,2,9}, last(s)-first(s) = 4.
{5,2,6}, last(s)-first(s) = 1.
{5,9,6}, last(s)-first(s) = 1.
{2,9,6}, last(s)-first(s) = 4.
{5,2,9,6}, last(s)-first(s) = 1.

Output  = -3+4+1+7+4-3+4+1+1+4+1
        = 21.

```

**这个问题的一个简单解决方案**是找到集合 S 的每个子集 S 的最后一个元素和第一个元素之间的差，并输出这些差的和 ll。该方法的时间复杂度为 0(2<sup>n</sup>)。

**解决线性时间复杂度问题的有效解决方案**。
给我们一个由 n 个数字组成的集合 S，我们需要计算 S 的每个子集的最后一个元素和第一个元素之间的差的和，即
sumSetDiff(S) = ∑(最后一个(S)–第一个(S))，其中和覆盖 S 的所有子集 S。
等价地，
sumSetDiff(S) = ∑(最后一个(S))–∑(第一个(S))，
换句话说，我们可以计算每个子集的最后一个元素的和，并且

假设 S 的元素是{a1，a2，a3，…，an}。请注意以下观察结果:

1.  包含元素 **a1** 作为第一个元素的子集可以通过取{a2，a3，…，an}的任意子集，然后将 a1 包含进去得到。此类子集的数量为 2 <sup>n-1</sup> 。
2.  包含元素 a2 作为第一个元素的子集可以通过取{a3，a4，…，an}的任意子集，然后将 a2 包含在其中而得到。此类子集的数量为 2 <sup>n-2</sup> 。
3.  Subsets containing element ai as the first element can be obtained by taking any subset of {ai, a(i+1),…, an} and then including ai into it. Number of such subsets will be 2<sup>n-i</sup>.

    因此，所有子集的第一个元素之和将为:
    SumF = a 1.2<sup>n-1</sup>+a 2.2<sup>n-2</sup>+…+an . 1

    以类似的方式，我们可以计算 S 的所有子集的最后一个元素的和(在每一步将 ai 作为最后一个元素而不是第一个元素，然后获得所有子集)。
    SumL = a 1.1+a 2.2+…+an . 2<sup>n-1</sup>

    最后，我们问题的答案将是**SumL–SumF**。

    **执行:**

    ## C++

    ```
    // A C++ program to find sum of difference between
    // last and first element of each subset
    #include<bits/stdc++.h>

    // Returns the sum of first elements of all subsets
    int SumF(int S[], int n)
    {
        int sum = 0;

        // Compute the SumF as given in the above explanation
        for (int i = 0; i < n; i++)
            sum = sum + (S[i] * pow(2, n-i-1));
        return sum;
    }

    // Returns the sum of last elements of all subsets
    int SumL(int S[], int n)
    {
        int sum = 0;

        // Compute the SumL as given in the above explanation
        for (int i = 0; i < n; i++)
            sum = sum + (S[i] * pow(2, i));
        return sum;
    }

    // Returns the difference between sum of last elements of
    // each subset and the sum of first elements of each subset
    int sumSetDiff(int S[], int n)
    {
        return SumL(S, n) - SumF(S, n);
    }

    // Driver program to test above function
    int main()
    {
        int n = 4;
        int S[] = {5, 2, 9, 6};
        printf("%d\n", sumSetDiff(S, n));
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // A Java program to find sum of difference 
    // between last and first element of each 
    // subset
    class GFG {

        // Returns the sum of first elements 
        // of all subsets
        static int SumF(int S[], int n)
        {
            int sum = 0;

            // Compute the SumF as given in 
            // the above explanation
            for (int i = 0; i < n; i++)
                sum = sum + (int)(S[i] * 
                    Math.pow(2, n - i - 1));
            return sum;
        }

        // Returns the sum of last elements 
        // of all subsets
        static int SumL(int S[], int n)
        {
            int sum = 0;

            // Compute the SumL as given in 
            // the above explanation
            for (int i = 0; i < n; i++)
                sum = sum + (int)(S[i] *
                             Math.pow(2, i));

            return sum;
        }

        // Returns the difference between sum 
        // of last elements of each subset and 
        // the sum of first elements of each 
        // subset
        static int sumSetDiff(int S[], int n)
        {
            return SumL(S, n) - SumF(S, n);
        }

        // Driver program
        public static void main(String arg[])
        {
            int n = 4;
            int S[] = { 5, 2, 9, 6 };

            System.out.println(sumSetDiff(S, n));
        }
    }

    // This code is contributed by Anant Agarwal.
    ```

    ## 蟒蛇 3

    ```
    # Python3 program to find sum of
    # difference between last and 
    # first element of each subset

    # Returns the sum of first
    # elements of all subsets
    def SumF(S, n):

        sum = 0

        # Compute the SumF as given
        # in the above explanation
        for i in range(n):
            sum = sum + (S[i] * pow(2, n - i - 1))
        return sum

    # Returns the sum of last
    # elements of all subsets
    def SumL(S, n):

        sum = 0

        # Compute the SumL as given
        # in the above explanation
        for i in range(n):
            sum = sum + (S[i] * pow(2, i))
        return sum

    # Returns the difference between sum
    # of last elements of each subset and
    # the sum of first elements of each subset
    def sumSetDiff(S, n):

        return SumL(S, n) - SumF(S, n)

    # Driver program
    n = 4
    S = [5, 2, 9, 6]
    print(sumSetDiff(S, n))

    # This code is contributed by Anant Agarwal.
    ```

    ## C#

    ```
    // A C# program to find sum of difference 
    // between last and first element of each 
    // subset
    using System;
    class GFG {

        // Returns the sum of first elements 
        // of all subsets
        static int SumF(int []S, int n)
        {
            int sum = 0;

            // Compute the SumF as given in 
            // the above explanation
            for (int i = 0; i < n; i++)
                sum = sum + (int)(S[i] * 
                    Math.Pow(2, n - i - 1));
            return sum;
        }

        // Returns the sum of last elements 
        // of all subsets
        static int SumL(int []S, int n)
        {
            int sum = 0;

            // Compute the SumL as given in 
            // the above explanation
            for (int i = 0; i < n; i++)
                sum = sum + (int)(S[i] *
                             Math.Pow(2, i));

            return sum;
        }

        // Returns the difference between sum 
        // of last elements of each subset and 
        // the sum of first elements of each 
        // subset
        static int sumSetDiff(int []S, int n)
        {
            return SumL(S, n) - SumF(S, n);
        }

        // Driver program
        public static void Main()
        {
            int n = 4;
            int []S = { 5, 2, 9, 6 };

            Console.Write(sumSetDiff(S, n));
        }
    }

    // This code is contributed by nitin mittal.
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php
    // A PHP program to find sum 
    // of difference between last 
    // and first element of each subset

    // Returns the sum of first 
    // elements of all subsets
    function SumF( $S, $n)
    {
        $sum = 0;

        // Compute the SumF as given 
        // in the above explanation
        for ($i = 0; $i < $n; $i++)
            $sum = $sum + ($S[$i] * 
                   pow(2, $n - $i - 1));
        return $sum;
    }

    // Returns the sum of last
    // elements of all subsets
    function SumL( $S, $n)
    {
        $sum = 0;

        // Compute the SumL as given
        // in the above explanation
        for($i = 0; $i < $n; $i++)
            $sum = $sum + ($S[$i] * 
                        pow(2, $i));
        return $sum;
    }

    // Returns the difference between
    // sum of last elements of
    // each subset and the sum of
    // first elements of each subset
    function sumSetDiff( $S, $n)
    {
        return SumL($S, $n) - SumF($S, $n);
    }

        // Driver Code
        $n = 4;
        $S = array(5, 2, 9, 6);
        echo sumSetDiff($S, $n);

    // This code is contributed by anuj_67.
    ?>
    ```

    Output:

    ```
    21

    ```

    时间复杂度:0(n)

    本文由 **Akash Aggarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。