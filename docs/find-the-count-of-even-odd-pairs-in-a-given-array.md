# 求给定数组中偶奇对的个数

> 原文:[https://www . geeksforgeeks . org/find-给定数组中奇偶对的计数/](https://www.geeksforgeeks.org/find-the-count-of-even-odd-pairs-in-a-given-array/)

给定一个数组 **arr[]** ，任务是找出数组中的奇偶对的个数。
**例:**

> **输入:** arr[] = { 1，2，1，3 }
> **输出:** 2
> **解释:**
> 该形式的 2 对(偶数，奇数)为{2，1}和{2，3 }。
> 
> **输入:** arr[] = { 5，4，1，2，3}
> **输出:** 3

**天真方法:**

1.  运行两个嵌套循环来获取数组中所有可能的数字对。
2.  对于每对，检查 a[i]是否为偶数，a[j]是否为奇数。
3.  如果是，则将所需计数增加 1。
4.  检查完所有对后，最后打印计数。

下面是上述方法的实现:

## C++

```
// C++ program to count the pairs in array
// of the form (even, odd)

#include <bits/stdc++.h>
using namespace std;

// Function to count the pairs in array
// of the form (even, odd)
int findCount(int arr[], int n)
{
    // variable to store count of such pairs
    int res = 0;

    // Iterate through all pairs
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)

            // Increment count
            // if condition is satisfied
            if ((arr[i] % 2 == 0)
                && (arr[j] % 2 == 1)) {
                res++;
            }

    return res;
}

// Driver code
int main()
{
    int a[] = { 5, 4, 1, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << findCount(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the pairs in array
// of the form (even, odd)
import java.util.*;

class GFG{

// Function to count the pairs in array
// of the form (even, odd)
static int findCount(int arr[], int n)
{
    // Variable to store count of such pairs
    int res = 0;

    // Iterate through all pairs
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)

            // Increment count
            // if condition is satisfied
            if ((arr[i] % 2 == 0) &&
                (arr[j] % 2 == 1))
            {
                res++;
            }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 5, 4, 1, 2, 3 };
    int n = a.length;
    System.out.print(findCount(a, n));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to count the pairs
# in array of the form (even, odd)

# Function to count the pairs in 
# array of the form (even, odd)
def findCount(arr, n):

    # Variable to store count
    # of such pairs
    res = 0

    # Iterate through all pairs
    for i in range(0, n - 1):
        for j in range(i + 1, n):

            # Increment count
            # if condition is satisfied
            if ((arr[i] % 2 == 0) and
                (arr[j] % 2 == 1)):
                res = res + 1

    return res

# Driver code
a = [ 5, 4, 1, 2, 3 ]
n = len(a)

print(findCount(a, n))

# This code is contributed by PratikBasu
```

## C#

```
// C# program to count the pairs in array
// of the form (even, odd)
using System;

class GFG{

// Function to count the pairs in array
// of the form (even, odd)
static int findCount(int []arr, int n)
{

    // Variable to store count of such pairs
    int res = 0;

    // Iterate through all pairs
    for(int i = 0; i < n - 1; i++)
       for(int j = i + 1; j < n; j++)

          // Increment count
          // if condition is satisfied
          if ((arr[i] % 2 == 0) &&
              (arr[j] % 2 == 1))
          {
              res++;
          }

    return res;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 5, 4, 1, 2, 3 };
    int n = a.Length;

    Console.Write(findCount(a, n));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program to count the pairs in array
// of the form (even, odd)

// Function to count the pairs in array
// of the form (even, odd)
function findCount(arr, n)
{
    // variable to store count of such pairs
    let res = 0;

    // Iterate through all pairs
    for (let i = 0; i < n - 1; i++)
        for (let j = i + 1; j < n; j++)

            // Increment count
            // if condition is satisfied
            if ((arr[i] % 2 == 0)
                && (arr[j] % 2 == 1)) {
                res++;
            }

    return res;
}

// Driver code
let a = [ 5, 4, 1, 2, 3 ];
let n = a.length;
document.write(findCount(a, n));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(n <sup>2</sup> )*

***辅助空间:** O(1)*

**有效方法:**

1.  对于从索引 0 开始的每个元素，我们将检查它是否为偶数。
2.  如果是偶数，我们将计数增加 1。
3.  否则我们将通过计数来增加最终答案。

下面是上述方法的实现:

## C++

```
// C++ program to count the pairs in array
// of the form (even, odd)

#include <bits/stdc++.h>
using namespace std;

// Function to count the pairs in array
// of the form (even, odd)
int findCount(int arr[], int n)
{
    int count = 0, ans = 0;
    for (int i = 0; i < n; i++) {

        // check if number is even or not
        if (arr[i] % 2 == 0)
            count++;
        else
            ans = ans + count;
    }
    return ans;
}

// Driver code
int main()
{
    int a[] = { 5, 4, 1, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << findCount(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the pairs
// in array of the form (even, odd)
class GFG{

// Function to count the pairs in 
// array of the form (even, odd)
static int findCount(int arr[], int n)
{
    int count = 0, ans = 0;
    for(int i = 0; i < n; i++)
    {

       // Check if number is even
       // or not
       if (arr[i] % 2 == 0)
       {
           count++;
       }
       else
       {
           ans = ans + count;
       }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 5, 4, 1, 2, 3 };
    int n = a.length;

    System.out.print(findCount(a, n));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to count the pairs
# in array of the form (even, odd)

# Function to count the pairs in
# array of the form (even, odd)
def findCount(arr, n):

    count = 0
    ans = 0

    for i in range(0, n):

        # Check if number is even or not
        if (arr[i] % 2 == 0):
            count = count + 1
        else:
            ans = ans + count

    return ans

# Driver code
a = [ 5, 4, 1, 2, 3 ]
n = len(a)

print(findCount(a, n))

# This code is contributed by PratikBasu
```

## C#

```
// C# program to count the pairs in
// array of the form (even, odd)
using System;

class GFG{

// Function to count the pairs in
// array of the form (even, odd)
static int findCount(int []arr, int n)
{
    int count = 0, ans = 0;
    for(int i = 0; i < n; i++)
    {

       // Check if number is even or not
       if (arr[i] % 2 == 0)
       {
           count++;  
       }
       else
       {
           ans = ans + count;
       }
    }
    return ans;
}

// Driver code
public static void Main()
{
    int []a = { 5, 4, 1, 2, 3 };
    int n = a.Length;

    Console.WriteLine(findCount(a, n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript program to count the pairs in array
// of the form (even, odd)

// Function to count the pairs in array
// of the form (even, odd)
function findCount(arr, n)
{
    let count = 0, ans = 0;
    for (let i = 0; i < n; i++) {

        // check if number is even or not
        if (arr[i] % 2 == 0)
            count++;
        else
            ans = ans + count;
    }
    return ans;
}

// Driver code
let a = [ 5, 4, 1, 2, 3 ];
let n = a.length;
document.write(findCount(a, n));

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*