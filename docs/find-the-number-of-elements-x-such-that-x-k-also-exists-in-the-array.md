# 求元素 X 的个数，使得 X + K 也存在于数组中

> 原文:[https://www . geesforgeks . org/find-元素数量-x-so-x-k-也存在于数组中/](https://www.geeksforgeeks.org/find-the-number-of-elements-x-such-that-x-k-also-exists-in-the-array/)

给定一个**数组 a[]和一个整数 k** ，求该数组中元素 x 的个数，使得 x 和 k 的和也存在于该数组中。
**例:**

```
Input:  { 3, 6, 2, 8, 7, 6, 5, 9 } and k = 2
Output: 5 
Explanation:
Elements {3, 6, 7, 6, 5} in this array have x + 2 value that is
{5, 8, 9, 8, 7} present in this array.

Input:  { 1, 2, 3, 4, 5} and k = 1
Output: 4
Explanation:
Elements {1, 2, 3, 4} in this array have x + 2 value that is
{2, 3, 4, 5} present in this array.
```

这个问题类似于[求数组](https://www.geeksforgeeks.org/given-an-array-a-and-a-number-x-check-for-pair-in-a-with-sum-as-x/)中给定和的对的个数。
**天真的方法:**
解决上面提到的问题我们可以使用蛮力的方法并找到结果。迭代两个循环，检查数组中的每个 x 是否存在 x+2。如果存在，则增加计数，最后返回计数。
**高效方法:**
解决问题的高效方法是使用一个 HashMap，Map 中的键会作为这个数组中唯一的元素，对应的值会告诉我们这个元素的出现频率。
迭代该图，并为该图中的每个键 x 找到键 x + k 是否存在于该图中，如果存在，则将该频率添加到答案中，即对于该元素 x，我们在该数组中有 x+k。最后，返回答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of find number
// of elements x in this array
// such x+k also present in this array.
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// count of element x such that
// x+k also lies in this array
int count_element(int N, int K, int* arr)
{
    // Key in map will store elements
    // and value will store the
    // frequency of the elements
    map<int, int> mp;

    for (int i = 0; i < N; ++i)
        mp[arr[i]]++;

    int answer = 0;

    for (auto i : mp) {

        // Find if i.first + K is
        // present in this map or not
        if (mp.find(i.first + K) != mp.end())

            // If we find i.first or key + K in this map
            // then we have to increase in answer
            // the frequency of this element
            answer += i.second;
    }

    return answer;
}

// Driver code
int main()
{
    // array initialisation
    int arr[] = { 3, 6, 2, 8, 7, 6, 5, 9 };

    // size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // initialise k
    int K = 2;

    cout << count_element(N, K, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of find number
// of elements x in this array
// such x+k also present in this array.
import java.util.*;

class GFG{

// Function to return the
// count of element x such that
// x+k also lies in this array
static int count_element(int N, int K, int[] arr)
{
    // Key in map will store elements
    // and value will store the
    // frequency of the elements
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    for (int i = 0; i < N; ++i)
        if(mp.containsKey(arr[i])){
            mp.put(arr[i], mp.get(arr[i])+1);
        }else{
            mp.put(arr[i], 1);
    }

    int answer = 0;

    for (Map.Entry<Integer,Integer> i : mp.entrySet()) {

        // Find if i.first + K is
        // present in this map or not
        if (mp.containsKey(i.getKey() + K) )

            // If we find i.first or key + K in this map
            // then we have to increase in answer
            // the frequency of this element
            answer += i.getValue();
    }

    return answer;
}

// Driver code
public static void main(String[] args)
{
    // array initialisation
    int arr[] = { 3, 6, 2, 8, 7, 6, 5, 9 };

    // size of array
    int N = arr.length;

    // initialise k
    int K = 2;

    System.out.print(count_element(N, K, arr));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of find number
# of elements x in this array
# such x+k also present in this array.

# Function to return the
# count of element x such that
# x+k also lies in this array
def count_element(N, K, arr):

    # Key in map will store elements
    # and value will store the
    # frequency of the elements
    mp = dict()

    for i in range(N):
        mp[arr[i]] = mp.get(arr[i], 0) + 1

    answer = 0

    for i in mp:

        # Find if i.first + K is
        # present in this map or not
        if i + K in mp:

            # If we find i.first or key + K in this map
            # then we have to increase in answer
            # the frequency of this element
            answer += mp[i]

    return answer

# Driver code
if __name__ == '__main__':
    # array initialisation
    arr=[3, 6, 2, 8, 7, 6, 5, 9]

    # size of array
    N = len(arr)

    # initialise k
    K = 2

    print(count_element(N, K, arr))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# implementation of find number
// of elements x in this array
// such x+k also present in this array.
using System;
using System.Collections.Generic;

public class GFG{

// Function to return the
// count of element x such that
// x+k also lies in this array
static int count_element(int N, int K, int[] arr)
{
    // Key in map will store elements
    // and value will store the
    // frequency of the elements
    Dictionary<int,int> mp = new Dictionary<int,int>();

    for (int i = 0; i < N; ++i)
        if(mp.ContainsKey(arr[i])){
            mp[arr[i]] = mp[arr[i]]+1;
        }else{
            mp.Add(arr[i], 1);
    }

    int answer = 0;

    foreach (KeyValuePair<int,int> i in mp) {

        // Find if i.first + K is
        // present in this map or not
        if (mp.ContainsKey(i.Key + K) )

            // If we find i.first or key + K in this map
            // then we have to increase in answer
            // the frequency of this element
            answer += i.Value;
    }

    return answer;
}

// Driver code
public static void Main(String[] args)
{
    // array initialisation
    int []arr = { 3, 6, 2, 8, 7, 6, 5, 9 };

    // size of array
    int N = arr.Length;

    // initialise k
    int K = 2;

    Console.Write(count_element(N, K, arr));
}
}
// This code contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation of find number
// of elements x in this array
// such x+k also present in this array.

// Function to return the
// count of element x such that
// x+k also lies in this array
function count_element(N, K, arr)
{

    // Key in map will store elements
    // and value will store the
    // frequency of the elements
    let mp = new Map();

    for (let i = 0; i < N; ++i)
        if (mp.has(arr[i])) {
            mp.set(arr[i], mp.get(arr[i]) + 1)
        } else {
            mp.set(arr[i], 1)
        }

    let answer = 0;

    for (let i of mp) {

        // Find if i.first + K is
        // present in this map or not
        if (mp.has(i[0] + K))

            // If we find i.first or key + K in this map
            // then we have to increase in answer
            // the frequency of this element
            answer += i[1];
    }

    return answer;
}

// Driver code

// array initialisation
let arr = [3, 6, 2, 8, 7, 6, 5, 9];

// size of array
let N = arr.length;

// initialise k
let K = 2;

document.write(count_element(N, K, arr));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
5
```