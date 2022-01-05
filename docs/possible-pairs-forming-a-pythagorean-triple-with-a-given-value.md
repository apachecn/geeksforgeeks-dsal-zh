# 形成具有给定值的毕达哥拉斯三元组的可能对

> 原文:[https://www . geeksforgeeks . org/可能的对-形成-a-勾股-带给定值的三元组/](https://www.geeksforgeeks.org/possible-pairs-forming-a-pythagorean-triple-with-a-given-value/)

给定一个整数 **C** ，任务是在范围**【1，C】**内找到所有可能的配对 **(A，B)** ，使得:

1.  **A<sup>2</sup>+B<sup>2</sup>= C<sup>2</sup>T7】**
2.  **甲**T4**乙**

**示例:**

> **输入:** C = 5
> **输出:** (3，4)
> **解释:**
> (3)<sup>2</sup>+(4)<sup>2</sup>= 9+16 = 25 = 5<sup>2</sup>
> 
> **输入:** C = 25
> **输出:** (15，20)，(7，24)
> **说明:**两对都满足必要条件。

**进场:**

1.  检查范围[1，C]内所有可能的 A 和 B 值。
2.  存储所有满足给定条件的配对。

下面是上述方法的实现:

## C++

```
// C++ program to compute
// all the possible
// pairs that forms a
// pythagorean triple
// with a given value
#include <bits/stdc++.h>
using namespace std;

// Function to generate all
// possible pairs
vector<pair<int, int> > Pairs(int C)
{
    // Vector to store all the
    // possible pairs
    vector<pair<int, int> > ans;

    // Checking all the possible
    // pair in the range of [1, c)
    for (int i = 1; i < C; i++) {
        for (int j = i + 1; j < C;
             j++) {

            // If the pair satisfies
            // the condition push it
            // in the vector
            if ((i * i) + (j * j) == (C * C)) {
                ans.push_back(make_pair(i, j));
            }
        }
    }
    return ans;
}

// Driver Program
int main()
{
    int C = 13;
    vector<pair<int, int> > ans
        = Pairs(C);

    // If no valid pair exist
    if (ans.size() == 0) {
        cout << "No valid pair exist"
             << endl;
        return 0;
    }

    // Print all valid pairs
    for (auto i = ans.begin();
         i != ans.end(); i++) {
        cout << "(" << i->first << ", "
             << i->second << ")" << endl;
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute all
// the possible pairs that forms
// a pythagorean triple with a
// given value
import java.util.*;

class GFG{
static class pair
{
    int first, second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to generate all
// possible pairs
static Vector<pair> Pairs(int C)
{

    // Vector to store all the
    // possible pairs
    Vector<pair> ans = new Vector<pair>();

    // Checking all the possible
    // pair in the range of [1, c)
    for(int i = 1; i < C; i++)
    {
       for(int j = i + 1; j < C; j++)
       {

          // If the pair satisfies
          // the condition push it
          // in the vector
          if ((i * i) + (j * j) == (C * C))
          {
              ans.add(new pair(i, j));
          }
       }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int C = 13;
    Vector<pair> ans = Pairs(C);

    // If no valid pair exist
    if (ans.size() == 0)
    {
        System.out.print("No valid pair " +
                         "exist" + "\n");
        return;
    }

    // Print all valid pairs
    for(pair i:ans)
    {
       System.out.print("(" + i.first +
                       ", " + i.second +
                        ")" + "\n");
    }
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to compute all
# the possible pairs that forms a
# pythagorean triple with a given value

# Function to generate all
# possible pairs
def Pairs(C):

    # Vector to store all the
    # possible pairs
    ans = []

    # Checking all the possible
    # pair in the range of [1, c)
    for i in range(C):
        for j in range(i + 1, C):

            # If the pair satisfies
            # the condition push it
            # in the vector
            if ((i * i) + (j * j) == (C * C)):
                ans.append([i, j])

    return ans;

# Driver code
if __name__=="__main__":

    C = 13;
    ans = Pairs(C);

    # If no valid pair exist
    if (len(ans) == 0):
        print("No valid pair exist")
        exit()

    # Print all valid pairs
    for i in range(len(ans)):
        print("(" + str(ans[i][0]) +
             ", " + str(ans[i][1]) + ")")

# This code is contributed by rutvik_56
```

## C#

```
// C# program to compute all
// the possible pairs that forms
// a pythagorean triple with a
// given value
using System;
using System.Collections.Generic;

class GFG{
class pair
{
    public int first, second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to generate all
// possible pairs
static List<pair> Pairs(int C)
{

    // List to store all the
    // possible pairs
    List<pair> ans = new List<pair>();

    // Checking all the possible
    // pair in the range of [1, c)
    for(int i = 1; i < C; i++)
    {
        for(int j = i + 1; j < C; j++)
        {

            // If the pair satisfies
            // the condition push it
            // in the vector
            if ((i * i) + (j * j) == (C * C))
            {
                ans.Add(new pair(i, j));
            }
        }
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int C = 13;
    List<pair> ans = Pairs(C);

    // If no valid pair exist
    if (ans.Count == 0)
    {
        Console.Write("No valid pair " +
                      "exist" + "\n");
        return;
    }

    // Print all valid pairs
    foreach(pair i in ans)
    {
    Console.Write("(" + i.first +
                 ", " + i.second +
                  ")" + "\n");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to compute
// all the possible
// pairs that forms a
// pythagorean triple
// with a given value

// Function to generate all
// possible pairs
function Pairs(C)
{
    // Vector to store all the
    // possible pairs
    var ans = [];

    // Checking all the possible
    // pair in the range of [1, c)
    for (var i = 1; i < C; i++) {
        for (var j = i + 1; j < C;
             j++) {

            // If the pair satisfies
            // the condition push it
            // in the vector
            if ((i * i) + (j * j) == (C * C)) {
                ans.push([i, j]);
            }
        }
    }
    return ans;
}

// Driver Program
var C = 13;
var ans
    = Pairs(C);

// If no valid pair exist
if (ans.length == 0) {
    document.write( "No valid pair exist<br>");
}

// Print all valid pairs
ans.forEach(x => {

    document.write( "(" + x[0] + ", "
         + x[1] + ")" + "<br>");
});

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
(5, 12)
```

***时间复杂度:** O(C <sup>2</sup> )*