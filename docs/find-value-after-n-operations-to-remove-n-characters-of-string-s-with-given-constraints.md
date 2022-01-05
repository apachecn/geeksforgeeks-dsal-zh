# 在给定约束条件下，N 次运算去除字符串 S 的 N 个字符后求值

> 原文:[https://www . geeksforgeeks . org/n-operations-to-remove-n-characters-of-string-s-with-given-constraints/](https://www.geeksforgeeks.org/find-value-after-n-operations-to-remove-n-characters-of-string-s-with-given-constraints/)

给定一根大小为 **N** 的绳子 **S** 。最初，计数的值是 **0** 。任务是在 **N** 次操作后找到计数值，以删除给定字符串 **S** 的所有 **N** 个字符，其中每次操作为:

*   在每个操作中，按字母顺序选择字符串 **S** 中最小的字符，并从 **S** 中删除该字符，并将其索引添加到计数中。
*   如果有多个字符，则删除索引最小的字符。

**注意:**将字符串视为基于 1 的索引。

**示例:**

> **输入:** N = 5，S =“abcab”
> **输出:** 8
> **解释:**
> 去掉字符‘a’则字符串变成“bcab”，计数= 1。
> 删除字符“a”，则字符串变为“bcb”，计数= 1 + 3 = 4。
> 去掉字符“b”，字符串变成“cb”，计数= 4 + 1 = 5。
> 去掉字符“b”，字符串变成“c”，计数= 5 + 2 = 7。
> 去掉字符‘c’，则字符串变为“”，计数= 7 + 1 = 8。
> 
> **输入:** N = 5 S = "aabbc"
> **输出:** 5
> **说明:**
> 去除 String aabbc 全部 5 个字符 5 次运算后的值为 5。

**天真方法:**想法是[检查字符串是否为空](https://www.geeksforgeeks.org/program-to-check-if-the-string-is-empty-in-java/)。如果它不是空的，那么下面是解决问题的步骤:

*   找到当前字符串中最小字母的第一个出现，比如 ***ind*** 并将其从字符串中移除。
*   将计数增加**至** + 1。
*   重复上述步骤，直到字符串变为空。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
#include <string>
using namespace std;

// Function to find the value after
// N operations to remove all the N
// characters of string S
void charactersCount(string str, int n)
{
    int count = 0;

    // Iterate till N
    while (n > 0) {

        char cur = str[0];
        int ind = 0;

        for (int j = 1; j < n; j++) {

            if (str[j] < cur) {
                cur = str[j];
                ind = j;
            }
        }

        // Remove character at ind and
        // decrease n(size of string)
        str.erase(str.begin() + ind);
        n--;

        // Increase count by ind+1
        count += ind + 1;
    }
    cout << count << endl;
}

// Driver Code
int main()
{
    // Given string str
    string str = "aabbc";
    int n = 5;

    // Function call
    charactersCount(str, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the value after
// N operations to remove all the N
// characters of String S
static void charactersCount(String str, int n)
{
    int count = 0;

    // Iterate till N
    while (n > 0)
    {
        char cur = str.charAt(0);
        int ind = 0;

        for(int j = 1; j < n; j++)
        {
            if (str.charAt(j) < cur)
            {
                cur = str.charAt(j);
                ind = j;
            }
        }

        // Remove character at ind and
        // decrease n(size of String)
        str = str.substring(0, ind) +
              str.substring(ind + 1);
        n--;

        // Increase count by ind+1
        count += ind + 1;
    }
    System.out.print(count + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given String str
    String str = "aabbc";

    int n = 5;

    // Function call
    charactersCount(str, n);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the value after
# N operations to remove all the N
# characters of String S
def charactersCount(str, n):

    count = 0;

    # Iterate till N
    while (n > 0):
        cur = str[0];
        ind = 0;

        for j in range(1, n):
            if (str[j] < cur):
                cur = str[j];
                ind = j;

        # Remove character at ind and
        # decrease n(size of String)
        str = str[0 : ind] + str[ind + 1:];
        n -= 1;

        # Increase count by ind+1
        count += ind + 1;

    print(count);

# Driver Code
if __name__ == '__main__':

    # Given String str
    str = "aabbc";

    n = 5;

    # Function call
    charactersCount(str, n);

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the value after
// N operations to remove all the N
// characters of String S
static void charactersCount(String str, int n)
{
    int count = 0;

    // Iterate till N
    while (n > 0)
    {
        char cur = str[0];
        int ind = 0;

        for(int j = 1; j < n; j++)
        {
            if (str[j] < cur)
            {
                cur = str[j];
                ind = j;
            }
        }

        // Remove character at ind and
        // decrease n(size of String)
        str = str.Substring(0, ind) +
              str.Substring(ind + 1);
        n--;

        // Increase count by ind+1
        count += ind + 1;
    }
    Console.Write(count + "\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Given String str
    String str = "aabbc";

    int n = 5;

    // Function call
    charactersCount(str, n);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the value after
    // N operations to remove all the N
    // characters of String S
    function charactersCount(str, n)
    {
        let count = 0;

        // Iterate till N
        while (n > 0)
        {
            let cur = str[0].charCodeAt();
            let ind = 0;

            for(let j = 1; j < n; j++)
            {
                if (str[j].charCodeAt() < cur)
                {
                    cur = str[j].charCodeAt();
                    ind = j;
                }
            }

            // Remove character at ind and
            // decrease n(size of String)
            str = str.substring(0, ind) +
                  str.substring(ind + 1);
            n--;

            // Increase count by ind+1
            count += ind + 1;
        }
        document.write(count + "</br>");
    }

    // Given String str
    let str = "aabbc";

    let n = 5;

    // Function call
    charactersCount(str, n);

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**这个问题可以使用[二元索引树或分支树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)的概念来解决。以下是步骤:

*   最初，以递增的顺序存储所有字符/字母表的索引值。
*   从最小的字母**‘a’**开始，按照出现的顺序去掉所有的**‘a’**。删除后，选择下一个字母 **'b'** ，重复此步骤，直到所有字母被删除。
*   删除字符意味着其在数组中的对应值变为 **0** ，表示被删除。
*   移除之前，使用**分威克树**中的 **sum()** 方法找到字符串中字符的位置，并将位置值添加到计数中。
*   移除字符串中的所有字符后，将获得 count 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of Fenwick tree
struct FenwickTree {

    // Binary indexed tree
    vector<int> bit;

    // bit[0] is not involved
    int n;

    // Constructor
    FenwickTree(int n)
    {
        this->n = n + 1;
        bit = vector<int>(n, 0);
    }

    // Constructor
    FenwickTree(vector<int> a)
        : FenwickTree(a.size())
    {
        for (size_t i = 0; i < a.size(); i++)
            add(i, a[i]);
    }

    // Sum of arr[0] + arr[1] + ...
    // + arr[idx] where arr is array
    int sum(int idx)
    {
        int ret = 0;

        // Index in BITree[] is 1 more
        // than the index in arr[]
        idx = idx + 1;

        // Traverse the ancestors of
        // BITree[index]
        while (idx > 0) {

            // Add current element
            // of BITree to sum
            ret += bit[idx];

            // Move index to parent
            // node in getSum View
            idx -= idx & (-idx);
        }

        // Return the result
        return ret;
    }

    // Function for adding arr[idx]
    // is equals to arr[idx] + val
    void add(int idx, int val)
    {

        // Val is nothing but "DELTA"
        // index in BITree[] is 1
        // more than the index in arr[]
        idx = idx + 1;

        // Traverse all ancestors
        // and add 'val'
        while (idx <= n) {

            // Add 'val' to current
            // node of BI Tree
            bit[idx] += val;

            // Update index to that
            // of parent in update View
            idx += idx & (-idx);
        }
    }

    // Update the index
    void update(int idx, int val)
    {
        add(idx, val - valat(idx));
    }

    // Perform the sum arr[l] + arr[l+1]
    // + ... + arr[r]
    int sum(int l, int r)
    {
        return sum(r) - sum(l - 1);
    }

    int valat(int i)
    {
        return sum(i, i);
    }

    void clr(int sz)
    {
        bit.clear();
        n = sz + 1;
        bit.resize(n + 1, 0);

        // Initially mark all
        // are present (i.e. 1)
        for (int i = 0; i < n; i++)
            add(i, 1);
    }
};

// Function to count the characters
void charactersCount(string str, int n)
{
    int i, count = 0;

    // Store the values of indexes
    // for each alphabet
    vector<vector<int> > mp
        = vector<vector<int> >(26,
                               vector<int>());

    // Create FenwickTree of size n
    FenwickTree ft = FenwickTree(n);
    ft.clr(n);

    // Initially no indexes are
    // stored for each character
    for (i = 0; i < 26; i++)
        mp[i].clear();

    i = 0;
    for (char ch : str) {

        // Push 'i' to mp[ch]
        mp[ch - 'a'].push_back(i);
        i++;
    }

    // Start with smallest character
    // and move towards larger character
    // i.e., from 'a' to 'z' (0 to 25)
    for (i = 0; i < 26; i++) {

        // index(ind) of current character
        // corres to i are obtained
        // in increasing order
        for (int ind : mp[i]) {

            // Find the number of characters
            // currently present before
            // ind using ft.sum(ind)
            count += ft.sum(ind);

            // Mark the corresponding
            // ind as removed and
            // make value at ind as 0
            ft.update(ind, 0);
        }
    }

    // Print the value of count
    cout << count << endl;
}

// Driver Code
int main()
{
    // Given string str
    string str = "aabbc";

    int n = 5;

    // Function call
    charactersCount(str, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of Fenwick tree
struct FenwickTree {

    // Binary indexed tree
    vector<int> bit;

    // bit[0] is not involved
    int n;

    // Constructor
    FenwickTree(int n)
    {
        this->n = n + 1;
        bit = vector<int>(n, 0);
    }

    // Constructor
    FenwickTree(vector<int> a)
        : FenwickTree(a.size())
    {
        for (size_t i = 0; i < a.size(); i++)
            add(i, a[i]);
    }

    // Sum of arr[0] + arr[1] + ...
    // + arr[idx] where arr is array
    int sum(int idx)
    {
        int ret = 0;

        // Index in BITree[] is 1 more
        // than the index in arr[]
        idx = idx + 1;

        // Traverse the ancestors of
        // BITree[index]
        while (idx > 0) {

            // Add current element
            // of BITree to sum
            ret += bit[idx];

            // Move index to parent
            // node in getSum View
            idx -= idx & (-idx);
        }

        // Return the result
        return ret;
    }

    // Function for adding arr[idx]
    // is equals to arr[idx] + val
    void add(int idx, int val)
    {

        // Val is nothing but "DELTA"
        // index in BITree[] is 1
        // more than the index in arr[]
        idx = idx + 1;

        // Traverse all ancestors
        // and add 'val'
        while (idx <= n) {

            // Add 'val' to current
            // node of BI Tree
            bit[idx] += val;

            // Update index to that
            // of parent in update View
            idx += idx & (-idx);
        }
    }

    // Update the index
    void update(int idx, int val)
    {
        add(idx, val - valat(idx));
    }

    // Perform the sum arr[l] + arr[l+1]
    // + ... + arr[r]
    int sum(int l, int r)
    {
        return sum(r) - sum(l - 1);
    }

    int valat(int i)
    {
        return sum(i, i);
    }

    void clr(int sz)
    {
        bit.clear();
        n = sz + 1;
        bit.resize(n + 1, 0);

        // Initially mark all
        // are present (i.e. 1)
        for (int i = 0; i < n; i++)
            add(i, 1);
    }
};

// Function to count the characters
void charactersCount(string str, int n)
{
    int i, count = 0;

    // Store the values of indexes
    // for each alphabet
    vector<vector<int> > mp
        = vector<vector<int> >(26,
                               vector<int>());

    // Create FenwickTree of size n
    FenwickTree ft = FenwickTree(n);
    ft.clr(n);

    // Initially no indexes are
    // stored for each character
    for (i = 0; i < 26; i++)
        mp[i].clear();

    i = 0;
    for (char ch : str) {

        // Push 'i' to mp[ch]
        mp[ch - 'a'].push_back(i);
        i++;
    }

    // Start with smallest character
    // and move towards larger character
    // i.e., from 'a' to 'z' (0 to 25)
    for (i = 0; i < 26; i++) {

        // index(ind) of current character
        // corres to i are obtained
        // in increasing order
        for (int ind : mp[i]) {

            // Find the number of character
            // currently present before
            // ind using ft.sum(ind)
            count += ft.sum(ind);

            // Mark the corresponding
            // ind as removed and
            // make value at ind as 0
            ft.update(ind, 0);
        }
    }

    // Print the value of count
    cout << count << endl;
}

// Driver Code
int main()
{
    // Given string str
    string str = "aabbc";

    int n = 5;

    // Function call
    charactersCount(str, n);
    return 0;
}
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Structure of Fenwick tree
public class FenwickTree
{

    // Binary indexed tree
    public int []bit;

    // bit[0] is not involved
    int n;

    // Constructor
    public FenwickTree(int n)
    {
        this.n = n + 1;
        bit = new int[n];
    }

    // Constructor
    public FenwickTree(List<int> a)
    {
        for(int i = 0; i < a.Count; i++)
            add(i, a[i]);
    }

    // Sum of arr[0] + arr[1] + ...
    // + arr[idx] where arr is array
    public int sum(int idx)
    {
        int ret = 0;

        // Index in BITree[] is 1 more
        // than the index in []arr
        idx = idx + 1;

        // Traverse the ancestors of
        // BITree[index]
        while (idx > 0)
        {

            // Add current element
            // of BITree to sum
            ret += bit[idx];

            // Move index to parent
            // node in getSum View
            idx -= idx & (-idx);
        }

        // Return the result
        return ret;
    }

    // Function for adding arr[idx]
    // is equals to arr[idx] + val
    public void add(int idx, int val)
    {

        // Val is nothing but "DELTA"
        // index in BITree[] is 1
        // more than the index in []arr
        idx = idx + 1;

        // Traverse all ancestors
        // and add 'val'
        while (idx <= n)
        {

            // Add 'val' to current
            // node of BI Tree
            bit[idx] += val;

            // Update index to that
            // of parent in update View
            idx += idx & (-idx);
        }
    }

    // Update the index
    public void update(int idx, int val)
    {
        add(idx, val - valat(idx));
    }

    // Perform the sum arr[l] + arr[l+1]
    // + ... + arr[r]
    public int sum(int l, int r)
    {
        return sum(r) - sum(l - 1);
    }

    public int valat(int i)
    {
        return sum(i, i);
    }

    public void clr(int sz)
    {
        n = sz + 1;
        bit = new int[n + 1];

        // Initially mark all
        // are present (i.e. 1)
        for(int i = 0; i < n; i++)
            add(i, 1);
    }
};

// Function to count the characters
static void charactersCount(String str, int n)
{
    int i, count = 0;

    // Store the values of indexes
    // for each alphabet
    List<int> []mp = new List<int>[26];
    for(i = 0; i < mp.Length; i++)
        mp[i] = new List<int>();

    // Create FenwickTree of size n
    FenwickTree ft = new FenwickTree(n);
    ft.clr(n);

    // Initially no indexes are
    // stored for each character
    for(i = 0; i < 26; i++)
        mp[i].Clear();

    i = 0;
    foreach(char ch in str.ToCharArray())
    {

        // Push 'i' to mp[ch]
        mp[ch - 'a'].Add(i);
        i++;
    }

    // Start with smallest character
    // and move towards larger character
    // i.e., from 'a' to 'z' (0 to 25)
    for(i = 0; i < 26; i++)
    {

        // index(ind) of current character
        // corres to i are obtained
        // in increasing order
        foreach(int ind in mp[i])
        {

            // Find the number of characters
            // currently present before
            // ind using ft.sum(ind)
            count += ft.sum(ind);

            // Mark the corresponding
            // ind as removed and
            // make value at ind as 0
            ft.update(ind, 0);
        }
    }

    // Print the value of count
    Console.Write(count + "\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Given String str
    String str = "aabbc";

    int n = 5;

    // Function call
    charactersCount(str, n);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Structure of Fenwick tree
class FenwickTree
{
    constructor(n)
    {
        this.n = n + 1;
        this.bit = new Array(n);
    }
    _FenwickTree(a)
    {
        for(let i = 0; i < a.length; i++)
            this.add(i, a.get(i));
    }

    // Sum of arr[0] + arr[1] + ...
    // + arr[idx] where arr is array
    sum(idx)
    {
        let ret = 0;

        // Index in BITree[] is 1 more
        // than the index in arr[]
        idx = idx + 1;

        // Traverse the ancestors of
        // BITree[index]
        while (idx > 0)
        {

            // Add current element
            // of BITree to sum
            ret += this.bit[idx];

            // Move index to parent
            // node in getSum View
            idx -= idx & (-idx);
        }

        // Return the result
        return ret;
    }

    // Function for adding arr[idx]
    // is equals to arr[idx] + val
    add(idx,val)
    {
        // Val is nothing but "DELTA"
        // index in BITree[] is 1
        // more than the index in arr[]
        idx = idx + 1;

        // Traverse all ancestors
        // and add 'val'
        while (idx <= this.n)
        {

            // Add 'val' to current
            // node of BI Tree
            this.bit[idx] += val;

            // Update index to that
            // of parent in update View
            idx += idx & (-idx);
        }
    }

    // Update the index
    update(idx,val)
    {
        this.add(idx, val - this.valat(idx));
    }

    // Perform the sum arr[l] + arr[l+1]
    // + ... + arr[r]
    _sum(l,r)
    {
        return this.sum(r) - this._sum(l - 1);
    }

    valat(i)
    {
        return this.sum(i, i);
    }

    clr(sz)
    {
        this.n = sz + 1;
        this.bit = new Array(this.n + 1);
         for(let i=0;i<this.n+1;i++)
            this.bit[i]=0;

        // Initially mark all
        // are present (i.e. 1)
        for(let i = 0; i < n; i++)
            this.add(i, 1);
    }
}

// Function to count the characters
function charactersCount(str,n)
{
    let i, count = 0;

    // Store the values of indexes
    // for each alphabet

    let mp = new Array(26);
    for(i = 0; i < mp.length; i++)
        mp[i] = [];

    // Create FenwickTree of size n
    let ft = new FenwickTree(n);
    ft.clr(n);

    // Initially no indexes are
    // stored for each character
    for(i = 0; i < 26; i++)
        mp[i]=[];

    i = 0;
    for(let ch of str.split("").values())
    {

        // Push 'i' to mp[ch]
        mp[ch.charCodeAt(0) - 'a'.charCodeAt(0)].push(i);
        i++;
    }

    // Start with smallest character
    // and move towards larger character
    // i.e., from 'a' to 'z' (0 to 25)
    for(i = 0; i < 26; i++)
    {

        // index(ind) of current character
        // corres to i are obtained
        // in increasing order
        for(let ind of mp[i].values())
        {

            // Find the number of characters
            // currently present before
            // ind using ft.sum(ind)
            count += ft.sum(ind);

            // Mark the corresponding
            // ind as removed and
            // make value at ind as 0
            ft.update(ind, 0);
        }
    }

    // Print the value of count
    document.write(count + "<br>");
}

// Driver Code
// Given String str
let str = "aabbc";

let n = 5;

// Function call
charactersCount(str, n);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*