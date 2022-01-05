# 下一个数字不同的数字

> 原文:[https://www . geesforgeks . org/next-number-with-distinct-digits/](https://www.geeksforgeeks.org/next-number-with-distinct-digits/)

给定一个整数 **N** ，任务是找到下一个数字，其中有不同的数字。

**示例:**

> **输入:** N = 20
> **输出:**21
> 20 后所有不同数字的下一个整数是 21。
> 
> **输入:**N = 2019
> T3】输出: 2031

**进场:**

1.  使用本文[中讨论的方法计算数字 **N** 中的总位数。](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)
2.  计算 **N** 中不同数字的总数。
3.  如果总位数和 **N** 中不同位数的计数相等，则返回该数，否则将该数增加 1，并重复前面的步骤。

下面是上述方法的实现:

## C++

```
// C++ program to find next consecutive
// Number with all distinct digits
#include <bits/stdc++.h>
using namespace std;

// Function to count distinct
// digits in a number
int countDistinct(int n)
{
    // To count the occurrence of digits
    // in number from 0 to 9
    int arr[10] = { 0 };
    int count = 0;

    // Iterate over the digits of the number
    // Flag those digits as found in the array
    while (n) {
        int r = n % 10;
        arr[r] = 1;
        n /= 10;
    }

    // Traverse the array arr and count the
    // distinct digits in the array
    for (int i = 0; i < 10; i++) {
        if (arr[i])
            count++;
    }
    return count;
}

// Function to return the total number
// of digits in the number
int countDigit(int n)
{
    int c = 0;

    // Iterate over the digits of the number
    while (n) {
        int r = n % 10;
        c++;
        n /= 10;
    }
    return c;
}

// Function to return the next
// number with distinct digits
int nextNumberDistinctDigit(int n)
{
    while (n < INT_MAX) {

        // Count the distinct digits in N + 1
        int distinct_digits = countDistinct(n + 1);

        // Count the total number of digits in N + 1
        int total_digits = countDigit(n + 1);

        if (distinct_digits == total_digits) {

            // Return the next consecutive number
            return n + 1;
        }

        else
            // Increment Number by 1
            n++;
    }
    return -1;
}

// Driver code
int main()
{
    int n = 2019;

    cout << nextNumberDistinctDigit(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next consecutive
// Number with all distinct digits
class GFG
{

    final static int INT_MAX = Integer.MAX_VALUE ;

    // Function to count distinct
    // digits in a number
    static int countDistinct(int n)
    {

        // To count the occurrence of digits
        // in number from 0 to 9
        int arr[] = new int[10];
        int count = 0;

        // Iterate over the digits of the number
        // Flag those digits as found in the array
        while (n != 0)
        {
            int r = n % 10;
            arr[r] = 1;
            n /= 10;
        }

        // Traverse the array arr and count the
        // distinct digits in the array
        for (int i = 0; i < 10; i++)
        {
            if (arr[i] != 0)
                count++;
        }
        return count;
    }

    // Function to return the total number
    // of digits in the number
    static int countDigit(int n)
    {
        int c = 0;

        // Iterate over the digits of the number
        while (n != 0)
        {
            int r = n % 10;
            c++;
            n /= 10;
        }
        return c;
    }

    // Function to return the next
    // number with distinct digits
    static int nextNumberDistinctDigit(int n)
    {
        while (n < INT_MAX)
        {

            // Count the distinct digits in N + 1
            int distinct_digits = countDistinct(n + 1);

            // Count the total number of digits in N + 1
            int total_digits = countDigit(n + 1);

            if (distinct_digits == total_digits)
            {

                // Return the next consecutive number
                return n + 1;
            }

            else

                // Increment Number by 1
                n++;
        }
        return -1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 2019;

        System.out.println(nextNumberDistinctDigit(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find next consecutive
# Number with all distinct digits
import sys

INT_MAX = sys.maxsize;

# Function to count distinct
# digits in a number
def countDistinct(n):

    # To count the occurrence of digits
    # in number from 0 to 9
    arr = [0] * 10;
    count = 0;

    # Iterate over the digits of the number
    # Flag those digits as found in the array
    while (n != 0):
        r = int(n % 10);
        arr[r] = 1;
        n //= 10;

    # Traverse the array arr and count the
    # distinct digits in the array
    for i in range(10):
        if (arr[i] != 0):
            count += 1;

    return count;

# Function to return the total number
# of digits in the number
def countDigit(n):
    c = 0;

    # Iterate over the digits of the number
    while (n != 0):
        r = n % 10;
        c+=1;
        n //= 10;

    return c;

# Function to return the next
# number with distinct digits
def nextNumberDistinctDigit(n):
    while (n < INT_MAX):

        # Count the distinct digits in N + 1
        distinct_digits = countDistinct(n + 1);

        # Count the total number of digits in N + 1
        total_digits = countDigit(n + 1);

        if (distinct_digits == total_digits):

            # Return the next consecutive number
            return n + 1;
        else:

            # Increment Number by 1
            n += 1;

    return -1;

# Driver code
if __name__ == '__main__':
    n = 2019;

    print(nextNumberDistinctDigit(n));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to find next consecutive
// Number with all distinct digits
using System;

class GFG
{

    readonly static int INT_MAX = int.MaxValue ;

    // Function to count distinct
    // digits in a number
    static int countDistinct(int n)
    {

        // To count the occurrence of digits
        // in number from 0 to 9
        int []arr = new int[10];
        int count = 0;

        // Iterate over the digits of the number
        // Flag those digits as found in the array
        while (n != 0)
        {
            int r = n % 10;
            arr[r] = 1;
            n /= 10;
        }

        // Traverse the array arr and count the
        // distinct digits in the array
        for (int i = 0; i < 10; i++)
        {
            if (arr[i] != 0)
                count++;
        }
        return count;
    }

    // Function to return the total number
    // of digits in the number
    static int countDigit(int n)
    {
        int c = 0;

        // Iterate over the digits of the number
        while (n != 0)
        {
            int r = n % 10;
            c++;
            n /= 10;
        }
        return c;
    }

    // Function to return the next
    // number with distinct digits
    static int nextNumberDistinctDigit(int n)
    {
        while (n < INT_MAX)
        {

            // Count the distinct digits in N + 1
            int distinct_digits = countDistinct(n + 1);

            // Count the total number of digits in N + 1
            int total_digits = countDigit(n + 1);

            if (distinct_digits == total_digits)
            {

                // Return the next consecutive number
                return n + 1;
            }

            else

                // Increment Number by 1
                n++;
        }
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 2019;

        Console.WriteLine(nextNumberDistinctDigit(n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript program to find next consecutive
    // Number with all distinct digits

    let INT_MAX = Number.MAX_VALUE;

    // Function to count distinct
    // digits in a number
    function countDistinct(n)
    {

        // To count the occurrence of digits
        // in number from 0 to 9
        let arr = new Array(10);
        arr.fill(0);
        let count = 0;

        // Iterate over the digits of the number
        // Flag those digits as found in the array
        while (n != 0)
        {
            let r = n % 10;
            arr[r] = 1;
            n = parseInt(n / 10, 10);
        }

        // Traverse the array arr and count the
        // distinct digits in the array
        for (let i = 0; i < 10; i++)
        {
            if (arr[i] != 0)
                count++;
        }
        return count;
    }

    // Function to return the total number
    // of digits in the number
    function countDigit(n)
    {
        let c = 0;

        // Iterate over the digits of the number
        while (n != 0)
        {
            let r = n % 10;
            c++;
            n = parseInt(n / 10, 10);
        }
        return c;
    }

    // Function to return the next
    // number with distinct digits
    function nextNumberDistinctDigit(n)
    {
        while (n < INT_MAX)
        {

            // Count the distinct digits in N + 1
            let distinct_digits = countDistinct(n + 1);

            // Count the total number of digits in N + 1
            let total_digits = countDigit(n + 1);

            if (distinct_digits == total_digits)
            {

                // Return the next consecutive number
                return n + 1;
            }

            else

                // Increment Number by 1
                n++;
        }
        return -1;
    }

    let n = 2019;

      document.write(nextNumberDistinctDigit(n));

</script>
```

**Output**

```
2031
```

**另一种方法:**

我们可以使用 set STL 来检查一个数字是否只有唯一的数字，而不是每次都计算数字的数量。

然后我们可以比较由给定数字和新创建的集合形成的字符串的大小。

例如，让我们考虑数字 1987，然后我们可以将该数字转换为字符串，

## C++

```
int n;
cin>>n;
string s = to_string(n);
```

之后，用字符串 s 的内容初始化一个集合。

## C++

```
set<int> uniDigits(s.begin(), s.end());
```

然后我们可以比较字符串 s 的大小和新创建的一组单音数字。

这是总代码

## C++

```
// CPP program for the above program
#include <bits/stdc++.h>
using namespace std;

// Function to find next number
// with digit distinct
void nextNumberDistinctDigit(int n)
{

    // Iterate from n + 1 to inf
    for (int i = n + 1;; i++) {

        // Convert the no. to
        // string
        string s = to_string(i);

        // Convert string to set using stl
        set<int> uniDigits(s.begin(), s.end());

        // Output if condition satisfies
        if (s.size() == uniDigits.size()) {
            cout << i;
            break;
        }
    }
}

// Driver Code
int main()
{
    int n = 2019; // input the no.

    // Function Call
    nextNumberDistinctDigit(n);
    return 0;
}
```

**Output**

```
2031
```