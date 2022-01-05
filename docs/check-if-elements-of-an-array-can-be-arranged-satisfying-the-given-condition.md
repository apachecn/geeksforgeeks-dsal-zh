# 检查一个数组的元素是否能满足给定的条件

> 原文:[https://www . geeksforgeeks . org/check-如果一个数组中的元素可以被排列-满足给定的条件/](https://www.geeksforgeeks.org/check-if-elements-of-an-array-can-be-arranged-satisfying-the-given-condition/)

给定一个由 **N** (偶数)整数元素组成的数组**。任务是检查是否有可能对数组元素重新排序，例如:** 

```
**arr[2*i + 1] = 2 * A[2 * i]** 

for **i = 0 ... N-1**. 
```

**有可能的话打印**真**，否则打印**假**。
**例:**** 

> ****输入:** arr[] = {4，-2，2，-4}
> **输出:** True
> {-2，-4，2，4}是有效排列，-2 * 2 = -4 和 2 * 2 = 4
> **输入:** arr[] = {1，2，4，16，8，4}
> **输出:** False**

****方法:**想法是，如果 **k** 是数组中当前的最小元素，那么它必须与 **2 * k** 配对，因为不存在任何其他元素 **k / 2** 与之配对。
我们按照升序检查元素。当我们检查一个元素 **k** 而它没有被使用时，它必须与 **2 * k** 配对。我们将尝试先安排 **k** 后安排 **2 * k** 但是如果不能，那么答案就是**假**。最后，如果所有操作都成功，则打印**真**。
我们将存储每个元素的计数，以跟踪我们尚未考虑的内容。
以下是上述方法的实施:** 

## **C++**

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return true if the elements
// can be arranged in the desired order
string canReorder(int A[],int n)
{
    map<int,int> m;

    for(int i=0;i<n;i++)
    m[A[i]]++;

    sort(A,A+n);
    int count = 0;

    for(int i=0;i<n;i++)
    {
        if (m[A[i]] == 0)
            continue;

        // If 2 * x is not found to pair
        if (m[2 * A[i]]){

        count+=2;

        // Remove an occurrence of x
        // and an occurrence of 2 * x
        m[A[i]] -= 1;
        m[2 * A[i]] -= 1;
        }
    }
    if(count ==n)
    return "true";
    else
    return "false";
}

// Driver Code
int main()
{
int A[] = {4, -2, 2, -4};
int n= sizeof(A)/sizeof(int);

// Function call to print required answer
cout<<(canReorder(A,n));

return 0;
}
//contributed by Arnab Kundu
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.util.HashMap;
import java.util.Map;
import java.util.Arrays;

class GfG
{

    // Function to return true if the elements
    // can be arranged in the desired order
    static String canReorder(int A[],int n)
    {
        HashMap<Integer,Integer> m = new HashMap<>();

        for(int i = 0; i < n; i++)
        {

            if (m.containsKey(A[i]))
                m.put(A[i], m.get(A[i]) + 1);
            else
                m.put(A[i], 1);
        }

        Arrays.sort(A);
        int count = 0;

        for(int i = 0; i < n; i++)
        {
            if (m.get(A[i]) == 0)
                continue;

            // If 2 * x is not found to pair
            if (m.containsKey(2 * A[i]))
            {

                count += 2;

                // Remove an occurrence of x
                // and an occurrence of 2 * x
                m.put(A[i], m.get(A[i]) - 1);
                m.put(2 * A[i], m.get(2 * A[i]) - 1);
            }
        }

        if(count == n)
            return "true";
        else
            return "false";
    }

    // Driver code
    public static void main(String []args)
    {

        int A[] = {4, -2, 2, -4};
        int n = A.length;

        // Function call to print required answer
        System.out.println(canReorder(A,n));
    }
}

// This code is contributed by Rituraj Jain
```

## **计算机编程语言**

```
# Python implementation of the approach
import collections

# Function to return true if the elements
# can be arranged in the desired order
def canReorder(A):

    count = collections.Counter(A)

    for x in sorted(A, key = abs):
        if count[x] == 0:
            continue

        # If 2 * x is not found to pair
        if count[2 * x] == 0:
            return False

        # Remove an occurrence of x
        # and an occurrence of 2 * x
        count[x] -= 1
        count[2 * x] -= 1

    return True

# Driver Code
A = [4, -2, 2, -4]

# Function call to print required answer
print(canReorder(A))
```

## **C#**

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return true if the elements
// can be arranged in the desired order
static String canReorder(int []A,int n)
{
    Dictionary<int,
               int> m = new Dictionary<int,
                                       int>();

    for(int i = 0; i < n; i++)
    {
        if (m.ContainsKey(A[i]))
            m[A[i]]= m[A[i]] + 1;
        else
            m.Add(A[i], 1);
    }

    Array.Sort(A);
    int count = 0;

    for(int i = 0; i < n; i++)
    {
        if (m[A[i]] == 0)
            continue;

        // If 2 * x is not found to pair
        if (m.ContainsKey(2 * A[i]))
        {
            count += 2;

            // Remove an occurrence of x
            // and an occurrence of 2 * x
            m[A[i]]= m[A[i]] - 1;
            if (m.ContainsKey(2 * A[i]))
                m[2 * A[i]]= m[2 * A[i]] - 1;
            else
                m.Add(2 * A[i], m[2 * A[i]] - 1);
        }
    }
    if(count == n)
        return "True";
    else
        return "False";
}

// Driver code
public static void Main(String []args)
{
    int []A = {4, -2, 2, -4};
    int n = A.Length;

    // Function call to print required answer
    Console.WriteLine(canReorder(A,n));
}
}

// This code is contributed by Rajput-Ji
```

## **java 描述语言**

```
<script>

// JavaScript implementation of the approach

// Function to return true if the elements
// can be arranged in the desired order
function canReorder(A, n)
{
    let m = new Map();

    for(let i=0;i<n;i++){
        if(m.has(A[i])){
            m.set(A[i], m.get(A[i]) + 1)
        }else{
            m.set(A[i], 1)
        }
    }

    A.sort((a, b) =>  a - b);
    let count = 0;

    for(let i=0;i<n;i++)
    {
        if (m.get(A[i]) == 0)
            continue;

        // If 2 * x is not found to pair
        if (m.get(2 * A[i])){

        count+=2;

        // Remove an occurrence of x
        // and an occurrence of 2 * x
        m.set(A[i], m.get(A[i]) - 1);
        m.set(2 * A[i], m.get(2 * A[i])- 1);
        }
    }
    if(count ==n)
    return "True";
    else
    return "False";
}

// Driver Code

let A = [4, -2, 2, -4];
let n= A.length;

// Function call to print required answer
document.write((canReorder(A,n)));

// This code is contributed by _saurabh_jaiswal

</script>
```

****Output:** 

```
True
```**