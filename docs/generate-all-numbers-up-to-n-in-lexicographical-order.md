# 按照字典顺序生成 N 以内的所有数字

> 原文:[https://www . geesforgeks . org/generate-all-numbers-up-n-in-in-accordinary-order/](https://www.geeksforgeeks.org/generate-all-numbers-up-to-n-in-lexicographical-order/)

给定一个整数 **N** ，任务是按照[字典顺序](https://en.wikipedia.org/wiki/Lexicographical_order)打印所有到 **N** 的数字。

**示例:**

> **输入:** N = 15
> **输出:**
> 1 10 11 12 13 14 15 2 3 4 5 6 7 8 9
> 
> **输入:** N = 19
> **输出:**
> 1 10 11 12 13 14 15 16 17 18 19 2 3 4 5 7 8 9

**进场:**
为了解决问题，按照以下步骤进行:

*   从 1 迭代到 N，以字符串的形式存储所有的数字。
*   [对包含字符串的向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)进行排序。

下面是上述方法的实现:

## C++

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all the
// numbers up to n in
// lexicographical order
void lexNumbers(int n)
{
    vector<string> s;

    for (int i = 1; i <= n; i++) {
        s.push_back(to_string(i));
    }

    sort(s.begin(), s.end());
    vector<int> ans;
    for (int i = 0; i < n; i++)
        ans.push_back(stoi(s[i]));

    for (int i = 0; i < n; i++)
        cout << ans[i] << " ";
}
// Driver Program
int main()
{

    int n = 15;
    lexNumbers(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the
// above approach
import java.util.*;
class GFG{

// Function to print all the
// numbers up to n in
// lexicographical order
static void lexNumbers(int n)
{
    Vector<String> s = new Vector<String>();

    for (int i = 1; i <= n; i++)
    {
        s.add(String.valueOf(i));
    }

    Collections.sort(s);
    Vector<Integer> ans = new Vector<Integer>();
    for (int i = 0; i < n; i++)
        ans.add(Integer.valueOf(s.get(i)));

    for (int i = 0; i < n; i++)
        System.out.print(ans.get(i) + " ");
}
// Driver Program
public static void main(String[] args)
{
    int n = 15;
    lexNumbers(n);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to implement
# above approach

# Function to print all the
# numbers up to n in
# lexicographical order
def lexNumbers(n):

    s = []
    for i in range(1, n + 1):
        s.append(str(i))

    s.sort()
    ans = []

    for i in range(n):
        ans.append(int(s[i]))

    for i in range(n):
        print(ans[i], end = ' ')

# Driver Code
if __name__ == "__main__":

    n = 15
    lexNumbers(n)

# This code is contributed by Ediga_Manisha
```

## C#

```
// C# program to implement the
// above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print all the
// numbers up to n in
// lexicographical order
static void lexNumbers(int n)
{
    List<String> s = new List<String>();

    for(int i = 1; i <= n; i++)
    {
       s.Add(String.Join("", i));
    }

    s.Sort();
    List<int> ans = new List<int>();

    for(int i = 0; i < n; i++)
       ans.Add(Int32.Parse(s[i]));

    for(int i = 0; i < n; i++)
       Console.Write(ans[i] + " ");
}

// Driver code
public static void Main(String[] args)
{
    int n = 15;

    lexNumbers(n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript Program to implement the
// above approach

// Function to print all the
// numbers up to n in
// lexicographical order
function lexNumbers(n)
{
    let s = [];

    for (let i = 1; i <= n; i++)
    {
        s.push(i.toString());
    }

    s.sort();
    let ans = [];
    for (let i = 0; i < n; i++)
        ans.push(parseInt(s[i]));

    for (let i = 0; i < n; i++)
        document.write(ans[i] + " ");
}

// Driver Program
let n = 15;
lexNumbers(n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
1 10 11 12 13 14 15 2 3 4 5 6 7 8 9 
```

**另一种方法:**

*   使用 DFS:始终将温度乘以 10，直到温度* 10 大于 n
*   当 temp 的最后一位不等于 9 时，将 temp 增加 1

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

void dfs(int temp, int n, vector<int> &sol);

void lexNumbers(int n)
{
    vector<int> sol;
    dfs(1, n, sol);
    cout << "[" << sol[0];
    for (int i = 1; i < sol.size(); i++)
       cout << ", "<< sol[i];
    cout << "]";
}

void dfs(int temp, int n, vector<int> &sol)
{
    if (temp > n)
        return;
    sol.push_back(temp);
    dfs(temp * 10, n, sol);
    if (temp % 10 != 9)
        dfs(temp + 1, n, sol);
}

int main()
{
    int n = 15;
    lexNumbers(n);
    return 0;
}

// This Code is contributed by ShubhamSingh10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    public static void lexNumbers(int n)
    {
        List<Integer> sol = new ArrayList<>();
        dfs(1, n, sol);
        System.out.println(sol);
    }

    public static void dfs(int temp, int n,
                           List<Integer> sol)
    {
        if (temp > n)
            return;
        sol.add(temp);
        dfs(temp * 10, n, sol);
        if (temp % 10 != 9)
            dfs(temp + 1, n, sol);
    }

    public static void main(String[] args)
    {
        int n = 15;
        lexNumbers(n);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach
def lexNumbers(n):
    sol = []
    dfs(1, n, sol)
    print("[", sol[0], end= "", sep ="")
    for i in range(1,n):
        print(", ", sol[i], end= "", sep ="")
    print("]")

def dfs(temp, n, sol):
    if (temp > n):
        return
    sol.append(temp)
    dfs(temp * 10, n, sol)
    if (temp % 10 != 9):
        dfs(temp + 1, n, sol)

n = 15
lexNumbers(n)

# This Code is contributed by ShubhamSingh10
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

public static void lexNumbers(int n)
{
    List<int> sol = new List<int>();
    dfs(1, n, sol);
    Console.WriteLine("[" + string.Join(", ", sol) + "]");
}

public static void dfs(int temp, int n,
                       List<int> sol)
{
    if (temp > n)
        return;

    sol.Add(temp);
    dfs(temp * 10, n, sol);

    if (temp % 10 != 9)
        dfs(temp + 1, n, sol);
}

// Driver code
public static void Main()
{
    int n = 15;
    lexNumbers(n);
}
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
function lexNumbers(n)
{
    var sol = [];
    dfs(1, n, sol);
    document.write("["+ sol[0]);
    for (var i = 1; i < sol.length; i++)
       document.write(", "+ sol[i]);
    document.write("]");
}

function dfs(temp, n, sol)
{
    if (temp > n)
        return;
    sol.push(temp);
    dfs(temp * 10, n, sol);
    if (temp % 10 != 9)
        dfs(temp + 1, n, sol);
}

var n = 15;
lexNumbers(n);

// This Code is contributed by ShubhamSingh10

</script>
```

**Output**

```
[1, 10, 11, 12, 13, 14, 15, 2, 3, 4, 5, 6, 7, 8, 9]
```

**时间复杂度:**O(N)
T3】辅助空间: O (1)

**当存在范围时:-**

给定两个整数 L 和 R，任务是以字典顺序打印 L 到 R(包括 L 和 R)范围内的所有数字。

**示例:**

```
Input: L = 9 , R = 21
Output:  
10 11 12 13 14 15 16 17 18 19 20 21 9
Input: L = 1 , R= 13
Output:  
1 10 11 12 13 2 3 4 5 6 7 8 9
```

**进场:**

为了解决问题，请按照以下步骤操作:

*   从 L 迭代到 R(包括 L 和 R)，并将所有数字以字符串的形式存储。
*   对包含字符串的向量进行排序。

下面是上述方法的实现:

## C++

```
// C++ program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all the
// numbers form l to r in
// lexicographical order
void lexNumbers(int l, int r)
{
    vector<string> s;

    for(int i = l; i <= r; i++)
    {
        s.push_back(to_string(i));
    }

    sort(s.begin(),s.end());
    vector<int> ans;

    for(int i = 0; i < s.size(); i++)
        ans.push_back(stoi(s[i]));

    for(int i = 0; i < s.size(); i++)
        cout << ans[i] << " ";
}

// Driver code
int main()
{
    int l = 9;
    int r = 21;

    lexNumbers(l, r);
}

// This code is contributed by ajaykr00kj
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the
// above approach
import java.util.*;
class GFG {

    // Function to print all the
    // numbers form l to r in
    // lexicographical order
    static void lexNumbers(int l, int r)
    {
        Vector<String> s = new Vector<String>();

        for (int i = l; i <= r; i++) {
            s.add(String.valueOf(i));
        }

        Collections.sort(s);
        Vector<Integer> ans = new Vector<Integer>();
        for (int i = 0; i < s.size(); i++)
            ans.add(Integer.valueOf(s.get(i)));

        for (int i = 0; i < s.size(); i++)
            System.out.print(ans.get(i) + " ");
    }
    // Driver Program
    public static void main(String[] args)
    {
        int l = 9;
        int r = 21;
        lexNumbers(l, r);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Function to print all the
# numbers form l to r in
# lexicographical order
def lexNumbers(l, r):

    s = []

    for i in range(l, r + 1):
        s.append(str(i))

    s.sort()
    ans = []

    for i in range(len(s)):
        ans.append(int(s[i]))

    for i in range(len(s)):
        print(ans[i], end = " ")

# Driver code
if __name__ == "__main__":

    l = 9
    r = 21
    lexNumbers(l, r)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement the
// above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to print all the
  // numbers form l to r in
  // lexicographical order
  static void lexNumbers(int l, int r)
  {
    List<String> s = new List<String>();

    for (int i = l; i <= r; i++)
    {
      s.Add(String.Join("", i));
    }

    s.Sort();
    List<int> ans = new List<int>();

    for (int i = 0; i < s.Count; i++)
      ans.Add(Int32.Parse(s[i]));

    for (int i = 0; i < s.Count; i++)
      Console.Write(ans[i] + " ");
  }

  // Driver Program
  static public void Main()
  {
    int l = 9;
    int r = 21;
    lexNumbers(l, r);
  }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
// Javascript Program to implement the
// above approach

    // Function to print all the
    // numbers form l to r in
    // lexicographical order
    function lexNumbers(l,r)
    {
        let s = [];

        for (let i = l; i <= r; i++) {
            s.push((i).toString());
        }

        s.sort();
        let ans = [];
        for (let i = 0; i < s.length; i++)
            ans.push(parseInt(s[i]));

        for (let i = 0; i < s.length; i++)
            document.write(ans[i] + " ");
    }

    // Driver Program
    let  l = 9;
    let r = 21;
    lexNumbers(l, r);

// This code is contributed by rag2127
</script>
```

**Output**

```
10 11 12 13 14 15 16 17 18 19 20 21 9 
```

**时间复杂度:**O(N * logN)
T3】辅助空间: O (1)