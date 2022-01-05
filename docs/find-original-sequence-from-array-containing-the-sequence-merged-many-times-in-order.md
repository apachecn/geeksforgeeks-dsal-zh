# 从包含按顺序多次合并的序列的数组中找到原始序列

> 原文:[https://www . geesforgeks . org/find-origin-sequence-from-array-containing-sequence-merged-多次按顺序/](https://www.geeksforgeeks.org/find-original-sequence-from-array-containing-the-sequence-merged-many-times-in-order/)

给定一个数字 **N** 和一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，该数组由任意次数的不同整数的合并 **N** 长度序列组成，保持初始序列中元素的相对顺序。任务是找到保持正确顺序的长度 **N** 的初始序列。

**示例:**

> **输入:** N = 4，arr[] = {1，13，1，24，13，24，2，2}
> **输出:** 1 13 24 2
> **解释:**
> 这里给定的序列是通过合并 1 13 24 2 保持元素的相对顺序得到的。所以，答案是 1 13 24 2。
> 
> **输入:** N = 3，arr[] = {3，2，3，1，2，3，2，1，1}
> **输出:**3 2 1
> T6】解释:
> 这里给定的序列是通过合并 3 2 1 保持元素的相对顺序得到的。所以，答案是 3 2 1。

**方法:**想法是观察在给定序列中首先出现的元素是合成的恢复序列的第一个元素。在我们恢复的序列中获取该元素，不要包含给定序列的副本。对其余元素执行相同的操作，直到我们到达终点。这个想法可以通过 C++中的[](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)**和 [**集合**](https://www.geeksforgeeks.org/set-in-cpp-stl/) 来实现。**

****使用地图****

1.  **从左到右遍历给定的序列。**
2.  **序列中第一次出现的元素会被考虑在内，并使用地图进行标记。**
3.  **遍历时标记的元素被忽略。**
4.  **步骤 2 和步骤 3 继续进行，直到到达给定序列的末尾。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the restored
// permutation
vector<int> restore(int arr[], int N)
{
    // Vector to store the result
    vector<int> result;

    // Map to mark the elements
    // which are taken in result
    map<int, int> mp;
    for (int i = 0; i < N; i++) {

        // Check if the element is
        // coming first time
        if (mp[arr[i]] == 0) {

            // Push in result vector
            result.push_back(arr[i]);

            // Mark it in the map
            mp[arr[i]]++;
        }
    }

    // Return the answer
    return result;
}

// Function to print the result
void print_result(vector<int> result)
{
    for (int i = 0; i < result.size(); i++)
        cout << result[i] << " ";
}

// Driver Code
int main()
{
    // Given Array
    int arr[] = { 1, 13, 1, 24, 13, 24, 2, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    print_result(restore(arr, N));
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function that returns the restored
// permutation
static Vector<Integer> restore(int arr[], int N)
{
    // Vector to store the result
    Vector<Integer> result = new Vector<>();

    // Map to mark the elements
    // which are taken in result
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();
    for (int i = 0; i < N; i++)
    {

        // Check if the element is
        // coming first time
        if (mp.containsKey(arr[i]) &&
            mp.get(arr[i]) == 0)
        {

            // Push in result vector
            result.add(arr[i]);

            // Mark it in the map
            if(mp.containsKey(arr[i]))
            {
                mp.put(arr[i], mp.get(arr[i]) + 1);
            }
            else
            {
                mp.put(arr[i], 1);
            }
        }
        else
            mp.put(arr[i], 0);
    }

    // Return the answer
    return result;
}

// Function to print the result
static void print_result(Vector<Integer> result)
{
    for (int i = 0; i < result.size(); i++)
        System.out.print(result.get(i) + " ");
}

// Driver Code
public static void main(String[] args)
{
    // Given Array
    int arr[] = { 1, 13, 1, 24, 13, 24, 2, 2 };

    int N = arr.length;

    // Function Call
    print_result(restore(arr, N));
}
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function that returns the restored
# permutation
def restore(arr, N):

    # List to store the result
    result = []

    # Map to mark the elements
    # which are taken in result
    mp = {}

    for i in range(N):

        # Checking if the element is
        # coming first time
        if not arr[i] in mp:

            # Push in result vector
            result.append(arr[i])

            # Mark it in the map
            mp[arr[i]] = 1

    # Return the answer
    return result

# Function to print the result
def print_result(result):

    for i in range(len(result)):
        print(result[i], end = " ")

# Driver code
def main():

    # Given array
    arr = [ 1, 13, 1, 24, 13, 24, 2, 2 ]
    N = len(arr)

    # Function call
    print_result(restore(arr, N))

main()

# This code is contributed by Stuti Pathak
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function that returns the restored
// permutation
static List<int> restore(int []arr, int N)
{

    // List to store the result
    List<int> result = new List<int>();

    // Map to mark the elements
    // which are taken in result
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();
    for(int i = 0; i < N; i++)
    {

        // Check if the element is
        // coming first time
        if (mp.ContainsKey(arr[i]) &&
            mp[arr[i]] == 0)
        {

            // Push in result vector
            result.Add(arr[i]);

            // Mark it in the map
            if(mp.ContainsKey(arr[i]))
            {
                mp[arr[i]] = mp[arr[i]] + 1;
            }
            else
            {
                mp.Add(arr[i], 1);
            }
        }
        else
            mp.Add(arr[i], 0);
    }

    // Return the answer
    return result;
}

// Function to print the result
static void print_result(List<int> result)
{
    for(int i = 0; i < result.Count; i++)
        Console.Write(result[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{

    // Given Array
    int []arr = { 1, 13, 1, 24, 13, 24, 2, 2 };

    int N = arr.Length;

    // Function call
    print_result(restore(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function that returns the restored
// permutation
function restore(arr, N)
{
    // Vector to store the result
    var result = [];

    // Map to mark the elements
    // which are taken in result
    var mp = new Map();

    for (var i = 0; i < N; i++) {

        // Check if the element is
        // coming first time
        if (!mp.has(arr[i])) {

            // Push in result vector
            result.push(arr[i]);

            // Mark it in the map
            mp.set(arr[i], mp.get(arr[i])+1);
        }
    }

    // Return the answer
    return result;
}

// Function to print the result
function print_result(result)
{
    for (var i = 0; i < result.length; i++)
    {
        document.write( result[i] + " ");
    }

}

// Driver Code
// Given Array
var arr = [1, 13, 1, 24, 13, 24, 2, 2];
var N = arr.length;
// Function Call
print_result(restore(arr, N));

</script>
```

****Output:** 

```
1 13 24 2
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**

****使用设置****

1.  **从左到右遍历给定的序列。**
2.  **取一个计数器并初始化为 1。**
3.  **将元素逐一插入集合中。如果在某个时刻集合和计数器的大小相同，则考虑该元素，并将计数器增加 1。**
4.  **继续步骤 3 和步骤 4，直到到达给定序列的末尾。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the restored
// permutation
vector<int> restore(int arr[], int N)
{
    // Vector to store the result
    vector<int> result;
    int count1 = 1;

    // Set to insert unique elements
    set<int> s;
    for (int i = 0; i < N; i++) {

        s.insert(arr[i]);

        // Check if the element is
        // coming first time
        if (s.size() == count1) {

            // Push in result vector
            result.push_back(arr[i]);

            count1++;
        }
    }

    return result;
}

// Function to print the result
void print_result(vector<int> result)
{
    for (int i = 0; i < result.size(); i++)
        cout << result[i] << " ";
}

// Driver Code
int main()
{
    // Given Array
    int arr[] = { 1, 13, 1, 24, 13, 24, 2, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    print_result(restore(arr, N));
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that returns the restored
// permutation
static Vector<Integer> restore(int arr[], int N)
{

    // Vector to store the result
    Vector<Integer> result = new Vector<Integer>();

    int count1 = 1;

    // Set to insert unique elements
    HashSet<Integer> s = new HashSet<Integer>();

    for(int i = 0; i < N; i++)
    {
        s.add(arr[i]);

        // Check if the element is
        // coming first time
        if (s.size() == count1)
        {

            // Push in result vector
            result.add(arr[i]);
            count1++;
        }
    }
    return result;
}

// Function to print the result
static void print_result(Vector<Integer> result)
{
    for(int i = 0; i < result.size(); i++)
        System.out.print(result.get(i) + " ");
}

// Driver Code
public static void main(String[] args)
{

    // Given Array
    int arr[] = { 1, 13, 1, 24, 13, 24, 2, 2 };

    int N = arr.length;

    // Function call
    print_result(restore(arr, N));
}
}

// This code is contributed by Princi Singh
```

## **蟒蛇 3**

```
# Python3 program for the
# above approach

# Function that returns the
# restored permutation
def restore(arr, N):

    # Vector to store the
    # result
    result = []
    count1 = 1

    # Set to insert unique
    # elements
    s = set([])

    for i in range(N):
        s.add(arr[i])

        # Check if the element is
        # coming first time
        if (len(s) == count1):

            # Push in result vector
            result.append(arr[i])

            count1 += 1

    return result

# Function to print the
# result
def print_result(result):

    for i in range(len(result)):
        print(result[i],
              end = " ")

# Driver Code
if __name__ == "__main__":

    # Given Array
    arr = [1, 13, 1, 24,
           13, 24, 2, 2]

    N = len(arr)

    # Function Call
    print_result(restore(arr, N))

# This code is contributed by Chitranayal
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function that returns the restored
// permutation
static List<int> restore(int []arr, int N)
{

    // List to store the result
    List<int> result = new List<int>();

    int count1 = 1;

    // Set to insert unique elements
    HashSet<int> s = new HashSet<int>();

    for(int i = 0; i < N; i++)
    {
        s.Add(arr[i]);

        // Check if the element is
        // coming first time
        if (s.Count == count1)
        {

            // Push in result vector
            result.Add(arr[i]);
            count1++;
        }
    }
    return result;
}

// Function to print the result
static void print_result(List<int> result)
{
    for(int i = 0; i < result.Count; i++)
        Console.Write(result[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{

    // Given Array
    int []arr = { 1, 13, 1, 24, 13, 24, 2, 2 };

    int N = arr.Length;

    // Function call
    print_result(restore(arr, N));
}
}

// This code is contributed by PrinciRaj1992
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function that returns the restored
// permutation
function restore(arr, N)
{

    // Vector to store the result
    let result = [];

    let count1 = 1;

    // Set to insert unique elements
    let s = new Set();

    for(let i = 0; i < N; i++)
    {
        s.add(arr[i]);

        // Check if the element is
        // coming first time
        if (s.size == count1)
        {

            // Push in result vector
            result.push(arr[i]);
            count1++;
        }
    }
    return result;
}

// Function to print the result
function print_result(result)
{
    for(let i = 0; i < result.length; i++)
        document.write(result[i] + " ");
}

// Driver Code
let arr = [ 1, 13, 1, 24, 13, 24, 2, 2 ];
let N = arr.length;

// Function call
print_result(restore(arr, N));

// This code is contributed by avanitrachhadiya2155

</script>
```

****Output:** 

```
1 13 24 2
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**