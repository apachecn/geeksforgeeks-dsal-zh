# 通过递增 X 或乘以 Y 从 0 开始以 K 步生成最大的 N 位数

> 原文:[https://www . geeksforgeeks . org/generate-最大 n 位数-从 0 开始-k 步-递增-x-或乘以-y/](https://www.geeksforgeeks.org/generate-largest-n-digit-number-from-0-in-k-steps-by-incrementing-x-or-multiplying-by-y/)

给定整数 N，K，X 和 y。任务是从 0 开始，在 K 步中找到最大可能的 N 位数。使用下面给出的操作:

*   将该值增加 X，或
*   将该值乘以 Y

**示例:**

> **输入:** N = 2，K = 5，X = 2，Y = 3
> **输出:** 72
> **解释:**序列应为{ 0->2->6->8->24->72 }
> 
> **输入:** N = 2，K = 10，X = 2，Y = 3
> **输出:** 98
> **解释:**序列应为
> { 0->0->0->2->6->8->10->30->32->96->98 }。
> 注意上面提到的序列 0 乘以 3 两次。
> 另一个可能的序列是
> { 0->0->2->4->6->8->10->30->32->96->98 }。
> 
> **输入:** N = 3，K = 4
> **输出:** -1
> **说明:**不可能分 4 步创建 3 位数

**方法:**利用 [**递归**](http://www.geeksforgeeks.org/recursion/) 的概念可以解决问题。遵循以下步骤:

1.  对于每个递归步骤，在以下情况下退出递归调用:
    *   如果所采取的步骤数变得**大于 K** ，则必须停止递归。
    *   如果当前号码**的**位数**超过 N** ，则无需在该分支上搜索。
    *   如果当前编号变为**等于可能生成的**最大 N 位数**，则无需进一步处理。它将减少额外的递归调用次数。**
    *   最大可能**N**-随时可能产生的数字是**(10<sup>N</sup>–1)**。
2.  现在递归调用当前数字增加 **X** 和当前步长增加 **1** 的方法。
3.  用当前数字乘以 **Y** ，当前步长增加 **1** 进行另一次递归调用。
4.  将两个结果都存储在一个变量中。
5.  在任何递归点，返回变量中存储的两个结果的最大值。

下面是上述方法的实现

## C++

```
// C++ code to implement the approach
#include <bits/stdc++.h>
using namespace std;

// Function for generating largest
//  N-digit number in K-steps.
int largestNDigitNumber(int N, int currentStep,
                        int K, int X, int Y,
                        int currentValue)
{
    // Further processing is useless
    // ifcCurrent value already becomes equal
    // to largest N-digit number that
    // can be generated
    if (currentValue == pow(10, N) - 1)
        return currentValue;

    // Return 0 steps taken is greater than K
    // and also if N or K equal to Zero.
    if (currentStep > K || N < 1 || K < 1)
        return 0;

    // currentValue exceeds maxValue,
    // so there is no need to
    // keep searching on that branch.
    if (currentValue >= pow(10, N))
        return 0;

    // Recursive calls
    int result2 = largestNDigitNumber(
        N, currentStep + 1, K, X, Y,
        currentValue + X);
    int result1 = largestNDigitNumber(
        N, currentStep + 1, K, X, Y,
        currentValue * Y);

    // If both the results are zero
    // it means maximum is reached.
    if (result1 == 0 && result2 == 0)
        return currentValue;

    // Checking for maximum of the two results.
    return result1 > result2 ? result1 : result2;
}

// Driver code
int main()
{
    int N = 2, K = 10, X = 2, Y = 3;
    int largest = largestNDigitNumber(
        N, 0, K, X, Y, 0);

    // Checking whether the returned result
    //  is a N-digit number or not.
    if (largest < pow(10, (N - 1))) {
        cout << ("-1");
    }
    else
        cout << largest;
    return 0;
}
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function for generating largest
       //  N-digit number in K-steps.
       function largestNDigitNumber(N, currentStep,
                                   K, X, Y,
                                   currentValue)
       {

           // Further processing is useless
           // ifcCurrent value already becomes equal
           // to largest N-digit number that
           // can be generated
           if (currentValue == Math.pow(10, N) - 1)
               return currentValue;

           // Return 0 steps taken is greater than K
           // and also if N or K equal to Zero.
           if (currentStep > K || N < 1 || K < 1)
               return 0;

           // currentValue exceeds maxValue,
           // so there is no need to
           // keep searching on that branch.
           if (currentValue >= Math.pow(10, N))
               return 0;

           // Recursive calls
           let result2 = largestNDigitNumber(
               N, currentStep + 1, K, X, Y,
               currentValue + X);
           let result1 = largestNDigitNumber(
               N, currentStep + 1, K, X, Y,
               currentValue * Y);

           // If both the results are zero
           // it means maximum is reached.
           if (result1 == 0 && result2 == 0)
               return currentValue;

           // Checking for maximum of the two results.
           return result1 > result2 ? result1 : result2;
       }

       // Driver code
       let N = 2, K = 10, X = 2, Y = 3;
       let largest = largestNDigitNumber(
           N, 0, K, X, Y, 0);

       // Checking whether the returned result
       //  is a N-digit number or not.
       if (largest < Math.pow(10, (N - 1))) {
           document.write("-1");
       }
       else
           document.write(largest);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
98
```

***时间复杂度:***O(2<sup>K</sup>)
***辅助空间:*** O(1)