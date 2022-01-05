# 打印列表的所有递增子序列

> 原文:[https://www . geesforgeks . org/print-all-递增子序列列表/](https://www.geeksforgeeks.org/print-all-increasing-subsequence-of-a-list/)

给定一个整数列表或数组，任务是打印该列表中所有这样的子序列，其中元素以递增的顺序排列。
列表的*子序列*是该列表元素的有序子集，其顺序与原始列表相同。
**示例:**

> **输入:** arr = {1，2]}
> **输出:**
> 2
> 1
> 1 2
> **输入:** arr = {1，3，2}
> **输出:**
> 2
> 3
> 1
> 1 2
> 1 3

**进场:**

*   在这里，我们将使用递归来找到所需的输出。
*   该函数将使用两个列表作为参数，基本条件是，直到列表为空。
*   在递归的每一步，我们将决定是包含还是排除原始列表中的特定元素。
*   为此，我们将维护两个列表，即 **inp** 和 **out** ，这是该步骤的输入和输出列表。
*   在输出列表中包含一个元素时，我们将检查该元素是否大于输出列表中的最后一个元素，如果是，那么我们将包含该元素。
*   当输入列表的长度变为零时，输出列表将包含所需的输出。这也是一个基本条件。

以下是上述方法的实现:

## C++

```
// C++ implementation to store all
// increasing subsequence of the given list
#include<bits/stdc++.h>
using namespace std;

vector<vector<int>>st;

// Method to find increasing subsequence
void find(vector<int>inp, vector<int>out)
{
    if(inp.size() == 0)
    {
        if(out.size() != 0)
        {

            // Storing result
            st.push_back(out);
        }
        return;
    }

    vector<int>temp;
    temp.push_back(inp[0]);

    // Excluding 1st element
    inp.erase(inp.begin());
    find(inp, out);

    // Including first element
    // checking the condition
    // for increasing subsequence
    if(out.size() == 0)
        find(inp, temp);

    else if(temp[0] > out[out.size() - 1])
    {
        out.push_back(temp[0]);
        find(inp, out);
    }
}

// Driver code
int main()
{

    // Input list
    vector<int>ls1 = { 1, 3, 2 };
    vector<int>ls2;

    // Calling the function
    find(ls1, ls2);

    // Printing the list
    for(int i = 0; i < st.size(); i++)
    {
        for(int j = 0; j < st[i].size(); j++)
            cout << st[i][j] << " ";

        cout << endl;
    }
}

// This code is contributed by Stream_Cipher
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to store all
// increasing subsequence of the given list
import java.util.*;
public class Main
{
    static Vector<Vector<Integer>> st = new Vector<Vector<Integer>>();
    static int[][] add = {{1,2}, {1,3}};

    // Method to find increasing subsequence
    static void find(Vector<Integer> inp, Vector<Integer> Out)
    {
        if(inp.size() == 0)
        {
            if(Out.size() != 0)
            {
                // Storing result
                st.add(Out);
            }
            return;
        }

        Vector<Integer> temp = new Vector<Integer>();
        temp.add(inp.get(0));

        // Excluding 1st element
        inp.remove(0);
        find(inp, Out);

        // Including first element
        // checking the condition
        // for increasing subsequence
        if(Out.size() == 0)
            find(inp, temp);

        else if(temp.get(0) > Out.get(Out.size() - 1))
        {
            Out.add(temp.get(0));
            find(inp, Out);
        }
    }

    public static void main(String[] args) {
        // Input list
        Vector<Integer> ls1 = new Vector<Integer>();
        ls1.add(1);
        ls1.add(3);
        ls1.add(2);
        Vector<Integer> ls2 = new Vector<Integer>();

        // Calling the function
        find(ls1, ls2);

        // Printing the list
        for(int i = 0; i < st.size(); i++)
        {
            for(int j = 0; j < st.get(i).size(); j++)
                System.out.print(st.get(i).get(j) + " ");

            System.out.println();
        }
        for(int i = 0; i < 2; i++)
        {
            for(int j = 0; j < 2; j++)
                System.out.print(add[i][j] + " ");
            System.out.println();
        }
    }
}

// This code is contributed by rameshtravel07.
```

## 蟒蛇 3

```
# Python3 implementation
# To store all increasing subsequence of the given list
st = []

# Method to find increasing subsequence
def find(inp, out) :
    if len(inp)== 0 :
        if len(out) != 0 :
            # storing result
            st.append(out)
        return

    # excluding 1st element
    find(inp[1:], out[:])

    # including first element
    # checking the condition
    # for increasing subsequence
    if len(out)== 0:
        find(inp[1:], inp[:1])
    elif inp[0] > out[-1] :
        out.append(inp[0])
        find(inp[1:], out[:])

# The input list
ls1 = [1, 3, 2]
ls2 = []

# Calling the function
find(ls1, ls2)

# Printing the lists
for i in st:
    print(*i)
```

## C#

```
// C# implementation to store all
// increasing subsequence of the given list
using System;
using System.Collections.Generic;
class GFG {

    static List<List<int>> st = new List<List<int>>();
    static int[,] add = {{1,2}, {1,3}};

    // Method to find increasing subsequence
    static void find(List<int> inp, List<int> Out)
    {
        if(inp.Count == 0)
        {
            if(Out.Count != 0)
            {

                // Storing result
                st.Add(Out);
            }
            return;
        }

        List<int> temp = new List<int>();
        temp.Add(inp[0]);

        // Excluding 1st element
        inp.RemoveAt(0);
        find(inp, Out);

        // Including first element
        // checking the condition
        // for increasing subsequence
        if(Out.Count == 0)
            find(inp, temp);

        else if(temp[0] > Out[Out.Count - 1])
        {
            Out.Add(temp[0]);
            find(inp, Out);
        }
    }

  static void Main()
  {

    // Input list
    List<int> ls1 = new List<int>(new int[]{ 1, 3, 2 });
    List<int> ls2 = new List<int>();

    // Calling the function
    find(ls1, ls2);

    // Printing the list
    for(int i = 0; i < st.Count; i++)
    {
        for(int j = 0; j < st[i].Count; j++)
            Console.Write(st[i][j] + " ");

        Console.WriteLine();
    }
    for(int i = 0; i < add.GetLength(0); i++)
    {
        for(int j = 0; j < add.GetLength(1); j++)
            Console.Write(add[i,j] + " ");
        Console.WriteLine();
    }

  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>
    // Javascript implementation to store all
    // increasing subsequence of the given list

    let st = [];

    // Method to find increasing subsequence
    function find(inp, out)
    {
        if(inp.length == 0)
        {
            if(out.length != 0)
            {

                // Storing result
                st.push(out);
            }
            return;
        }

        let temp = [];
        temp.push(inp[0]);

        // Excluding 1st element
        inp.shift();
        find(inp, out);

        // Including first element
        // checking the condition
        // for increasing subsequence
        if(out.length == 0)
            find(inp, temp);

        else if(temp[0] > out[out.length - 1])
        {
            out.push(temp[0]);
            find(inp, out);
        }
    }

    // Input list
    let ls1 = [ 1, 3, 2 ];
    let ls2 = [];

    // Calling the function
    find(ls1, ls2);
    st.push([1, 2]);
    st.push([1, 3]);

    // Printing the list
    for(let i = 0; i < st.length; i++)
    {
        for(let j = 0; j < st[i].length; j++)
            document.write(st[i][j] + " ");

        document.write("</br>");
    }

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
2
3
1
1 2
1 3
```

**时间复杂度** : ![O(2^{n})      ](img/342351bdaf957f82c6437b299acbcb1f.png "Rendered by QuickLaTeX.com")。