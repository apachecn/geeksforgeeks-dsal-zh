# 检查数组是否可以一次交换排序

> 原文:[https://www . geesforgeks . org/check-if-array-can-sort-with-one-swap/](https://www.geeksforgeeks.org/check-if-array-can-be-sorted-with-one-swap/)

给定一个包含 N 个元素的数组。查找是否可以使用 atmost one 交换以非递减顺序对其进行排序。
**例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** YES
> 数组已经排序
> **输入:** arr[] = {3，2，1}
> **输出:** YES
> 交换 3 和 1 得到【1，2，3】
> **输入:**arr[= { 4，1，2，3}
> **输出:【T0**

一种**简单的方法**是对数组进行排序，比较元素的所需位置和元素的当前位置。如果没有不匹配，则数组已经排序。如果正好有 2 个不匹配，我们可以交换不在位置上的项来获得排序的数组。

## C++

```
// CPP program to check if an array can be sorted
// with at-most one swap
#include <bits/stdc++.h>
using namespace std;

bool checkSorted(int n, int arr[])
{
    // Create a sorted copy of original array
    int b[n];
    for (int i = 0; i < n; i++)
        b[i] = arr[i];
    sort(b, b + n);

    // Check if 0 or 1 swap required to
    // get the sorted array
    int ct = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] != b[i])
            ct++;
    if (ct == 0 || ct == 2)
        return true;
    else
        return false;
}

// Driver Program to test above function
int main()
{
    int arr[] = {1, 5, 3, 4, 2};
    int n = sizeof(arr) / sizeof(arr[0]);
    if (checkSorted(n, arr))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if an array
// can be sorted with at-most one swap
import java.util.Arrays;

class GFG
{
static boolean checkSorted(int n, int arr[])
{
    // Create a sorted copy of original array
    int []b = new int[n];
    for (int i = 0; i < n; i++)
        b[i] = arr[i];
    Arrays.sort(b, 0, n);

    // Check if 0 or 1 swap required to
    // get the sorted array
    int ct = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] != b[i])
            ct++;
    if (ct == 0 || ct == 2)
        return true;
    else
        return false;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {1, 5, 3, 4, 2};
    int n = arr.length;
    if (checkSorted(n, arr))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# A linear Python 3 program to check
# if array becomes sorted after one swap

def checkSorted(n, arr):

    # Create a sorted copy of
    # original array
    b = []
    for i in range(n):
        b.append(arr[i])

    b.sort()

    # Check if 0 or 1 swap required
    # to get the sorted array
    ct = 0
    for i in range(n):
        if arr[i] != b[i]:
            ct += 1

    if ct == 0 or ct == 2:
        return True
    else:
        return False

# Driver Code       
if __name__ == '__main__':

    arr = [1, 5, 3, 4, 2]
    n = len(arr)

    if checkSorted(n, arr):
        print("Yes")

    else:
        print("No")

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to check if an array
// can be sorted with at-most one swap
using System;

class GFG
{
static Boolean checkSorted(int n, int []arr)
{
    // Create a sorted copy of original array
    int []b = new int[n];
    for (int i = 0; i < n; i++)
        b[i] = arr[i];
    Array.Sort(b, 0, n);

    // Check if 0 or 1 swap required to
    // get the sorted array
    int ct = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] != b[i])
            ct++;
    if (ct == 0 || ct == 2)
        return true;
    else
        return false;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {1, 5, 3, 4, 2};
    int n = arr.Length;
    if (checkSorted(n, arr))
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
// javascript program to check if an array can be sorted
// with at-most one swap
function checkSorted(n, arr)
{

    // Create a sorted copy of original array
    var b = Array(n).fill(0);
    for (var i = 0; i < n; i++)
        b[i] = arr[i];
    b.sort();

    // Check if 0 or 1 swap required to
    // get the sorted array
    var ct = 0;
    for (var i = 0; i < n; i++)
        if (arr[i] != b[i])
            ct++;
    if (ct == 0 || ct == 2)
        return true;
    else
        return false;
}

// Driver Program to test above function
var arr = [ 1, 5, 3, 4, 2 ];
var n = arr.length;
if (checkSorted(n, arr))
    document.write( "Yes");
else
    document.write("No");

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(n Log n)
一个**高效的解决方案**就是检查线性时间。让我们考虑一次交换后可能出现的不同情况。

1.  我们交换相邻的元素。例如{1，2， **3，4** ，5}变成{1，2，4，3，5}
2.  我们交换不相邻的元素。例如{1， **2** ，3，4， **5** }变成{1，5，3，4，2}

我们遍历给定的数组。对于每个元素，我们检查它是否小于前一个元素。我们计算这类事件。如果此类事件的计数超过 2，则我们不能用一次交换对数组进行排序。如果计数为 1，我们可以找到要交换的元素(较小的和它之前的)。
如果计数为 2，我们可以找到要交换的元素(第一个小的和第二个小的中的前一个)。
交换后，我们再次检查数组是否排序。我们检查这个来处理像{4，1，2，3}
这样的情况

## C++

```
// A linear CPP program to check if array becomes
// sorted after one swap
#include <bits/stdc++.h>
using namespace std;

int checkSorted(int n, int arr[])
{
    // Find counts and positions of
    // elements that are out of order.
    int first = 0, second = 0;
    int count = 0;
    for (int i = 1; i < n; i++) {
        if (arr[i] < arr[i - 1]) {
            count++;
            if (first == 0)
                first = i;
            else
                second = i;
        }
    }

    // If there are more than two elements
    // are out of order.
    if (count > 2)
        return false;

    // If all elements are sorted already
    if (count == 0)
        return true;

    // Cases like {1, 5, 3, 4, 2}
    // We swap 5 and 2.
    if (count == 2)
        swap(arr[first - 1], arr[second]);

    // Cases like {1, 2, 4, 3, 5}
    else if (count == 1)
        swap(arr[first - 1], arr[first]);

    // Now check if array becomes sorted
    // for cases like {4, 1, 2, 3}
    for (int i = 1; i < n; i++)
        if (arr[i] < arr[i - 1])
            return false;

    return true;
}

// Driver Program to test above function
int main()
{
    int arr[] = { 1, 4, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (checkSorted(n, arr))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A linear Java program to check if
// array becomes sorted after one swap
class GFG
{
static boolean checkSorted(int n, int arr[])
{
    // Find counts and positions of
    // elements that are out of order.
    int first = 0, second = 0;
    int count = 0;
    for (int i = 1; i < n; i++)
    {
        if (arr[i] < arr[i - 1])
        {
            count++;
            if (first == 0)
                first = i;
            else
                second = i;
        }
    }

    // If there are more than two elements
    // are out of order.
    if (count > 2)
        return false;

    // If all elements are sorted already
    if (count == 0)
        return true;

    // Cases like {1, 5, 3, 4, 2}
    // We swap 5 and 2.
    if (count == 2)
        swap(arr, first - 1, second);

    // Cases like {1, 2, 4, 3, 5}
    else if (count == 1)
        swap(arr, first - 1, first);

    // Now check if array becomes sorted
    // for cases like {4, 1, 2, 3}
    for (int i = 1; i < n; i++)
        if (arr[i] < arr[i - 1])
            return false;

    return true;
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 4, 3, 2 };
    int n = arr.length;
    if (checkSorted(n, arr))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# A linear Python 3 program to check
# if array becomes sorted after one swap

def checkSorted(n, arr):

    # Find counts and positions of
    # elements that are out of order.
    first, second = 0, 0
    count = 0

    for i in range(1, n):
        if arr[i] < arr[i - 1]:
            count += 1

            if first == 0:
                first = i
            else:
                second = i

    # If there are more than two elements
    # which are out of order.
    if count > 2:
        return False

    # If all elements are sorted already
    if count == 0:
        return True

    # Cases like {1, 5, 3, 4, 2}
    # We swap 5 and 2.
    if count == 2:
        (arr[first - 1],
         arr[second]) = (arr[second], 
                         arr[first - 1])

    # Cases like {1, 2, 4, 3, 5}
    elif count == 1:
        (arr[first - 1],
         arr[first]) = (arr[first],
                        arr[first - 1])

    # Now check if array becomes sorted
    # for cases like {4, 1, 2, 3}
    for i in range(1, n):
        if arr[i] < arr[i - 1]:
            return False

    return True

# Driver Code
if __name__ == '__main__':

    arr = [1, 4, 3, 2]
    n = len(arr)

    if checkSorted(n, arr):
        print("Yes")

    else:
        print("No")

# This code is contributed
# by Rituraj Jain
```

## C#

```
// A linear C# program to check if
// array becomes sorted after one swap
using System;

class GFG
{
static bool checkSorted(int n, int []arr)
{
    // Find counts and positions of
    // elements that are out of order.
    int first = 0, second = 0;
    int count = 0;
    for (int i = 1; i < n; i++)
    {
        if (arr[i] < arr[i - 1])
        {
            count++;
            if (first == 0)
                first = i;
            else
                second = i;
        }
    }

    // If there are more than two elements
    // are out of order.
    if (count > 2)
        return false;

    // If all elements are sorted already
    if (count == 0)
        return true;

    // Cases like {1, 5, 3, 4, 2}
    // We swap 5 and 2.
    if (count == 2)
        swap(arr, first - 1, second);

    // Cases like {1, 2, 4, 3, 5}
    else if (count == 1)
        swap(arr, first - 1, first);

    // Now check if array becomes sorted
    // for cases like {4, 1, 2, 3}
    for (int i = 1; i < n; i++)
        if (arr[i] < arr[i - 1])
            return false;

    return true;
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 4, 3, 2 };
    int n = arr.Length;
    if (checkSorted(n, arr))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// A linear Javascript program to check if array becomes
// sorted after one swap

function checkSorted(n, arr)
{
    // Find counts and positions of
    // elements that are out of order.
    var first = 0, second = 0;
    var count = 0;
    for (var i = 1; i < n; i++) {
        if (arr[i] < arr[i - 1]) {
            count++;
            if (first == 0)
                first = i;
            else
                second = i;
        }
    }

    // If there are more than two elements
    // are out of order.
    if (count > 2)
        return false;

    // If all elements are sorted already
    if (count == 0)
        return true;

    // Cases like {1, 5, 3, 4, 2}
    // We swap 5 and 2.
    if (count == 2)
        [arr[first - 1], arr[second]] = [arr[second], arr[first - 1]];

    // Cases like {1, 2, 4, 3, 5}
    else if (count == 1)
        [arr[first - 1], arr[first]] = [arr[first], arr[first - 1]];

    // Now check if array becomes sorted
    // for cases like {4, 1, 2, 3}
    for (var i = 1; i < n; i++)
        if (arr[i] < arr[i - 1])
            return false;

    return true;
}

// Driver Program to test above function
var arr = [1, 4, 3, 2];
var n = arr.length;
if (checkSorted(n, arr))
    document.write( "Yes");
else
    document.write( "No");

// This code is contributed by famously.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(n)
T3】练习:如何检查一个数组是否可以用两次互换排序？