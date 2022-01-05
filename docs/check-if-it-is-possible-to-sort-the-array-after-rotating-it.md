# 旋转数组后检查是否可以排序

> 原文:[https://www . geeksforgeeks . org/check-如果有可能对旋转后的阵列进行排序/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-sort-the-array-after-rotating-it/)

给定一个大小为 N 的数组，任务是确定是否可以只通过一次洗牌来对数组进行排序。在一次洗牌中，我们可以从数组的末尾转移一些连续的元素，并将其放在数组的前面。
**为例:**

> 1.  A = {2 2,3,1,2}, we can sort by moving {1,2} from the end of the array to the front of the array.
> 2.  A = {1 1,2,3,2} We can't sort the array because we can't sort it in one shuffle.

**例:**

```
Input: arr[] = {1, 2, 3, 4} 
Output: Possible 
Since this array is already sorted hence no need for shuffle.

Input: arr[] = {6, 8, 1, 2, 5}
Output: Possible
Place last three elements at the front 
in the same order i.e. {1, 2, 5, 6, 8}
```

**进场:**

1.  检查数组是否已经排序。如果是，返回真。
2.  否则开始遍历数组元素，直到当前元素小于下一个元素。存储索引，其中 arr[i] > arr[i+1]。
3.  从该点开始遍历，检查索引元素是否按递增顺序排列。
4.  如果满足以上两个条件，则检查最后一个元素是否小于或等于给定数组的第一个元素。
5.  如果满足上述三个条件，则打印“可能”，否则如果上述三个条件中的任何一个失败，则打印“不可能”。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
bool isPossible(int a[], int n)
{
    // step 1
    if (is_sorted(a, a + n)) {
        cout << "Possible" << endl;
    }

    else {

        // break where a[i] > a[i+1]
        bool flag = true;
        int i;
        for (i = 0; i < n - 1; i++) {
            if (a[i] > a[i + 1]) {
                break;
            }
        }
        // break point + 1
        i++;

        // check whether the sequence is
        // further increasing or not
        for (int k = i; k < n - 1; k++) {
            if (a[k] > a[k + 1]) {
                flag = false;
                break;
            }
        }

        // If not increasing after break point
        if (!flag)
            return false;

        else {

            // last element <= First element
            if (a[n - 1] <= a[0])
                return true;

            else
                return false;
        }
    }
}

// Driver code
int main()
{

    int arr[] = { 3, 1, 2, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (isPossible(arr, n))
        cout << "Possible";

    else
        cout << "Not Possible";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class solution
{
    //check if array is sorted
static boolean is_sorted(int a[],int n)
{
    int c1=0,c2=0;
    //if array is ascending
    for(int i=0;i<n-1;i++)
    {
        if(a[i]<=a[i+1])
        c1++;
    }

    //if array is descending
    for(int i=1;i<n;i++)
    {
        if(a[i]<=a[i-1])
        c2++;
    }
    if(c1==n||c2==n)
    return true;

    return false;
}
// Function to check if it is possible
static boolean isPossible(int a[], int n)
{
    // step 1
    if (is_sorted(a,n)) {
        System.out.println("Possible");
    }

    else {

        // break where a[i] > a[i+1]
        boolean flag = true;
        int i;
        for (i = 0; i < n - 1; i++) {
            if (a[i] > a[i + 1]) {
                break;
            }
        }
        // break point + 1
        i++;

        // check whether the sequence is
        // further increasing or not
        for (int k = i; k < n - 1; k++) {
            if (a[k] > a[k + 1]) {
                flag = false;
                break;
            }
        }

        // If not increasing after break point
        if (!flag)
            return false;

        else {

            // last element <= First element
            if (a[n - 1] <= a[0])
                return true;

            else
                return false;
        }
    }
    return false;
}

// Driver code
public static void main(String[] args)
{

    int arr[] = { 3, 1, 2, 2, 3 };
    int n = arr.length;

    if (isPossible(arr, n))
        System.out.println("Possible");

    else
        System.out.println("Not Possible");

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach
def is_sorted(a):
    all(a[i] <= a[i + 1]
    for i in range(len(a) - 1))

# Function to check if
# it is possible
def isPossible(a, n):

    # step 1
    if (is_sorted(a)) :
        print("Possible")

    else :

        # break where a[i] > a[i+1]
        flag = True
        for i in range(n - 1) :
            if (a[i] > a[i + 1]) :
                break

        # break point + 1
        i += 1

        # check whether the sequence is
        # further increasing or not
        for k in range(i, n - 1) :
            if (a[k] > a[k + 1]) :
                flag = False
                break

        # If not increasing after
        # break point
        if (not flag):
            return False

        else :

            # last element <= First element
            if (a[n - 1] <= a[0]):
                return True

            else:
                return False

# Driver code
if __name__ == "__main__":

    arr = [ 3, 1, 2, 2, 3 ]
    n = len(arr)

    if (isPossible(arr, n)):
        print("Possible")

    else:
        print("Not Possible")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;
class GFG
{
// check if array is sorted
static bool is_sorted(int []a, int n)
{
    int c1 = 0, c2 = 0;

    // if array is ascending
    for(int i = 0; i < n - 1; i++)
    {
        if(a[i] <= a[i + 1])
        c1++;
    }

    // if array is descending
    for(int i = 1; i < n; i++)
    {
        if(a[i] <= a[i - 1])
        c2++;
    }
    if(c1 == n || c2 == n)
    return true;

    return false;
}

// Function to check if it is possible
static bool isPossible(int []a, int n)
{
    // step 1
    if (is_sorted(a,n))
    {
        Console.WriteLine("Possible");
    }

    else
    {

        // break where a[i] > a[i+1]
        bool flag = true;
        int i;
        for (i = 0; i < n - 1; i++)
        {
            if (a[i] > a[i + 1])
            {
                break;
            }
        }

        // break point + 1
        i++;

        // check whether the sequence is
        // further increasing or not
        for (int k = i; k < n - 1; k++)
        {
            if (a[k] > a[k + 1])
            {
                flag = false;
                break;
            }
        }

        // If not increasing after
        // break point
        if (!flag)
            return false;

        else
        {

            // last element <= First element
            if (a[n - 1] <= a[0])
                return true;

            else
                return false;
        }
    }
    return false;
}

// Driver code
public static void Main()
{

    int []arr = { 3, 1, 2, 2, 3 };
    int n = arr.Length;

    if (isPossible(arr, n))
        Console.WriteLine("Possible");

    else
        Console.WriteLine("Not Possible");
}
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of
// above approach

// Function to check if
// it is possible
function is_sorted($a, $n)
{
    $c1 = 0; $c2 = 0;

    // if array is ascending
    for($i = 0; $i < $n - 1; $i++)
    {
        if($a[$i] <= $a[$i + 1])
        $c1++;
    }

    // if array is descending
    for($i = 1; $i < $n; $i++)
    {
        if($a[$i] <= $a[$i - 1])
        $c2++;
    }

    if($c1 == $n || $c2 == $n)
    return true;

    return false;
}

function isPossible($a, $n)
{
    // step 1
    if (is_sorted($a, $n))
    {
        echo "Possible" . "\n";
    }

    else
    {

        // break where a[i] > a[i+1]
        $flag = true;
        $i;
        for ($i = 0; $i < $n - 1; $i++)
        {
            if ($a[$i] > $a[$i + 1])
            {
                break;
            }
        }

        // break point + 1
        $i++;

        // check whether the sequence is
        // further increasing or not
        for ($k = $i; $k < $n - 1; $k++)
        {
            if ($a[$k] > $a[$k + 1])
            {
                $flag = false;
                break;
            }
        }

        // If not increasing after
        // break point
        if (!$flag)
            return false;

        else
        {

            // last element <= First element
            if ($a[$n - 1] <= $a[0])
                return true;

            else
                return false;
        }
    }
}

// Driver code
$arr = array( 3, 1, 2, 2, 3 );
$n = sizeof($arr);

if (isPossible($arr, $n))
    echo "Possible";
else
    echo "Not Possible";

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above approach 
// check if array is sorted
    function is_sorted(a)
    {
        let c1=0,c2=0;
        // if array is ascending
        for(let i=0;i<n-1;i++)
        {
            if(a[i]<=a[i+1])
            {
                c1++;
            }
        }
        // if array is descending
        for(let i=1;i<n;i++)
        {
            if(a[i]<=a[i-1])
                c2++;
        }
        if(c1==n||c2==n)
        {
            return true;
        }
        return false;
    }
    // Function to check if it is possible
    function isPossible(a,n)
    {
        // step 1
        if (is_sorted(a,n))
        {
            document.write("Possible");   
        }
        else
        {
            // break where a[i] > a[i+1]
            let flag = true;
            let i;
            for (i = 0; i < n - 1; i++)
            {
                if (a[i] > a[i + 1])
                {
                    break;
                }
            }
            // break point + 1 
            i++;
            // check whether the sequence is 
            // further increasing or not 
            for (let k = i; k < n - 1; k++)
            {
                if (a[k] > a[k + 1])
                {
                    flag = false; 
                    break;
                }
            }
            // If not increasing after break point 
            if (!flag) 
            {
                return false;
            }
            else
            {
                // last element <= First element 
                if (a[n - 1] <= a[0]) 
                    return true; 

                else
                    return false; 
            }
        }

        return false;
    }
    // Driver code 
    let arr=[3, 1, 2, 2, 3];
    let n = arr.length;
    if(isPossible(arr, n))
        document.write("Possible");
    else
        document.write("Not Possible");

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Possible
```