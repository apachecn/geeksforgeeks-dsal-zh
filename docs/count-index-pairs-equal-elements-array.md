# 数组中元素相等的索引对的计数

> 原文:[https://www . geesforgeks . org/count-index-pairs-equal-elements-array/](https://www.geeksforgeeks.org/count-index-pairs-equal-elements-array/)

给定一组 **n 个**元素。任务是计算索引(I，j)的总数，使得 arr[i] = arr[j]和 i < j
**示例:**

```
Input : arr[] = {1, 1, 2}
Output : 1
As arr[0] = arr[1], the pair of indices is (0, 1)

Input : arr[] = {1, 1, 1}
Output : 3
As arr[0] = arr[1], the pair of indices is (0, 1), 
(0, 2) and (1, 2)

Input : arr[] = {1, 2, 3}
Output : 0
```

**方法 1(蛮力):**
对于每个索引 I，在其后查找与 arr[i]值相同的元素。以下是本办法的实施情况:

## C++

```
// C++ program to count of pairs with equal
// elements in an array.
#include<bits/stdc++.h>
using namespace std;

// Return the number of pairs with equal
// values.
int countPairs(int arr[], int n)
{
    int ans = 0;

    // for each index i and j
    for (int i = 0; i < n; i++)
        for (int j = i+1; j < n; j++)

            // finding the index with same
            // value but different index.
            if (arr[i] == arr[j])
                ans++;
    return ans;
}

// Driven Program
int main()
{
    int arr[] = { 1, 1, 2 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << countPairs(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of pairs with equal
// elements in an array.
class GFG {

    // Return the number of pairs with equal
    // values.
    static int countPairs(int arr[], int n)
    {
        int ans = 0;

        // for each index i and j
        for (int i = 0; i < n; i++)
            for (int j = i+1; j < n; j++)

                // finding the index with same
                // value but different index.
                if (arr[i] == arr[j])
                    ans++;
        return ans;
    }

    //driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 1, 2 };
        int n = arr.length;

        System.out.println(countPairs(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to
# count of pairs with equal
# elements in an array.

# Return the number of
# pairs with equal values.
def countPairs(arr, n):

    ans = 0

    # for each index i and j
    for i in range(0 , n):
        for j in range(i + 1, n):

            # finding the index
            # with same value but
            # different index.
            if (arr[i] == arr[j]):
                ans += 1
    return ans

# Driven Code
arr = [1, 1, 2 ]
n = len(arr)
print(countPairs(arr, n))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to count of pairs with equal
// elements in an array.
using System;

class GFG {

    // Return the number of pairs with equal
    // values.
    static int countPairs(int []arr, int n)
    {
        int ans = 0;

        // for each index i and j
        for (int i = 0; i < n; i++)
            for (int j = i+1; j < n; j++)

                // finding the index with same
                // value but different index.
                if (arr[i] == arr[j])
                    ans++;
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 1, 1, 2 };
        int n = arr.Length;

        Console.WriteLine(countPairs(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count of
// pairs with equal elements
// in an array.

// Return the number of pairs
// with equal values.
function countPairs( $arr, $n)
{
    $ans = 0;

    // for each index i and j
    for ( $i = 0; $i < $n; $i++)
        for ( $j = $i + 1; $j < $n; $j++)

            // finding the index with same
            // value but different index.
            if ($arr[$i] == $arr[$j])
                $ans++;
    return $ans;
}

// Driven Code
$arr = array( 1, 1, 2 );
$n = count($arr);
echo countPairs($arr, $n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to count of pairs with equal
// elements in an array.

    // Return the number of pairs with equal
    // values.
    function countPairs(arr, n)
    {
        let ans = 0;

        // for each index i and j
        for (let i = 0; i < n; i++)
            for (let j = i+1; j < n; j++)

                // finding the index with same
                // value but different index.
                if (arr[i] == arr[j])
                    ans++;
        return ans;
    }

// Driver code   

    let arr = [ 1, 1, 2 ];
    let n = arr.length;

    document.write(countPairs(arr, n));

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
1
```

时间复杂度:O(n)<sup>2</sup>)
**方法 2(高效途径):**
思路是统计每个数字出现的频率，然后找出元素相等的对的个数。假设一个数字 x 在索引 i <sub>1</sub> 出现 k 次，i <sub>2</sub> ，…。，i <sub>k</sub> 。然后选择任意两个指数 i <sub>x</sub> 和 i <sub>y</sub> ，它们将被计为 1 对。同样，i <sub>y</sub> 和 i <sub>x</sub> 也可以配对。所以，选择 <sup>n</sup> C <sub>2</sub> 是对的数量，这样 arr[i] = arr[j] = x.
下面是这个方法的实现:

## C++

```
// C++ program to count of index pairs with
// equal elements in an array.
#include<bits/stdc++.h>
using namespace std;

// Return the number of pairs with equal
// values.
int countPairs(int arr[], int n)
{
    unordered_map<int, int> mp;

    // Finding frequency of each number.
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    // Calculating pairs of each value.
    int ans = 0;
    for (auto it=mp.begin(); it!=mp.end(); it++)
    {
        int count = it->second;
        ans += (count * (count - 1))/2;
    }

    return ans;
}

// Driven Program
int main()
{
    int arr[] = {1, 1, 2};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << countPairs(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count of index pairs with
// equal elements in an array.
import java.util.*;

class GFG {

    public static int countPairs(int arr[], int n)
    {
        //A method to return number of pairs with
        // equal values

        HashMap<Integer,Integer> hm = new HashMap<>();

        // Finding frequency of each number.
        for(int i = 0; i < n; i++)
        {
        if(hm.containsKey(arr[i]))
            hm.put(arr[i],hm.get(arr[i]) + 1);
        else
            hm.put(arr[i], 1);
        }
        int ans=0;

        // Calculating count of pairs with equal values
        for(Map.Entry<Integer,Integer> it : hm.entrySet())
        {
            int count = it.getValue();
            ans += (count * (count - 1)) / 2;
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = new int[]{1, 2, 3, 1};
        System.out.println(countPairs(arr,arr.length));
    }
}

// This Code is Contributed
// by Adarsh_Verma
```

## 蟒蛇 3

```
# Python3 program to count of index pairs
# with equal elements in an array.
import math as mt

# Return the number of pairs with
# equal values.
def countPairs(arr, n):

    mp = dict()

    # Finding frequency of each number.
    for i in range(n):
        if arr[i] in mp.keys():
            mp[arr[i]] += 1
        else:
            mp[arr[i]] = 1

    # Calculating pairs of each value.
    ans = 0
    for it in mp:
        count = mp[it]
        ans += (count * (count - 1)) // 2
    return ans

# Driver Code
arr = [1, 1, 2]
n = len(arr)
print(countPairs(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count of index pairs with
// equal elements in an array.
using System;
using System.Collections.Generic;

class GFG
{

    // Return the number of pairs with
    // equal values.
    public static int countPairs(int []arr, int n)
    {
        // A method to return number of pairs
        // with equal values
        Dictionary<int,
                   int> hm = new Dictionary<int,
                                            int>();

        // Finding frequency of each number.
        for(int i = 0; i < n; i++)
        {
            if(hm.ContainsKey(arr[i]))
            {
                int a = hm[arr[i]];
                hm.Remove(arr[i]);
                hm.Add(arr[i], a + 1);
            }
            else
                hm.Add(arr[i], 1);
        }
        int ans = 0;

        // Calculating count of pairs with
        // equal values
        foreach(var it in hm)
        {
            int count = it.Value;
            ans += (count * (count - 1)) / 2;
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = new int[]{1, 2, 3, 1};
        Console.WriteLine(countPairs(arr,arr.Length));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to count of index pairs with
// equal elements in an array.

    function countPairs(arr,n)
    {
        //A method to return number of pairs with
        // equal values

        let hm = new Map();

        // Finding frequency of each number.
        for(let i = 0; i < n; i++)
        {
        if(hm.has(arr[i]))
            hm.set(arr[i],hm.get(arr[i]) + 1);
        else
            hm.set(arr[i], 1);
        }
        let ans=0;

        // Calculating count of pairs with equal values
        for(let [key, value] of hm.entries())
        {
            let count = value;
            ans += (count * (count - 1)) / 2;
        }
        return ans;
    }

    // Driver code
    let arr=[1, 2, 3, 1];
    document.write(countPairs(arr,arr.length));

// This code is contributed by patel2127
</script>
```

**输出:**

```
1
```

**时间复杂度:** O(n)
**来源**:
[http://stackoverflow . com/questions/26772364/arr # comment 42124861 _ 26772516](http://stackoverflow.com/questions/26772364/efficient-algorithm-for-counting-number-of-pairs-of-identical-elements-in-an-arr#comment42124861_26772516)
本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。