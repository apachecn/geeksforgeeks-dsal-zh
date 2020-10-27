# 查找数组

中第 K 个最常出现的元素

给定大小为 **N** 的整数 **arr []** 和数字 **K** 的数组，任务是找到第个 **K <sup>]</sup>** 此数组中最常出现的元素。
**注意**：如果数组中有多个具有相同频率的数字，则认为这两个数字的发生级别相同。 因此，请同时打印两个数字。

**示例**：

> **输入**：arr [] = {1、2、2、2、4、4、4、5、5、5、5、5、7、7、8、8、8、8}， K = 1
> **输出**：5
> **说明**：
> 元素的出现如下：
> 1-1
> 2-3
> 4 – 3
> 5 – 5
> 7 – 2
> 8 – 4
> 显然，5 是数组中最常出现的元素。
> 
> **输入**：arr [] = {1、2、2、2、4、4、4、5、5、5、5、5、7、7、8、8、8、8， }，K =3。
> **输出**：

**方法**：这个想法是使用两个[字典数据结构](https://www.geeksforgeeks.org/python-dictionary/)来存储元素的所有频率。

*   [迭代给定数组](https://www.geeksforgeeks.org/iterating-arrays-java/)。
*   [查找所有元素的频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)并将其存储在字典中，以便键是数字，值是频率。
*   初始化另一个字典，以将键存储为频率，并将值存储为具有该频率的所有元素。
*   最后，由于对字典进行了排序，因此在字典中[M-K] 位置找到数组，其中 M 是数组中唯一元素的数量。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find K-th
// most occurring element in an array
#include <bits/stdc++.h>

using namespace std;

// Function to find K-th most
// occurring element in an array
vector<int> findKthMostOccurring(vector<int> arr, int K){

    // Initializing a dictionary
    map<int,int> d;

    // Iterating through the array
    for (int i:arr){

        // If the element is not in
        // the dictionary, adding it
        // with the frequency as 1
        if (d.find(i) == d.end())
            d[i] = 1;

        // If the element is already
        // present in the dictionary,
        // increment its frequency
        else{
            int temp = d[i];
            temp += 1;
            d[i] = temp;
        }
        }

    // Now, the dictionary signifies
    // the number of unique elements.
    // If the count of this is
    // less than K, then we cant find
    // the elements whose occurrence is
    // K-th most occurring.
    if(d.size() < K)
        return {};

    // Initializing a new dictionary
    // to store the elements according
    // to their frequency
    map<int,vector<int> > occu;

    // Iterating through the dictionary
    for (auto freq:d){

        // If the element is not in
        // the dictionary, then store
        // the element in an array
        // with key as the frequency
        if(occu.find(freq.second) == occu.end())
            occu[freq.second].push_back(freq.first);

        // Else, add the element to
        // the array of elements
        else{
            occu[freq.second].push_back(freq.first);
        }
        }

    // Since the dictionary is sorted
    // and not indexed, find (M - K)-th
    // element where M is the length
    // of the dictionary
    K = occu.size() - K;

    // Since we for sure know that the
    // element exists, we iterate
    // through the dictionary and
    // return the element
    for(auto a:occu){
        if(K == 0)
            return a.second;
        K -= 1;
    }
}

// Driver code
int main()
{
    vector<int>arr = {1, 4, 4, 4, 2, 2, 2, 5, 5, 
                       5, 5, 5, 7, 7, 8, 8, 8, 8};
    int K = 3;
    vector<int> a = findKthMostOccurring(arr, K);
    cout << "[";
    for(int i = 0; i < a.size() - 1; i++)
        cout << a[i] << ", ";
    cout << a[a.size()-1] << "]";
    return 0;
}

// This code is contributed by mohit kumar 29

```

## Java

```java

// Java implementation to find K-th
// most occurring element in an array
import java.io.*;
import java.util.*;

class GFG{

// Function to find K-th most
// occurring element in an array
static ArrayList<Integer>findKthMostOccurring(
       ArrayList<Integer> arr, int K)
{

    // Initializing a dictionary
    HashMap<Integer, Integer> d = new HashMap<>();

    // Iterating through the array
    for(int i = 0; i < arr.size(); i++)
    {

        // If the element is not in
        // the dictionary, adding it
        // with the frequency as 1
        if (!d.containsKey(arr.get(i)))
            d.put(arr.get(i), 1);

        // If the element is already
        // present in the dictionary,
        // increment its frequency
        else
        {
            int temp = d.get(arr.get(i));
            temp += 1;
            d.put(arr.get(i), temp);
        }
    }

    // Now, the dictionary signifies
    // the number of unique elements.
    // If the count of this is
    // less than K, then we cant find
    // the elements whose occurrence is
    // K-th most occurring.
    if (d.size() < K)
        return new ArrayList<Integer>();

    // Initializing a new dictionary
    // to store the elements according
    // to their frequency
    HashMap<Integer, 
            ArrayList<Integer>> occu = new HashMap<Integer,
                                                   ArrayList<Integer>>();

    // Iterating through the dictionary
    for(Map.Entry<Integer, Integer> freq : d.entrySet())
    {

        // If the element is not in
        // the dictionary, then store
        // the element in an array
        // with key as the frequency
        if (!occu.containsKey(freq.getValue())) 
        {
            occu.put(freq.getValue(),
                     new ArrayList<Integer>());
            occu.get(freq.getValue()).add(
                     freq.getKey());
        }

        // Else, add the element to
        // the array of elements
        else
        {
            occu.get(freq.getValue()).add(
                     freq.getKey());
        }
    }

    // Since the dictionary is sorted
    // and not indexed, find (M - K)-th
    // element where M is the length
    // of the dictionary
    K = occu.size() - K;

    // Since we for sure know that the
    // element exists, we iterate
    // through the dictionary and
    // return the element
    for(Map.Entry<Integer, 
        ArrayList<Integer>> a : occu.entrySet()) 
    {
        if (K == 0)
            return a.getValue();

        K -= 1;
    }
    return new ArrayList<Integer>();
}

// Driver code
public static void main(String[] args)
{
    ArrayList<Integer> arr = new ArrayList<Integer>(
        Arrays.asList(1, 4, 4, 4, 2, 2, 2, 5, 5,
                      5, 5, 5, 7, 7, 8, 8, 8, 8));

    int K = 3;
    ArrayList<Integer> a = new ArrayList<Integer>(
        findKthMostOccurring(arr, K));

    System.out.print("[");
    for(int i = 0; i < a.size() - 1; i++)
    {
        System.out.print(a.get(i) + ", ");
    }

    if (a.size() >= 1)
        System.out.print((int)a.get(
            a.size() - 1) + "]");
}
}

// This code is contributed by akhilsaini

```

## Python3

```py

# Python implementation to find K-th 
# most occurring element in an array

# Function to find K-th most 
# occurring element in an array
def findKthMostOccurring(arr, K):

    # Initializing a dictionary
    d = dict()

    # Iterating through the array
    for i in arr:

        # If the element is not in 
        # the dictionary, adding it
        # with the frequency as 1
        if i not in d:
            d[i] = 1

        # If the element is already
        # present in the dictionary, 
        # increment its frequency
        else:
            temp = d[i]
            temp += 1
            d[i] = temp

    # Now, the dictionary signifies 
    # the number of unique elements.
    # If the count of this is 
    # less than K, then we cant find 
    # the elements whose occurrence is 
    # K-th most occurring.
    if(len(d) < K):
        return []

    # Initializing a new dictionary
    # to store the elements according
    # to their frequency
    occu = dict()

    # Iterating through the dictionary
    for num, freq in d.items():

        # If the element is not in
        # the dictionary, then store
        # the element in an array
        # with key as the frequency
        if(freq not in occu):
            occu[freq] = [num]

        # Else, add the element to
        # the array of elements
        else:
            temp = occu[freq]
            temp.append(num)
            occu[freq] = temp

    # Since the dictionary is sorted
    # and not indexed, find (M - K)-th
    # element where M is the length
    # of the dictionary
    K = len(occu) - K 

    # Since we for sure know that the 
    # element exists, we iterate 
    # through the dictionary and 
    # return the element
    for num, a in occu.items():
        if(K == 0):
            return a
        K -= 1

# Driver code           
if __name__ == "__main__":
    arr = [1, 4, 4, 4, 2, 2, 2, 5, 5, 5, 5, 5, 7, 7, 8, 8, 8, 8]
    K = 3
    print(findKthMostOccurring(arr, K))

```

## C#

```cs

// C# implementation to find K-th
// most occurring element in an array
using System;
using System.Collections;
using System.Collections.Generic; 

class GFG{

// Function to find K-th most
// occurring element in an array
static ArrayList findKthMostOccurring(ArrayList arr,
                                      int K)
{

    // Initializing a dictionary
    SortedDictionary<int, 
                     int> d = new SortedDictionary<int,
                                                   int>();

    // Iterating through the array
    foreach(int i in arr)
    {

        // If the element is not in
        // the dictionary, adding it
        // with the frequency as 1
        if (!d.ContainsKey(i))
            d[i] = 1;

        // If the element is already
        // present in the dictionary,
        // increment its frequency
        else
        {
            int temp = d[i];
            temp += 1;
            d[i] = temp;
        }
    }

    // Now, the dictionary signifies
    // the number of unique elements.
    // If the count of this is
    // less than K, then we cant find
    // the elements whose occurrence is
    // K-th most occurring.
    if (d.Count < K)
        return new ArrayList();

    // Initializing a new dictionary
    // to store the elements according
    // to their frequency
    SortedDictionary<int,
                     ArrayList> occu = new SortedDictionary<int,
                                                            ArrayList>();

    // Iterating through the dictionary
    foreach(KeyValuePair<int, int> freq in d) 
    {

        // If the element is not in
        // the dictionary, then store
        // the element in an array
        // with key as the frequency
        if (!occu.ContainsKey(freq.Value))
        {
            occu[freq.Value] = new ArrayList();
            occu[freq.Value].Add(freq.Key);
        }

        // Else, add the element to
        // the array of elements
        else
        {
            occu[freq.Value].Add(freq.Key);
        }
    }

    // Since the dictionary is sorted
    // and not indexed, find (M - K)-th
    // element where M is the length
    // of the dictionary
    K = occu.Count - K;

    // Since we for sure know that the
    // element exists, we iterate
    // through the dictionary and
    // return the element
    foreach(KeyValuePair<int, ArrayList> a in occu)
    {
        if (K == 0)
            return a.Value;

        K -= 1;
    }
    return new ArrayList();
}  

// Driver code
public static void Main(string[] args)
{
    ArrayList arr = new ArrayList(){ 1, 4, 4, 4, 2, 2,
                                     2, 5, 5, 5, 5, 5,
                                     7, 7, 8, 8, 8, 8 };
    int K = 3;
    ArrayList a = findKthMostOccurring(arr, K);

    Console.Write("[");
    for(int i = 0; i < a.Count - 1; i++)
    {
        Console.Write(a[i] + ", ");
    }
    Console.Write((int)a[a.Count - 1] + "]");
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
[2, 4]

```



* * *

* * *



