# 检查两个数组是否彼此置换

> 原文：[https://www.geeksforgeeks.org/check-if-two-arrays-are-permutations-of-each-other/](https://www.geeksforgeeks.org/check-if-two-arrays-are-permutations-of-each-other/)

给定两个相同大小的未排序数组，编写一个函数，如果两个数组彼此置换，则返回`true`，否则返回`false`。

示例：

```
Input: arr1[] = {2, 1, 3, 5, 4, 3, 2}
       arr2[] = {3, 2, 2, 4, 5, 3, 1}
Output: Yes

Input: arr1[] = {2, 1, 3, 5,}
       arr2[] = {3, 2, 2, 4}
Output: No

```

**我们强烈建议您最小化浏览器，然后自己尝试。**

一个**简单解决方案**是对两个数组都排序并比较排序后的数组。 该解决方案的时间复杂度为`O(NlogN)`

。**更好的解决方案**是使用[哈希](http://quiz.geeksforgeeks.org/hashing-set-1-introduction/)。

1.  为`arr1[]`的所有元素创建一个哈希映射，以使数组元素为键，其计数为值。

2.  遍历`arr2[]`并在哈希映射中搜索`arr2[]`的每个元素。 如果找到一个元素，则在哈希映射中减少其计数。 如果找不到，则返回`false`。

3.  如果找到了所有元素，则返回`true`。

以下是此方法的实现。

## Java

```java

// A Java program to find one array is permutation of other array
import java.util.HashMap;

class Permutaions
{
    // Returns true if arr1[] and arr2[] are permutations of each other
    static Boolean arePermutations(int arr1[], int arr2[])
    {
        // Creates an empty hashMap hM
        HashMap<Integer, Integer> hM = new HashMap<Integer, Integer>();

        // Traverse through the first array and add elements to hash map
        for (int i = 0; i < arr1.length; i++)
        {
            int x = arr1[i];
            if (hM.get(x) == null)
                hM.put(x, 1);
            else
            {
                int k = hM.get(x);
                hM.put(x, k+1);
            }
        }

        // Traverse through second array and check if every element is
        // present in hash map
        for (int i = 0; i < arr2.length; i++)
        {
            int x = arr2[i];

            // If element is not present in hash map or element
            // is not present less number of times
            if (hM.get(x) == null || hM.get(x) == 0)
                return false;

            int k = hM.get(x);
            hM.put(x, k-1);
        }
        return true;
    }

    // Driver function to test above function
    public static void main(String arg[])
    {
        int arr1[] = {2, 1, 3, 5, 4, 3, 2};
        int arr2[] = {3, 2, 2, 4, 5, 3, 1};
        if (arePermutations(arr1, arr2))
            System.out.println("Arrays are permutations of each other");
        else
            System.out.println("Arrays are NOT permutations of each other");
    }
}

```

## Python3

```py

# Python3 program to find one 
# array is permutation of other array
from collections import defaultdict

# Returns true if arr1[] and 
# arr2[] are permutations of 
# each other
def arePermutations(arr1, arr2):

    # Creates an empty hashMap hM
    hM = defaultdict (int)

    # Traverse through the first 
    # array and add elements to 
    # hash map
    for i in range (len(arr1)):

        x = arr1[i]
        hM[x] += 1

    # Traverse through second array 
    # and check if every element is
    # present in hash map
    for i in range (len(arr2)):
        x = arr2[i]

        # If element is not present 
        # in hash map or element
        # is not present less number 
        # of times
        if x not in hM or hM[x] == 0:
             return False

        hM[x] -= 1

    return True

# Driver code
if __name__ == "__main__":

    arr1 = [2, 1, 3, 5, 4, 3, 2]
    arr2 = [3, 2, 2, 4, 5, 3, 1]
    if (arePermutations(arr1, arr2)):
        print("Arrays are permutations of each other")
    else:
        print("Arrays are NOT permutations of each other")

# This code is contributed by Chitranayal

```

## C#

```cs

// C# program to find one array 
// is permutation of other array
using System;
using System.Collections.Generic; 

public class Permutaions
{
    // Returns true if arr1[] and arr2[] 
    // are permutations of each other
    static Boolean arePermutations(int []arr1, int []arr2)
    {
        // Creates an empty hashMap hM
        Dictionary<int, int> hM = new Dictionary<int, int>();

        // Traverse through the first array
        // and add elements to hash map
        for (int i = 0; i < arr1.Length; i++)
        {
            int x = arr1[i];
            if (!hM.ContainsKey(x))
                hM.Add(x, 1);
            else
            {
                int k = hM[x];
                hM.Remove(x);
                hM.Add(x, k+1);
            }
        }

        // Traverse through second array and check if every element is
        // present in hash map
        for (int i = 0; i < arr2.Length; i++)
        {
            int x = arr2[i];

            // If element is not present in hash map or element
            // is not present less number of times
            if (!hM.ContainsKey(x))
                return false;

            int k = hM[x];
            if (!hM.ContainsKey(x))
                hM.Add(x, k-1);
            else{
                int a = hM[x];
                hM.Remove(x);
                hM.Add(x, a+1);
            }
        }
        return true;
    }

    // Driver code
    public static void Main()
    {
        int []arr1 = {2, 1, 3, 5, 4, 3, 2};
        int []arr2 = {3, 2, 2, 4, 5, 3, 1};
        if (arePermutations(arr1, arr2))
            Console.WriteLine("Arrays are permutations of each other");
        else
            Console.WriteLine("Arrays are NOT permutations of each other");
    }
}

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
Arrays are permutations of each other

```

在我们有一个哈希函数在`O(1)`时间中插入并找到元素的假设下，此方法的时间复杂度为`O(n)`。

本文由 **Ravi** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请写评论.

