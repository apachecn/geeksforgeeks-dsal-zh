# 求给定范围内每个数与其频率乘积的和

> 原文:[https://www . geeksforgeeks . org/find-给定频率范围内每个数字和平方的乘积之和/](https://www.geeksforgeeks.org/find-sum-of-product-of-every-number-and-square-of-its-frequency-in-given-range/)

给定一个整数数组**【arr】**和一个查询数组**，任务是在给定的范围**【L，R】**内找到每个数字与其频率的乘积之和，其中每个范围在查询数组中给定。**

****示例:****

> ****输入:** arr[] = [1，2，1]，查询:[{1，2}，{1，3}]
> **输出:**【3，4】
> **解释:**
> 对于查询[1，2]，freq[1] = 1，freq[2] = 1，ans =(1 * freq[1])+(2 * freq[2])=>ans =(1 * 1+2 * 1)= 3【T9ans =(1 * freq[1])+(2 * freq[2])=>ans =(1 * 2)+(2 * 1)= 4**
> 
> ****输入:**arr[]=【1，1，2，2，1，3，1，1】，查询:[{2，7}，{1，6}]
> **输出:**【10，10】
> **解释:**
> 对于查询(2，7)，freq[1] = 3，freq[2] = 2，freq[3]= 3；
> ans =(1 * freq[1])+(2 * freq[2])+(3 * freq[3])
> ans =(1 * 3)+(2 * 2)+(3 * 1)= 10**

****天真方法:**
为了解决上面提到的问题，天真方法是迭代查询中给出的子数组。为子阵列中每个数字的频率维护一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，并在地图上迭代计算答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation to find
// sum of product of every number
// and square of its frequency
// in the given range

#include <bits/stdc++.h>
using namespace std;

// Function to solve queries
void answerQueries(
    int arr[], int n,
    vector<pair<int, int> >& queries)
{

    for (int i = 0; i < queries.size(); i++) {

        // Calculating answer
        // for every query
        int ans = 0;

        // The end points
        // of the ith query
        int l = queries[i].first - 1;
        int r = queries[i].second - 1;

        // map for storing frequency
        map<int, int> freq;
        for (int j = l; j <= r; j++) {

            // Iterating over the given
            // subarray and storing
            // frequency in a map

            // Incrementing the frequency
            freq[arr[j]]++;
        }

        // Iterating over map to find answer
        for (auto& i : freq) {

            // adding the contribution
            // of ith number
            ans += (i.first
                    * i.second);
        }

        // print answer
        cout << ans << endl;
    }
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    vector<pair<int, int> > queries
        = { { 1, 2 },
            { 1, 3 } };
    answerQueries(arr, n, queries);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find sum of
// product of every number and
// square of its frequency in
// the given range
import java.util.*;

class GFG{

// Function to solve queries    
public static void answerQueries(int[] arr,
                                 int n,
                                 int[][] queries)
{
    for(int i = 0; i < queries.length; i++)
    {

        // Calculating answer
        // for every query    
        int ans = 0;

        // The end points
        // of the ith query
        int l = queries[i][0] - 1;
        int r = queries[i][1] - 1;

        // Hashmap for storing frequency
        Map<Integer,
            Integer> freq = new HashMap<>();

        for(int j = l; j < r + 1; j++)
        {

            // Iterating over the given
            // subarray and storing
            // frequency in a map

            // Incrementing the frequency
            freq.put(arr[j],
                     freq.getOrDefault(arr[j], 0) + 1);
        }
        for(int k: freq.keySet())
        {

            // Adding the contribution
            // of ith number
            ans += k * freq.get(k);
        }

    // Print answer
    System.out.println(ans);
    }
}

// Driver code
public static void main(String args[] )
{
    int[] arr = { 1, 2, 1 };
    int n = arr.length;
    int[][] queries = { { 1, 2 },
                        { 1, 3 } };

    // Calling function
    answerQueries(arr, n, queries);
}
}

// This code contributed by dadi madhav
```

## **蟒蛇 3**

```
# Python3 implementation to find
# sum of product of every number
# and square of its frequency
# in the given range

# Function to solve queries
def answerQueries(arr, n, queries):

    for i in range(len(queries)):

        # Calculating answer
        # for every query
        ans = 0

        # The end points
        # of the ith query
        l = queries[i][0] - 1
        r = queries[i][1] - 1

        # Map for storing frequency
        freq = dict()
        for j in range(l, r + 1):

            # Iterating over the given
            # subarray and storing
            # frequency in a map

            # Incrementing the frequency
            freq[arr[j]] = freq.get(arr[j], 0) + 1

        # Iterating over map to find answer
        for i in freq:

            # Adding the contribution
            # of ith number
            ans += (i * freq[i])

        # Print answer
        print(ans)

# Driver code
if __name__ == '__main__':

    arr = [ 1, 2, 1 ]
    n = len(arr)

    queries = [ [ 1, 2 ],
                [ 1, 3 ] ]

    answerQueries(arr, n, queries)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program to find sum of
// product of every number and 
// square of its frequency in 
// the given range
using System;
using System.Collections.Generic;

class GFG{

// Function to solve queries
public static void answerQueries(int[] arr, int n,
                                 int[,] queries)
{
    for(int i = 0; i < queries.GetLength(0); i++)
    {

        // Calculating answer 
        // for every query 
        int ans = 0;

        // The end points 
        // of the ith query
        int l = queries[i, 0] - 1;
        int r = queries[i, 1] - 1;

        // Hashmap for storing frequency
        Dictionary<int,
                   int> freq = new Dictionary<int,
                                              int>();
        for(int j = l; j < r+ 1; j++)
        {

            // Iterating over the given 
            // subarray and storing 
            // frequency in a map 

            // Incrementing the frequency
            freq[arr[j]] = freq.GetValueOrDefault(arr[j], 0) + 1;
        }
        foreach(int k in freq.Keys)
        {

            // Adding the contribution 
            // of ith number
            ans += k * freq[k];
        }

        // Print answer
        Console.WriteLine(ans);
    }
}

// Driver code
static public void Main()
{
    int[] arr = { 1, 2, 1 };
    int n = arr.Length;
    int[,] queries = { { 1, 2 }, { 1, 3 } };

    // Calling function
    answerQueries(arr, n, queries);
}
}

// This code is contributed by avanitrachhadiya2155
```

## **java 描述语言**

```
<script>

// Javascript implementation to find
// sum of product of every number
// and square of its frequency
// in the given range

// Function to solve queries
function answerQueries(arr, n, queries)
{
    for(var i = 0; i < queries.length; i++)
    {

        // Calculating answer
        // for every query
        var ans = 0;

        // The end points
        // of the ith query
        var l = queries[i][0] - 1;
        var r = queries[i][1] - 1;

        // map for storing frequency
        var freq = new Map();
        for(var j = l; j <= r; j++)
        {

            // Iterating over the given
            // subarray and storing
            // frequency in a map

            // Incrementing the frequency
            if (freq.has(arr[j]))
                freq.set(arr[j], freq.get(arr[j]) + 1)
            else
                freq.set(arr[j], 1)
        }

        // Iterating over map to find answer
        freq.forEach((value, key) => {

            // Adding the contribution
            // of ith number
            ans += (key * value);
        });

        // Print answer
        document.write(ans + "<br>");
    }
}

// Driver code
var arr = [ 1, 2, 1 ];
var n = arr.length;
var queries = [ [ 1, 2 ],
                [ 1, 3 ] ];

answerQueries(arr, n, queries);

// This code is contributed by itsok

</script>
```

****Output:** 

```
3
4
```** 

*****时间复杂度:** O(Q * N)*
***辅助空间复杂度:** O(N)***

****高效方法:**
为了优化上述方法，我们将尝试使用[莫算法来实现该问题。](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/)**

*   ****首先使用自定义比较器根据查询的块![\sqrt{N}      ](img/1dba36ff0d5f37a6adda960099df335a.png "Rendered by QuickLaTeX.com")大小对查询进行排序**，并将每个查询的索引存储在地图中，以便按顺序打印。**
*   **现在，我们将维护两个指针 L 和 R，我们迭代数组来回答查询。当我们移动指针时，如果我们在我们的范围内添加一些数字，我们将首先从答案中移除其先前频率的贡献，然后增加频率，最后在答案中添加新频率的贡献。**
*   **如果我们从范围中移除一些元素，我们也会这样做，移除这个数字的现有 freq 的贡献，减少 freq，加上它的新频率的贡献。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation to find sum
// of product of every number
// and square of its frequency
// in the given range

#include <bits/stdc++.h>
using namespace std;

// Stores frequency
const int N = 1e5 + 5;

// Frequency array
vector<int> freq(N);

int sq;

// Function for comparator
bool comparator(
    pair<int, int>& a,
    pair<int, int>& b)
{
    // comparator for sorting
    // according to the which query
    // lies in the which block;
    if (a.first / sq != b.first / sq)
        return a.first < b.first;

    // if same block,
    // return which query end first
    return a.second < b.second;
}

// Function to add numbers in range
void add(int x, int& ans, int arr[])
{
    // removing contribution of
    // old frequency from answer
    ans -= arr[x]
           * freq[arr[x]];

    // incrementing the frequency
    freq[arr[x]]++;

    // adding contribution of
    // new frequency to answer
    ans += arr[x]
           * freq[arr[x]];
}

void remove(int x, int& ans, int arr[])
{
    // removing contribution of
    // old frequency from answer
    ans -= arr[x]
           * freq[arr[x]];

    // Decrement the frequency
    freq[arr[x]]--;

    // adding contribution of
    // new frequency to answer
    ans += arr[x]
           * freq[arr[x]];
}

// Function to answer the queries
void answerQueries(
    int arr[], int n,
    vector<pair<int, int> >& queries)
{

    sq = sqrt(n) + 1;

    vector<int> answer(
        int(queries.size()));

    // map for storing the
    // index of each query
    map<pair<int, int>, int> idx;

    // Store the index of queries
    for (int i = 0; i < queries.size(); i++)
        idx[queries[i]] = i;

    // Sort the queries
    sort(queries.begin(),
         queries.end(),
         comparator);

    int ans = 0;

    // pointers for iterating
    // over the array
    int x = 0, y = -1;
    for (auto& i : queries) {

        // iterating over all
        // the queries
        int l = i.first - 1, r = i.second - 1;
        int id = idx[i];

        while (x > l) {
            // decrementing the left
            // pointer and adding the
            // xth number's contribution
            x--;
            add(x, ans, arr);
        }
        while (y < r) {

            // incrementing the right
            // pointer and adding the
            // yth number's contribution
            y++;
            add(y, ans, arr);
        }
        while (x < l) {

            // incrementing the left pointer
            // and removing the
            // xth number's contribution
            remove(x, ans, arr);
            x++;
        }
        while (y > r) {

            // decrementing the right
            // pointer and removing the
            // yth number's contribution
            remove(y, ans, arr);
            y--;
        }
        answer[id] = ans;
    }

    // printing the answer of queries
    for (int i = 0; i < queries.size(); i++)
        cout << answer[i] << endl;
}

// Driver Code
int main()
{

    int arr[] = { 1, 1, 2, 2, 1, 3, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    vector<pair<int, int> > queries
        = { { 2, 7 },
            { 1, 6 } };
    answerQueries(arr, n, queries);
}
```

****Output:** 

```
10
10
```** 

*****时间复杂度:** O(N * sqrt{N})*
***辅助空间复杂度:** O(N)***