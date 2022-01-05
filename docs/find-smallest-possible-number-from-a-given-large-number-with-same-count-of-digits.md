# 用相同的位数从给定的大数中找出最小的可能数

> 原文:[https://www . geesforgeks . org/find-从给定的大数字中找出最小可能的数字，位数相同/](https://www.geeksforgeeks.org/find-smallest-possible-number-from-a-given-large-number-with-same-count-of-digits/)

给定一个长度为 **N** 的数字 **K** ，任务是通过任意次数的数字交换，找到由 N 个数字中的 K 个数字组成的最小可能数。

**示例:**

> **输入:** N = 15，K = 325343273113434
> **输出:**1122333334457
> **说明:**
> 交换给定数字的数字后可能的最小数字是 11223333334457
> 
> **输入:** N = 7，K = 3416781
> T3】输出: 1134678

**方法:**想法是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。为了实现散列，创建了大小为 10 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 。给定的数字被迭代，并且每个数字的出现计数被存储在散列中相应的索引处。然后迭代散列数组，并根据其频率打印带有数字的**。输出将是所需的最小 N 位数。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <iostream>
using namespace std;

// Function for finding the smallest
// possible number after swapping
// the digits any number of times
string smallestPoss(string s, int n)
{
    // Variable to store the final answer
    string ans = "";

    // Array to store the count of
    // occurrence of each digit
    int arr[10] = { 0 };

    // Loop to calculate the number
    // of occurrences of every digit
    for (int i = 0; i < n; i++) {
        arr[s[i] - 48]++;
    }

    // Loop to get smallest number
    for (int i = 0; i < 10; i++) {
        for (int j = 0; j < arr[i]; j++)
            ans = ans + to_string(i);
    }

    // Returning the answer
    return ans;
}

// Driver code
int main()
{
    int N = 15;
    string K = "325343273113434";

    cout << smallestPoss(K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function for finding the smallest
// possible number after swapping
// the digits any number of times
static String smallestPoss(String s, int n)
{
    // Variable to store the final answer
    String ans = "";

    // Array to store the count of
    // occurrence of each digit
    int arr[] = new int[10];

    // Loop to calculate the number
    // of occurrences of every digit
    for (int i = 0; i < n; i++)
    {
        arr[s.charAt(i) - 48]++;
    }

    // Loop to get smallest number
    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < arr[i]; j++)
            ans = ans + String.valueOf(i);
    }

    // Returning the answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N = 15;
    String K = "325343273113434";

    System.out.print(smallestPoss(K, N));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function for finding the smallest
# possible number after swapping
# the digits any number of times
def smallestPoss(s, n):

    # Variable to store the final answer
    ans = "";

    # Array to store the count of
    # occurrence of each digit
    arr = [0]*10;

    # Loop to calculate the number
    # of occurrences of every digit
    for i in range(n):
        arr[ord(s[i]) - 48] += 1;

    # Loop to get smallest number
    for i in range(10):
        for j in range(arr[i]):
            ans = ans + str(i);

    # Returning the answer
    return ans;

# Driver code
if __name__ == '__main__':
    N = 15;
    K = "325343273113434";

    print(smallestPoss(K, N));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function for finding the smallest
// possible number after swapping
// the digits any number of times
static String smallestPoss(String s, int n)
{
    // Variable to store the readonly answer
    String ans = "";

    // Array to store the count of
    // occurrence of each digit
    int []arr = new int[10];

    // Loop to calculate the number
    // of occurrences of every digit
    for (int i = 0; i < n; i++)
    {
        arr[s[i] - 48]++;
    }

    // Loop to get smallest number
    for (int i = 0; i < 10; i++)
    {
        for (int j = 0; j < arr[i]; j++)
            ans = ans + String.Join("",i);
    }

    // Returning the answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int N = 15;
    String K = "325343273113434";

    Console.Write(smallestPoss(K, N));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function for finding the smallest
// possible number after swapping
// the digits any number of times
function smallestPoss(s, n)
{
    // Variable to store the final answer
    var ans = "";

    // Array to store the count of
    // occurrence of each digit
    var arr = Array(10).fill(0);

    // Loop to calculate the number
    // of occurrences of every digit
    for (var i = 0; i < n; i++) {
        arr[s[i].charCodeAt(0) - 48]++;
    }

    // Loop to get smallest number
    for (var i = 0; i < 10; i++) {
        for (var j = 0; j < arr[i]; j++)
            ans = ans + i.toString();
    }

    // Returning the answer
    return ans;
}

// Driver code
var N = 15;
var K = "325343273113434";
document.write( smallestPoss(K, N));

</script>
```

**Output:** 

```
112233333344457
```