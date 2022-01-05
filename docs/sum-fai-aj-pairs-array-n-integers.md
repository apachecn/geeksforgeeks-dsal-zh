# n 个整数数组中所有对的 f(a[i]，a[j])之和

> 原文:[https://www . geesforgeks . org/sum-fai-aj-pairs-array-n-integers/](https://www.geeksforgeeks.org/sum-fai-aj-pairs-array-n-integers/)

给定 n 个整数的数组，求所有对(I，j)的 f(a[i]，a[j])的和，使得(1 <= i < j <= n). 

**f(a[i]，a[j]):**

```
If |a[j]-a[i]| > 1
   f(a[i], a[j]) = a[j] - a[i] 
Else // if |a[j]-a[i]| <= 1
   f(a[i], a[j]) = 0
```

**示例:**

```
Input : 6 6 4 4 
Output : -8 
Explanation: 
All pairs are: (6 - 6) + (6 - 6) +
(6 - 6) + (4 - 6) + (4 - 6) + (4 - 6) + 
(4 - 6) + (4 - 4) + (4 - 4) = -8

Input: 1 2 3 1 3
Output: 4 
Explanation: the pairs that add up are:
(3, 1), (3, 1) to give 4, rest all pairs 
according to condition gives 0\.  
```

一种**天真的方法**是遍历所有对并计算 f(a[i]，a[j])，在遍历两个嵌套循环的同时对其求和将给出我们的答案。
**时间复杂度:** O(n^2)

一种有效的方法是使用映射/散列函数来记录每个出现的数字，然后遍历列表。遍历列表时，我们将它前面的数字的计数与数字本身相乘。然后用该数之前的数的预和减去这个结果，得到该数所有可能对的差的和。要删除绝对差为< =1 的所有对，只需从先前计算的总和中减去(数字-1)和(数字+1)的出现次数。这里，我们从计算的和中减去(数字-1)的计数，就像它之前被加到和中一样，并且我们加上(数字+1)的计数，因为负数已经被加到所有对的预先计算的和中。
**时间复杂度:** O(n)

**以下是上述方法的实现:**

## C++

```
// CPP program to calculate the
// sum of f(a[i], aj])
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
int sum(int a[], int n)
{
    // map to keep a count of occurrences
    unordered_map<int, int> cnt;

    // Traverse in the list from start to end
    // number of times a[i] can be in a pair and
    // to get the difference we subtract pre_sum.
    int ans = 0, pre_sum = 0;
    for (int i = 0; i < n; i++) {
        ans += (i * a[i]) - pre_sum;
        pre_sum += a[i];

        // if the (a[i]-1) is present then
        // subtract that value as f(a[i], a[i]-1)=0
        if (cnt[a[i] - 1])
            ans -= cnt[a[i] - 1];

        // if the (a[i]+1) is present then
        // add that value as f(a[i], a[i]-1)=0
        // here we add as a[i]-(a[i]-1)<0 which would
        // have been added as negative sum, so we add 
        // to remove this pair from the sum value
        if (cnt[a[i] + 1])
            ans += cnt[a[i] + 1];

        // keeping a counter for every element
        cnt[a[i]]++;
    }
    return ans;
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 1, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << sum(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate 
// the sum of f(a[i], aj])
import java.util.*;
public class GfG {

    // Function to calculate the sum
    public static int sum(int a[], int n)
    {
        // Map to keep a count of occurrences
        Map<Integer,Integer> cnt = new HashMap<Integer,Integer>();

        // Traverse in the list from start to end
        // number of times a[i] can be in a pair and
        // to get the difference we subtract pre_sum
        int ans = 0, pre_sum = 0;
        for (int i = 0; i < n; i++) {
            ans += (i * a[i]) - pre_sum;
            pre_sum += a[i];

            // If the (a[i]-1) is present then subtract
            // that value as f(a[i], a[i]-1) = 0
            if (cnt.containsKey(a[i] - 1))
                ans -= cnt.get(a[i] - 1);

            // If the (a[i]+1) is present then
            // add that value as f(a[i], a[i]-1)=0
            // here we add as a[i]-(a[i]-1)<0 which would
            // have been added as negative sum, so we add
            // to remove this pair from the sum value
            if (cnt.containsKey(a[i] + 1))
                ans += cnt.get(a[i] + 1);

            // keeping a counter for every element
            if(cnt.containsKey(a[i])) {
                cnt.put(a[i], cnt.get(a[i]) + 1);
            }
            else {
                cnt.put(a[i], 1);
            }
        }
        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int a[] = { 1, 2, 3, 1, 3 };
        int n = a.length;
        System.out.println(sum(a, n));
    }
}

// This code is contributed by Swetank Modi
```

## 蟒蛇 3

```
# Python3 program to calculate the
# sum of f(a[i], aj])

# Function to calculate the sum
def sum(a, n):

    # map to keep a count of occurrences
    cnt = dict()

    # Traverse in the list from start to end
    # number of times a[i] can be in a pair and
    # to get the difference we subtract pre_sum.
    ans = 0
    pre_sum = 0
    for i in range(n):
        ans += (i * a[i]) - pre_sum
        pre_sum += a[i]

        # if the (a[i]-1) is present then
        # subtract that value as f(a[i], a[i]-1)=0
        if (a[i] - 1) in cnt:
            ans -= cnt[a[i] - 1]

        # if the (a[i]+1) is present then add that 
        # value as f(a[i], a[i]-1)=0 here we add
        # as a[i]-(a[i]-1)<0 which would have been
        # added as negative sum, so we add to remove 
        # this pair from the sum value
        if (a[i] + 1) in cnt:
            ans += cnt[a[i] + 1]

        # keeping a counter for every element
        if a[i] not in cnt:
            cnt[a[i]] = 0
        cnt[a[i]] += 1

    return ans

# Driver Code
if __name__ == '__main__':
    a = [1, 2, 3, 1, 3]
    n = len(a)
    print(sum(a, n))

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
using System;
using System.Collections.Generic;

// C#  program to calculate  
// the sum of f(a[i], aj])
public class GfG
{

    // Function to calculate the sum
    public static int sum(int[] a, int n)
    {
        // Map to keep a count of occurrences
        IDictionary<int, int> cnt = new Dictionary<int, int>();

        // Traverse in the list from start to end
        // number of times a[i] can be in a pair and
        // to get the difference we subtract pre_sum
        int ans = 0, pre_sum = 0;
        for (int i = 0; i < n; i++)
        {
            ans += (i * a[i]) - pre_sum;
            pre_sum += a[i];

            // If the (a[i]-1) is present then subtract
            // that value as f(a[i], a[i]-1) = 0
            if (cnt.ContainsKey(a[i] - 1))
            {
                ans -= cnt[a[i] - 1];
            }

            // If the (a[i]+1) is present then
            // add that value as f(a[i], a[i]-1)=0
            // here we add as a[i]-(a[i]-1)<0 which would 
            // have been added as negative sum, so we add 
            // to remove this pair from the sum value
            if (cnt.ContainsKey(a[i] + 1))
            {
                ans += cnt[a[i] + 1];
            }

            // keeping a counter for every element
            if (cnt.ContainsKey(a[i]))
            {
                cnt[a[i]] = cnt[a[i]] + 1;
            }
            else
            {
                cnt[a[i]] = 1;
            }
        }
        return ans;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int[] a = new int[] {1, 2, 3, 1, 3};
        int n = a.Length;
        Console.WriteLine(sum(a, n));
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to calculate the
// sum of f(a[i], aj])

// Function to calculate the sum
function sum(a, n)
{
    // map to keep a count of occurrences
    var cnt = new Map();

    // Traverse in the list from start to end
    // number of times a[i] can be in a pair and
    // to get the difference we subtract pre_sum.
    var ans = 0, pre_sum = 0;
    for (var i = 0; i < n; i++) {
        ans += (i * a[i]) - pre_sum;
        pre_sum += a[i];

        // if the (a[i]-1) is present then
        // subtract that value as f(a[i], a[i]-1)=0
        if (cnt.has(a[i] - 1))
            ans -= cnt.get(a[i] - 1);

        // if the (a[i]+1) is present then
        // add that value as f(a[i], a[i]-1)=0
        // here we add as a[i]-(a[i]-1)<0 which would
        // have been added as negative sum, so we add 
        // to remove this pair from the sum value
        if(cnt.has(a[i] + 1))
            ans += cnt.get(a[i] + 1);

        // keeping a counter for every element
        if(cnt.has(a[i]))
            cnt.set(a[i], cnt.get(a[i])+1)
        else
            cnt.set(a[i], 1)
    }
    return ans;
}

// Driver code
var a = [1, 2, 3, 1, 3];
var n = a.length;
document.write( sum(a, n));

</script>
```

**输出:**

```
4
```