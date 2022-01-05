# 最小周期的周期二进制串和给定的二进制串作为子序列。

> 原文:[https://www . geesforgeks . org/periodic-binary-string-with-minimum-periodic-string-and-给定的二进制字符串作为子序列/](https://www.geeksforgeeks.org/periodic-binary-string-with-minimum-period-and-a-given-binary-string-as-subsequence/)

**周期二进制串**:如果一个二进制串可以写成长度更小或相同的二进制串的重复，那么这个二进制串就叫做周期串。例如，101010 是一个周期为 10 的周期二进制字符串，因为我们可以通过重复向它本身附加 10 来获得该字符串。一般来说，字符串 **S** 带句号 **P** 表示，S <sub>i</sub> 等于 S<sub>I+</sub>**<sub>P</sub>**。

问题:给定一个二进制字符串 **S** ，任务是在以下附加条件下找到具有最小可能周期的**周期**字符串
1)给定的字符串 S 应该是结果的子序列
2)结果的长度不应该超过输入字符串长度的两倍。

**示例:**

> **输入:** S = "01"
> **输出:** 0101
> **说明:**输出字符串的周期为 2，给定字符串为子序列。
> 
> **输入:**S = " 111 "
> T3】输出:111
> T6】说明:输出字符串的周期为 1。
> 
> **输入:** S = "110"
> **输出:** 101010
> **说明:**输出字符串的周期为 2，给定字符串为子序列。请注意，110110 不是答案，因为周期较长。

**进场:**
主要思路取决于两种可能:

1.  如果字符串由全 1 或全 0 组成，则答案是给定字符串 **S** 本身的周期为 **1** 。
2.  如果字符串由不同的元素组成，找到周期为 **2** 的字符串，其长度为给定字符串 **S** 长度的两倍

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation to find the
// periodic string with minimum period
#include <bits/stdc++.h>
using namespace std;

// Function to find the periodic string
// with minimum period
void findPeriodicString(string S)
{
    int l = 2 * S.length();

    int count = 0;
    for (int i = 0; i < S.length(); i++) {
        if (S[i] == '1')
            count++;
    }

    // Print the string S if it
    // consists of similar elements
    if (count == S.length() || count == 0)
        cout << S << "\n";

    // Find the required periodic
    // string with period 2
    else {
        char arr[l];
        for (int i = 0; i < l; i += 2) {
            arr[i] = '1';
            arr[i + 1] = '0';
        }

        for (int i = 0; i < l; i++)
            cout << arr[i];
        cout << "\n";
    }
}

// Driver Code
int main()
{
    string S = "1111001";
    findPeriodicString(S);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation to find the
// periodic string with minimum period
class GFG{

// Function to find the periodic string
// with minimum period
static void findPeriodicString(String S)
{
    int l = 2 * S.length();
    int count = 0;

    for(int i = 0; i < S.length(); i++)
    {
        if (S.charAt(i) == '1')
            count++;
    }

    // Print the string S if it
    // consists of similar elements
    if (count == S.length() || count == 0)
        System.out.println(S);

    // Find the required periodic
    // string with period 2
    else
    {
        char arr[] = new char[l];
        for(int i = 0; i < l; i += 2)
        {
            arr[i] = '1';
            arr[i + 1] = '0';
        }

        for(int i = 0; i < l; i++)
            System.out.print(arr[i]);
        System.out.println();
    }
}

// Driver Code
public static void main (String[] args)
{
    String S = "1111001";

    findPeriodicString(S);
}
}

// This code is contributed by chitranayal
```

## **蟒蛇 3**

```
# Python3 implementation to find the
# periodic with minimum period

# Function to find the periodic string
# with minimum period
def findPeriodicString(S):
    l = 2 * len(S)

    count = 0
    for i in range(len(S)):
        if (S[i] == '1'):
            count += 1

    # Print the S if it
    # consists of similar elements
    if (count == len(S) or count == 0):
        print(S)

    # Find the required periodic
    # with period 2
    else:
        arr = ['0']*l
        for i in range(0, l, 2):
            arr[i] = '1'
            arr[i + 1] = '0'

        for i in range(l):
            print(arr[i],end="")

# Driver Code
if __name__ == '__main__':
    S = "1111001"
    findPeriodicString(S)

# This code is contributed by mohit kumar 29 
```

## **C#**

```
// C# implementation to find the
// periodic string with minimum period
using System;

class GFG{

// Function to find the periodic string
// with minimum period
static void findPeriodicString(string S)
{
    int l = 2 * S.Length;
    int count = 0;

    for(int i = 0; i < S.Length; i++)
    {
        if (S[i] == '1')
            count++;
    }

    // Print the string S if it
    // consists of similar elements
    if (count == S.Length || count == 0)
        Console.WriteLine(S);

    // Find the required periodic
    // string with period 2
    else
    {
        char[] arr = new char[l];
        for(int i = 0; i < l; i += 2)
        {
            arr[i] = '1';
            arr[i + 1] = '0';
        }

        for(int i = 0; i < l; i++)
            Console.Write(arr[i]);

        Console.WriteLine();
    }
}

// Driver code
public static void Main ()
{
    string S = "1111001";

    findPeriodicString(S);
}
}

// This code is contributed by sanjoy_62
```

## **java 描述语言**

```
<script>

// Javascript implementation to find the
// periodic string with minimum period

// Function to find the periodic string
// with minimum period
function findPeriodicString(S)
{
    let l = 2 * S.length;
    let count = 0;

    for(let i = 0; i < S.length; i++)
    {
        if (S[i] == '1')
            count++;
    }

    // Print the string S if it
    // consists of similar elements
    if (count == S.length || count == 0)
        document.write(S + "<br>");

    // Find the required periodic
    // string with period 2
    else
    {
        let arr = new Array(l);
        for(let i = 0; i < l; i += 2)
        {
            arr[i] = '1';
            arr[i + 1] = '0';
        }

        for(let i = 0; i < l; i++)
            document.write(arr[i]);

        document.write("<br>");
    }
}

// Driver Code
let S = "1111001";
findPeriodicString(S);

// This code is contributed by avanitrachhadiya2155

</script>
```

****Output:** 

```
10101010101010
```** 

****时间复杂度:** O(N)**