# 求数列 1、2、3、6、9、18、27、54、…的和，直到 N 项

> 原文:[https://www . geesforgeks . org/find-the-sum-the-series-1-2-3-6-9-18-27-54-till-n-terms/](https://www.geeksforgeeks.org/find-the-sum-of-the-series-1-2-3-6-9-18-27-54-till-n-terms/)

给定一个数字 **N** ，任务是找到下面系列的和，直到 N 项。

> ![1, 2, 3, 6, 9, 18, 27, 54, 81, 162... ](img/f6a65ece7c228f2629bd43daae6cf98f.png "Rendered by QuickLaTeX.com")

**例:**

> **输入:** N = 8
> **输出:**201
> 1+2+3+6+9+18+27+54+81 = 201
> **输入:** N = 12
> **输出:**1821
> 1+2+3+6+9+18+27+54+81+162+243+486+729 = 0

**方法:**从给定的序列中，找到第 n 项的公式:

```
1st term = 1
2nd term = 2 = 2 * 1
3rd term = 3 = 3/2 * 2
4th term = 6 = 2 * 3
5th term = 9 = 3/2 * 6
6th term = 18 = 2 * 9
.
.
Nth term = [2 * (N-1)th term], if N is even
           [3/2 * (N-1)th term], if N is odd
```

因此:

> **该系列的第 n 项**
> 
> ```
> *** QuickLaTeX cannot compile formula:
>  
> 
> *** Error message:
> Error: Nothing to show, formula is empty
> 
> ```

然后在**【1，N】**范围内的数字上迭代，使用上面的公式找到所有的项，并计算它们的和。
**方法:**通过观察给定序列中的模式，序列的下一个数字交替乘以 **2** 和 **3/2** 。
以下是上述方法的实施:

## C++

```
// C++ program for the above series
#include <iostream>
using namespace std;

// Function to find the sum of series
void printSeriesSum(int N)
{
    double sum = 0;

    int a = 1;
    int cnt = 0;

    // Flag to find the multiplicating
    // factor.. i.e, by 2 or 3/2
    bool flag = true;

    // First term
    sum += a;

    while (cnt < N) {

        int nextElement;

        // If flag is true, multiply by 2
        if (flag) {
            nextElement = a * 2;
            sum += nextElement;
            flag = !flag;
        }

        // If flag is false, multiply by 3/2
        else {
            nextElement = a * 3 / 2;
            sum += nextElement;
            flag = !flag;
        }

        // Update the previous element
        // to nextElement
        a = nextElement;
        cnt++;
    }

    // Print the sum
    cout << sum << endl;
}

// Driver Code
int main()
{

    int N = 8;

    printSeriesSum(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above series
class GFG {

    // Function to find the sum of series
    static void printSeriesSum(int N)
    {
        double sum = 0;

        int a = 1;
        int cnt = 0;

        // Flag to find the multiplicating
        // factor.. i.e, by 2 or 3/2
        boolean flag = true;

        // First term
        sum += a;

        while (cnt < N) {

            int nextElement;

            // If flag is true, multiply by 2
            if (flag == true) {
                nextElement = a * 2;
                sum += nextElement;
                flag = !flag;
            }

            // If flag is false, multiply by 3/2
            else {
                nextElement = a * 3 / 2;
                sum += nextElement;
                flag = !flag;
            }

            // Update the previous element
            // to nextElement
            a = nextElement;
            cnt++;
        }

        // Print the sum
        System.out.println(sum);
    }

    // Driver Code
    public static void main (String[] args)
    {

        int N = 8;

        printSeriesSum(N);
    }
}
// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program for the above series

# Function to find the sum of series
def printSeriesSum(N) :

    sum = 0;

    a = 1;
    cnt = 0;

    # Flag to find the multiplicating
    # factor.. i.e, by 2 or 3/2
    flag = True;

    # First term
    sum += a;

    while (cnt < N) :

        nextElement = None;

        # If flag is true, multiply by 2
        if (flag) :
            nextElement = a * 2;
            sum += nextElement;
            flag = not flag;

        # If flag is false, multiply by 3/2
        else :
            nextElement = a * (3 / 2);
            sum += nextElement;
            flag = not flag;

        # Update the previous element
        # to nextElement
        a = nextElement;
        cnt += 1

    # Print the sum
    print(sum);

# Driver Code
if __name__ == "__main__" :

    N = 8;

    printSeriesSum(N);

    # This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above series
using System;

class GFG {

    // Function to find the sum of series
    static void printSeriesSum(int N)
    {
        double sum = 0;

        int a = 1;
        int cnt = 0;

        // Flag to find the multiplicating
        // factor.. i.e, by 2 or 3/2
        bool flag = true;

        // First term
        sum += a;

        while (cnt < N) {

            int nextElement;

            // If flag is true, multiply by 2
            if (flag == true) {
                nextElement = a * 2;
                sum += nextElement;
                flag = !flag;
            }

            // If flag is false, multiply by 3/2
            else {
                nextElement = a * 3 / 2;
                sum += nextElement;
                flag = !flag;
            }

            // Update the previous element
            // to nextElement
            a = nextElement;
            cnt++;
        }

        // Print the sum
        Console.WriteLine(sum);
    }

    // Driver Code
    public static void Main (string[] args)
    {

        int N = 8;

        printSeriesSum(N);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript program for the above series

// Function to find the sum of series
function printSeriesSum( N)
{
    let sum = 0;

    let a = 1;
    let cnt = 0;

    // Flag to find the multiplicating
    // factor.. i.e, by 2 or 3/2
    let flag = true;

    // First term
    sum += a;

    while (cnt < N) {

        let nextElement;

        // If flag is true, multiply by 2
        if (flag) {
            nextElement = a * 2;
            sum += nextElement;
            flag = !flag;
        }

        // If flag is false, multiply by 3/2
        else {
            nextElement = a * 3 / 2;
            sum += nextElement;
            flag = !flag;
        }

        // Update the previous element
        // to nextElement
        a = nextElement;
        cnt++;
    }

    // Print the sum
   document.write(sum );
}

// Driver Code

    let N = 8;

    printSeriesSum(N);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
201
```

时间复杂度:0(N)

辅助空间:0(1)