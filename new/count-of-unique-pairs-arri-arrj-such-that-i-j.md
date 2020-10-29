# 唯一对（arr [i]，arr [j]）的计数，使得 i < j

> 原文：[https://www.geeksforgeeks.org/count-of-unique-pairs-arri-arrj-such-that-i-j/](https://www.geeksforgeeks.org/count-of-unique-pairs-arri-arrj-such-that-i-j/)

给定数组 **arr []** ，任务是打印唯一对**（arr [i]，arr [j]）**的计数，以便 **i < j** 。

**示例**：

> **输入**：arr [] = {1、2、1、4、5、2}
> **输出**：11
> 可能的对是（1、2）， （1，1），（1，4），（1，5），（2，1），（2，4），（2，5），（2，2），（4，5），（4 ，2），（5，2）
> 
> **输入**：arr [] = {1、2、3、4}
> **输出**：6
> 可能的对是（1、2），（1、3 ），（1、4），（2、3），（2、4），（3、4）

**朴素的方法**：最简单的方法是遍历每个可能的对，如果满足条件，则将其添加到集合中。 然后，我们可以返回集合的大小作为答案。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach
#include <iostream>
#include <set>
using namespace std;

// Function to return the count  
// of unique pairs in the array  
int getPairs(int arr[], int n)
{
    // Set to store unique pairs  
    set<pair<int, int>> h;
    for(int i = 0; i < (n - 1); i++)
    { 
        for (int j = i + 1; j < n; j++) 
        {
            // Create pair of (arr[i], arr[j])  
            // and add it to the hashset  
            h.insert(make_pair(arr[i], arr[j]));  
        }
    }

    // Return the size of the HashSet  
    return h.size(); 
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 4, 2, 5, 3, 5 };
    int  n = sizeof(arr) / sizeof(arr[0]);
    printf("%d", getPairs(arr, n)) ;
    return 0;
}

// This code is contributed by SHUBHAMSINGH10

```

## Java

```java

// Java implementation of the approach
import java.util.HashSet;
import javafx.util.Pair;

class GFG {

    // Function to return the count
    // of unique pairs in the array
    static int getPairs(int arr[], int n)
    {

        // HashSet to store unique pairs
        HashSet<Pair> h = new HashSet<Pair>();
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {

                // Create pair of (a[i], a[j])
                // and add it to the hashset
                Pair<Integer, Integer> p
                    = new Pair<>(arr[i], arr[j]);
                h.add(p);
            }
        }

        // Return the size of the HashSet
        return h.size();
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 2, 4, 2, 5, 3, 5 };
        int n = arr.length;
        System.out.println(getPairs(arr, n));
    }
}

```

## Python3

```py

# Python3 implementation of the approach 

# Function to return the count 
# of unique pairs in the array 
def getPairs(arr, n) :

    # Set to store unique pairs 
    h = set() 
    for i in range(n - 1) :
        for j in range(i + 1, n) :

            # Create pair of (a[i], a[j]) 
            # and add it to the hashset 
            h.add((arr[i], arr[j])); 

    # Return the size of the HashSet 
    return len(h); 

# Driver code 
if __name__ == "__main__" :

    arr = [ 1, 2, 2, 4, 2, 5, 3, 5 ] 
    n = len(arr) 

    print(getPairs(arr, n))

# This code is contributed by Ryuga

```

## C#

```cs

// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the count
// of unique pairs in the array
static int getPairs(int []arr, int n)
{

    // HashSet to store unique pairs
    HashSet<Tuple<int,
                  int>> h = new HashSet<Tuple<int,
                                              int>>();

    for(int i = 0; i < n - 1; i++)
    {
        for(int j = i + 1; j < n; j++) 
        {

            // Create pair of (a[i], a[j])
            // and add it to the hashset
            Tuple<int, 
                  int> p = new Tuple<int,
                                     int>(arr[i], 
                                          arr[j]);
            h.Add(p);
        }
    }

    // Return the size of the HashSet
    return h.Count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 2, 4, 2, 5, 3, 5 };
    int n = arr.Length;

    Console.WriteLine(getPairs(arr, n));
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
14

```

**时间复杂度**：`O(N ^ 2)`

**注意**：请使用离线 IDE 编译以上代码。 在线编译器可能不支持 JavaFX。

**有效方法**：每个元素 **arr [i]** 可以与元素 **arr [j]** 成对，如果 **i < j** 。 但是**（arr [i]，arr [j]）**应该是唯一的，因此对于每个唯一的 **arr [i]** ，可能的对将等于子图中不同数字的数量 数组 **arr [i + 1]，arr [i + 2]，…，arr [n – 1]** 。 因此，对于每个 **arr [i]** ，我们将从右到左找到唯一的元素。 对于此任务，使用哈希表很容易跟踪所访问的元素。 这样，对于每个唯一的 **arr [j]** ，我们将拥有唯一的 **arr [i]** 。 现在，我们将求和每个唯一的 **arr [i]** 的值，这是所需的对数。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the count
// of unique pairs in the array
int getPairs(int a[], int n)
{
    set<int> visited1;

    // un[i] stores number of unique elements
    // from un[i + 1] to un[n - 1]
    int un[n] ;

    // Last element will have no unique elements
    // after it
    un[n - 1] = 0;

    // To count unique elements after every a[i]
    int count = 0;
     // auto pos = s.find(3); 

     // prints the set elements 
     // cout << "The set elements after 3 are: "; 
     // for (auto it = pos; it != s.end(); it++) 
    // cout << *it << " "
    for (int i = n - 1; i > 0; i--)
    {

        // If current element has already been used
        // i.e. not unique
        auto pos = visited1.find(a[i]); 
        if (pos != visited1.end())
            un[i - 1] = count;
        else
            un[i - 1] = ++count;

        // Set to true if a[i] is visited
        visited1.insert(a[i]);
    }

    set<int>visited2;

    // To know which a[i] is already visited
    int answer = 0;
    for (int i = 0; i < n - 1; i++) 
    {

        // If visited, then the pair would
        // not be unique
        auto pos = visited2.find(a[i]); 
        if (pos != visited2.end())
            continue;

        // Calculating total unqiue pairs
        answer += un[i];

        // Set to true if a[i] is visited
        visited2.insert(a[i]);
    }
    return answer;
}

// Driver code
int main()
{
    int a[] = { 1, 2, 2, 4, 2, 5, 3, 5 };
    int n = sizeof(a)/sizeof(a[0]);

    // Print the count of unique pairs
    cout<<(getPairs(a, n));
}

// This code is contributed by Rajput-Ji

```

## Java

```java

// Java implementation of the approach
import java.util.HashSet;

public class GFG {

    // Function to return the count
    // of unique pairs in the array
    static int getPairs(int a[], int n)
    {
        HashSet<Integer> visited1 = new HashSet<Integer>();

        // un[i] stores number of unique elements
        // from un[i + 1] to un[n - 1]
        int un[] = new int[n];

        // Last element will have no unique elements
        // after it
        un[n - 1] = 0;

        // To count unique elements after every a[i]
        int count = 0;
        for (int i = n - 1; i > 0; i--) {

            // If current element has already been used
            // i.e. not unique
            if (visited1.contains(a[i]))
                un[i - 1] = count;
            else
                un[i - 1] = ++count;

            // Set to true if a[i] is visited
            visited1.add(a[i]);
        }

        HashSet<Integer> visited2 = new HashSet<Integer>();

        // To know which a[i] is already visited
        int answer = 0;
        for (int i = 0; i < n - 1; i++) {

            // If visited, then the pair would
            // not be unique
            if (visited2.contains(a[i]))
                continue;

            // Calculating total unqiue pairs
            answer += un[i];

            // Set to true if a[i] is visited
            visited2.add(a[i]);
        }
        return answer;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 1, 2, 2, 4, 2, 5, 3, 5 };
        int n = a.length;

        // Print the count of unique pairs
        System.out.println(getPairs(a, n));
    }
}

```

## Python3

```py

# Python3 implementation of the approach 

# Function to return the count 
# of unique pairs in the array 
def getPairs(a, n):

    visited1 = set() 

    # un[i] stores number of unique elements 
    # from un[i + 1] to un[n - 1] 
    un = [0] * n

    # Last element will have no unique elements 
    # after it 
    un[n - 1] = 0

    # To count unique elements after every a[i] 
    count = 0
    for i in range(n - 1, -1, -1):

        # If current element has already been used 
        # i.e. not unique 
        if (a[i] in visited1):
            un[i - 1] = count 
        else:
            count += 1
            un[i - 1] = count 

        # Set to true if a[i] is visited 
        visited1.add(a[i]) 

    visited2 = set()

    # To know which a[i] is already visited 
    answer = 0
    for i in range(n - 1):

        # If visited, then the pair would 
        # not be unique 
        if (a[i] in visited2):
            continue

        # Calculating total unqiue pairs 
        answer += un[i] 

        # Set to true if a[i] is visited 
        visited2.add(a[i]) 

    return answer 

# Driver code 

a = [1, 2, 2, 4, 2, 5, 3, 5]
n = len(a)

# Print the count of unique pairs 
print(getPairs(a, n)) 

# This code is contributed by SHUBHAMSINGH10

```

## C#

```cs

// C# implementation of the approach 
using System;
using System.Collections.Generic; 

class GFG 
{ 

    // Function to return the count 
    // of unique pairs in the array 
    static int getPairs(int []a, int n) 
    { 
        HashSet<int> visited1 = new HashSet<int>(); 

        // un[i] stores number of unique elements 
        // from un[i + 1] to un[n - 1] 
        int []un = new int[n]; 

        // Last element will have no unique elements 
        // after it 
        un[n - 1] = 0; 

        // To count unique elements after every a[i] 
        int count = 0; 
        for (int i = n - 1; i > 0; i--) 
        { 

            // If current element has already been used 
            // i.e. not unique 
            if (visited1.Contains(a[i])) 
                un[i - 1] = count; 
            else
                un[i - 1] = ++count; 

            // Set to true if a[i] is visited 
            visited1.Add(a[i]); 
        } 

        HashSet<int> visited2 = new HashSet<int>(); 

        // To know which a[i] is already visited 
        int answer = 0; 
        for (int i = 0; i < n - 1; i++) 
        { 

            // If visited, then the pair would 
            // not be unique 
            if (visited2.Contains(a[i])) 
                continue; 

            // Calculating total unqiue pairs 
            answer += un[i]; 

            // Set to true if a[i] is visited 
            visited2.Add(a[i]); 
        } 
        return answer; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int []a = { 1, 2, 2, 4, 2, 5, 3, 5 }; 
        int n = a.Length; 

        // Print the count of unique pairs 
        Console.WriteLine(getPairs(a, n)); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:** 

```
14

```

**时间复杂度**：`O(n)`



* * *

* * *



