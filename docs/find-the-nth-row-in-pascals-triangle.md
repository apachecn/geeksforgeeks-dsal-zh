# 找到帕斯卡三角形的第 n 行

> 原文:[https://www . geeksforgeeks . org/find-the-n-row-in-Pascal-triangle/](https://www.geeksforgeeks.org/find-the-nth-row-in-pascals-triangle/)

给定一个非负整数 **N** ，任务是找到[帕斯卡三角](https://www.geeksforgeeks.org/pascal-triangle/)的 **N <sup>第</sup>行**。

***注:**行索引从 0 开始。*

> **帕斯卡的三角形:**
> 【1】
> 1 3 3 3 1
> 1 4 6 4 4 4 1

**示例:**

> **输入:** N = 3
> **输出:** 1、3、3、1
> **说明:**
> 3<sup>rd</sup>行的元素为 1 3 3 1。
> 
> **输入:**N = 0
> T3】输出: 1

**天真方法:**
解决问题最简单的方法就是用[递归](https://www.geeksforgeeks.org/recursion/)。先用递归找到**前一个索引**的行，然后借助前一行计算当前行的值。重复此过程直到第 N<sup>行。</sup>

下面是上述方法的实现:

## C++

```
// C++ program to find the Nth
// index row in Pascal's triangle
#include <bits/stdc++.h>
using namespace std;

// Function to find the elements
// of rowIndex in Pascal's Triangle
vector<int> getRow(int rowIndex)
{
    vector<int> currow;

    // 1st element of every row is 1
    currow.push_back(1);

    // Check if the row that has to
    // be returned is the first row
    if (rowIndex == 0)
    {
        return currow;
    }

    // Generate the previous row
    vector<int> prev = getRow(rowIndex - 1);

    for(int i = 1; i < prev.size(); i++)
    {

        // Generate the elements
        // of the current row
        // by the help of the
        // previous row
        int curr = prev[i - 1] + prev[i];
        currow.push_back(curr);
    }
    currow.push_back(1);

    // Return the row
    return currow;
}

// Driver Code   
int main()
{
    int n = 3;
    vector<int> arr = getRow(n);

    for(int i = 0; i < arr.size(); i++)
    {
        if (i == arr.size() - 1)
            cout << arr[i];
        else
            cout << arr[i] << ", ";
    }
    return 0;
}

// This code is contributed by divyesh072019
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the Nth
// index row in Pascal's triangle
import java.util.ArrayList;
public class geeks {

    // Function to find the elements
    // of rowIndex in Pascal's Triangle
    public static ArrayList<Integer> getRow(
        int rowIndex)
    {
        ArrayList<Integer> currow
            = new ArrayList<Integer>();
        // 1st element of every row is 1
        currow.add(1);

        // Check if the row that has to
        // be returned is the first row
        if (rowIndex == 0) {
            return currow;
        }
        // Generate the previous row
        ArrayList<Integer> prev = getRow(rowIndex
                                         - 1);

        for (int i = 1; i < prev.size(); i++) {
            // Generate the elements
            // of the current row
            // by the help of the
            // previous row
            int curr = prev.get(i - 1)
                       + prev.get(i);
            currow.add(curr);
        }
        currow.add(1);

        // Return the row
        return currow;
    }

    // Driver Program
    public static void main(String[] args)
    {
        int n = 3;
        ArrayList<Integer> arr = getRow(n);

        for (int i = 0; i < arr.size(); i++) {
            if (i == arr.size() - 1)
                System.out.print(arr.get(i));
            else
                System.out.print(arr.get(i)
                                 + ", ");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the Nth
# index row in Pascal's triangle

# Function to find the elements
# of rowIndex in Pascal's Triangle
def getRow(rowIndex) :

    currow = []

    # 1st element of every row is 1
    currow.append(1)

    # Check if the row that has to
    # be returned is the first row
    if (rowIndex == 0) :

        return currow

    # Generate the previous row
    prev = getRow(rowIndex - 1)

    for i in range(1, len(prev)) :

        # Generate the elements
        # of the current row
        # by the help of the
        # previous row
        curr = prev[i - 1] + prev[i]
        currow.append(curr)

    currow.append(1)

    # Return the row
    return currow

n = 3
arr = getRow(n)

for i in range(len(arr)) :

    if (i == (len(arr) - 1)) :
        print(arr[i])
    else :
        print(arr[i] , end = ", ")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find the Nth
// index row in Pascal's triangle
using System;
using System.Collections.Generic;

class GFG{

// Function to find the elements
// of rowIndex in Pascal's Triangle
public static List<int> getRow(int rowIndex)
{
    List<int> currow = new List<int>();

    // 1st element of every row is 1
    currow.Add(1);

    // Check if the row that has to
    // be returned is the first row
    if (rowIndex == 0)
    {
        return currow;
    }
    // Generate the previous row
    List<int> prev = getRow(rowIndex - 1);

    for(int i = 1; i < prev.Count; i++)
    {

        // Generate the elements
        // of the current row
        // by the help of the
        // previous row
        int curr = prev[i - 1] + prev[i];
        currow.Add(curr);
    }
    currow.Add(1);

    // Return the row
    return currow;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;
    List<int> arr = getRow(n);

    for(int i = 0; i < arr.Count; i++)
    {
        if (i == arr.Count - 1)
            Console.Write(arr[i]);
        else
            Console.Write(arr[i] + ", ");
    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript program to find the Nth
    // index row in Pascal's triangle

    // Function to find the elements
    // of rowIndex in Pascal's Triangle
    function getRow(rowIndex)
    {
        let currow = [];

        // 1st element of every row is 1
        currow.push(1);

        // Check if the row that has to
        // be returned is the first row
        if (rowIndex == 0)
        {
            return currow;
        }
        // Generate the previous row
        let prev = getRow(rowIndex - 1);

        for(let i = 1; i < prev.length; i++)
        {

            // Generate the elements
            // of the current row
            // by the help of the
            // previous row
            let curr = prev[i - 1] + prev[i];
            currow.push(curr);
        }
        currow.push(1);

        // Return the row
        return currow;
    }

    let n = 3;
    let arr = getRow(n);

    for(let i = 0; i < arr.length; i++)
    {
        if (i == arr.length - 1)
            document.write(arr[i]);
        else
            document.write(arr[i] + ", ");
    }

</script>
```

**Output:** 

```
1, 3, 3, 1
```

**高效方法:**
按照以下步骤优化上述方法:

*   与上面的方法不同，我们将只生成第 N<sup>行的数字。</sup>
*   我们可以观察到帕斯卡三角形的第**N**行由以下序列组成:

```
<sub>NC0, NC1, ......, NCN - 1, NCN</sub>
```

*   由于， **<sub>N</sub> C <sub>0</sub> = 1** ，序列的以下值可以通过以下等式生成:

```
<sub>NCr = (NCr - 1 * (N - r + 1)) / r</sub> where 1 ≤ r ≤ N
```

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Print the N-th row of the
// Pascal's Triangle
void generateNthrow(int N)
{
    // nC0 = 1
    int prev = 1;
    cout << prev;

    for (int i = 1; i <= N; i++) {
        // nCr = (nCr-1 * (n - r + 1))/r
        int curr = (prev * (N - i + 1)) / i;
        cout << ", " << curr;
        prev = curr;
    }
}

// Driver Program
int main()
{

    int N = 5;
    generateNthrow(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
import java.io.*;

class GFG{

// Print the N-th row of the
// Pascal's Triangle
static void generateNthrow(int N)
{

    // nC0 = 1
    int prev = 1;
    System.out.print(prev);

    for(int i = 1; i <= N; i++)
    {

       // nCr = (nCr-1 * (n - r + 1))/r
       int curr = (prev * (N - i + 1)) / i;
       System.out.print(", " + curr);
       prev = curr;
    }
}

// Driver code
public static void main (String[] args)
{
    int N = 5;
    generateNthrow(N);
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program to implement the above approach

# Print the N-th row of the
# Pascal's Triangle
def generateNthRow (N):

    # nC0 = 1
    prev = 1
    print(prev, end = '')

    for i in range(1, N + 1):

        # nCr = (nCr-1 * (n - r + 1))/r
        curr = (prev * (N - i + 1)) // i
        print(",", curr, end = '')
        prev = curr

# Driver code
N = 5

# Function calling
generateNthRow(N)

# This code is contributed by himanshu77
```

## C#

```
// C# program to implement the above approach
using System;
using System.Collections.Generic;
class GFG{

// Print the N-th row of the
// Pascal's Triangle
static void generateNthrow(int N)
{

    // nC0 = 1
    int prev = 1;
    Console.Write(prev);

    for(int i = 1; i <= N; i++)
    {

        // nCr = (nCr-1 * (n - r + 1))/r
        int curr = (prev * (N - i + 1)) / i;
        Console.Write(", " + curr);
        prev = curr;
    }
}

// Driver code
public static void Main(String[] args)
{
    int N = 5;
    generateNthrow(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Print the N-th row of the
    // Pascal's Triangle
    function generateNthrow(N)
    {

        // nC0 = 1
        let prev = 1;
        document.write(prev);

        for(let i = 1; i <= N; i++)
        {

            // nCr = (nCr-1 * (n - r + 1))/r
            let curr = (prev * (N - i + 1)) / i;
            document.write(", " + curr);
            prev = curr;
        }
    }

    let N = 5;
    generateNthrow(N);

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
1, 5, 10, 10, 5, 1
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*