# 检查任何一点是否有 K 个范围重叠

> 原文:[https://www . geesforgeks . org/check-if-any-k-ranges-在任意点重叠/](https://www.geeksforgeeks.org/check-if-any-k-ranges-overlap-at-any-point/)

给定 **N** 范围**【L，R】**和整数 **K** ，任务是检查是否有任何 **K** 范围在任何点重叠。

**示例:**

> **输入:**范围[][] = {{1，3}，{2，4}，{3，4}，{7，10}}，K = 3
> **输出:**是
> 3 是
> 范围{1，3}，{2，4}和{3，4}中的一个公共点。
> 
> **输入:**范围[][] = {{1，2}，{3，4}，{5，6}，{7，8}}，K = 2
> **输出:**否

**做法:**思路是做一个对的向量，把这个向量中每个范围的起点作为对存储为(起点，-1)，终点作为(终点，1)。现在，对向量进行排序，然后遍历向量，如果当前元素是起点，则将它推入堆栈，如果它是终点，则从堆栈中弹出一个元素。如果在任何时刻，堆栈的大小大于或等于 **K** 则打印**是**否则最终打印**否**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Comparator to sort the vector of pairs
bool sortby(const pair<int, int>& a,
            const pair<int, int>& b)
{
    if (a.first != b.first)
        return a.first < b.first;
    return (a.second < b.second);
}

// Function that returns true if any k
// segments overlap at any point
bool kOverlap(vector<pair<int, int> > pairs, int k)
{
    // Vector to store the starting point
    // and the ending point
    vector<pair<int, int> > vec;
    for (int i = 0; i < pairs.size(); i++) {

        // Starting points are marked by -1
        // and ending points by +1
        vec.push_back({ pairs[i].first, -1 });
        vec.push_back({ pairs[i].second, +1 });
    }

    // Sort the vector by first element
    sort(vec.begin(), vec.end());

    // Stack to store the overlaps
    stack<pair<int, int> > st;

    for (int i = 0; i < vec.size(); i++) {
        // Get the current element
        pair<int, int> cur = vec[i];

        // If it is the starting point
        if (cur.second == -1) {
            // Push it in the stack
            st.push(cur);
        }

        // It is the ending point
        else {
            // Pop an element from stack
            st.pop();
        }

        // If more than k ranges overlap
        if (st.size() >= k) {
            return true;
        }
    }

    return false;
}

// Driver code
int main()
{
    vector<pair<int, int> > pairs;
    pairs.push_back(make_pair(1, 3));
    pairs.push_back(make_pair(2, 4));
    pairs.push_back(make_pair(3, 5));
    pairs.push_back(make_pair(7, 10));

    int n = pairs.size(), k = 3;

    if (kOverlap(pairs, k))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.Stack;

class GFG{

static class Pair
{
    int first, second;

    public Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function that returns true if any k
// segments overlap at any point
static boolean kOverlap(ArrayList<Pair> pairs,
                        int k)
{

    // Vector to store the starting point
    // and the ending point
    ArrayList<Pair> vec = new ArrayList<>();
    for(int i = 0; i < pairs.size(); i++)
    {

        // Starting points are marked by -1
        // and ending points by +1
        vec.add(new Pair(pairs.get(i).first, -1));
        vec.add(new Pair(pairs.get(i).second, +1));
    }

    // Sort the vector by first element
    Collections.sort(vec, new Comparator<Pair>()
    {

        // Comparator to sort the vector of pairs
        public int compare(Pair a, Pair b)
        {
            if (a.first != b.first)
                return a.first - b.first;

            return (a.second - b.second);
        }
    });

    // Stack to store the overlaps
    Stack<Pair> st = new Stack<>();

    for(int i = 0; i < vec.size(); i++)
    {

        // Get the current element
        Pair cur = vec.get(i);

        // If it is the starting point
        if (cur.second == -1)
        {

            // Push it in the stack
            st.push(cur);
        }

        // It is the ending point
        else
        {

            // Pop an element from stack
            st.pop();
        }

        // If more than k ranges overlap
        if (st.size() >= k)
        {
            return true;
        }
    }
    return false;
}

// Driver code
public static void main(String[] args)
{
    ArrayList<Pair> pairs = new ArrayList<>();
    pairs.add(new Pair(1, 3));
    pairs.add(new Pair(2, 4));
    pairs.add(new Pair(3, 5));
    pairs.add(new Pair(7, 10));

    int n = pairs.size(), k = 3;

    if (kOverlap(pairs, k))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if any k
# segments overlap at any point
def kOverlap(pairs: list, k):

    # Vector to store the starting point
    # and the ending point
    vec = list()
    for i in range(len(pairs)):

        # Starting points are marked by -1
        # and ending points by +1
        vec.append((pairs[0], -1))
        vec.append((pairs[1], 1))

    # Sort the vector by first element
    vec.sort(key = lambda a: a[0])

    # Stack to store the overlaps
    st = list()

    for i in range(len(vec)):

        # Get the current element
        cur = vec[i]

        # If it is the starting point
        if cur[1] == -1:

            # Push it in the stack
            st.append(cur)

        # It is the ending point
        else:

            # Pop an element from stack
            st.pop()

        # If more than k ranges overlap
        if len(st) >= k:
            return True
    return False

# Driver Code
if __name__ == "__main__":
    pairs = list()
    pairs.append((1, 3))
    pairs.append((2, 4))
    pairs.append((3, 5))
    pairs.append((7, 10))

    n = len(pairs)
    k = 3

    if kOverlap(pairs, k):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic;
class GFG
{

// Function that returns true if any k
// segments overlap at any point
static bool kOverlap(List<Tuple<int,int>> pairs,
                        int k)
{

    // Vector to store the starting point
    // and the ending point
    List<Tuple<int,int>> vec = new List<Tuple<int,int>>();
    for(int i = 0; i < pairs.Count; i++)
    {

        // Starting points are marked by -1
        // and ending points by +1
        vec.Add(new Tuple<int,int>(pairs[i].Item1,-1));
        vec.Add(new Tuple<int,int>(pairs[i].Item2,1));
    }
    vec.Sort();

    // Stack to store the overlaps
    Stack st = new Stack();
    for(int i = 0; i < vec.Count; i++)
    {

        // Get the current element
        Tuple<int,int> cur = vec[i];

        // If it is the starting point
        if (cur.Item2 == -1)
        {

            // Push it in the stack
            st.Push(cur);
        }

        // It is the ending point
        else
        {

            // Pop an element from stack
            st.Pop();
        }

        // If more than k ranges overlap
        if (st.Count >= k)
        {
            return true;
        }
    }
    return false;
}

// Driver code
public static void Main(params string[] args)
{
    List<Tuple<int,int>> pairs = new List<Tuple<int,int>>();
    pairs.Add(new Tuple<int,int>(1, 3));
    pairs.Add(new Tuple<int,int>(2, 4));
    pairs.Add(new Tuple<int,int>(3, 5));
    pairs.Add(new Tuple<int,int>(7, 10));

    int n = pairs.Count, k = 3;
    if (kOverlap(pairs, k))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by rutvik_56/
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if any k
// segments overlap at any point
function kOverlap(pairs, k)
{
    // Vector to store the starting point
    // and the ending point
    var vec = [];
    for (var i = 0; i < pairs.length; i++) {

        // Starting points are marked by -1
        // and ending points by +1
        vec.push([pairs[i][0], -1 ]);
        vec.push([pairs[i][1], +1 ]);
    }

    // Sort the vector by first element
    vec.sort((a,b)=>{
        if(a[0]!=b[0])
            return a[0]-b[0]
        return a[1]-b[1]
    });

    // Stack to store the overlaps
    var st = [];

    for (var i = 0; i < vec.length; i++) {
        // Get the current element
        var cur = vec[i];

        // If it is the starting point
        if (cur[1] == -1) {
            // Push it in the stack
            st.push(cur);
        }

        // It is the ending point
        else {
            // Pop an element from stack
            st.pop();
        }

        // If more than k ranges overlap
        if (st.length >= k) {
            return true;
        }
    }

    return false;
}

// Driver code
var pairs = [];
pairs.push([1, 3]);
pairs.push([2, 4]);
pairs.push([3, 5]);
pairs.push([7, 10]);
var n = pairs.length, k = 3;
if (kOverlap(pairs, k))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```