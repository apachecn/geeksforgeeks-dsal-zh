# 使用就地排序算法对对象进行排序

> 原文:[https://www . geeksforgeeks . org/排序-对象-使用就地排序-算法/](https://www.geeksforgeeks.org/sorting-objects-using-in-place-sorting-algorithm/)

给定一个由**红色**、**蓝色**和**黄色**对象组成的数组，任务是使用就地排序算法对数组进行排序，使所有蓝色对象出现在所有红色对象之前，所有红色对象出现在所有黄色对象之前。
**举例:**

> **输入:** arr[] = {“蓝”“红”“黄”“蓝”“黄”}
> T3】输出:蓝蓝红黄
> T6】输入: arr[] = {“红”“蓝”“红”“黄”“蓝”}
> T9】输出:蓝蓝红黄

**方法:**首先[使用哈希表将**蓝色**、**红色**和**黄色**对象的值分别映射到 **1** 、 **2** 和 **3** 。现在，只要需要比较两个对象，就使用这些映射值。因此，该算法将对对象数组进行排序，以便首先出现所有**蓝色**对象(映射到值 1)，然后出现所有**红色**对象(映射到值 2)，然后出现所有**黄色**对象(映射到值 3)。
以下是上述方法的实施:](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Partition function which will partition
// the array and into two parts
int partition(vector<string>& objects, int l, int r,
            unordered_map<string, int>& hash)
{
    int j = l - 1;

    int last_element = hash[objects[r]];

    for (int i = l; i < r; i++) {

        // Compare hash values of objects
        if (hash[objects[i]] <= last_element) {
            j++;
            swap(objects[i], objects[j]);
        }
    }

    j++;

    swap(objects[j], objects[r]);

    return j;
}

// Classic quicksort algorithm
void quicksort(vector<string>& objects, int l, int r,
                    unordered_map<string, int>& hash)
{
    if (l < r) {
        int mid = partition(objects, l, r, hash);
        quicksort(objects, l, mid - 1, hash);
        quicksort(objects, mid + 1, r, hash);
    }
}

// Function to sort and print the objects
void sortObj(vector<string>& objects)
{

    // Create a hash table
    unordered_map<string, int> hash;

    // As the sorting order is blue objects,
    // red objects and then yellow objects
    hash["blue"] = 1;
    hash["red"] = 2;
    hash["yellow"] = 3;

    // Quick sort function
    quicksort(objects, 0, int(objects.size() - 1), hash);

    // Printing the sorted array
    for (int i = 0; i < objects.size(); i++)
        cout << objects[i] << " ";
}

// Driver code
int main()
{

    // Let's represent objects as strings
    vector<string> objects{ "red", "blue",
                            "red", "yellow", "blue" };

    sortObj(objects);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Partition function which will partition
// the array and into two parts
static int partition(Vector<String> objects, int l, int r,
                        Map<String, Integer> hash)
{
    int j = l - 1;

    int last_element = hash.get(objects.get(r));

    for (int i = l; i < r; i++)
    {

        // Compare hash values of objects
        if (hash.get(objects.get(i)) <= last_element)
        {
            j++;
            Collections.swap(objects, i, j);
        }
    }

    j++;

    Collections.swap(objects, j, r);

    return j;
}

// Classic quicksort algorithm
static void quicksort(Vector<String> objects, int l, int r,
                         Map<String, Integer> hash)
{
    if (l < r)
    {
        int mid = partition(objects, l, r, hash);
        quicksort(objects, l, mid - 1, hash);
        quicksort(objects, mid + 1, r, hash);
    }
}

// Function to sort and print the objects
static void sortObj(Vector<String> objects)
{

    // Create a hash table
    Map<String, Integer> hash = new HashMap<>();

    // As the sorting order is blue objects,
    // red objects and then yellow objects
    hash. put("blue", 1);
    hash. put("red", 2);
    hash. put("yellow", 3);

    // Quick sort function
    quicksort(objects, 0, objects.size() - 1, hash);

    // Printing the sorted array
    for (int i = 0; i < objects.size(); i++)
        System.out.print(objects.get(i) + " ");
}

// Driver code
public static void main(String []args)
{
    // Let's represent objects as strings
    Vector<String> objects = new Vector<>(Arrays.asList( "red", "blue",
                                                         "red", "yellow",
                                                         "blue" ));

    sortObj(objects);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Partition function which will partition
# the array and into two parts
objects = []
hash = dict()

def partition(l, r):
    global objects, hash
    j = l - 1

    last_element = hash[objects[r]]

    for i in range(l, r):

        # Compare hash values of objects
        if (hash[objects[i]] <= last_element):
            j += 1
            (objects[i],
             objects[j]) = (objects[j],
                            objects[i])

    j += 1

    (objects[j],
     objects[r]) = (objects[r],
                    objects[j])

    return j

# Classic quicksort algorithm
def quicksort(l, r):
    if (l < r):
        mid = partition(l, r)
        quicksort(l, mid - 1)
        quicksort(mid + 1, r)

# Function to sort and print the objects
def sortObj():
    global objects, hash

    # As the sorting order is blue objects,
    # red objects and then yellow objects
    hash["blue"] = 1
    hash["red"] = 2
    hash["yellow"] = 3

    # Quick sort function
    quicksort(0, int(len(objects) - 1))

    # Printing the sorted array
    for i in objects:
        print(i, end = " ")

# Driver code

# Let's represent objects as strings
objects = ["red", "blue", "red",
               "yellow", "blue"]

sortObj()

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Partition function which will partition
// the array and into two parts
static int partition(List<String> objects, int l, int r,
                           Dictionary<String, int> hash)
{
    int j = l - 1;
    String temp;
    int last_element = hash[objects[r]];

    for (int i = l; i < r; i++)
    {

        // Compare hash values of objects
        if (hash[objects[i]] <= last_element)
        {
            j++;
            temp = objects[i];
            objects[i] = objects[j];
            objects[j] = temp;
        }
    }

    j++;

    temp = objects[r];
    objects[r] = objects[j];
    objects[j] = temp;

    return j;
}

// Classic quicksort algorithm
static void quicksort(List<String> objects, int l, int r,
                            Dictionary<String, int> hash)
{
    if (l < r)
    {
        int mid = partition(objects, l, r, hash);
        quicksort(objects, l, mid - 1, hash);
        quicksort(objects, mid + 1, r, hash);
    }
}

// Function to sort and print the objects
static void sortObj(List<String> objects)
{

    // Create a hash table
    Dictionary<String,
               int> hash = new Dictionary<String,
                                          int>();

    // As the sorting order is blue objects,
    // red objects and then yellow objects
    hash.Add("blue", 1);
    hash.Add("red", 2);
    hash.Add("yellow", 3);

    // Quick sort function
    quicksort(objects, 0, objects.Count - 1, hash);

    // Printing the sorted array
    for (int i = 0; i < objects.Count; i++)
        Console.Write(objects[i] + " ");
}

// Driver code
public static void Main(String []args)
{
    // Let's represent objects as strings
    List<String> objects = new List<String>{"red", "blue",
                                            "red", "yellow",
                                            "blue"};

    sortObj(objects);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Partition function which will partition
// the array and into two parts
function partition(objects, l, r, hash)
{
    let j = l - 1;

    let last_element = hash.get(objects[r]);

    for (let i = l; i < r; i++)
    {

        // Compare hash values of objects
        if (hash.get(objects[i]) <= last_element)
        {
            j++;
            let temp = objects[i];
            objects[i] = objects[j];
            objects[j] = temp;
        }
    }

    j++;

    let temp = objects[r];
            objects[r] = objects[j];
            objects[j] = temp;

    return j;
}

// Classic quicksort algorithm
function quicksort(objects, l, r, hash)
{
    if (l < r)
    {
        let mid = partition(objects, l, r, hash);
        quicksort(objects, l, mid - 1, hash);
        quicksort(objects, mid + 1, r, hash);
    }
}

// Function to sort and print the objects
function sortObj(objects)
{

    // Create a hash table
    let hash = new Map();

    // As the sorting order is blue objects,
    // red objects and then yellow objects
    hash. set("blue", 1);
    hash. set("red", 2);
    hash. set("yellow", 3);

    // Quick sort function
    quicksort(objects, 0, objects.length - 1, hash);

    // Printing the sorted array
    for (let i = 0; i < objects.length; i++)
        document.write(objects[i] + " ");
}

// Driver code
let objects = ["red", "blue","red", "yellow", "blue"];
sortObj(objects);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
blue blue red red yellow
```