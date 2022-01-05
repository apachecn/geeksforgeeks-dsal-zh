# 计数连续的相同元素对

> 原文:[https://www . geesforgeks . org/count-连续对相同元素/](https://www.geeksforgeeks.org/count-consecutive-pairs-of-same-elements/)

给定一个数组 **arr[]** ，任务是计算一对中两个元素相同的连续元素形成的对的数量。
**例:**

> **输入:** arr[] = {1，2，2，3，4，4，5，5，5，5}
> **输出:** 5
> (1，2)、(4，5)、(6，7)、(7，8)和(8，9)是连续元素相等的有效索引对
> 。
> **输入:** arr[] = {1，2，3，4，5，6，7，8，9，10}
> **输出:** 0
> 给定数组中没有两个连续的元素相等。

**方法:**初始化**计数= 0** 并遍历数组从**arr【0】**到**arr【n–2】**。如果当前元素等于数组中的下一个元素，则增加**计数**。最后打印**计数**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count of consecutive
// elements in the array which are equal
int countCon(int ar[], int n)
{
    int cnt = 0;

    for (int i = 0; i < n - 1; i++) {

        // If consecutive elements are same
        if (ar[i] == ar[i + 1])
            cnt++;
    }
    return cnt;
}

// Driver code
int main()
{
    int ar[] = { 1, 2, 2, 3, 4, 4, 5, 5, 5, 5 };
    int n = sizeof(ar) / sizeof(ar[0]);
    cout << countCon(ar, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GfG
{

    // Function to return the count of consecutive
    // elements in the array which are equal
    static int countCon(int ar[], int n)
    {
        int cnt = 0;

        for (int i = 0; i < n - 1; i++)
        {

            // If consecutive elements are same
            if (ar[i] == ar[i + 1])
                cnt++;
        }
        return cnt;
    }

    // Driver Code
    public static void main(String []args){

        int ar[] = { 1, 2, 2, 3, 4, 4, 5, 5, 5, 5 };
        int n = ar.length;
        System.out.println(countCon(ar, n));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of consecutive
# elements in the array which are equal
def countCon(ar, n):
    cnt = 0

    for i in range(n - 1):

        # If consecutive elements are same
        if (ar[i] == ar[i + 1]):
            cnt += 1

    return cnt

# Driver code
ar = [1, 2, 2, 3, 4,
      4, 5, 5, 5, 5]
n = len(ar)
print(countCon(ar, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to return the count of consecutive
    // elements in the array which are equal
    static int countCon(int[] ar, int n)
    {
        int cnt = 0;

        for (int i = 0; i < n - 1; i++)
        {

            // If consecutive elements are same
            if (ar[i] == ar[i + 1])
                cnt++;
        }
        return cnt;
    }

    // Driver Code
    public static void Main()
    {

        int[] ar = { 1, 2, 2, 3, 4, 4, 5, 5, 5, 5 };
        int n = ar.Length;
        Console.WriteLine(countCon(ar, n));
    }
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of consecutive
// elements in the array which are equal
function countCon($ar, $n)
{
    $cnt = 0;

    for ($i = 0; $i < $n - 1; $i++)
    {

        // If consecutive elements are same
        if ($ar[$i] == $ar[$i + 1])
            $cnt++;
    }
    return $cnt;
}

// Driver code
$ar = array(1, 2, 2, 3, 4, 4, 5, 5, 5, 5);
$n = sizeof($ar);
echo countCon($ar, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

    // Function to return the count of consecutive
    // elements in the array which are equal
    function countCon(ar,n)
    {
        let cnt = 0;

        for (let i = 0; i < n - 1; i++)
        {

            // If consecutive elements are same
            if (ar[i] == ar[i + 1])
                cnt++;
        }
        return cnt;
    }

    // Driver Code
    let ar = [1, 2, 2, 3, 4, 4, 5, 5, 5, 5 ];
    let n = ar.length;
    document.write(countCon(ar, n));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
5
```