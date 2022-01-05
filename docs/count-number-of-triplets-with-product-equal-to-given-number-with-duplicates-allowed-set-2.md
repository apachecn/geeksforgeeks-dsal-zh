# 计数乘积等于给定数的三元组数，允许重复| Set-2

> 原文:[https://www . geesforgeks . org/count-三胞胎数量-带乘积等于给定数量-允许重复-集合-2/](https://www.geeksforgeeks.org/count-number-of-triplets-with-product-equal-to-given-number-with-duplicates-allowed-set-2/)

给定一个正整数数组(可能包含重复项)和一个数字“m”，求无序三元组的数量 **((A <sub>i</sub> 、A <sub>j</sub> 、A <sub>k</sub> )和(A <sub>j</sub> 、A <sub>i</sub> 、A <sub>k</sub> )其他排列只算一个)**乘积等于“m”。

**示例:**

> **输入:** arr[] = { 1，4，6，2，3，8}，M = 24
> **输出:** 3
> 三胞胎为{ 1，4，6} {1，3，8} {4，2，3}
> 
> **输入:** arr[] = { 0，4，6，2，3，8}，M = 18
> T3】输出: 0
> 这种情况下没有三胞胎

在之前的[帖子](https://www.geeksforgeeks.org/count-number-of-triplets-with-product-equal-to-given-number-with-duplicates-allowed/)中已经讨论过 O(N <sup>2</sup> 的解决方案。在这篇文章中，我们讨论了一种复杂度更低的更好的方法。

**方法:**按照下面的算法解决上述问题。

*   使用哈希映射计算给定数组中每个元素的频率。
*   声明一个可以存储三元组的集合，这样只有无序的三元组才会被计数。
*   在一个循环中从 1 迭代到 sqrt(m)(让变量为 I)，因为 M 可被整除的最大数是 sqrt(M)，省略了 M。
*   检查 M 是否能被 I 整除，I 是否出现在整数数组中，如果是，则再次从 1 循环到 M/i(让循环变量为 j)。
*   再次检查 M 是否能被 j 整除，j 是否存在于整数数组中，如果是，则检查剩余的数字 **( (M / i) / j)** 是否存在。
*   如果它存在，那么三重态就形成了。为了避免重复的三元组，请按排序顺序将它们插入集合中。
*   检查插入三元组后集合的大小是否增加，如果增加，则使用组合学来查找三元组的数量。
*   要找到三胞胎的数量，需要满足以下条件。
    1.  如果所有的 A <sub>i</sub> ，A <sub>j</sub> 和 A <sub>k</sub> 都是唯一的，那么组合的数量将是它们频率的乘积。
    2.  如果它们都一样，那么我们只能选择其中的三个，因此公式位于![frequency \choose 3            ](img/0ee1c4a1e70db420ea518a5fe13efdb8.png "Rendered by QuickLaTeX.com")。
    3.  如果两者中的任何一个相同(让 Ai 和 Aj)，计数将是![frequency[Ai] \choose 2            ](img/ff4a170722f145e0cd956897f2d3d475.png "Rendered by QuickLaTeX.com") *频率【A <sub> k</sub>

下面是上述方法的实现。

## C++

```
// C++ program to find the
// number of triplets in array
// whose product is equal to M
#include <bits/stdc++.h>
using namespace std;

// Function to count the triplets
int countTriplets(int a[], int m, int n)
{

    // hash-map to store the frequency of every number
    unordered_map<int, int> frequency;

    // set to store the unique triplets
    set<pair<int, pair<int, int> > > st;

    // count the number of times
    // every element appears in a map
    for (int i = 0; i < n; i++) {
        frequency[a[i]] += 1;
    }

    // stores the answer
    int ans = 0;

    // iterate till sqrt(m) since tnum2t is the
    // maximum number tnum2t can divide M except itself
    for (int i = 1; i * i <= m; i++) {

        // if divisible and present
        if (m % i == 0 and frequency[i]) {

            // remaining number after division
            int num1 = m / i;

            // iterate for the second number of the triplet
            for (int j = 1; j * j <= num1; j++) {

                // if divisible and present
                if (num1 % j == 0 and frequency[j]) {

                    // remaining number after division
                    int num2 = num1 / j;

                    // if the third number is present in array
                    if (frequency[num2]) {

                        // a temp array to store the triplet
                        int temp[] = { num2, i, j };

                        // sort the triplets
                        sort(temp, temp + 3);

                        // get the size of set
                        int setsize = st.size();

                        // insert the triplet in ascending order
                        st.insert({ temp[0], { temp[1], temp[2] } });

                        // if the set size increases after insertion,
                        //  it means a new triplet is found
                        if (setsize != st.size()) {

                            // if all the number in triplets are unique
                            if (i != j and j != num2)
                                ans += frequency[i] * frequency[j] * frequency[num2];

                            // if Ai and Aj are same among triplets
                            else if (i == j && j != num2)
                                ans += (frequency[i] * (frequency[i] - 1) / 2)
                                       * frequency[num2];

                            // if Aj and Ak are same among triplets
                            else if (j == num2 && j != i)
                                ans += (frequency[j] * (frequency[j] - 1) / 2)
                                       * frequency[i];

                            // if three of them are
                            // same among triplets
                            else if (i == j and j == num2)
                                ans += (frequency[i] * (frequency[i] - 1) * (frequency[i] - 2) / 6);

                            // if Ai and Ak are same among triplets
                            else
                                ans += (frequency[i] * (frequency[i] - 1) / 2)
                                       * frequency[j];
                        }
                    }
                }
            }
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int a[] = { 1, 4, 6, 2, 3, 8 };
    int m = 24;
    int n = sizeof(a) / sizeof(a[0]);

    cout << countTriplets(a, m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// number of triplets in array
// whose product is equal to M
import java.util.*;

class GFG
{

// Function to count the triplets
static int countTriplets(int a[], int m, int n)
{

    // hash-map to store
    // the frequency of every number
    HashMap<Integer, Integer> frequency
            = new HashMap<>();

    // put to store the unique triplets
    Set<String> st = new HashSet<String>();

    // count the number of times
    // every element appears in a map
    for (int i = 0; i < n; i++)
    {
        frequency.put(a[i],(frequency.get(a[i]) ==
                null ? 1:(frequency.get(a[i]) + 1)));
    }

    // stores the answer
    int ans = 0;

    // iterate till sqrt(m) since tnum2t is the
    // maximum number tnum2t can divide M except itself
    for (int i = 1; i * i <= m; i++)
    {

        // if divisible && present
        if (m % i == 0 && frequency.get(i)!=null)
        {

            // remaining number after division
            int num1 = m / i;

            // iterate for the second number of the triplet
            for (int j = 1; j * j <= num1; j++)
            {

                // if divisible && present
                if (num1 % j == 0 && frequency.get(j) != null)
                {

                    // remaining number after division
                    int num2 = num1 / j;

                    // if the third number is present in array
                    if (frequency.get(num2) != null)
                    {

                        // a temp array to store the triplet
                        int temp[] = { num2, i, j };

                        // sort the triplets
                        Arrays.sort(temp);

                        // get the size of put
                        int setsize = st.size();

                        // add the triplet in ascending order
                        st.add(temp[0]+" "+ temp[1]+" " +temp[2] );

                        // if the put size increases after addition,
                        // it means a new triplet is found
                        if (setsize != st.size())
                        {

                            // if all the number in triplets are unique
                            if (i != j && j != num2)
                                ans += frequency.get(i) *
                                        frequency.get(j) *
                                        frequency.get(num2);

                            // if Ai && Aj are same among triplets
                            else if (i == j && j != num2)
                                ans += (frequency.get(i) *
                                        (frequency.get(i) - 1) / 2)
                                        * frequency.get(num2);

                            // if Aj && Ak are same among triplets
                            else if (j == num2 && j != i)
                                ans += (frequency.get(j) *
                                        (frequency.get(j) - 1) / 2)
                                        * frequency.get(i);

                            // if three of them are
                            // same among triplets
                            else if (i == j && j == num2)
                                ans += (frequency.get(i) *
                                        (frequency.get(i) - 1) *
                                        (frequency.get(i) - 2) / 6);

                            // if Ai && Ak are same among triplets
                            else
                                ans += (frequency.get(i) *
                                        (frequency.get(i) - 1) / 2)
                                        * frequency.get(j);
                        }
                    }
                }
            }
        }
    }
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 1, 4, 6, 2, 3, 8 };
    int m = 24;
    int n = a.length;

    System.out.println(countTriplets(a, m, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find the
# number of triplets in array
# whose product is equal to M
import math

# Function to count the triplets
def countTriplets(a, m, n):

    # hash-map to store
    # the frequency of every number
    frequency = {}

    # put to store the unique triplets
    st = set({})

    # count the number of times
    # every element appears in a map
    for i in range(n):
        if a[i] in frequency:
            frequency[a[i]] += 1
        else:
            frequency[a[i]] = 1

    # stores the answer
    ans = 0

    # iterate till sqrt(m) since tnum2t is the
    # maximum number tnum2t can divide M except itself
    i = 1
    while i * i <= m:

        # if divisible && present
        if (m % i == 0 and i in frequency):

            # remaining number after division
            num1 = int(m / i)

            # iterate for the second number of the triplet
            j = 1
            while j * j <= num1:
                # if divisible && present
                if (num1 % j == 0 and j in frequency):
                    # remaining number after division
                    num2 = math.floor(num1 / j)

                    # if the third number is present in array
                    if num2 in frequency:
                        # a temp array to store the triplet
                        temp = [ num2, i, j ]

                        # sort the triplets
                        temp.sort()

                        # get the size of put
                        setsize = len(st)

                        # add the triplet in ascending order
                        st.add(str(temp[0])+" "+ str(temp[1])+" " +str(temp[2]))

                        # if the put size increases after addition,
                        # it means a new triplet is found
                        if setsize != len(st):
                            # if all the number in
                            # triplets are unique
                            if (i != j and j != num2):
                                ans += frequency[i] * frequency[j] * frequency[num2]

                            # if Ai && Aj are same among triplets
                            elif (i == j and j != num2):
                                ans += (frequency[i] * (frequency[i] - 1) / 2) * frequency[num2]

                            # if Aj && Ak are same among triplets
                            elif (j == num2 and j != i):
                                ans += (frequency[j] * (frequency[j] - 1) / 2) * frequency[i]

                            # if three of them are
                            # same among triplets
                            elif (i == j and j == num2):
                                ans += (frequency[i] * (frequency[i] - 1) * (frequency[i] - 2) / 6)

                            # if Ai && Ak are same among triplets
                            else:
                                ans += (frequency[i] * (frequency[i] - 1) / 2) * frequency[j]
                j += 1
        i += 1
    return int(ans)

a=[1, 4, 6, 2, 3, 8 ]
m = 24;
n = len(a)
print(countTriplets(a, m, n))

# This code is contributed by rameshtravel07.
```

## C#

```
// C# program to find the
// number of triplets in array
// whose product is equal to M
using System;
using System.Collections.Generic;
class GFG {

    // Function to count the triplets
    static int countTriplets(int[] a, int m, int n)
    {

        // hash-map to store
        // the frequency of every number
        Dictionary<int, int> frequency = new Dictionary<int, int>();

        // put to store the unique triplets
        HashSet<string> st = new HashSet<string>();

        // count the number of times
        // every element appears in a map
        for (int i = 0; i < n; i++)
        {
            if(frequency.ContainsKey(a[i]))
            {
                frequency[a[i]] += 1;
            }
            else{
                frequency[a[i]] = 1;
            }
        }

        // stores the answer
        int ans = 0;

        // iterate till sqrt(m) since tnum2t is the
        // maximum number tnum2t can divide M except itself
        for (int i = 1; i * i <= m; i++)
        {

            // if divisible && present
            if (m % i == 0 && frequency.ContainsKey(i))
            {

                // remaining number after division
                int num1 = m / i;

                // iterate for the second number of the triplet
                for (int j = 1; j * j <= num1; j++)
                {

                    // if divisible && present
                    if (num1 % j == 0 && frequency.ContainsKey(j))
                    {

                        // remaining number after division
                        int num2 = num1 / j;

                        // if the third number is present in array
                        if (frequency.ContainsKey(num2))
                        {

                            // a temp array to store the triplet
                            int[] temp = { num2, i, j };

                            // sort the triplets
                            Array.Sort(temp);

                            // get the size of put
                            int setsize = st.Count;

                            // add the triplet in ascending order
                            st.Add(temp[0].ToString()+" "+ temp[1].ToString()+" " +temp[2].ToString());

                            // if the put size increases after addition,
                            // it means a new triplet is found
                            if (setsize != st.Count)
                            {

                                // if all the number in triplets are unique
                                if (i != j && j != num2)
                                    ans += frequency[i] *
                                            frequency[j] *
                                            frequency[num2];

                                // if Ai && Aj are same among triplets
                                else if (i == j && j != num2)
                                    ans += (frequency[i] *
                                            (frequency[i] - 1) / 2)
                                            * frequency[num2];

                                // if Aj && Ak are same among triplets
                                else if (j == num2 && j != i)
                                    ans += (frequency[j] *
                                            (frequency[j] - 1) / 2)
                                            * frequency[i];

                                // if three of them are
                                // same among triplets
                                else if (i == j && j == num2)
                                    ans += (frequency[i] *
                                            (frequency[i] - 1) *
                                            (frequency[i] - 2) / 6);

                                // if Ai && Ak are same among triplets
                                else
                                    ans += (frequency[i] *
                                            (frequency[i] - 1) / 2)
                                            * frequency[j];
                            }
                        }
                    }
                }
            }
        }
        return ans;
    }

  // Driver code
  static void Main() {
    int[] a = { 1, 4, 6, 2, 3, 8 };
    int m = 24;
    int n = a.Length;

    Console.Write(countTriplets(a, m, n));
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>

// JavaScript program to find the
// number of triplets in array
// whose product is equal to M

// Function to count the triplets
function countTriplets(a,m,n)
{
    // hash-map to store
    // the frequency of every number
    let frequency = new Map();

    // put to store the unique triplets
    let st = new Set();

    // count the number of times
    // every element appears in a map
    for (let i = 0; i < n; i++)
    {
        frequency.set(a[i],(frequency.get(a[i]) ==
                null ? 1:(frequency.get(a[i]) + 1)));
    }

    // stores the answer
    let ans = 0;

    // iterate till sqrt(m) since tnum2t is the
    // maximum number tnum2t can divide M except itself
    for (let i = 1; i * i <= m; i++)
    {

        // if divisible && present
        if (m % i == 0 && frequency.get(i)!=null)
        {

            // remaining number after division
            let num1 = m / i;

            // iterate for the second number of the triplet
            for (let j = 1; j * j <= num1; j++)
            {

                // if divisible && present
                if (num1 % j == 0 && frequency.get(j) != null)
                {

                    // remaining number after division
                    let num2 = Math.floor(num1 / j);

                    // if the third number is present in array
                    if (frequency.get(num2) != null)
                    {

                        // a temp array to store the triplet
                        let temp = [ num2, i, j ];

                        // sort the triplets
                        temp.sort(function(a,b){return a-b;});

                        // get the size of put
                        let setsize = st.size;

                        // add the triplet in ascending order
                        st.add(temp[0]+" "+ temp[1]+" " +temp[2] );

                        // if the put size increases after addition,
                        // it means a new triplet is found
                        if (setsize != st.size)
                        {

                            // if all the number in
                            // triplets are unique
                            if (i != j && j != num2)
                                ans += frequency.get(i) *
                                        frequency.get(j) *
                                        frequency.get(num2);

                            // if Ai && Aj are same among triplets
                            else if (i == j && j != num2)
                                ans += (frequency.get(i) *
                                        (frequency.get(i) - 1) / 2)
                                        * frequency.get(num2);

                            // if Aj && Ak are same among triplets
                            else if (j == num2 && j != i)
                                ans += (frequency.get(j) *
                                        (frequency.get(j) - 1) / 2)
                                        * frequency.get(i);

                            // if three of them are
                            // same among triplets
                            else if (i == j && j == num2)
                                ans += (frequency.get(i) *
                                        (frequency.get(i) - 1) *
                                        (frequency.get(i) - 2) / 6);

                            // if Ai && Ak are same among triplets
                            else
                                ans += (frequency.get(i) *
                                        (frequency.get(i) - 1) / 2)
                                        * frequency.get(j);
                        }
                    }
                }
            }
        }
    }
    return ans;
}

// Driver Code
let a=[1, 4, 6, 2, 3, 8 ];
let m = 24;
let n = a.length;
document.write(countTriplets(a, m, n));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N * log N)