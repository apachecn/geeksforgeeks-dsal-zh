# 找出一组给定坐标可以形成的矩形数量

> 原文:[https://www . geeksforgeeks . org/find-从给定的一组坐标中可以形成的矩形数量/](https://www.geeksforgeeks.org/find-number-of-rectangles-that-can-be-formed-from-a-given-set-of-coordinates/)

给定一个由表示坐标的一对整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[][]** 。任务是计算使用给定坐标可以形成的矩形的总数。

**示例:**

> **输入:** arr[][] = {{0，0}、{0，1}、{1，0}、{1，1}、{2，0}、{2，1}、{11，11}}
> **输出:** 3
> **解释:**以下是使用给定坐标形成的矩形。
> 第一个矩形(0，0)、(0，1)、(1，0)、(1，1)
> 第二个矩形(0，0)、(0，1)、(2，0)、(2，1)
> 第三个矩形(1，0)、(1，1)、(2，0)、(2，1)
> 
> **输入:** arr[][] = {{10，0}，{0，10}，{11，11}，{0，11}，{12，10}}
> **输出:** 0
> **解释:**使用这些坐标无法形成矩形

**方法:这个问题可以通过使用矩形的属性和[哈希映射](https://www.geeksforgeeks.org/hashing-data-structure/)来解决。如果一个矩形的两个坐标是已知的，那么剩下的两个坐标就很容易确定。对于每一对坐标，找出另外两个可以形成矩形的坐标。**

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find number of possible rectangles
int countRectangles(vector<pair<int, int> >& ob)
{

    // Creating TreeSet containing elements
    set<pair<int, int> > it;

    // Inserting the pairs in the set
    for (int i = 0; i < ob.size(); ++i) {
        it.insert(ob[i]);
    }

    int ans = 0;
    for (int i = 0; i < ob.size(); ++i)
    {
        for (int j = 0; j < ob.size(); ++j)
        {
            if (ob[i].first != ob[j].first
                && ob[i].second != ob[j].second)
            {

                // Searching the pairs in the set
                if (it.count({ ob[i].first, ob[j].second })
                    && it.count(
                        { ob[j].first, ob[i].second }))
                {

                    // Increase the answer
                    ++ans;
                }
            }
        }
    }

    // Return the final answer
    return ans / 4;
}

// Driver Code
int main()
{

    int N = 7;
    vector<pair<int, int> > ob(N);

    // Inserting the pairs
    ob[0] = { 0, 0 };
    ob[1] = { 1, 0 };
    ob[2] = { 1, 1 };
    ob[3] = { 0, 1 };
    ob[4] = { 2, 0 };
    ob[5] = { 2, 1 };
    ob[6] = { 11, 23 };

    cout << countRectangles(ob);

    return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;
import java.util.*;

class Main {

    // Creataing pair class and
    // implements comparable interface
    static class Pair implements Comparable<Pair> {
        int first;
        int second;
        Pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
        // Changing sorting order of the pair class
        @Override
        public int compareTo(Pair o)
        {
            // Checking the x axis
            if (this.first == o.first) {
                return this.second - o.second;
            }

            return this.first - o.first;
        }
    }

    // Function to find number of possible rectangles
    static int countRectangles(Pair ob[])
    {

        // Creating TreeSet containing elements
        TreeSet<Pair> it = new TreeSet<>();

        // Inserting the pairs in the set
        for (int i = 0; i < ob.length; ++i) {
            it.add(ob[i]);
        }

        int ans = 0;
        for (int i = 0; i < ob.length; ++i) {
            for (int j = 0; j < ob.length; ++j) {
                if (ob[i].first != ob[j].first
                    && ob[i].second != ob[j].second) {
                    // Searching the pairs in the set
                    if (it.contains(new Pair(ob[i].first,
                                             ob[j].second))
                        && it.contains(new Pair(
                               ob[j].first, ob[i].second))) {
                        // Increase the answer
                        ++ans;
                    }
                }
            }
        }

        // Return the final answer
        return ans / 4;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int N = 7;
        Pair ob[] = new Pair[N];

        // Inserting the pairs
        ob[0] = new Pair(0, 0);
        ob[1] = new Pair(1, 0);
        ob[2] = new Pair(1, 1);
        ob[3] = new Pair(0, 1);
        ob[4] = new Pair(2, 0);
        ob[5] = new Pair(2, 1);
        ob[6] = new Pair(11, 23);

        System.out.print(countRectangles(ob));
    }
}
```

## 蟒蛇 3

```
# Python program for above approach

# Function to find number of possible rectangles
def countRectangles(ob):

    # Creating TreeSet containing elements
    it = set()

    # Inserting the pairs in the set
    for i in range(len(ob)):
        it.add(f"{ob[i]}");

    ans = 0;
    for i in range(len(ob)):
        for j in range(len(ob)):
            if (ob[i][0] != ob[j][0] and ob[i][1] != ob[j][1]):

                # Searching the pairs in the set
                if (f"{[ob[i][0], ob[j][1]]}" in it and f"{[ob[j][0], ob[i][1]]}" in it):

                    # Increase the answer
                    ans += 1

    # Return the final answer
    return int(ans / 4);

# Driver Code
N = 7;
ob = [0] * N

# Inserting the pairs
ob[0] = [0, 0];
ob[1] = [1, 0];
ob[2] = [1, 1];
ob[3] = [0, 1];
ob[4] = [2, 0];
ob[5] = [2, 1];
ob[6] = [11, 23];

print(countRectangles(ob));

# This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to find number of possible rectangles
function countRectangles(ob) {

    // Creating TreeSet containing elements
    let it = new Set();

    // Inserting the pairs in the set
    for (let i = 0; i < ob.length; ++i) {
        it.add(`${ob[i]}`);
    }

    let ans = 0;
    for (let i = 0; i < ob.length; ++i) {
        for (let j = 0; j < ob.length; ++j) {
            if (ob[i][0] != ob[j][0]
                && ob[i][1] != ob[j][1]) {
                // Searching the pairs in the set
                if (it.has(`${[ob[i][0], ob[j][1]]}`)
                    && it.has(`${[ob[j][0], ob[i][1]]}`)) {

                    // Increase the answer
                    ++ans;
                }
            }
        }
    }

    // Return the final answer
    return ans / 4;
}

// Driver Code

let N = 7;
let ob = new Array(N).fill(0);

// Inserting the pairs
ob[0] = [0, 0];
ob[1] = [1, 0];
ob[2] = [1, 1];
ob[3] = [0, 1];
ob[4] = [2, 0];
ob[5] = [2, 1];
ob[6] = [11, 23];

document.write(countRectangles(ob));

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output:** 

```
3
```

时间复杂度:O(N <sup>2</sup> ，其中 N 为数组的大小。
辅助空间:O(N)，其中 N 是数组的大小。