# 字符串范围查询，查找等于给定字符串的子集数量

> 原文:[https://www . geesforgeks . org/string-range-query-to-find-子集数-等于给定的字符串/](https://www.geeksforgeeks.org/string-range-queries-to-find-the-number-of-subsets-equal-to-a-given-string/)

给定一个长度为 N 的字符串 S，以下类型的 M 个查询:

> **类型 1:** 1 L x，
> 表示通过字符‘x’更新字符串 S 的 Lth 索引。
> **类型 2:** 2 L R str
> 求 L 到 R
> 范围内的子集数，等于字符串模 1000000007。
> **约束:**
> |S| < = 100000、
> M < = 100000、
> 1 < = L、R < = |S|、
> |str| < = 26、
> str 中所有字符都是唯一的，
> S & str 由小写拉丁字母组成。

**示例:**

> **输入:** N = 16，M = 3，S =“geekkksgskegks”
> 类型= 2: L = 1，R = 7，str =“gek”
> 类型= 1:索引= 2，字符= 'x'
> 类型= 2: L = 1，R = 7，str =“gek”
> **输出:** 9 6 4
> 查询 2:等于**的字符串 S i 范围[1…7]中的子集数
> 查询 1:第二次查询后字符串 S 变为**gxeekkksgskegks**。
> 查询 2:字符串 S i 范围[1…7]中等于 **gek** 的子集数为 6。**

**天真方法:**
查询类型 1:我们将计算查询字符串的每个字符在[L…R]范围内的频率，然后将所有计算出的频率相乘，得到想要的结果。
查询类型 2:我们将用给定的字符替换字符串的第 I 个字符。

**时间复杂度:** 0(m*n)

**有效方法:**

1.  使用*段树*我们可以在 log(n)时间内执行这两个操作。段树的每个节点将包含范围[1]内的字符频率..R]。
2.  函数**构建**需要 n*log(n)时间来创建一个段树，其中每个节点都包含字符串某个段的字符频率。
3.  函数 **get** 返回一个包含所有字符频率的向量。给定查询字符串的所有频率的乘积以 1e9+7 为模得到期望的结果。
4.  功能**更新**减少了先前放置的字符的频率，并增加了一个出现在分段树节点中的新字符的频率。
5.  函数 **add_two_result** 将两个向量相加并返回它们的结果。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

#define N 400005
#define mod 1000000007

vector <int> seg_tree[N];
string str;

// A recursive function that constructs
// Segment Tree for given string
void build(int pos, int st, int en)
{

    if (st == en)
    {
        // Increment the frequency of character
        // by one if st is equal to en
        seg_tree[pos][str[st - 1] - 'a']++;
        return ;
    }

    int mid = st + en >> 1;

    // Build the segment tree for range st to mid
    build(2 * pos, st, mid);

    // Build the segment tree for range mid+1 to en
    build(2 * pos + 1, mid + 1, en);

    // It stores addition of frequency of
    // characters of both of its child after
    // segment tree is build
    for (int i = 0; i < 26; i++)
        seg_tree[pos][i] = seg_tree[2 * pos + 1][i]
                             + seg_tree[2 * pos][i];

}

// A utility function for
// addition of two vectors
vector <int> add_two_result(vector <int> v1,
                                  vector <int> v2)
{
    vector <int> added_vec(26);

    // Adding two vector and storing
    // it in another vector
    for (int i = 0; i < 26; i++)
        added_vec[i] = v1[i] + v2[i];

    // Returning final vector
    return added_vec;

}

// A recursive function that return vector
// which contains frequency of every character
vector <int> get(int pos, int l, int r,
                               int st, int en)
{
    // If segment of this node is
    // outside the given range
    if (l > en || r < st)
    {
        vector <int> empty(26, 0);
        return  empty;
    }

    // If segment of this node is a part
    // of given range, then return the
    // frequency every character of the segment
    if (st >= l && en <= r)
    {
        return seg_tree[pos];
    }

    // getting mid of st and en
    int mid = st + en >> 1;

    //storing answer of left child n v1
    vector <int> v1 = get(2 * pos, l,
                                    r, st, mid);
    //storing answer of left child n v1
    vector <int> v2 = get(2 * pos + 1,
                             l, r, mid + 1, en);

    //returning the addition of both vectors
    return add_two_result(v1, v2);

}

// A recursive function that update
// frequency of new and old character
void update(int pos, int indx, int st,
                    int en, char pre, char cur) {

    // If segment of this node is
    // outside the given range
    if (indx > en || indx < st) return;

    // Subtract frequency of previous character
    seg_tree[pos][pre - 'a']--;

    // Add frequency of new character
    seg_tree[pos][cur - 'a']++;

    if (st != en)
    {
        int mid = st + en >> 1;

        // update left child
        update(2 * pos, indx, st,
                              mid, pre, cur);

        // update right child
        update(2 * pos + 1, indx,
                       mid + 1, en, pre, cur);
    }

}

// Utility function to
// initialize seg_tree vector
void initialize()
{
    for (int i = 0; i < N; i++)
        seg_tree[i].resize(26, 0);
}

int count_frequency(string s, vector <int> v)
{
    int ans = 1;
    // multiplying frequency of all
    // characters in string hard
    for (int i = 0; s[i]; i++)
        ans = (ans * v[s[i] - 'a']) % mod;

    return ans;
}

// Driver Code
int main()
{
    int n, q, ans;
    vector <int> v;

    n = 15;
    str = "haardhhardrddrd";

    //initialize and build the seg_tree vector
    initialize();
    build(1, 1, n);
    string s = "hard";

    // getting frequency of all
    // characters from 1 to 5
    v = get(1, 1, 5, 1, n);

    // Calling count_frequency
    ans = count_frequency(s, v);

    cout << ans << '\n';

    // Updating character at index 3
    update(1, 3, 1, n, str[2], 'x');
    str[2] = 'x';

    // getting frequency of all
    // characters from 1 to 5
    v = get(1, 1, 5, 1, n);

    //calling count_frequency
    ans = count_frequency(s, v);

    cout << ans << '\n';

    return 0;

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    final static int N = 400005;
    final static int mod = 1000000007;

    static int[][] seg_tree = new int[N][26];
    static StringBuilder str;

    // A recursive function that constructs
    // Segment Tree for given String
    static void build(int pos, int st, int en) {

        if (st == en) {

            // Increment the frequency of character
            // by one if st is equal to en
            seg_tree[pos][str.charAt(st - 1) - 'a']++;
            return;
        }

        int mid = st + en >> 1;

        // Build the segment tree for range st to mid
        build(2 * pos, st, mid);

        // Build the segment tree for range mid+1 to en
        build(2 * pos + 1, mid + 1, en);

        // It stores addition of frequency of
        // characters of both of its child after
        // segment tree is build
        for (int i = 0; i < 26; i++)
            seg_tree[pos][i] = seg_tree[2 * pos + 1][i] + seg_tree[2 * pos][i];

    }

    // A utility function for
    // addition of two vectors
    static int[] add_two_result(int[] v1, int[] v2) {
        int[] added_vec = new int[26];

        // Adding two vector and storing
        // it in another vector
        for (int i = 0; i < 26; i++)
            added_vec[i] = v1[i] + v2[i];

        // Returning final vector
        return added_vec;

    }

    // A recursive function that return vector
    // which contains frequency of every character
    static int[] get(int pos, int l, int r, int st, int en) {

        // If segment of this node is
        // outside the given range
        if (l > en || r < st) {
            int[] empty = new int[26];
            return empty;
        }

        // If segment of this node is a part
        // of given range, then return the
        // frequency every character of the segment
        if (st >= l && en <= r) {
            return seg_tree[pos];
        }

        // getting mid of st and en
        int mid = st + en >> 1;

        // storing answer of left child n v1
        int[] v1 = get(2 * pos, l, r, st, mid);

        // storing answer of left child n v1
        int[] v2 = get(2 * pos + 1, l, r, mid + 1, en);

        // returning the addition of both vectors
        return add_two_result(v1, v2);
    }

    // A recursive function that update
    // frequency of new and old character
    static void update(int pos, int indx, int st, int en, char pre, char cur) {

        // If segment of this node is
        // outside the given range
        if (indx > en || indx < st)
            return;

        // Subtract frequency of previous character
        seg_tree[pos][pre - 'a']--;

        // Add frequency of new character
        seg_tree[pos][cur - 'a']++;

        if (st != en) {
            int mid = st + en >> 1;

            // update left child
            update(2 * pos, indx, st, mid, pre, cur);

            // update right child
            update(2 * pos + 1, indx, mid + 1, en, pre, cur);
        }
    }

    static int count_frequency(String s, int[] v) {
        int ans = 1;

        // multiplying frequency of all
        // characters in String hard
        for (int i = 0; i < s.length(); i++)
            ans = (ans * v[s.charAt(i) - 'a']) % mod;

        return ans;
    }

    // Driver Code
    public static void main(String[] args) {

        int n, q, ans;
        int[] v;

        n = 15;
        str = new StringBuilder("haardhhardrddrd");

        build(1, 1, n);
        String s = "hard";

        // getting frequency of all
        // characters from 1 to 5
        v = get(1, 1, 5, 1, n);

        // Calling count_frequency
        ans = count_frequency(s, v);

        System.out.println(ans);

        // Updating character at index 3
        update(1, 3, 1, n, str.charAt(2), 'x');
        str.setCharAt(2, 'x');

        // getting frequency of all
        // characters from 1 to 5
        v = get(1, 1, 5, 1, n);

        // calling count_frequency
        ans = count_frequency(s, v);

        System.out.println(ans);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 400005
mod = 1000000007

seg_tree = [[0 for i in range(26)] for i in range(N)]
str = ""

# A recursive function that constructs
# Segment Tree for given
def build(pos, st, en):

    if (st == en):

        # Increment the frequency of character
        # by one if st is equal to en
        seg_tree[pos][ord(str[st - 1] )- ord('a')]+=1
        return

    mid = st + en >> 1

    # Build the segment tree for range st to mid
    build(2 * pos, st, mid)

    # Build the segment tree for range mid+1 to en
    build(2 * pos + 1, mid + 1, en)

    # It stores addition of frequency of
    # characters of both of its child after
    # segment tree is build
    for i in range(26):
        seg_tree[pos][i] = seg_tree[2 * pos + 1][i] + \
                            seg_tree[2 * pos][i]

# A utility function for
# addition of two vectors
def add_two_result(v1,v2):

    added_vec=[0]*(26)

    # Adding two vector and storing
    # it in another vector
    for i in range(26):
        added_vec[i] = v1[i] + v2[i]

    # Returning final vector
    return added_vec

# A recursive function that return vector
# which contains frequency of every character
def get(pos, l, r,st, en):

    # If segment of this node is
    # outside the given range
    if (l > en or r < st):
        empty = [0]*26
        return empty

    # If segment of this node is a part
    # of given range, then return the
    # frequency every character of the segment
    if (st >= l and en <= r):

        return seg_tree[pos]

    # getting mid of st and en
    mid = st + en >> 1

    # storing answer of left child n v1
    v1 = get(2 * pos, l,r, st, mid)

    # storing answer of left child n v1
    v2 = get(2 * pos + 1,l, r, mid + 1, en)

    # returning the addition of both vectors
    return add_two_result(v1, v2)

# A recursive function that update
# frequency of new and old character
def update(pos, indx, st,en,pre,cur):

    # If segment of this node is
    # outside the given range
    if (indx > en or indx < st):
        return

    # Subtract frequency of previous character
    seg_tree[pos][ord(pre) - ord('a')]-=1

    # Add frequency of new character
    seg_tree[pos][ord(cur) - ord('a')]+=1

    if (st != en):

        mid = st + en >> 1

        # update left child
        update(2 * pos,indx, st,mid, pre, cur)

        # update right child
        update(2 * pos + 1, indx,mid + 1, en, pre, cur)

def count_frequency(s,v):

    ans = 1

    # multiplying frequency of all
    # characters in hard
    i = 0
    while i < len(s):
        ans = (ans * v[ord(s[i]) - ord('a')]) % mod
        i += 1

    return ans

# Driver Code
if __name__ == '__main__':
    v=[]

    n = 15
    str = "haardhhardrddrd"
    str=[i for i in str]

    build(1, 1, n)
    s = "hard"

    # getting frequency of all
    # characters from 1 to 5
    v = get(1, 1, 5, 1, n)

    # Calling count_frequency
    ans = count_frequency(s, v)

    print(ans)

    # Updating character at index 3
    update(1, 3, 1, n, str[2], 'x')
    str[2] = 'x'

    # getting frequency of all
    # characters from 1 to 5
    v = get(1, 1, 5, 1, n)

    # calling count_frequency
    ans = count_frequency(s, v)

    print(ans)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Text;

class GFG{

readonly static int N = 400005;
readonly static int mod = 1000000007;

static int[,] seg_tree = new int[N, 26];
static StringBuilder str;

// A recursive function that constructs
// Segment Tree for given String
static void build(int pos, int st, int en)
{
    if (st == en)
    {

        // Increment the frequency of character
        // by one if st is equal to en
        seg_tree[pos,str[st - 1] - 'a']++;
        return;
    }

    int mid = st + en >> 1;

    // Build the segment tree for range st to mid
    build(2 * pos, st, mid);

    // Build the segment tree for range mid+1 to en
    build(2 * pos + 1, mid + 1, en);

    // It stores addition of frequency of
    // characters of both of its child after
    // segment tree is build
    for(int i = 0; i < 26; i++)
        seg_tree[pos, i] = seg_tree[2 * pos + 1, i] +
                           seg_tree[2 * pos, i];
}

// A utility function for
// addition of two vectors
static int[] add_two_result(int[] v1, int[] v2)
{
    int[] added_vec = new int[26];

    // Adding two vector and storing
    // it in another vector
    for(int i = 0; i < 26; i++)
        added_vec[i] = v1[i] + v2[i];

    // Returning readonly vector
    return added_vec;
}

// A recursive function that return vector
// which contains frequency of every character
static int[] get(int pos, int l, int r, int st, int en)
{

    // If segment of this node is
    // outside the given range
    if (l > en || r < st)
    {
        int[] empty = new int[26];
        return empty;
    }

    // If segment of this node is a part
    // of given range, then return the
    // frequency every character of the segment
    if (st >= l && en <= r)
    {
        return GetRow(seg_tree, pos);
    }

    // Getting mid of st and en
    int mid = st + en >> 1;

    // Storing answer of left child n v1
    int[] v1 = get(2 * pos, l, r, st, mid);

    // Storing answer of left child n v1
    int[] v2 = get(2 * pos + 1, l, r, mid + 1, en);

    // Returning the addition of both vectors
    return add_two_result(v1, v2);
}

// A recursive function that update
// frequency of new and old character
static void update(int pos, int indx, int st,
                   int en, char pre, char cur)
{

    // If segment of this node is
    // outside the given range
    if (indx > en || indx < st)
        return;

    // Subtract frequency of previous character
    seg_tree[pos,pre - 'a']--;

    // Add frequency of new character
    seg_tree[pos,cur - 'a']++;

    if (st != en)
    {
        int mid = st + en >> 1;

        // update left child
        update(2 * pos, indx, st, mid, pre, cur);

        // update right child
        update(2 * pos + 1, indx, mid + 1,
               en, pre, cur);
    }
}

static int count_frequency(String s, int[] v)
{
    int ans = 1;

    // Multiplying frequency of all
    // characters in String hard
    for(int i = 0; i < s.Length; i++)
        ans = (ans * v[s[i] - 'a']) % mod;

    return ans;
}

public static int[] GetRow(int[,] matrix, int row)
{
    var rowLength = matrix.GetLength(1);
    var rowVector = new int[rowLength];

    for(var i = 0; i < rowLength; i++)
        rowVector[i] = matrix[row, i];

    return rowVector;
}

// Driver Code
public static void Main(String[] args)
{

    int n, ans;
    int[] v;

    n = 15;
    str = new StringBuilder("haardhhardrddrd");

    build(1, 1, n);
    String s = "hard";

    // Getting frequency of all
    // characters from 1 to 5
    v = get(1, 1, 5, 1, n);

    // Calling count_frequency
    ans = count_frequency(s, v);

    Console.WriteLine(ans);

    // Updating character at index 3
    update(1, 3, 1, n, str[2], 'x');
    str[2] = 'x';

    // Getting frequency of all
    // characters from 1 to 5
    v = get(1, 1, 5, 1, n);

    // Calling count_frequency
    ans = count_frequency(s, v);

    Console.WriteLine(ans);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var N = 400005;
var mod = 1000000007;

var seg_tree = Array.from(Array(N), ()=>Array(26).fill(0));
var str = "";

// A recursive function that constructs
// Segment Tree for given String
function build(pos, st, en)
{
    if (st == en)
    {

        // Increment the frequency of character
        // by one if st is equal to en
        seg_tree[pos][str[st - 1].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        return;
    }

    var mid = st + en >> 1;

    // Build the segment tree for range st to mid
    build(2 * pos, st, mid);

    // Build the segment tree for range mid+1 to en
    build(2 * pos + 1, mid + 1, en);

    // It stores addition of frequency of
    // characters of both of its child after
    // segment tree is build
    for(var i = 0; i < 26; i++)
        seg_tree[pos][ i] = seg_tree[2 * pos + 1][ i] +
                           seg_tree[2 * pos][ i];
}

// A utility function for
// addition of two vectors
function add_two_result(v1, v2)
{
    var added_vec = Array(26).fill(0);

    // Adding two vector and storing
    // it in another vector
    for(var i = 0; i < 26; i++)
        added_vec[i] = v1[i] + v2[i];

    // Returning readonly vector
    return added_vec;
}

// A recursive function that return vector
// which contains frequency of every character
function get(pos, l, r, st, en)
{

    // If segment of this node is
    // outside the given range
    if (l > en || r < st)
    {
        var empty = Array(26).fill(0);
        return empty;
    }

    // If segment of this node is a part
    // of given range, then return the
    // frequency every character of the segment
    if (st >= l && en <= r)
    {
        return GetRow(seg_tree, pos);
    }

    // Getting mid of st and en
    var mid = st + en >> 1;

    // Storing answer of left child n v1
    var v1 = get(2 * pos, l, r, st, mid);

    // Storing answer of left child n v1
    var v2 = get(2 * pos + 1, l, r, mid + 1, en);

    // Returning the addition of both vectors
    return add_two_result(v1, v2);
}

// A recursive function that update
// frequency of new and old character
function update(pos, indx, st, en, pre, cur)
{

    // If segment of this node is
    // outside the given range
    if (indx > en || indx < st)
        return;

    // Subtract frequency of previous character
    seg_tree[pos][pre.charCodeAt(0) - 'a'.charCodeAt(0)]--;

    // Add frequency of new character
    seg_tree[pos][cur.charCodeAt(0) - 'a'.charCodeAt(0)]++;

    if (st != en)
    {
        var mid = st + en >> 1;

        // update left child
        update(2 * pos, indx, st, mid, pre, cur);

        // update right child
        update(2 * pos + 1, indx, mid + 1,
               en, pre, cur);
    }
}

function count_frequency(s, v)
{
    var ans = 1;

    // Multiplying frequency of all
    // characters in String hard
    for(var i = 0; i < s.length; i++)
        ans = (ans * v[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]) % mod;

    return ans;
}

function GetRow(matrix, row)
{
    var rowLength = matrix[0].length;
    var rowVector = Array(rowLength).fill(0);

    for(var i = 0; i < rowLength; i++)
        rowVector[i] = matrix[row][i];

    return rowVector;
}

// Driver Code
var n, ans;
var v = [];
n = 15;
str = "haardhhardrddrd".split('');
build(1, 1, n);
var s = "hard";

// Getting frequency of all
// characters from 1 to 5
v = get(1, 1, 5, 1, n);

// Calling count_frequency
ans = count_frequency(s, v);
document.write(ans+"<br>");

// Updating character at index 3
update(1, 3, 1, n, str[2], 'x');
str[2] = 'x';

// Getting frequency of all
// characters from 1 to 5
v = get(1, 1, 5, 1, n);

// Calling count_frequency
ans = count_frequency(s, v);
document.write(ans);

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
2
1
```

**时间复杂度:** 0(m*log(n)+n*log(n))
**辅助空间:** O(n)