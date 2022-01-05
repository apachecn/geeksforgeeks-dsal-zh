# 一个数组中的双毕达哥拉斯三元组

> 原文:[https://www . geesforgeks . org/twin-毕达哥拉斯-数组中的三元组/](https://www.geeksforgeeks.org/twin-pythagorean-triplets-in-an-array/)

给定一个整数数组 **arr[]** ，任务是检查数组中是否有**双勾股三元组**。

> A **孪生毕达哥拉斯三元组**是一个毕达哥拉斯三元组(a，b，c)，其中两个值是连续的整数。前几个双胞胎三联体是(3，4，5)，(5，12，13)，(7，24，25)，(20，21，29)，(9，40，41)，(11，60，61)，(13，84，85)，(15，112，113)，…。

**示例**:

> **输入** : arr[] = {3，1，4，6，5}
> **输出**:真
> **说明:**
> 有一个孪生毕达哥拉斯三元组(3，4，5)
> 
> **输入** : arr[] = {6，8，10}
> **输出** : False
> **解释:**
> 6<sup>2</sup>+8<sup>2</sup>= 10<sup>2</sup>
> 但在(6，8，10)中没有连续的元素。
> 所以不存在孪生毕达哥拉斯三元组。

**天真方法:**一个简单的解决方案是运行三个循环，三个循环挑选三个数组元素，并检查当前的三个元素是否形成一个孪生毕达哥拉斯三元组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if there exist
// a twin pythagorean triplet in
// the given array
bool isTriplet(int ar[], int n)
{
    // Loop to check if there is a
    // Pythagorean triplet in the array
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            for (int k = j + 1; k < n; k++) {

                // Check if there is
                // consecutive triple
                if (abs(ar[i] - ar[j]) == 1
                    || abs(ar[j] - ar[k]) == 1
                    || abs(ar[i] - ar[k]) == 1) {

                    // Calculate square of
                    // array elements
                    int x = ar[i] * ar[i],
                        y = ar[j] * ar[j],
                        z = ar[k] * ar[k];

                    if (x == y + z
                        || y == x + z
                        || z == x + y)
                        return true;
                }
            }
        }
    }

    return false;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 1, 4, 6, 5 };
    int ar_size = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    isTriplet(arr, ar_size)
        ? cout << "Yes"
        : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if there exist
// a twin pythagorean triplet in
// the given array
static boolean isTriplet(int ar[], int n)
{

    // Loop to check if there is a
    // Pythagorean triplet in the array
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {
            for(int k = j + 1; k < n; k++)
            {

                // Check if there is
                // consecutive triple
                if (Math.abs(ar[i] - ar[j]) == 1 ||
                    Math.abs(ar[j] - ar[k]) == 1 ||
                    Math.abs(ar[i] - ar[k]) == 1)
                {

                    // Calculate square of
                    // array elements
                    int x = ar[i] * ar[i],
                        y = ar[j] * ar[j],
                        z = ar[k] * ar[k];

                    if (x == y + z ||
                        y == x + z ||
                        z == x + y)
                        return true;
                }
            }
        }
    }
    return false;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 3, 1, 4, 6, 5 };
    int ar_size = arr.length;

    // Function call
    if(isTriplet(arr, ar_size))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if there exist
# a twin pythagorean triplet in
# the given array
def isTriplet(ar, n):

    # Loop to check if there is a
    # Pythagorean triplet in the array
    for i in range(n):
        for j in range(i + 1, n):
            for k in range(j + 1, n):

                # Check if there is
                # consecutive triple
                if (abs(ar[i] - ar[j]) == 1 or
                    abs(ar[j] - ar[k]) == 1 or
                    abs(ar[i] - ar[k]) == 1):

                        # Calculate square of
                        # array elements
                        x = ar[i] * ar[i]
                        y = ar[j] * ar[j]
                        z = ar[k] * ar[k]

                        if (x == y + z or
                            y == x + z or
                            z == x + y):
                            return True

    return False

# Driver Code
if __name__=='__main__':

    # Given array arr[]
    arr = [ 3, 1, 4, 6, 5 ]
    ar_size = len(arr)

    # Function call
    if isTriplet(arr, ar_size):
        print('Yes')
    else:
        print('No')

# This code is contributed by rutvik_56   
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if there exist
// a twin pythagorean triplet in
// the given array
static bool isTriplet(int []ar, int n)
{

    // Loop to check if there is a
    // Pythagorean triplet in the array
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {
            for(int k = j + 1; k < n; k++)
            {

                // Check if there is
                // consecutive triple
                if (Math.Abs(ar[i] - ar[j]) == 1 ||
                    Math.Abs(ar[j] - ar[k]) == 1 ||
                    Math.Abs(ar[i] - ar[k]) == 1)
                {

                    // Calculate square of
                    // array elements
                    int x = ar[i] * ar[i],
                        y = ar[j] * ar[j],
                        z = ar[k] * ar[k];

                    if (x == y + z ||
                        y == x + z ||
                        z == x + y)
                        return true;
                }
            }
        }
    }
    return false;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 3, 1, 4, 6, 5 };
    int ar_size = arr.Length;

    // Function call
    if(isTriplet(arr, ar_size))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if there exist
// a twin pythagorean triplet in
// the given array
function isTriplet(ar, n)
{
    // Loop to check if there is a
    // Pythagorean triplet in the array
    for (var i = 0; i < n; i++) {
        for (var j = i + 1; j < n; j++) {

            for (var k = j + 1; k < n; k++) {

                // Check if there is
                // consecutive triple
                if (Math.abs(ar[i] - ar[j]) == 1
                    || Math.abs(ar[j] - ar[k]) == 1
                    || Math.abs(ar[i] - ar[k]) == 1) {

                    // Calculate square of
                    // array elements
                    var x = ar[i] * ar[i],
                        y = ar[j] * ar[j],
                        z = ar[k] * ar[k];

                    if (x == y + z
                        || y == x + z
                        || z == x + y)
                        return true;
                }
            }
        }
    }

    return false;
}

// Driver Code

// Given array arr[]
var arr = [ 3, 1, 4, 6, 5 ];
var ar_size = arr.length;

// Function Call
isTriplet(arr, ar_size)
    ? document.write( "Yes")
    : document.write( "No");

// This code is contributed by itsok.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(N<sup>3</sup>)*
**辅助村:** *O(1)*

**有效方法:**

*   求输入数组中每个元素的平方。这一步需要 O(n)个时间。
*   按递增顺序对方形数组进行排序。这一步需要 0(nLogn)时间。
*   要找到一个三元组(a，b，c)，使得**a<sup>2</sup>= b<sup>2</sup>+c<sup>2</sup>**和至少一对是连续的，请执行以下操作。
    *   将“a”固定为排序数组的最后一个元素。
    *   现在搜索子数组中第一个元素和“a”之间的对(b，c)。使用本文方法 1 中讨论的中间相遇算法，可以在 O(n)时间内找到给定和的一对(b，c)。
    *   如果没有找到当前“a”的配对，则将“a”向后移动一个位置，并重复上一步。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to check if any of the
// two numbers are consecutive
// in the given triplet
bool isConsective(int a, int b, int c)
{
    return abs(a - b) == 1
           || abs(b - c) == 1
           || abs(c - a) == 1;
}

// Function to check if there exist a
// pythagorean triplet in the array
bool isTriplet(int arr[], int n)
{

    // Square array elements
    for (int i = 0; i < n; i++)
        arr[i] = arr[i] * arr[i];

    // Sort array elements
    sort(arr, arr + n);

    // Now fix one element one by one
    // and find the other two elements
    for (int i = n - 1; i >= 2; i--) {

        // To find the other two elements,
        // start two index variables from
        // two corners of the array and move
        // them toward each other
        int l = 0;
        int r = i - 1;

        while (l < r) {

            // A triplet found
            if (arr[l] + arr[r] == arr[i]
                && isConsective(sqrt(arr[l]),
                                sqrt(arr[r]),
                                sqrt(arr[i]))) {

                return true;
            }

            // Else either move 'l' or 'r'
            (arr[l] + arr[r] < arr[i])
                ? l++
                : r--;
        }
    }

    // If we reach here,
    // then no triplet found
    return false;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 1, 4, 6, 5 };
    int arr_size = sizeof(arr)
                   / sizeof(arr[0]);

    // Function Call
    isTriplet(arr, arr_size)
        ? cout << "Yes"
        : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if any of the
// two numbers are consecutive
// in the given triplet
static boolean isConsective(int a, int b, int c)
{
    return Math.abs(a - b) == 1 ||
           Math.abs(b - c) == 1 ||
           Math.abs(c - a) == 1;
}

// Function to check if there exist a
// pythagorean triplet in the array
static boolean isTriplet(int arr[], int n)
{

    // Square array elements
    for(int i = 0; i < n; i++)
        arr[i] = arr[i] * arr[i];

    // Sort array elements
    Arrays.sort(arr);

    // Now fix one element one by one
    // and find the other two elements
    for(int i = n - 1; i >= 2; i--)
    {

        // To find the other two elements,
        // start two index variables from
        // two corners of the array and move
        // them toward each other
        int l = 0;
        int r = i - 1;

        while (l < r)
        {

            // A triplet found
            if (arr[l] + arr[r] == arr[i] &&
                isConsective((int)Math.sqrt(arr[l]),
                             (int)Math.sqrt(arr[r]),
                             (int)Math.sqrt(arr[i])))
            {
                return true;
            }

            // Else either move 'l' or 'r'
            if(arr[l] + arr[r] < arr[i])
                l++;
            else
                r--;
        }
    }

    // If we reach here,
    // then no triplet found
    return false;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 3, 1, 4, 6, 5 };
    int arr_size = arr.length;

    // Function call
    if(isTriplet(arr, arr_size))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if any of the
# two numbers are consecutive
# in the given triplet
def isConsective(a, b, c):

    return bool(abs(a - b) == 1 or
                abs(b - c) == 1 or
                abs(c - a) == 1)

# Function to check if there exist a
# pythagorean triplet in the array
def isTriplet(arr, n):

    # Square array elements
    for i in range(n):
        arr[i] = arr[i] * arr[i]

    # Sort array elements
    arr.sort()

    # Now fix one element one by one
    # and find the other two elements
    for i in range(n - 1, 1, -1):

        # To find the other two elements,
        # start two index variables from
        # two corners of the array and move
        # them toward each other
        l = 0
        r = i - 1

        while (l < r):

            # A triplet found
            if (arr[l] + arr[r] == arr[i] and
                isConsective(math.sqrt(arr[l]),
                             math.sqrt(arr[r]),
                             math.sqrt(arr[i]))):

                return bool(True)

            # Else either move 'l' or 'r'
            if(arr[l] + arr[r] < arr[i]):
                l = l + 1
            else:
                r = r - 1

    # If we reach here,
    # then no triplet found
    return bool(False)

# Driver code

# Given array arr[]
arr = [ 3, 1, 4, 6, 5 ]
arr_size = len(arr)

# Function call
if(isTriplet(arr, arr_size)):
    print("Yes")
else:
    print("No")

# This code is contributed divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if any of the
// two numbers are consecutive
// in the given triplet
static bool isConsective(int a, int b, int c)
{
    return Math.Abs(a - b) == 1 ||
           Math.Abs(b - c) == 1 ||
           Math.Abs(c - a) == 1;
}

// Function to check if there exist a
// pythagorean triplet in the array
static bool isTriplet(int []arr, int n)
{

    // Square array elements
    for(int i = 0; i < n; i++)
        arr[i] = arr[i] * arr[i];

    // Sort array elements
    Array.Sort(arr);

    // Now fix one element one by one
    // and find the other two elements
    for(int i = n - 1; i >= 2; i--)
    {

        // To find the other two elements,
        // start two index variables from
        // two corners of the array and move
        // them toward each other
        int l = 0;
        int r = i - 1;

        while (l < r)
        {

            // A triplet found
            if (arr[l] + arr[r] == arr[i] &&
                isConsective((int)Math.Sqrt(arr[l]),
                             (int)Math.Sqrt(arr[r]),
                             (int)Math.Sqrt(arr[i])))
            {
                return true;
            }

            // Else either move 'l' or 'r'
            if(arr[l] + arr[r] < arr[i])
                l++;
            else
                r--;
        }
    }

    // If we reach here,
    // then no triplet found
    return false;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 3, 1, 4, 6, 5 };
    int arr_size = arr.Length;

    // Function call
    if(isTriplet(arr, arr_size))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to check if any of the
// two numbers are consecutive
// in the given triplet
function isConsective( a, b, c){
    return Math.abs(a - b) == 1
           || Math.abs(b - c) == 1
           || Math.abs(c - a) == 1;
}

// Function to check if there exist a
// pythagorean triplet in the array
function isTriplet( arr, n){
    // Square array elements
    for (let i = 0; i < n; i++)
        arr[i] = arr[i] * arr[i];

    // Sort array elements
    arr.sort(function(a, b){return a - b});

    // Now fix one element one by one
    // and find the other two elements
    for (let i = n - 1; i >= 2; i--) {

        // To find the other two elements,
        // start two index variables from
        // two corners of the array and move
        // them toward each other
        let l = 0;
        let r = i - 1;

        while (l < r) {

            // A triplet found
            if (arr[l] + arr[r] == arr[i]
                && isConsective(Math.sqrt(arr[l]),
                                Math.sqrt(arr[r]),
                                Math.sqrt(arr[i]))) {

                return true;
            }

            // Else either move 'l' or 'r'
            (arr[l] + arr[r] < arr[i])
                ? l++
                : r--;
        }
    }

    // If we reach here,
    // then no triplet found
    return false;
}

// Driver Code
// Given array arr[]
let arr = [ 3, 1, 4, 6, 5 ];
let arr_size = arr.length;

// Function Call
isTriplet(arr, arr_size)
        ?document.write( "Yes")
        : document.write( "No");
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(N<sup>2</sup>)*
**辅助空间:** *O(1)*