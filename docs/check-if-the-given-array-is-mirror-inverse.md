# 检查给定阵列是否镜像反转

> 原文:[https://www . geesforgeks . org/check-如果给定的阵列是镜像反转的/](https://www.geeksforgeeks.org/check-if-the-given-array-is-mirror-inverse/)

给定一个数组 **arr[]** ，任务是找出该数组是否镜像反转。数组的逆意味着如果数组元素与其对应的索引交换，并且数组的逆等于其本身，则该数组称为镜像逆。如果阵列为镜像反转，则打印**是**否则打印**否**。
**举例:**

> **输入:**arr[]=【3，4，2，0，1}
> **输出:**是
> 在给定数组中:
> 索引(0)—>值(3)
> 索引(1)—>值(4)
> 索引(2)—>值(2)
> 索引(3)—>值(0)
> 索引(4)—>值(1)
> 找到
> 索引(3)—>值(0)
> 索引(4)—>值(1)
> 索引(2)—>值(2)
> 索引(0)—>值(3)
> 索引(1)—>值(4)
> 逆 arr[] = {3，4，2，0，1}
> 所以，逆数组等于给定数组。
> **输入:** arr[] = {1，2，3，0}
> **输出:**否

一种简单的方法是通过交换给定数组的值和索引来创建一个新数组，并检查新数组是否等于原始数组。
一个**更好的方法**是遍历数组，对于所有的索引，如果满足 **arr[arr[index]] = index** ，那么给定的数组是镜像逆的。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function that returns true if
// the array is mirror-inverse
bool isMirrorInverse(int arr[], int n)
{
    for (int i = 0; i < n; i++)
    {

        // If condition fails for any element
        if (arr[arr[i]] != i)
            return false;
    }

    // Given array is mirror-inverse
    return true;
}

// Driver code
int main()
{
        int arr[] = { 1, 2, 3, 0 };
        int n = sizeof(arr)/sizeof(arr[0]);
        if (isMirrorInverse(arr,n))
            cout << "Yes";
        else
            cout << "No";
        return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function that returns true if
    // the array is mirror-inverse
    static boolean isMirrorInverse(int arr[])
    {
        for (int i = 0; i < arr.length; i++) {

            // If condition fails for any element
            if (arr[arr[i]] != i)
                return false;
        }

        // Given array is mirror-inverse
        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 0 };
        if (isMirrorInverse(arr))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if
# the array is mirror-inverse
def isMirrorInverse(arr, n) :

    for i in range(n) :

        # If condition fails for any element
        if (arr[arr[i]] != i) :
            return False;

    # Given array is mirror-inverse
    return true;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 0 ];

    n = len(arr) ;
    if (isMirrorInverse(arr,n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if
    // the array is mirror-inverse
    static bool isMirrorInverse(int []arr)
    {
        for (int i = 0; i < arr.Length; i++)
        {

            // If condition fails for any element
            if (arr[arr[i]] != i)
                return false;
        }

        // Given array is mirror-inverse
        return true;
    }

    // Driver code
    static public void Main ()
    {
        int []arr = { 1, 2, 3, 0 };
        if (isMirrorInverse(arr))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by ajit...
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if
// the array is mirror-inverse
function isMirrorInverse($arr)
{
    for ($i = 0; $i < sizeof($arr); $i++)
    {

        // If condition fails for any element
        if ($arr[$arr[$i]] != $i)
            return false;
    }

    // Given array is mirror-inverse
    return true;
}

// Driver code
$arr = array(1, 2, 3, 0);
if (isMirrorInverse($arr))
    echo("Yes");
else
    echo("No");

// These code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function that returns true if
    // the array is mirror-inverse
    function isMirrorInverse(arr) {
        for (i = 0; i < arr.length; i++) {

            // If condition fails for any element
            if (arr[arr[i]] != i)
                return false;
        }

        // Given array is mirror-inverse
        return true;
    }

    // Driver code

        var arr = [ 1, 2, 3, 0 ];
        if (isMirrorInverse(arr))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
No
```