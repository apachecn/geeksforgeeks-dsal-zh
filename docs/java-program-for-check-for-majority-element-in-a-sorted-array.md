# 用于检查排序数组中多数元素的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-check-多数元素在排序数组中/](https://www.geeksforgeeks.org/java-program-for-check-for-majority-element-in-a-sorted-array/)

**问题:**写一个函数，找出给定的整数 x 在 n 个整数的排序数组中出现的次数是否超过 n/2 次。
基本上，我们需要编写一个函数，比如 isMajority()，该函数以数组(arr[])、数组大小(n)和要搜索的数字(x)为参数，如果 x 是[多数元素](https://www.geeksforgeeks.org/majority-element/)(出现次数超过 n/2 次)，则返回 true。

**示例:**

```
Input: arr[] = {1, 2, 3, 3, 3, 3, 10}, x = 3
Output: True (x appears more than n/2 times in the given array)

Input: arr[] = {1, 1, 2, 4, 4, 4, 6, 6}, x = 4
Output: False (x doesn't appear more than n/2 times in the given array)

Input: arr[] = {1, 1, 1, 2, 2}, x = 1
Output: True (x appears more than n/2 times in the given array)
```

**方法 1(使用线性搜索)**
线性搜索元素的第一次出现，一旦找到它(让在索引 I 处)，检查索引 i + n/2 处的元素。如果 i+n/2 处存在元素，则返回 1，否则返回 0。

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Program to check for majority element in a sorted array */
import java.io.*;

class Majority {

    static boolean isMajority(int arr[], int n, int x)
    {
        int i, last_index = 0;

        /* get last index according to n (even or odd) */
        last_index = (n%2==0)? n/2: n/2+1;

        /* search for first occurrence of x in arr[]*/
        for (i = 0; i < last_index; i++)
        {
            /* check if x is present and is present more
               than n/2 times */
            if (arr[i] == x && arr[i+n/2] == x)
                return true;
        }
        return false;
    }

    /* Driver function to check for above functions*/
    public static void main (String[] args) {
        int arr[] = {1, 2, 3, 4, 4, 4, 4};
        int n = arr.length;
        int x = 4;
        if (isMajority(arr, n, x)==true)
           System.out.println(x+" appears more than "+
                              n/2+" times in arr[]");
        else
           System.out.println(x+" does not appear more than "+
                              n/2+" times in arr[]");
    }
}
/*This article is contributed by Devesh Agrawal*/
```

**输出:**

```
4 appears more than 3 times in arr[]
```

**时间复杂度:** O(n)

**方法 2(使用二分搜索法)**
使用二分搜索法方法找到给定数字的第一个出现。二分搜索法的标准在这里很重要。

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java Program to check for majority element in a sorted array */
import java.io.*;

class Majority {

    /* If x is present in arr[low...high] then returns the index of
        first occurrence of x, otherwise returns -1 */
    static int  _binarySearch(int arr[], int low, int high, int x)
    {
        if (high >= low)
        {
            int mid = (low + high)/2;  /*low + (high - low)/2;*/

            /* Check if arr[mid] is the first occurrence of x.
                arr[mid] is first occurrence if x is one of the following
                is true:
                (i)  mid == 0 and arr[mid] == x
                (ii) arr[mid-1] < x and arr[mid] == x
            */
            if ( (mid == 0 || x > arr[mid-1]) && (arr[mid] == x) )
                return mid;
            else if (x > arr[mid])
                return _binarySearch(arr, (mid + 1), high, x);
            else
                return _binarySearch(arr, low, (mid -1), x);
        }

        return -1;
    }

    /* This function returns true if the x is present more than n/2
        times in arr[] of size n */
    static boolean isMajority(int arr[], int n, int x)
    {
        /* Find the index of first occurrence of x in arr[] */
        int i = _binarySearch(arr, 0, n-1, x);

        /* If element is not present at all, return false*/
        if (i == -1)
            return false;

        /* check if the element is present more than n/2 times */
        if (((i + n/2) <= (n -1)) && arr[i + n/2] == x)
            return true;
        else
            return false;
    }

    /*Driver function to check for above functions*/
    public static void main (String[] args)  {

        int arr[] = {1, 2, 3, 3, 3, 3, 10};
        int n = arr.length;
        int x = 3;
        if (isMajority(arr, n, x)==true)
            System.out.println(x + " appears more than "+
                              n/2 + " times in arr[]");
        else
            System.out.println(x + " does not appear more than " +
                              n/2 + " times in arr[]");
    }
}
/*This code is contributed by Devesh Agrawal*/
```

**输出:**

```
3 appears more than 3 times in arr[]
```

**时间复杂度:** O(Logn)
**算法范式:**分而治之

**方法 3:** 如果已经给定数组已排序并且存在多数元素，那么检查某个特定元素是否像检查数组的中间元素是否是我们要检查的数字一样简单。

由于多数元素在数组中出现的次数超过 n/2 次，因此它将始终是中间元素。我们可以使用这个逻辑来检查给定的数字是否是多数元素。

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

static boolean isMajorityElement(int arr[], int n, 
                                 int key)
{
    if (arr[n / 2] == key)
        return true;
    else
        return false;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 3, 3, 3, 10 };
    int n = arr.length;
    int x = 3;

    if (isMajorityElement(arr, n, x))
        System.out.printf("%d appears more than %d " +
                          "times in arr[]", x, n / 2);
    else
        System.out.printf("%d does not appear more " +
                          "than %d times in " + "arr[]",
                          x, n / 2);
}
}

// This code is contributed by aashish1995
```

**Output**

```
3 appears more than 3 times in arr[]
```

***时间复杂度** : O(1)*
***辅助空间:** O(1)*

更多细节请参考完整的文章[检查排序数组](https://www.geeksforgeeks.org/check-for-majority-element-in-a-sorted-array/)中的多数元素！