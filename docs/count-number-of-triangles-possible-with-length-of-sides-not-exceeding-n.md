# 计算边长不超过 N 的三角形数量

> 原文:[https://www . geesforgeks . org/count-边长不超过-n 的可能三角形数/](https://www.geeksforgeeks.org/count-number-of-triangles-possible-with-length-of-sides-not-exceeding-n/)

给定一个整数 **N** ，任务是找出[直角三角形](https://www.geeksforgeeks.org/check-if-a-right-angled-triangle-can-be-formed-by-the-given-coordinates/)的总数，这些直角三角形可以形成为三角形任意一边的长度最多为 **N** 。

> 直角三角形满足以下条件:**X<sup>2</sup>+Y<sup>2</sup>= Z<sup>2</sup>T7【其中 Z 代表斜边的长度，X 和 Y 代表剩余两条边的长度。**

**示例:**

> **输入:** N = 5
> **输出:** 1
> **解释:**
> 形成直角三角形的边的唯一可能组合是{3，4，5}。
> 
> **输入:** N = 10
> **输出:** 2
> **解释:**
> 形成直角三角形的边的可能组合是{3，4，5}和{6，8，10}。

**天真方法:**想法是从范围**【1，N】**中生成具有整数的三元组的每个可能的组合，并且对于每个这样的组合，检查它是否是一个[直角三角形](https://en.wikipedia.org/wiki/Right_triangle#:~:text=A%20right%20triangle%20(American%20English,a%2090%2Ddegree%20angle).&text=The%20side%20opposite%20the%20right,side%20c%20in%20the%20figure).)。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include<bits/stdc++.h>
using namespace std;

// Function to count total
// number of right angled triangle
int right_angled(int n)
{
    // Initialise count with 0
    int count = 0;

    // Run three nested loops and
    // check all combinations of sides
    for (int z = 1; z <= n; z++) {
        for (int y = 1; y <= z; y++) {
            for (int x = 1; x <= y; x++) {

                // Condition for right
                // angled triangle
                if ((x * x) + (y * y) == (z * z)) {

                    // Increment count
                    count++;
                }
            }
        }
    }

    return count;
}

// Driver Code
int main()
{
    // Given N
    int n = 5;

    // Function Call
    cout << right_angled(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of 
// the above approach
import java.io.*;

class GFG{

// Function to count total
// number of right angled triangle
static int right_angled(int n)
{

    // Initialise count with 0
    int count = 0;

    // Run three nested loops and
    // check all combinations of sides
    for(int z = 1; z <= n; z++)
    {
        for(int y = 1; y <= z; y++)
        {
            for(int x = 1; x <= y; x++)
            {

                // Condition for right
                // angled triangle
                if ((x * x) + (y * y) == (z * z))
                {

                    // Increment count
                    count++;
                }
            }
        }
    }
    return count;
}

// Driver code
public static void main (String[] args)
{

    // Given N
    int n = 5;

    // Function call
    System.out.println(right_angled(n));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python implementation of 
# the above approach

# Function to count total
# number of right angled triangle
def right_angled(n):

    # Initialise count with 0
    count = 0

    # Run three nested loops and
    # check all combinations of sides
    for z in range(1, n + 1):
        for y in range(1, z + 1):
            for x in range(1, y + 1):

                # Condition for right
                # angled triangle
                if ((x * x) + (y * y) == (z * z)):

                    # Increment count
                    count += 1

    return count

# Driver Code

# Given N
n = 5

# Function call
print(right_angled(n))

# This code is contributed by code_hunt
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG{

// Function to count total
// number of right angled triangle
static int right_angled(int n)
{

    // Initialise count with 0
    int count = 0;

    // Run three nested loops and
    // check all combinations of sides
    for(int z = 1; z <= n; z++)
    {
        for(int y = 1; y <= z; y++)
        {
            for(int x = 1; x <= y; x++)
            {

                // Condition for right
                // angled triangle
                if ((x * x) + (y * y) == (z * z))
                {

                    // Increment count
                    count++;
                }
            }
        }
    }
    return count;
}

// Driver Code
public static void Main(string[] args)
{

    // Given N
    int n = 5;

    // Function call
    Console.Write(right_angled(n));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// javascript implementation of 
// the above approach

// Function to count total
// number of right angled triangle
function right_angled(n)
{

    // Initialise count with 0
    var count = 0;

    // Run three nested loops and
    // check all combinations of sides
    for(z = 1; z <= n; z++)
    {
        for(y = 1; y <= z; y++)
        {
            for(x = 1; x <= y; x++)
            {

                // Condition for right
                // angled triangle
                if ((x * x) + (y * y) == (z * z))
                {

                    // Increment count
                    count++;
                }
            }
        }
    }
    return count;
}

// Driver code
//Given N
var n = 5;

// Function call
document.write(right_angled(n));

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于这样的思想进行优化，即如果三角形的两条边都是已知的，则可以找出三角形的第三条边。按照以下步骤解决问题:

1.  迭代到 **N** 并生成两对可能的两边长度，使用关系**x<sup>2</sup>+y<sup>2</sup>= z<sup>2</sup>T9】找到第三条边**
2.  如果 sqrt(x <sup>2</sup> +y <sup>2</sup> )被发现是一个整数，将这三个相关的整数按照排序的顺序存储在一个[集合](https://www.geeksforgeeks.org/set-in-java/)中，因为它们可以形成一个直角三角形。
3.  打印所需计数的器械包最终尺寸。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count total
// number of right angled triangle
int right_angled(int n)
{
    // Consider a set to store
    // the three sides
    set<pair<int, pair<int, int> > > s;

    // Find possible third side
    for (int x = 1; x <= n; x++) {
        for (int y = 1; y <= n; y++) {

            // Condition for a right
            // angled triangle
            if (x * x + y * y <= n * n) {
                int z = sqrt(x * x + y * y);

                // Check if the third side
                // is an integer
                if (z * z != (x * x + y * y))
                    continue;

                vector<int> v;

                // Push the three sides
                v.push_back(x);
                v.push_back(y);
                v.push_back(sqrt(x * x + y * y));

                sort(v.begin(), v.end());

                // Insert the three sides in
                // the set to find unique triangles
                s.insert({ v[0], { v[1], v[2] } });
            }
            else
                break;
        }
    }

    // return the size of set
    return s.size();
}

// Driver code
int main()
{
    // Given N
    int n = 5;

    // Function Call
    cout << right_angled(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;

class Pair<F, S>
{

    // First member of pair
    private F first;

    // Second member of pair
    private S second;

    public Pair(F first, S second)
    {
        this.first = first;
        this.second = second;
    }
}

class GFG{

// Function to count total
// number of right angled triangle    
public static int right_angled(int n)
{

    // Consider a set to store
    // the three sides
    Set<Pair<Integer,
        Pair<Integer,
             Integer>>> s = new HashSet<Pair<Integer,
                                        Pair<Integer,
                                             Integer>>>();

    // Find possible third side
    for(int x = 1; x <= n; x++)
    {
        for(int y = 1; y <= n; y++)
        {

            // Condition for a right
            // angled triangle
            if (x * x + y * y <= n * n)
            {
                int z = (int)Math.sqrt(x * x + y * y);

                // Check if the third side
                // is an integer
                if (z * z != (x * x + y * y))
                    continue;

                Vector<Integer> v = new Vector<Integer>();

                // Push the three sides
                v.add(x);
                v.add(y);
                v.add((int)Math.sqrt(x * x + y * y));

                Collections.sort(v);

                // Add the three sides in
                // the set to find unique triangles
                s.add(new Pair<Integer,
                          Pair<Integer,
                               Integer>>(v.get(0),
                      new Pair<Integer,
                               Integer>(v.get(1),
                                        v.get(2))));
            }
            else
                break;
        }
    }

    // Return the size of set
    return s.size() - 1;
}

// Driver code
public static void main(String[] args)
{

    // Given N
    int n = 5;

    // Function call
    System.out.println(right_angled(n));
}
}

// This code is contributed by grand_master
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*