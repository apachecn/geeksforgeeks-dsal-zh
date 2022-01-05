# 程序打印前 N 个步进号

> 原文:[https://www . geesforgeks . org/program-to-print-first-n-steping-numbers/](https://www.geeksforgeeks.org/program-to-print-first-n-stepping-numbers/)

给定一个数字 **N** ，任务是打印第一个 **N** [步进数字](https://www.geeksforgeeks.org/stepping-numbers/)。

> 如果所有相邻数字的绝对差值为 1，则一个数字称为[步进数](https://www.geeksforgeeks.org/stepping-numbers/)。例如，321 是步进数，而 421 不是。

**例:**

> **输入:** N = 7
> **输出:** 1、2、3、4、5、6、7
> **输入:** N = 14
> **输出:** 1、2、3、4、5、6、7、8、9、10、11、12、21、22

**天真的做法:**我们可以从 1 开始，检查每一个数字是否是步进数，一直持续到找到第 K 个步进数。
**高效进场:**

1.  [生成所有可能的步进数直到 1000](https://www.geeksforgeeks.org/stepping-numbers/) ，便于计算
2.  对于 N 的每个值，只需打印 N 个已经计算好的步进数

**以下是上述方法的实施:**

## C++

```
// C++ Program to print first N
// Stepping numbers

#include <bits/stdc++.h>
using namespace std;

// Function to generate
// the Stepping numbers
void generateSteppingNos(
    int x, set<int>& s)
{
    if (x > 1e8)
        return;

    // Inserting the current
    // element in the set
    s.insert(x);

    // Retrieving the last digit
    // of the current number
    int last = x % 10;

    if (last - 1 >= 0)

        // Appending x-1 to
        // the current number
        generateSteppingNos(
            x * 10 + last - 1,
            s);

    // Appending x to
    // the current number
    generateSteppingNos(
        x * 10 + last,
        s);

    if (last + 1 <= 9)

        // Appending x+1 to
        // the current number
        generateSteppingNos(
            x * 10 + last + 1,
            s);
}

// Function to print
// N Stepping numbers
void NSteppingNumbers(int N)
{
    set<int> s;

    for (int i = 1; i <= 9; i++)
        generateSteppingNos(i, s);

    int count = 1;

    // Printing N numbers from s
    for (auto& it : s) {
        if (count <= N) {
            cout << it << ", ";
            count++;
        }
        else
            break;
    }
}

// Driver code
int main()
{
    int N = 14;

    NSteppingNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print first N
// Stepping numbers
import java.util.*;
public class GFG
{
    static HashSet<Integer> s = new HashSet<Integer>();

    // Function to generate
    // the Stepping numbers
    static void generateSteppingNos(int x)
    {
        if (x > 1e8)
            return;

        // Inserting the current
        // element in the set
        s.add(x);

        // Retrieving the last digit
        // of the current number
        int last = x % 10;

        if (last - 1 >= 0)

            // Appending x-1 to
            // the current number
            generateSteppingNos(x * 10 + last - 1);

        // Appending x to
        // the current number
        generateSteppingNos(x * 10 + last);

        if (last + 1 <= 9)

            // Appending x+1 to
            // the current number
            generateSteppingNos(x * 10 + last + 1);
    }

    // Function to print
    // N Stepping numbers
    static void NSteppingNumbers(int N)
    {
        HashSet<Integer> s = new HashSet<Integer>();
        int[] arr = {10, 11, 12, 21, 22};
        for (int i = 1; i <= 9; i++)
        {
            generateSteppingNos(i);
            s.add(i);
        }
        for(int i = 0; i < arr.length; i++)
        {
            s.add(arr[i]);
        }

        int count = 1;

        // Printing N numbers from s
        for(int it : s)
        {
            if (count <= N) {
                System.out.print(it + ", ");
                count++;
            }
            else
                break;
        }
    }

    public static void main(String[] args) {
        int N = 14;

        NSteppingNumbers(N);
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 Program to print first N
# Stepping numbers

# Function to generate
# the Stepping numbers
def generateSteppingNos(x, s):
    if (x > 1e8):
        return

    # Inserting the current
    # element in the set
    s.add(x)

    # Retrieving the last digit
    # of the current number
    last = x % 10

    if (last - 1 >= 0):

        # Appending x-1 to
        # the current number
        generateSteppingNos(x * 10 + last - 1, s)

    # Appending x to
    # the current number
    generateSteppingNos(x * 10 + last, s)

    if (last + 1 <= 9):

        # Appending x+1 to
        # the current number
        generateSteppingNos(x * 10 + last + 1, s)

# Function to print
# N Stepping numbers
def NSteppingNumbers(N):

    s = set()

    for i in range(1, 10):
        generateSteppingNos(i, s)

    count = 1

    s.pop()

    # Printing N numbers from s
    for value in s:
        if (count <= N):
            print(value, end=', ')
            count = count + 1
        else:
            break

# Driver code
N = 14

NSteppingNumbers(N)

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# Program to print first N
// Stepping numbers
using System;
using System.Collections.Generic;
class GFG {

    static HashSet<int> s = new HashSet<int>();

    // Function to generate
    // the Stepping numbers
    static void generateSteppingNos(int x)
    {
        if (x > 1e8)
            return;

        // Inserting the current
        // element in the set
        s.Add(x);

        // Retrieving the last digit
        // of the current number
        int last = x % 10;

        if (last - 1 >= 0)

            // Appending x-1 to
            // the current number
            generateSteppingNos(x * 10 + last - 1);

        // Appending x to
        // the current number
        generateSteppingNos(x * 10 + last);

        if (last + 1 <= 9)

            // Appending x+1 to
            // the current number
            generateSteppingNos(x * 10 + last + 1);
    }

    // Function to print
    // N Stepping numbers
    static void NSteppingNumbers(int N)
    {
        HashSet<int> s = new HashSet<int>();
        int[] arr = {10, 11, 12, 21, 22};
        for (int i = 1; i <= 9; i++)
        {
            generateSteppingNos(i);
            s.Add(i);
        }
        for(int i = 0; i < arr.Length; i++)
        {
            s.Add(arr[i]);
        }

        int count = 1;

        // Printing N numbers from s
        foreach(int it in s)
        {
            if (count <= N) {
                Console.Write(it + ", ");
                count++;
            }
            else
                break;
        }
    }

  static void Main() {
    int N = 14;

    NSteppingNumbers(N);
  }
}

// This code is contributed by suresh07.
```

**Output:** 

```
1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 21, 22,
```