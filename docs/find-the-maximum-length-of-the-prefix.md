# 求前缀的最大长度

> 原文:[https://www . geesforgeks . org/find-最大长度前缀/](https://www.geeksforgeeks.org/find-the-maximum-length-of-the-prefix/)

给定一个由 **N** 整数组成的数组 **arr[]** ，其中数组的所有元素都来自范围**【0，9】**即一个数字，任务是找到这个数组前缀的最大长度，这样从前缀中删除一个元素将使前缀中剩余元素的出现相同。
**示例:**

> **输入:** arr[] = {1，1，1，2，2，2}
> **输出:** 5
> 所需前缀为{1，1，1，2，2}
> 去掉 1 后，每个元素的频率相等，即{1，1，2，2}
> 
> **输入:** arr[] = {1，1，1，2，2，2，3，3，3，4，4，5}
> **输出:** 13
> 
> **输入:** arr[] = {10，2，5，4，1 }
> T3】输出: 5

**方法:**迭代所有前缀，检查每个前缀是否可以移除一个元素，使每个元素都有相同的出现。为了满足这个条件，下列条件之一必须成立:

*   前缀中只有一个元素。
*   前缀中的所有元素都出现 1。
*   每个元素都有相同的出现，只有一个元素的出现次数为 1。
*   每个元素都有相同的出现，只有一个元素的出现次数比其他元素多 1 次。

下面是上述方法的实现:

## C++14

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// length of the required prefix
int Maximum_Length(vector<int> a)
{

    // Array to store the frequency
    // of each element of the array
    int counts[11] = {0};

    // Iterating for all the elements
    int ans = 0;
    for(int index = 0;
            index < a.size();
            index++)
    {

        // Update the frequency of the
        // current element i.e. v
        counts[a[index]] += 1;

        // Sorted positive values
        // from counts array
        vector<int> k;
        for(auto i : counts)
            if (i != 0)
                k.push_back(i);

        sort(k.begin(), k.end());

        // If current prefix satisfies
        // the given conditions
        if (k.size() == 1 ||
           (k[0] == k[k.size() - 2] &&
            k.back() - k[k.size() - 2] == 1) ||
           (k[0] == 1 and k[1] == k.back()))
            ans = index;
    }

    // Return the maximum length
    return ans + 1;
}

// Driver code
int main()
{
    vector<int> a = { 1, 1, 1, 2, 2, 2 };

    cout << (Maximum_Length(a));
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
public class Main
{
    // Function to return the maximum
    // length of the required prefix
    public static int Maximum_Length(Vector<Integer> a)
    {

        // Array to store the frequency
        // of each element of the array
        int[] counts = new int[11];

        // Iterating for all the elements
        int ans = 0;
        for(int index = 0;
                index < a.size();
                index++)
        {

            // Update the frequency of the
            // current element i.e. v
            counts[a.get(index)] += 1;

            // Sorted positive values
            // from counts array
            Vector<Integer> k = new Vector<Integer>();
            for(int i : counts)
                if (i != 0)
                    k.add(i);

            Collections.sort(k); 

            // If current prefix satisfies
            // the given conditions
            if (k.size() == 1 ||
               (k.get(0) == k.get(k.size() - 2) &&
                k.get(k.size() - 1) - k.get(k.size() - 2) == 1) ||
               (k.get(0) == 1 && k.get(1) == k.get(k.size() - 1)))
                ans = index;
        }

        // Return the maximum length
        return ans + 1;
    }

    // Driver code
    public static void main(String[] args) {
        Vector<Integer> a = new Vector<Integer>();
        a.add(1);
        a.add(1);
        a.add(1);
        a.add(2);
        a.add(2);
        a.add(2);

        System.out.println(Maximum_Length(a));
    }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum
# length of the required prefix
def Maximum_Length(a):

    # Array to store the frequency
    # of each element of the array
    counts =[0]*11

    # Iterating for all the elements
    for index, v in enumerate(a):

        # Update the frequency of the
        # current element i.e. v
        counts[v] += 1

        # Sorted positive values from counts array
        k = sorted([i for i in counts if i])

        # If current prefix satisfies
        # the given conditions
        if len(k)== 1 or (k[0]== k[-2] and k[-1]-k[-2]== 1) or (k[0]== 1 and k[1]== k[-1]):
            ans = index

    # Return the maximum length
    return ans + 1

# Driver code
if __name__=="__main__":
    a = [1, 1, 1, 2, 2, 2]
    n = len(a)
    print(Maximum_Length(a))
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to return the maximum
    // length of the required prefix
    static int Maximum_Length(List<int> a)
    {

        // Array to store the frequency
        // of each element of the array
        int[] counts = new int[11];

        // Iterating for all the elements
        int ans = 0;
        for(int index = 0;
                index < a.Count;
                index++)
        {

            // Update the frequency of the
            // current element i.e. v
            counts[a[index]] += 1;

            // Sorted positive values
            // from counts array
            List<int> k = new List<int>();
            foreach(int i in counts)
                if (i != 0)
                    k.Add(i);

            k.Sort();

            // If current prefix satisfies
            // the given conditions
            if (k.Count == 1 ||
               (k[0] == k[k.Count - 2] &&
                k[k.Count - 1] - k[k.Count - 2] == 1) ||
               (k[0] == 1 && k[1] == k[k.Count - 1]))
                ans = index;
        }

        // Return the maximum length
        return ans + 1;
    }

  static void Main() {
    List<int> a = new List<int>(new int[]{ 1, 1, 1, 2, 2, 2 });
    Console.Write(Maximum_Length(a));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the maximum
    // length of the required prefix
    function Maximum_Length(a)
    {

        // Array to store the frequency
        // of each element of the array
        let counts = new Array(11);
        counts.fill(0);

        // Iterating for all the elements
        let ans = 0;
        for(let index = 0; index < a.length; index++)
        {

            // Update the frequency of the
            // current element i.e. v
            counts[a[index]] += 1;

            // Sorted positive values
            // from counts array
            let k = [];
            for(let i = 0; i < counts.length; i++)
            {
                if (counts[i] != 0)
                {
                    k.push(i);
                }
            }

            k.sort(function(a, b){return a - b});

            // If current prefix satisfies
            // the given conditions
            if (k.length == 1 ||
               (k[0] == k[k.length - 2] &&
                k[k.length - 1] - k[k.length - 2] == 1) ||
               (k[0] == 1 && k[1] == k[k.length - 1]))
                ans = index;
        }

        // Return the maximum length
        return (ans);
    }

    let a = [ 1, 1, 1, 2, 2, 2 ];
    document.write(Maximum_Length(a));

       // This code is contributed by suresh07.
</script>
```

**Output:** 

```
5
```