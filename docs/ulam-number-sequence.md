# 乌兰号序列

> 原文:[https://www.geeksforgeeks.org/ulam-number-sequence/](https://www.geeksforgeeks.org/ulam-number-sequence/)

给定一个正整数 *n* ，任务是打印*乌兰姆数序列*
[**乌兰姆数**](https://en.wikipedia.org/wiki/Ulam_number) **:** 在数学中，乌兰姆数是以术语 **U <sub>1</sub> = 1** 和 **U <sub>1</sub> = 2** 开始，然后为 **U <sub>n</sub>** 定义为大于 **U <sub>n-1</sub>** 的最小正整数，可以用一种方式表示为序列中两个不同的早期项之和。
例如

*   3 是一个乌兰数，因为它可以用一种方式
    (即 1 + 2)表示为两个不同的早期项的和
*   4 也是一个 Ulam 数。除了(1 + 3)之外，我们可以将 4 表示为(2 + 2)，但在(2 + 2)中，术语并不明确。所以我们只有一个办法
*   5 可以用两种方式表示为序列中两个不同的早期项的和
    为(1 + 4)和(2 + 3)，所以，5 不是一个乌兰姆数

Ulam 编号序列的前几个术语是-

> 1、2、3、4、6、8、11、13、16、18、26、28、36、38、47、48、53、57、62、69、72、77、82、87、97、99、102

**例:**

```
Input  : 5
Output : 6

Input : 9
Output : 16
```

一个**简单的解决方案**打印 ulam 编号序列的第 n 个<sup>第</sup>项是生成整个 Ulam 序列直到第 n 个并打印第 n 个<sup>第</sup>项，因为我们不能直接计算第 n 个<sup>第</sup>项。
**生成 ulam 编号序列的方法:**

*   作为，我们有序列的前两个项，如 U <sub>1</sub> =1 和 U <sub>2</sub> =2。我们可以从 i=3 开始搜索下一个 Ulam 号码。
*   对于“I”的每个值，使用两个循环遍历序列的早期项，并检查在添加序列的两个不同项时，我们是否能以一种方式得到 I 的和
*   如果是，那么“我”是下一个乌兰号码，存储它。然后搜索下一个 ulam 号码
*   如果不是，则增加“I”并重复同样的操作
*   继续搜索 ulam 编号，直到我们得到第 n 个术语

以下是上述思路的实现:

## C++

```
// CPP code to print nth
// Ulam number

#include <bits/stdc++.h>
using namespace std;

#define MAX 10000

// Array to store Ulam Number
vector<int> arr;

// function to compute ulam Number
void ulam()
{
    // push First 2 two term of the sequence
    // in the array
    // for further calculation

    arr.push_back(1);

    arr.push_back(2);

    // loop to generate Ulam number
    for (int i = 3; i < MAX; i++) {

        int count = 0;

        // traverse the array and check if
        // i can be represented as sum of
        // two distinct element of the array

        for (int j = 0; j < arr.size() - 1; j++) {

            for (int k = j + 1; k < arr.size(); k++) {

                if (arr[j] + arr[k] == i) {

                    count++;
                }
                if (count > 1)
                    break;
            }
            if (count > 1)
                break;
        }

        // If count is 1 that means
        // i can be represented as sum of
        // two distinct terms of the sequence

        if (count == 1) {
            // i is ulam number
            arr.push_back(i);
        }
    }
}

// Driver code
int main()
{
    // Pre compute Ulam Number sequence
    ulam();

    int n = 9;

    // Print nth Ulam number
    cout << arr[n - 1];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code to print nth
// Ulam number

import java.util.*;
class GFG {

    static final int MAX = 1000;

    // Array to store Ulam Number
    static Vector<Integer> arr = new Vector<Integer>();

    // Function to compute ulam Number
    static void ulam()
    {

        // push First 2 two term of the sequence
        // in the array
        // for further calculation

        arr.add(1);

        arr.add(2);

        // loop to generate Ulam number
        for (int i = 3; i < MAX; i++) {

            int count = 0;

            // traverse the array and check if
            // i can be represented as sum of
            // two distinct element of the array

            for (int j = 0; j < arr.size() - 1; j++) {

                for (int k = j + 1; k < arr.size(); k++) {

                    if (arr.get(j) + arr.get(k) == i) {

                        count++;
                    }
                    if (count > 1)
                        break;
                }
                if (count > 1)
                    break;
            }

            // If count is 2 that means
            // i can be represented as sum of
            // two distinct terms of the sequence

            if (count == 1) {
                // i is ulam number
                arr.add(i);
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // pre compute Ulam Number sequence
        ulam();

        int n = 9;

        // print nth Ulam number
        System.out.println(arr.get(n - 1));
    }
}
```

## 蟒蛇 3

```
# Python3 code to print nth
# Ulam number
MAX = 1000

# Array to store Ulam Number
arr = []

# function to compute ulam Number
def ulam():

    # push First 2 two term of the sequence
    # in the array
    # for further calculation
    arr.append(1);
    arr.append(2);

    # loop to generate Ulam number
    for i in range(3, MAX):
        count = 0;

        # traverse the array and check if
        # i can be represented as sum of
        # two distinct element of the array
        for j in range(len(arr) - 1):
            for k in range(j + 1, len(arr)):
                if (arr[j] + arr[k] == i):
                    count += 1
                if (count > 1):
                    break;           
            if (count > 1):
                break;

        # If count is 1 that means
        # i can be represented as sum of
        # two distinct terms of the sequence
        if (count == 1):

            # i is ulam number
            arr.append(i);

# Driver code
if __name__=='__main__':

    # Pre compute Ulam Number sequence
    ulam();
    n = 9;

    # Print nth Ulam number
    print(arr[n - 1])

# This code is contributed by rutvik_56.
```

## C#

```
// C# code to print nth
// Ulam number
using System;
using System.Collections.Generic;

class GFG
{
    static readonly int MAX = 1000;

    // Array to store Ulam Number
    static List<int> arr = new List<int>();

    // Function to compute ulam Number
    static void ulam()
    {

        // push First 2 two term of 
        // the sequence in the array
        // for further calculation

        arr.Add(1);
        arr.Add(2);

        // loop to generate Ulam number
        for (int i = 3; i < MAX; i++)
        {
            int count = 0;

            // traverse the array and check if
            // i can be represented as sum of
            // two distinct element of the array
            for (int j = 0; j < arr.Count - 1; j++)
            {

                for (int k = j + 1; k < arr.Count; k++)
                {
                    if (arr[j] + arr[k] == i)
                    {
                        count++;
                    }
                    if (count > 1)
                        break;
                }
                if (count > 1)
                    break;
            }

            // If count is 2 that means
            // i can be represented as sum of
            // two distinct terms of the sequence
            if (count == 1)
            {
                // i is ulam number
                arr.Add(i);
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        // pre compute Ulam Number sequence
        ulam();

        int n = 9;

        // print nth Ulam number
        Console.WriteLine(arr[n - 1]);
    }
}

// This code is contributed by Rajput-JI
```

## java 描述语言

```
<script>
// Javascript code to print nth
// Ulam number

var MAX = 10000;

// Array to store Ulam Number
var arr = [];

// function to compute ulam Number
function ulam()
{
    // push First 2 two term of the sequence
    // in the array
    // for further calculation
    arr.push(1);
    arr.push(2);

    // loop to generate Ulam number
    for (var i = 3; i < MAX; i++) {

        var count = 0;

        // traverse the array and check if
        // i can be represented as sum of
        // two distinct element of the array

        for (var j = 0; j < arr.length - 1; j++) {

            for (var k = j + 1; k < arr.length; k++) {

                if (arr[j] + arr[k] == i) {

                    count++;
                }
                if (count > 1)
                    break;
            }
            if (count > 1)
                break;
        }

        // If count is 1 that means
        // i can be represented as sum of
        // two distinct terms of the sequence

        if (count == 1)
        {

            // i is ulam number
            arr.push(i);
        }
    }
}

// Driver code
// Pre compute Ulam Number sequence
ulam();
var n = 9;

// Print nth Ulam number
document.write( arr[n - 1]);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
16
```

一个**有效的解决方案**是使用哈希表来存储序列的较早数字，这样我们就可以在一个循环中完成，而不是使用两个循环来检查“I”是否可以用一种方式来表示为两个不同项的总和。如果我们使用散列表，搜索将会很快。
以下是上述想法的实现:

## C++

```
// Cpp code to print nth
// Ulam number

#include <bits/stdc++.h>
using namespace std;

#define MAX 10000

// Array to store Ulam Number
vector<int> arr;

// function to compute ulam Number
void ulam()
{

    // Set to search specific Ulam number efficiently
    unordered_set<int> s;

    // push First 2 two term of the sequence
    // in the array and set
    // for further calculation

    arr.push_back(1);
    s.insert(1);

    arr.push_back(2);
    s.insert(2);

    // loop to generate Ulam number
    for (int i = 3; i < MAX; i++) {

        int count = 0;

        // traverse the array and check if
        // i can be represented as sum of
        // two distinct element of the array

        for (int j = 0; j < arr.size(); j++) {

            // Check if i-arr[j] exist in the array or not using set
            // If yes, Then i can be represented as
            // sum of arr[j] + (i- arr[j])

            if (s.find(i - arr[j]) != s.end() && arr[j] != (i - arr[j]))
                count++;

            // if Count is greater than 2
            // break the loop
            if (count > 2)
                break;
        }

        // If count is 2 that means
        // i can be represented as sum of
        // two distinct terms of the sequence

        if (count == 2) {
            // i is ulam number
            arr.push_back(i);
            s.insert(i);
        }
    }
}

// Driver code
int main()
{
    // pre compute Ulam Number sequence
    ulam();

    int n = 9;

    // print nth Ulam number
    cout << arr[n - 1];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code to print nth
// Ulam number

import java.util.*;
class GFG {

    static final int MAX = 10000;

    // Array to store Ulam Number
    static Vector<Integer> arr = new Vector<Integer>();

    // function to compute ulam Number
    static void ulam()
    {

        // Set to search specific Ulam number efficiently
        Set<Integer> s = new HashSet<Integer>();

        // push First 2 two term of the sequence
        // in the array and set
        // for further calculation

        arr.add(1);
        s.add(1);

        arr.add(2);
        s.add(2);

        // loop to generate Ulam number
        for (int i = 3; i < MAX; i++) {

            int count = 0;

            // traverse the array and check if
            // i can be represented as sum of
            // two distinct element of the array

            for (int j = 0; j < arr.size(); j++) {

                // Check if i-arr[j] exist in the array or not using set
                // If yes, Then i can be represented as
                // sum of arr[j] + (i- arr[j])

                if (s.contains(i - arr.get(j)) && arr.get(j) != (i - arr.get(j)))
                    count++;

                // if Count is greater than 2
                // break the loop
                if (count > 2)
                    break;
            }

            // If count is 2 that means
            // i can be represented as sum of
            // two distinct terms of the sequence

            if (count == 2) {
                // i is ulam number
                arr.add(i);
                s.add(i);
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // pre compute Ulam Number sequence
        ulam();

        int n = 9;

        // print nth Ulam number
        System.out.println(arr.get(n - 1));
    }
}
```

## 蟒蛇 3

```
# Python3 code to print nth Ulam number
MAX = 10000

# Array to store Ulam Number
arr = []

# function to compute ulam Number
def ulam():

    # Set to search specific Ulam
    # number efficiently
    s = set()

    # push First 2 two term of the
    # sequence in the array and set
    # for further calculation
    arr.append(1)
    s.add(1)

    arr.append(2)
    s.add(2)

    # loop to generate Ulam number
    for i in range(3, MAX):

        count = 0

        # traverse the array and check if
        # i can be represented as sum of
        # two distinct element of the array
        for j in range(0, len(arr)):

            # Check if i-arr[j] exist in the array
            # or not using set. If yes, Then i can
            # be represented as sum of arr[j] + (i- arr[j])
            if (i - arr[j]) in s and arr[j] != (i - arr[j]):
                count += 1

            # if Count is greater than 2
            # break the loop
            if count > 2:
                break

        # If count is 2 that means
        # i can be represented as sum of
        # two distinct terms of the sequence
        if count == 2:
            # i is ulam number
            arr.append(i)
            s.add(i)

# Driver Code   
if __name__ == "__main__":

    # pre compute Ulam Number sequence
    ulam()

    n = 9

    # print nth Ulam number
    print(arr[n - 1])

# This code is contributed by Rituraj Jain
```

## C#

```
// C# code to print nth
// Ulam number
using System;
using System.Collections.Generic;

class GFG
{

    static readonly int MAX = 10000;

    // Array to store Ulam Number
    static List<int> arr = new List<int>();

    // function to compute ulam Number
    static void ulam()
    {

        // Set to search specific Ulam number efficiently
        HashSet<int> s = new HashSet<int>();

        // push First 2 two term of the sequence
        // in the array and set
        // for further calculation
        arr.Add(1);
        s.Add(1);

        arr.Add(2);
        s.Add(2);

        // loop to generate Ulam number
        for (int i = 3; i < MAX; i++)
        {

            int count = 0;

            // traverse the array and check if
            // i can be represented as sum of
            // two distinct element of the array

            for (int j = 0; j < arr.Count; j++)
            {

                // Check if i-arr[j] exist in the array
                // or not using set If yes,
                // Then i can be represented as
                // sum of arr[j] + (i- arr[j])
                if (s.Contains(i - arr[j]) &&
                    arr[j] != (i - arr[j]))
                    count++;

                // if Count is greater than 2
                // break the loop
                if (count > 2)
                    break;
            }

            // If count is 2 that means
            // i can be represented as sum of
            // two distinct terms of the sequence
            if (count == 2)
            {
                // i is ulam number
                arr.Add(i);
                s.Add(i);
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        // pre compute Ulam Number sequence
        ulam();

        int n = 9;

        // print nth Ulam number
        Console.WriteLine(arr[n - 1]);
    }
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
16
```