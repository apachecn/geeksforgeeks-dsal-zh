# 给定数字 N 的偶数和的最小奇数

> 原文:[https://www . geeksforgeeks . org/给定数字 n 的最小奇数和偶数/](https://www.geeksforgeeks.org/smallest-odd-number-with-even-sum-of-digits-from-the-given-number-n/)

以弦**弦**的形式给出一个大数。任务是通过从给定字符串 **str** 中删除零个或多个字符来找到数字总和为偶数的最小奇数，在这里可以重新排列数字。

**示例**

> **输入:** str = "15470"
> **输出:** 15
> **说明:**
> 两个最小的奇数位为 1 & 5。因此所需的数字是 15。
> 
> **输入:** str = "124"
> **输出:** -1
> **说明:**
> 除 1 外没有最小的奇数位。因此所需的数字不能是形式。

**进场:**
仔细观察，凭直觉可以理解，最小可能奇数的位数是 2。这个数字中的每个数字都是奇数，因为两个奇数的总和总是偶数。因此，解决这个问题的想法是迭代给定的字符串，并将每个奇数存储在一个数组中。这个数组可以排序，前两个数字一起形成最小的奇数，其数字之和为偶数。

下面是上述方法的实现。

## C++

```
// C++ program to find the smallest odd number
// with even sum of digits from the given number N
#include<bits/stdc++.h>
using namespace std;

// Function to find the smallest odd number
// whose sum of digits is even from the given string
int smallest(string s)
{
    // Converting the given string
    // to a list of digits
    vector<int> a(s.length());
    for(int i = 0; i < s.length(); i++)
        a[i] = s[i]-'0';

    // An empty array to store the digits
    vector<int> b;

    // For loop to iterate through each digit
    for(int i = 0; i < a.size(); i++)
    {

        // If the given digit is odd then
        // the digit is appended to the array b
        if((a[i]) % 2 != 0)
            b.push_back(a[i]);
    }

    // Sorting the list of digits
    sort(b.begin(),b.end());

    // If the size of the list is greater than 1
    // then a 2 digit smallest odd number is returned
    // Since the sum of two odd digits is always even
    if(b.size() > 1)
        return (b[0])*10 + (b[1]);

    // Else, -1 is returned
    return -1;
}

// Driver code
int main()
{
    cout << (smallest("15470"));
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest
// odd number with even sum of digits
// from the given number N
import java.util.*;
class GFG{

// Function to find the smallest
// odd number whose sum of digits
// is even from the given string
public static int smallest(String s)
{

    // Converting the given string
    // to a list of digits
    int[] a = new int[s.length()];
    for(int i = 0; i < s.length(); i++)
        a[i] = s.charAt(i) - '0';

    // An empty array to store the digits
    Vector<Integer> b = new Vector<Integer>();

    // For loop to iterate through each digit
    for(int i = 0; i < a.length; i++)
    {

        // If the given digit is odd
        // then the digit is appended
        // to the array b
        if(a[i] % 2 != 0)
            b.add(a[i]);
    }

    // Sorting the list of digits
    Collections.sort(b);

    // If the size of the list is greater
    // than 1 then a 2 digit smallest odd
    // number is returned. Since the sum
    // of two odd digits is always even
    if(b.size() > 1)
        return (b.get(0)) * 10 + (b.get(1));

    // Else, -1 is returned
    return -1;
}

// Driver code
public static void main(String[] args)
{
    System.out.print(smallest("15470"));
}
}

// This code is contributed by divyeshrabadiya07
```

## 计算机编程语言

```
# Python program to find the smallest odd number
# with even sum of digits from the given number N

# Function to find the smallest odd number
# whose sum of digits is even from the given string
def smallest(s):

    # Converting the given string
    # to a list of digits
    a = list(s)

    # An empty array to store the digits
    b = []

    # For loop to iterate through each digit
    for i in range(len(a)):

        # If the given digit is odd then
        # the digit is appended to the array b
        if(int(a[i])%2 != 0):
            b.append(a[i])

    # Sorting the list of digits
    b = sorted(b)

    # If the size of the list is greater than 1
    # then a 2 digit smallest odd number is returned
    # Since the sum of two odd digits is always even
    if(len(b)>1):
        return int(b[0])*10 + int(b[1])

    # Else, -1 is returned   
    return -1

# Driver code
if __name__ == "__main__":
    print(smallest("15470"))
```

## C#

```
// C# program to find the smallest
// odd number with even sum of digits
// from the given number N
using System;
using System.Collections;

class GFG{

// Function to find the smallest
// odd number whose sum of digits
// is even from the given string
public static int smallest(string s)
{

    // Converting the given string
    // to a list of digits
    int[] a = new int[s.Length];

    for(int i = 0; i < s.Length; i++)
        a[i] = (int)(s[i] - '0');

    // An empty array to store the digits
    ArrayList b = new ArrayList();

    // For loop to iterate through each digit
    for(int i = 0; i < a.Length; i++)
    {

        // If the given digit is odd
        // then the digit is appended
        // to the array b
        if (a[i] % 2 != 0)
            b.Add(a[i]);
    }

    // Sorting the list of digits
    b.Sort();

    // If the size of the list is greater
    // than 1 then a 2 digit smallest odd
    // number is returned. Since the sum
    // of two odd digits is always even
    if (b.Count > 1)
        return ((int)b[0] * 10 + (int)b[1]);

    // Else, -1 is returned
    return -1;
}

// Driver code
public static void Main(string[] args)
{
    Console.Write(smallest("15470"));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to find the
// smallest odd number with even
// sum of digits from the given number N

// Function to find the smallest odd
// number whose sum of digits is even
// from the given string
function smallest(s)
{

    // Converting the given string
    // to a list of digits
    var a = Array(s.length);
    for(var i = 0; i < s.length; i++)
        a[i] = s[i].charCodeAt(0) -
                '0'.charCodeAt(0);

    // An empty array to store the digits
    var b = [];

    // For loop to iterate through each digit
    for(var i = 0; i < a.length; i++)
    {

        // If the given digit is odd then
        // the digit is appended to the array b
        if ((a[i]) % 2 != 0)
            b.push(a[i]);
    }

    // Sorting the list of digits
    b.sort((a, b) => a - b);

    // If the size of the list is greater
    // than 1 then a 2 digit smallest odd
    // number is returned. Since the sum
    // of two odd digits is always even
    if (b.length > 1)
        return (b[0]) * 10 + (b[1]);

    // Else, -1 is returned
    return -1;
}

// Driver code
document.write(smallest("15470"));

// This code is contributed by importantly

</script>
```

**Output:** 

```
15
```

**时间复杂度:** O(N)，其中 N =字符串长度。