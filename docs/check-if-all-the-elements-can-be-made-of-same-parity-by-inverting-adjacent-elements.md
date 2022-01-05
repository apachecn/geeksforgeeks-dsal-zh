# 通过反转相邻元素来检查所有元素是否可以由相同的奇偶校验构成

> 原文:[https://www . geeksforgeeks . org/check-if-all-the-elements-可以通过反转相邻元素来制造相同的奇偶校验/](https://www.geeksforgeeks.org/check-if-all-the-elements-can-be-made-of-same-parity-by-inverting-adjacent-elements/)

给定一个二元矩阵。在单个操作中，您可以选择两个相邻的元素并反转它们的奇偶性。该操作可以执行任意次数。写一个程序来检查数组的所有元素是否可以转换成一个奇偶校验。
**例:**

> **输入:** a[] = {1，0，1，1，0，1}
> **输出:**是
> 将第二个和第三个元素反相得到{1，1，0，1，0，1}
> 将第三个和第四个元素反相得到{1，1，1，0，1}
> 将第四个和第五个元素反相得到{1，1，1，1，1}
> **输入:** a[] = {1，1，1

**方法:**由于只需要翻转相邻的元素，因此奇偶数将给出问题的答案。一次只有偶数个元素被翻转，所以如果两个奇偶性的计数都是奇数，那么就不可能使所有的奇偶性都相同，否则就有可能。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if parity
// can be made same or not
bool flipsPossible(int a[], int n)
{

    int count_odd = 0, count_even = 0;

    // Iterate and count the parity
    for (int i = 0; i < n; i++) {

        // Odd
        if (a[i] & 1)
            count_odd++;

        // Even
        else
            count_even++;
    }

    // Condition check
    if (count_odd % 2 && count_even % 2)
        return false;

    else
        return true;
}

// Drivers code
int main()
{
    int a[] = { 1, 0, 1, 1, 0, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    if (flipsPossible(a, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG
{

    // Function to check if parity
    // can be made same or not
    static boolean flipsPossible(int []a, int n)
    {

        int count_odd = 0, count_even = 0;

        // Iterate and count the parity
        for (int i = 0; i < n; i++)
        {

            // Odd
            if ((a[i] & 1) == 1)
                count_odd++;

            // Even
            else
                count_even++;
        }

        // Condition check
        if (count_odd % 2 == 1 && count_even % 2 == 1)
            return false;

        else
            return true;
    }

    // Drivers code
    public static void main (String[] args)
    {
        int []a = { 1, 0, 1, 1, 0, 1 };
        int n = a.length;

        if (flipsPossible(a, n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to check if parity
# can be made same or not
def flipsPossible(a, n) :

    count_odd = 0; count_even = 0;

    # Iterate and count the parity
    for i in range(n) :

        # Odd
        if (a[i] & 1) :
            count_odd += 1;

        # Even
        else :
            count_even += 1;

    # Condition check
    if (count_odd % 2 and count_even % 2) :
        return False;
    else :
        return True;

# Driver Code
if __name__ == "__main__" :

    a = [ 1, 0, 1, 1, 0, 1 ];

    n = len(a);

    if (flipsPossible(a, n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to check if parity
    // can be made same or not
    static bool flipsPossible(int []a, int n)
    {

        int count_odd = 0, count_even = 0;

        // Iterate and count the parity
        for (int i = 0; i < n; i++)
        {

            // Odd
            if ((a[i] & 1) == 1)
                count_odd++;

            // Even
            else
                count_even++;
        }

        // Condition check
        if (count_odd % 2 == 1 && count_even % 2 == 1)
            return false;

        else
            return true;
    }

    // Drivers code
    public static void Main(String[] args)
    {
        int []a = { 1, 0, 1, 1, 0, 1 };
        int n = a.Length;

        if (flipsPossible(a, n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to check if parity
// can be made same or not
function flipsPossible(a, n){

    let count_odd = 0;
    let count_even = 0;

    // Iterate and count the parity
    for (let i = 0; i < n; i++)
    {

        // Odd
        if ((a[i] & 1) == 1)
            count_odd++;
        // Even
        else
            count_even++;
    }

    // Condition check
    if (count_odd % 2 == 1 && count_even % 2 == 1)
        return false;
    else
        return true;
}

// Drivers code

let a = [1, 0, 1, 1, 0, 1];
let n = a.length;

if (flipsPossible(a, n))
    document.write("Yes");
else
    document.write("No");

</script>
```

**Output**

```
Yes
```

**时间复杂度:** O(N)

**辅助空间:** O(1)