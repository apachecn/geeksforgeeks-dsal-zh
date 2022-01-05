# 最小异或值对

> 原文:[https://www.geeksforgeeks.org/minimum-xor-value-pair/](https://www.geeksforgeeks.org/minimum-xor-value-pair/)

给定一个整数数组。找到数组中具有最小异或值的对。
**例:**

```
Input : arr[] =  {9, 5, 3}
Output : 6
        All pair with xor value (9 ^ 5) => 12, 
        (5 ^ 3) => 6, (9 ^ 3) => 10.
        Minimum XOR value is 6

Input : arr[] = {1, 2, 3, 4, 5}
Output : 1 
```

一个简单的解决方案是生成给定数组的所有对，并计算它们的异或值。最后，返回最小异或值。该解决方案需要 0(n<sup>2</sup>时间。

## C++

```
// C++ program to find minimum XOR value in an array.
#include <bits/stdc++.h>
using namespace std;

// Returns minimum xor value of pair in arr[0..n-1]
int minXOR(int arr[], int n)
{
    int min_xor = INT_MAX; // Initialize result

    // Generate all pair of given array
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)

            // update minimum xor value if required
            min_xor = min(min_xor, arr[i] ^ arr[j]);

    return min_xor;
}

// Driver program
int main()
{
    int arr[] = { 9, 5, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minXOR(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum XOR value in an array.
class GFG {

    // Returns minimum xor value of pair in arr[0..n-1]
    static int minXOR(int arr[], int n)
    {
        int min_xor = Integer.MAX_VALUE; // Initialize result

        // Generate all pair of given array
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)

                // update minimum xor value if required
                min_xor = Math.min(min_xor, arr[i] ^ arr[j]);

        return min_xor;
    }

    // Driver program
    public static void main(String args[])
    {
        int arr[] = { 9, 5, 3 };
        int n = arr.length;
        System.out.println(minXOR(arr, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python program to find minimum
# XOR value in an array.

# Function to find minimum XOR pair
def minXOR(arr, n):

    # Sort given array
    arr.sort();

    min_xor = 999999
    val = 0

    # calculate min xor of
    # consecutive pairs
    for i in range (0, n-1):
        for j in range (i+1, n-1):

            # update minimum xor value
            # if required
            val = arr[i] ^ arr[j]
            min_xor = min(min_xor, val)
    return min_xor

# Driver program
arr = [ 9, 5, 3 ]
n = len(arr)

print(minXOR(arr, n))

# This code is contributed by Sam007.
```

## C#

```
// C# program to find minimum
// XOR value in an array.
using System;

class GFG {

    // Returns minimum xor value of
    // pair in arr[0..n-1]
    static int minXOR(int[] arr, int n)
    {
         // Initialize result
        int min_xor = int.MaxValue;

        // Generate all pair of given array
        for (int i = 0; i < n; i++)
            for (int j = i + 1; j < n; j++)

            // update minimum xor value if required
            min_xor = Math.Min(min_xor, arr[i] ^ arr[j]);

        return min_xor;
    }

    // Driver program
    public static void Main()
    {
        int[] arr = { 9, 5, 3 };
        int n = arr.Length;
        Console.WriteLine(minXOR(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// XOR value in an array.

// Returns minimum xor value
// of pair in arr[0..n-1]
function minXOR($arr, $n)
{
    // Initialize result
    $min_xor = PHP_INT_MAX;

    // Generate all pair of given array
    for ( $i = 0; $i < $n; $i++)
        for ( $j = $i + 1; $j < $n; $j++)

            // update minimum xor
            // value if required
            $min_xor = min($min_xor, $arr[$i] ^ $arr[$j]);

    return $min_xor;
}

    // Driver Code
    $arr = array(9, 5, 3);
    $n = count($arr);
    echo minXOR($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// minimum XOR value in an array.

// Returns minimum xor value of pair in arr[0..n-1]
function minXOR(arr, n)
{
    // Initialize result
    let min_xor = Number.MAX_VALUE;

    // Generate all pair of given array
    for (let i = 0; i < n; i++)
        for (let j = i + 1; j < n; j++)

            // update minimum xor value if required
            min_xor = Math.min(min_xor, arr[i] ^ arr[j]);

    return min_xor;
}

// Driver program
    let arr = [ 9, 5, 3 ];
    let n = arr.length;
    document.write(minXOR(arr, n));

</script>
```

**输出:**

```
6
```

一个**高效的解决方案**可以在 O(nlogn)时间内解决这个问题。下面是算法:

```
1). Sort the given array
2). Traverse and check XOR for every consecutive pair
```

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum XOR pair
int minXOR(int arr[], int n)
{
    // Sort given array
    sort(arr, arr + n);

    int minXor = INT_MAX;
    int val = 0;

    // calculate min xor of consecutive pairs
    for (int i = 0; i < n - 1; i++) {
        val = arr[i] ^ arr[i + 1];
        minXor = min(minXor, val);
    }

    return minXor;
}

// Driver program
int main()
{
    int arr[] = { 9, 5, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minXOR(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;
class GFG {

    // Function to find minimum XOR pair
    static int minXOR(int arr[], int n)
    {
        // Sort given array
        Arrays.parallelSort(arr);

        int minXor = Integer.MAX_VALUE;
        int val = 0;

        // calculate min xor of consecutive pairs
        for (int i = 0; i < n - 1; i++) {
            val = arr[i] ^ arr[i + 1];
            minXor = Math.min(minXor, val);
        }

        return minXor;
    }

    // Driver program
    public static void main(String args[])
    {
        int arr[] = { 9, 5, 3 };
        int n = arr.length;
        System.out.println(minXOR(arr, n));
    }
}

// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
import sys   

# Function to find minimum XOR pair
def minXOR(arr, n):

    # Sort given array
    arr.sort()

    minXor =  int(sys.float_info.max)
    val = 0

    # calculate min xor of consecutive pairs
    for i in range(0,n-1):
        val = arr[i] ^ arr[i + 1];
        minXor = min(minXor, val);

    return minXor

# Driver program
arr = [9, 5, 3]
n = len(arr)
print(minXOR(arr, n))

# This code is contributed by Sam007.
```

## C#

```
// C# program to find minimum
// XOR value in an array.
using System;

class GFG {

    // Function to find minimum XOR pair
    static int minXOR(int[] arr, int n)
    {
        // Sort given array
        Array.Sort(arr);

        int minXor = int.MaxValue;
        int val = 0;

        // calculate min xor of consecutive pairs
        for (int i = 0; i < n - 1; i++) {
            val = arr[i] ^ arr[i + 1];
            minXor = Math.Min(minXor, val);
        }

        return minXor;
    }

    // Driver program
    public static void Main()
    {
        int[] arr = { 9, 5, 3 };
        int n = arr.Length;
        Console.WriteLine(minXOR(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to find minimum XOR pair
function minXOR($arr, $n)
{
    // Sort given array
    sort($arr);

    $minXor = PHP_INT_MAX;
    $val = 0;

    // calculate min xor
    // of consecutive pairs
    for ($i = 0; $i < $n - 1; $i++)
    {
        $val = $arr[$i] ^ $arr[$i + 1];
        $minXor = min($minXor, $val);
    }

    return $minXor;
}

// Driver Code
$arr = array(9, 5, 3);
$n = count($arr);
echo minXOR($arr, $n);

// This code is contributed by Smitha.
?>
```

## java 描述语言

```
<script>

// Function to find minimum XOR pair
function minXOR(arr, n)
{
    // Sort given array
    arr.sort();

    let minXor = Number.MAX_VALUE;
    let val = 0;

    // calculate min xor of consecutive pairs
    for (let i = 0; i < n - 1; i++) {
        val = arr[i] ^ arr[i + 1];
        minXor = Math.min(minXor, val);
    }

    return minXor;
}

// Driver program
    let arr = [ 9, 5, 3 ];
    let n = arr.length;
    document.write(minXOR(arr, n));

</script>
```

**输出:**

```
6
```

时间复杂度:O(N*logN)
空间复杂度:O(1)
感谢乌特卡什·古普塔提出上述方法。
更进一步的**高效解**可以在整数取固定位数存储的假设下，在 O(n)时间内解决上述问题。这个想法是使用 Trie 数据结构。下面是算法。

```
1). Create an empty trie. Every node of trie contains two children
    for 0 and 1 bits.
2). Initialize min_xor = INT_MAX, insert arr[0] into trie
3). Traversal all array element one-by-one starting from second.
     a. First find minimum setbet difference value in trie 
        do xor of current element with minimum setbit diff that value 
     b. update min_xor value if required
     c. insert current array element in trie 
4). return min_xor

```

下面是上述算法的实现。

## C++

```
// C++ program to find minimum XOR value in an array.
#include <bits/stdc++.h>
using namespace std;
#define INT_SIZE 32

// A Trie Node
struct TrieNode {
    int value; // used in leaf node
    TrieNode* Child[2];
};

// Utility function to create a new Trie node
TrieNode* getNode()
{
    TrieNode* newNode = new TrieNode;
    newNode->value = 0;
    newNode->Child[0] = newNode->Child[1] = NULL;
    return newNode;
}

// utility function insert new key in trie
void insert(TrieNode* root, int key)
{
    TrieNode* temp = root;

    // start from the most significant bit, insert all
    // bit of key one-by-one into trie
    for (int i = INT_SIZE - 1; i >= 0; i--) {
        // Find current bit in given prefix
        bool current_bit = (key & (1 << i));

        // Add a new Node into trie
        if (temp->Child[current_bit] == NULL)
            temp->Child[current_bit] = getNode();

        temp = temp->Child[current_bit];
    }

    // store value at leafNode
    temp->value = key;
}

// Returns minimum XOR value of an integer inserted
// in Trie and given key.
int minXORUtil(TrieNode* root, int key)
{
    TrieNode* temp = root;

    for (int i = INT_SIZE - 1; i >= 0; i--) {
        // Find current bit in given prefix
        bool current_bit = (key & (1 << i));

        // Traversal Trie, look for prefix that has
        // same bit
        if (temp->Child[current_bit] != NULL)
            temp = temp->Child[current_bit];

        // if there is no same bit.then looking for
        // opposite bit
        else if (temp->Child[1 - current_bit] != NULL)
            temp = temp->Child[1 - current_bit];
    }

    // return xor value of minimum bit difference value
    // so we get minimum xor value
    return key ^ temp->value;
}

// Returns minimum xor value of pair in arr[0..n-1]
int minXOR(int arr[], int n)
{
    int min_xor = INT_MAX; // Initialize result

    // create a True and insert first element in it
    TrieNode* root = getNode();
    insert(root, arr[0]);

    // Traverse all array element and find minimum xor
    // for every element
    for (int i = 1; i < n; i++) {
        // Find minimum XOR value of current element with
        // previous elements inserted in Trie
        min_xor = min(min_xor, minXORUtil(root, arr[i]));

        // insert current array value into Trie
        insert(root, arr[i]);
    }
    return min_xor;
}

// Driver code
int main()
{
    int arr[] = { 9, 5, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minXOR(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum XOR value in an array.
class GFG {
    static final int INT_SIZE = 32;

    // A Trie Node
    static class TrieNode {
        int value; // used in leaf node
        TrieNode[] Child = new TrieNode[2];

        public TrieNode()
        {
            value = 0;
            Child[0] = null;
            Child[1] = null;
        }
    }
    static TrieNode root;

    // utility function insert new key in trie
    static void insert(int key)
    {
        TrieNode temp = root;

        // start from the most significant bit, insert all
        // bit of key one-by-one into trie
        for (int i = INT_SIZE - 1; i >= 0; i--) {
            // Find current bit in given prefix
            int current_bit = (key & (1 << i)) >= 1 ? 1 : 0;

            // Add a new Node into trie
            if (temp != null && temp.Child[current_bit] == null)
                temp.Child[current_bit] = new TrieNode();

            temp = temp.Child[current_bit];
        }

        // store value at leafNode
        temp.value = key;
    }

    // Returns minimum XOR value of an integer inserted
    // in Trie and given key.
    static int minXORUtil(int key)
    {
        TrieNode temp = root;

        for (int i = INT_SIZE - 1; i >= 0; i--) {
            // Find current bit in given prefix
            int current_bit = (key & (1 << i)) >= 1 ? 1 : 0;

            // Traversal Trie, look for prefix that has
            // same bit
            if (temp.Child[current_bit] != null)
                temp = temp.Child[current_bit];

            // if there is no same bit.then looking for
            // opposite bit
            else if (temp.Child[1 - current_bit] != null)
                temp = temp.Child[1 - current_bit];
        }

        // return xor value of minimum bit difference value
        // so we get minimum xor value
        return key ^ temp.value;
    }

    // Returns minimum xor value of pair in arr[0..n-1]
    static int minXOR(int arr[], int n)
    {
        int min_xor = Integer.MAX_VALUE; // Initialize result

        // create a True and insert first element in it
        root = new TrieNode();
        insert(arr[0]);

        // Traverse all array element and find minimum xor
        // for every element
        for (int i = 1; i < n; i++) {
            // Find minimum XOR value of current element with
            // previous elements inserted in Trie
            min_xor = Math.min(min_xor, minXORUtil(arr[i]));

            // insert current array value into Trie
            insert(arr[i]);
        }
        return min_xor;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 9, 5, 3 };
        int n = arr.length;
        System.out.println(minXOR(arr, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# class for the basic Trie Node
class TrieNode:
    def __init__(self):

        # Child array with 0 and 1
        self.child = [None]*2

        # meant foor the lead Node
        self.value = None

class Trie:

    def __init__(self):
        # initialise the root Node
        self.root = self.getNode()

    def getNode(self):
        # get a new Trie Node
        return TrieNode()

    # inserts a new element
    def insert(self,key):
        temp = self.root

        # 32 bit valued binary digit
        for i in range(31,-1,-1):

            # finding the bit at ith position
            curr = (key>>i)&(1)

            # if the child is None create one
            if(temp.child[curr] is None):
                temp.child[curr] = self.getNode()
            temp = temp.child[curr]

        # add value to the leaf node
        temp.value = key

    # traverse the trie and xor with the most similar element
    def xorUtil(self,key):
        temp = self.root

        # 32 bit valued binary digit
        for i in range(31,-1,-1):

            # finding the bit at ith position
            curr = (key>>i)&1

            # traverse for the same bit
            if(temp.child[curr] is not None):
                temp = temp.child[curr]

            # traverse if the same bit is not set in trie
            elif(temp.child[1-curr] is not None):
                temp = temp.child[1-curr]

        # return with the xor of the value
        return temp.value^key

def minXor(arr):

        # set m to a large number
        m = 2**30

        # initialize Trie
        trie = Trie()

        # insert the first element
        trie.insert(arr[0])

        # for each element in the array
        for i in range(1,len(arr)):

            # find the minimum xor value
            m = min(m,trie.xorUtil(arr[i]))

            # insert the new element
            trie.insert(arr[i])
        return m

# Driver Code
if __name__=="__main__":
    sample = [9,5,3]
    print(minXor(sample))

#code contributed by Ashwin Bhat   
```

**输出:**

```
6
```

时间复杂度 O(n)
本文由 [**尼尚特 _ 辛格(平图)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。