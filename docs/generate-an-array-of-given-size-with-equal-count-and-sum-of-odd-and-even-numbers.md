# 生成一个给定大小的数组，具有相等的计数以及奇数和偶数的和

> 原文:[https://www . geeksforgeeks . org/生成给定大小的奇数和偶数计数和总和数组/](https://www.geeksforgeeks.org/generate-an-array-of-given-size-with-equal-count-and-sum-of-odd-and-even-numbers/)

给定一个整数 **N** ，任务是找到一个长度为 **N** 的数组，该数组包含相同数量的奇数和偶数元素，并且该数组中的偶数和奇数元素的和相等。
**注意:**如果不可能有这样的阵，打印-1。
**示例:**

> **输入:** N = 4
> **输出:** 1 2 5 4
> **解释:**
> 数组的偶元素–{ 2，4}，S(偶)= 6
> 数组的奇元素–{ 1，5}，S(奇)= 6
> **输入:** N = 6
> **输出:** -1
> **解释:**
> 有

**逼近:**问题中的关键观察是，只有一个数组的长度是 **4** 的倍数，才能形成一个偶数和奇数元素相等且和相等的数组。以下是步骤说明:

*   数组的偶元素是从 2 开始的自然数的第一个 **N/2** 偶元素。
*   同样，数组的**(N/2–1)**奇数元素是从 1 开始的自然数的第一个**(N/2–1)**奇数元素。
*   The Last odd element of the array is the required value to make the sum of the even and odd elements of the array equal.

    ```
    Last Odd Element = 
       (sum of even elements) - 
       (sum of N/2 - 1 odd elements)
    ```

    以下是上述方法的实现:

    ## C++

    ```
    // C++ implementation to find the
    // array containing same count of
    // even and odd elements with equal
    // sum of even and odd elements

    #include <bits/stdc++.h>

    using namespace std;

    // Function to find the array such that
    // the array contains the same count
    // of even and odd elements with equal
    // sum of even and odd elements
    void findSolution(int N)
    {

        // Length of array which is not
        // divisible by 4 is unable to
        // form such array
        if (N % 4 != 0)
            cout << -1 << "\n";
        else {
            int temp = 0, sum_odd = 0,
                sum_even = 0;
            int result[N] = { 0 };

            // Loop to find the resulted
            // array containing the same
            // count of even and odd elements
            for (int i = 0; i < N; i += 2) {
                temp += 2;

                result[i + 1] = temp;
                // Find the total sum
                // of even elements
                sum_even += result[i + 1];

                result[i] = temp - 1;
                // Find the total sum
                // of odd elements
                sum_odd += result[i];
            }

            // Find the difference between the
            // total sum of even and odd elements
            int diff = sum_even - sum_odd;

            // The difference will be added
            // in the last odd element
            result[N - 2] += diff;

            for (int i = 0; i < N; i++)
                cout << result[i] << " ";
            cout << "\n";
        }
    }

    // Driver Code
    int main()
    {
        int N = 8;
        findSolution(N);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java implementation to find the
    // array containing same count of
    // even and odd elements with equal
    // sum of even and odd elements

    class GFG{

    // Function to find the array such that
    // the array contains the same count
    // of even and odd elements with equal
    // sum of even and odd elements
    static void findSolution(int N)
    {

        // Length of array which is not
        // divisible by 4 is unable to
        // form such array
        if (N % 4 != 0)
            System.out.print(-1 + "\n");

        else 
        {
            int temp = 0, sum_odd = 0;
            int sum_even = 0;
            int result[] = new int[N];

            // Loop to find the resulted
            // array containing the same
            // count of even and odd elements
            for(int i = 0; i < N; i += 2)
            {
               temp += 2;
               result[i + 1] = temp;

               // Find the total sum
               // of even elements
               sum_even += result[i + 1];
               result[i] = temp - 1;

               // Find the total sum
               // of odd elements
               sum_odd += result[i];
            }

            // Find the difference between the
            // total sum of even and odd elements
            int diff = sum_even - sum_odd;

            // The difference will be added
            // in the last odd element
            result[N - 2] += diff;

            for(int i = 0; i < N; i++)
               System.out.print(result[i] + " ");
            System.out.print("\n");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 8;
        findSolution(N);
    }
    }

    // This code is contributed by Amit Katiyar
    ```

    ## 蟒蛇 3

    ```
    # Python3 implementation to find the 
    # array containing same count of 
    # even and odd elements with equal 
    # sum of even and odd elements 

    # Function to find the array such that 
    # the array contains the same count 
    # of even and odd elements with equal 
    # sum of even and odd elements 
    def findSolution(N): 

        # Length of array which is not 
        # divisible by 4 is unable to 
        # form such array 
        if (N % 4 != 0): 
            print(-1) 
        else: 
            temp = 0
            sum_odd = 0
            sum_even = 0
            result = [0] * N 

            # Loop to find the resulted 
            # array containing the same 
            # count of even and odd elements 
            for i in range(0, N, 2): 
                temp += 2
                result[i + 1] = temp 

                # Find the total sum 
                # of even elements 
                sum_even += result[i + 1] 
                result[i] = temp - 1

                # Find the total sum 
                # of odd elements 
                sum_odd += result[i] 

            # Find the difference between the 
            # total sum of even and odd elements 
            diff = sum_even - sum_odd 

            # The difference will be added 
            # in the last odd element 
            result[N - 2] += diff 

            for i in range(N): 
                print(result[i], end = " ") 
            print() 

    # Driver Code 
    N = 8; 
    findSolution(N)

    # This code is contributed by divyamohan123 
    ```

    ## C#

    ```
    // C# implementation to find the
    // array containing same count of
    // even and odd elements with equal
    // sum of even and odd elements
    using System;

    class GFG{

    // Function to find the array such that
    // the array contains the same count
    // of even and odd elements with equal
    // sum of even and odd elements
    static void findSolution(int N)
    {

        // Length of array which is not
        // divisible by 4 is unable to
        // form such array
        if (N % 4 != 0)
            Console.Write(-1 + "\n");

        else
        {
            int temp = 0, sum_odd = 0;
            int sum_even = 0;
            int []result = new int[N];

            // Loop to find the resulted
            // array containing the same
            // count of even and odd elements
            for(int i = 0; i < N; i += 2)
            {
               temp += 2;
               result[i + 1] = temp;

               // Find the total sum
               // of even elements
               sum_even += result[i + 1];
               result[i] = temp - 1;

               // Find the total sum
               // of odd elements
               sum_odd += result[i];
            }

            // Find the difference between the
            // total sum of even and odd elements
            int diff = sum_even - sum_odd;

            // The difference will be added
            // in the last odd element
            result[N - 2] += diff;

            for(int i = 0; i < N; i++)
               Console.Write(result[i] + " ");
            Console.Write("\n");
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 8;
        findSolution(N);
    }
    }

    // This code is contributed by Rohit_ranjan
    ```

    ## java 描述语言

    ```
    <script>

    // JavaScript implementation to find the
    // array containing same count of
    // even and odd elements with equal
    // sum of even and odd elements

    // Function to find the array such that
    // the array contains the same count
    // of even and odd elements with equal
    // sum of even and odd elements
    function findSolution(N)
    {

        // Length of array which is not
        // divisible by 4 is unable to
        // form such array
        if (N % 4 != 0)
            document.write(-1 + "<br>");
        else {
            let temp = 0, sum_odd = 0,
                sum_even = 0;
            let result = new Uint8Array(N);

            // Loop to find the resulted
            // array containing the same
            // count of even and odd elements
            for (let i = 0; i < N; i += 2) {
                temp += 2;

                result[i + 1] = temp;
                // Find the total sum
                // of even elements
                sum_even += result[i + 1];

                result[i] = temp - 1;
                // Find the total sum
                // of odd elements
                sum_odd += result[i];
            }

            // Find the difference between the
            // total sum of even and odd elements
            let diff = sum_even - sum_odd;

            // The difference will be added
            // in the last odd element
            result[N - 2] += diff;

            for (let i = 0; i < N; i++)
                document.write(result[i] + " ");
            document.write("<br>");
        }
    }

    // Driver Code
        let N = 8;
        findSolution(N);

    // This code is contributed by Surbhi Tyagi.
    </script>
    ```

    **Output:** 

    ```
    1 2 3 4 5 6 11 8
    ```

    **业绩分析:**

    *   **时间复杂度:** *O(N)*
    *   **辅助空间:** *O(1)*