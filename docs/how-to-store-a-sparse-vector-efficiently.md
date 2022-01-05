# 如何高效存储稀疏向量？

> 原文:[https://www . geesforgeks . org/如何高效地存储稀疏向量/](https://www.geeksforgeeks.org/how-to-store-a-sparse-vector-efficiently/)

一个**稀疏向量**是一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，它有大量的零，所以需要不必要的空间来存储这些零。
任务是在不存储零的情况下有效地存储给定的稀疏向量。

**示例:**

```
Input: vector = { 2, 0, 0, 0, 0, 
                  3, 0, 4, 0, 0, 
                  0, 1, 5, 0, 0, 
                  0, 0, 0, 0, 0, 
                  0, 0, 4, 0, 0, 
                  0, 2, 0, 0, 0, 
                  0, 0, 0, 3, 0, 
                  0, 0, 1, 0, 0, 
                  0, 0, 5 }
Output: {2, 3, 4, 1, 5, 
        4, 2, 3, 1, 5}
```

**方法:**
为了有效地存储稀疏向量，可以使用成对的[向量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)。对的第一个元素将是稀疏向量元素(非零)的索引，第二个元素将是实际元素。

下面是上述方法的实现:

## C++

```
// C++ program to store sparse vectors
// with the help of vector of pair

#include <bits/stdc++.h>
using namespace std;

// Store the sparse vector
// as a vector of pairs
vector<pair<int, int> >
convertSparseVector(vector<int> v)
{
    vector<pair<int, int> > res;
    for (int i = 0; i < v.size(); i++) {
        if (v[i] != 0) {
            res.push_back(make_pair(i, v[i]));
        }
    }
    return res;
}

// Print the vector of pairs
void print(vector<pair<int, int> > res)
{

    for (auto x : res) {
        cout << "index: " << x.first
             << " -> value: "
             << x.second << endl;
    }
}

// Driver function
int main()
{

    // Get the sparse vector
    vector<int> v{ 2, 0, 0, 0, 0,
                   3, 0, 4, 0, 0,
                   0, 1, 5, 0, 0,
                   0, 0, 0, 0, 0,
                   0, 0, 4, 0, 0,
                   0, 2, 0, 0, 0,
                   0, 0, 0, 3, 0,
                   0, 0, 1, 0, 0,
                   0, 0, 5 };

    // Get the stored vector of pairs
    vector<pair<int, int> > res
        = convertSparseVector(v);

    // Print the vector of pairs
    print(res);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to store sparse vectors
// with the help of ArrayList of pair
import java.util.ArrayList;

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

// Store the sparse ArrayList
// as a ArrayList of pairs
static ArrayList<Pair> convertSparseVector(int[] v)
{
    ArrayList<Pair> res = new ArrayList<>();
    for(int i = 0; i < v.length; i++)
    {
        if (v[i] != 0)
        {
            res.add(new Pair(i, v[i]));
        }
    }
    return res;
}

// Print the ArrayList of pairs
static void print(ArrayList<Pair> res)
{
    for(Pair x : res)
    {
        System.out.printf("index: %d -> value: %d\n",
                          x.first, x.second);
    }
}

// Driver code
public static void main(String[] args)
{

    // Get the sparse ArrayList
    int[] v = { 2, 0, 0, 0, 0,
                3, 0, 4, 0, 0,
                0, 1, 5, 0, 0,
                0, 0, 0, 0, 0,
                0, 0, 4, 0, 0,
                0, 2, 0, 0, 0,
                0, 0, 0, 3, 0,
                0, 0, 1, 0, 0,
                0, 0, 5 };

    // Get the stored ArrayList of pairs
    ArrayList<Pair> res = convertSparseVector(v);

    // Print the ArrayList of pairs
    print(res);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to store sparse vectors
# with the help of vector of pair

# Store the sparse vector
# as a vector of pairs
def convertSparseVector(v):
    res = []
    for i in range(len(v)):
        if (v[i] != 0):
            res.append([i, v[i]])

    return res

# Print the vector of pairs
def printf(res):
    for x in res:
        print("index:", x[0],
              " -> value:", x[1])

# Driver Code
if __name__ == '__main__':

    # Get the sparse vector
    v = [2, 0, 0, 0, 0,
         3, 0, 4, 0, 0,
         0, 1, 5, 0, 0,
         0, 0, 0, 0, 0,
         0, 0, 4, 0, 0,
         0, 2, 0, 0, 0,
         0, 0, 0, 3, 0,
         0, 0, 1, 0, 0,
         0, 0, 5]

    # Get the stored vector of pairs
    res = convertSparseVector(v)

    # Print the vector of pairs
    printf(res)

# This code is contributed by Surendra_Gangwar
```

## java 描述语言

```
<script>

// JavaScript program to store sparse vectors
// with the help of vector of pair

// Store the sparse vector
// as a vector of pairs
function convertSparseVector(v) {
    let res = [];
    for (let i = 0; i < v.length; i++) {
        if (v[i] != 0) {
            res.push([i, v[i]]);
        }
    }
    return res;
}

// Print the vector of pairs
function print(res) {

    for (let x of res) {
        document.write("index: " + x[0] + " -> value: "
        + x[1] + "<br>");
    }
}

// Driver function

// Get the sparse vector
let v = [2, 0, 0, 0, 0,
    3, 0, 4, 0, 0,
    0, 1, 5, 0, 0,
    0, 0, 0, 0, 0,
    0, 0, 4, 0, 0,
    0, 2, 0, 0, 0,
    0, 0, 0, 3, 0,
    0, 0, 1, 0, 0,
    0, 0, 5];

// Get the stored vector of pairs
let res = convertSparseVector(v);

// Print the vector of pairs
print(res);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
index: 0 -> value: 2
index: 5 -> value: 3
index: 7 -> value: 4
index: 11 -> value: 1
index: 12 -> value: 5
index: 22 -> value: 4
index: 26 -> value: 2
index: 33 -> value: 3
index: 37 -> value: 1
index: 42 -> value: 5
```