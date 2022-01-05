# 检查非零元素的指数之间的最大差值是否大于 X

> 原文:[https://www . geeksforgeeks . org/check-如果非零元素的索引之间的最大差值大于-x/](https://www.geeksforgeeks.org/check-if-maximum-difference-between-indices-of-non-zero-elements-is-greater-than-x/)

给定一个数组 **arr[]** 和一个整数 **X** ，任务是检查非零元素的索引之间的最大差值是否大于或等于 **X**
**示例:**

> **输入:** arr[] = {1，0，1}，X = 3
> **输出:**否
> **说明:**
> 非零元素指数最大差值为 2。
> 
> **输入:** arr[] = {1，0，0，0，0，0，1}，X = 6
> **输出:**是
> **说明:**
> 非零元素指数最大差值为 6。

**方法:**想法是保持数组中最后一个非零元素的**出现，一旦有一个非零新元素，则比较最后一个出现索引和当前索引之间的距离。如果它们之间的差值大于或等于 x。然后，更新非零元素的最后一次出现，并继续检查。否则，返回 False。**

下面是上述方法的实现:

## C++

```
// C++ implementation to check that
// maximum difference of indices between
// non-zero elements if greater than X
#include<bits/stdc++.h>
using namespace std;

// Function to check that maximum 
// difference of indices between
// non-zero elements if greater than X
void findRuleFollowed(int arr[], int n, int x)
{
    int last_occur = -1;
    bool flag = true;

    // Loop to iterate over the elements 
    // of the array 
    for(int i = 0; i < n; i++)
    {

        // Condition if there is a last occured
        // non-zero element in the array
        if (arr[i] != 0 && last_occur != -1)
        {
            int diff = i - last_occur;
            if (diff >= x)
            {
                continue;
            }
            else
            {
                flag = false;
                break;
            }
        }
        else if (arr[i] != 0 && last_occur == -1)
        {
            last_occur = i;
        }
    }

    // Condition to check if the 
    // maximum difference is maintained
    if (flag)
        cout << "YES";
    else
        cout << "NO";
}

// Driver code
int main()
{
    int arr[] = { 0, 1, 0, 0, 1 };
    int n = sizeof(arr) / sizeof(0);
    int x = 3;

    // Function call
    findRuleFollowed(arr, n, x);
}

// This code is contributed by ankitkumar34
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check that
// maximum difference of indices between
// non-zero elements if greater than X
import java.util.*;

class GFG{

// Function to check that maximum
// difference of indices between
// non-zero elements if greater than X
static void findRuleFollowed(int arr[], int n, int x)
{
    int last_occur = -1;
    boolean flag = true;

    // Loop to iterate over the elements 
    // of the array 
    for(int i = 0; i < n; i++)
    {

        // Condition if there is a last occured
        // non-zero element in the array
        if (arr[i] != 0 && last_occur != -1)
        {
            int diff = i - last_occur;
            if (diff >= x)
            {
                continue;
            }
            else
            {
                flag = false;
                break;
            }
        }
        else if (arr[i] != 0 && last_occur == -1)
        {
            last_occur = i;
        }
    }

    // Condition to check if the 
    // maximum difference is maintained
    if (flag)
        System.out.println("YES");
    else
        System.out.println("NO");
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 0, 1, 0, 0, 1 };
    int n = arr.length;
    int x = 3;

    // Function call
    findRuleFollowed(arr, n, x);
}
}

// This code is contributed by ankitkumar34
```

## 蟒蛇 3

```
# Python3 implementation to check that
# maximum difference of indices between
# non-zero elements if greater than X

# Function to check that
# maximum difference of indices between
# non-zero elements if greater than X
def findRuleFollowed(arr, x):
    last_occur = -1
    flag = True

    # Loop to iterate over the elements 
    # of the array 
    for i in range(len(arr)):

        # Condition if there is a last occured
        # non-zero element in the array
        if arr[i] != 0 and last_occur != -1:
            diff = i - last_occur
            if diff >= x:
                continue
            else:
                flag = False
                break
        elif arr[i] != 0 and last_occur == -1:
            last_occur = i

    # Condition to check if the 
    # maximum difference is maintained
    if flag:
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == "__main__":
    arr = [0, 1, 0, 0, 1]
    x = 3

    # Function Call
    findRuleFollowed(arr, x)
```

## C#

```
// C# implementation to check that
// maximum difference of indices between
// non-zero elements if greater than X
using System;

class GFG{

// Function to check that maximum
// difference of indices between
// non-zero elements if greater than X
static void findRuleFollowed(int []arr, 
                             int n, int x)
{
    int last_occur = -1;
    bool flag = true;

    // Loop to iterate over the elements 
    // of the array 
    for(int i = 0; i < n; i++)
    {

        // Condition if there is a last occured
        // non-zero element in the array
        if (arr[i] != 0 && last_occur != -1)
        {
            int diff = i - last_occur;

            if (diff >= x)
            {
                continue;
            }
            else
            {
                flag = false;
                break;
            }
        }
        else if (arr[i] != 0 && last_occur == -1)
        {
            last_occur = i;
        }
    }

    // Condition to check if the 
    // maximum difference is maintained
    if (flag)
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 0, 1, 0, 0, 1 };
    int n = arr.Length;
    int x = 3;

    // Function call
    findRuleFollowed(arr, n, x);
}
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
YES

```

**时间复杂度:** O(N)