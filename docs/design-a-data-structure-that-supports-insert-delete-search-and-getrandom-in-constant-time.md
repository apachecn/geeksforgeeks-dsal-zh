# 设计一个支持恒定时间插入，删除，搜索和`getRandom`的数据结构

> 原文：[https://www.geeksforgeeks.org/design-a-data-structure-that-supports-insert-delete-search-and-getrandom-in-constant-time/](https://www.geeksforgeeks.org/design-a-data-structure-that-supports-insert-delete-search-and-getrandom-in-constant-time/)

设计一个数据结构，以支持在`Θ(1)`时间内进行以下操作。

`insert(x)`：将`x`插入数据结构（如果尚不存在）。

`remove(x)`：从数据结构中删除项`x`（如果存在）。

`search(x)`：在数据结构中搜索项目`x`。

`getRandom()`：从当前元素集中返回一个随机元素。

我们可以使用[散列](https://www.geeksforgeeks.org/tag/hashing/)支持`Θ(1)`时间内的前 3 个运算。 怎么做第四次操作？ 这个想法是将可调整大小的数组（Java 中为`ArrayList`，C 中为`vector`）与哈希一起使用。 [可调整大小的数组](https://www.geeksforgeeks.org/analysis-algorithm-set-5-amortized-analysis-introduction/)支持在`Θ(1)`摊销时间复杂度中插入。 为了实现`getRandom()`，我们可以简单地选择一个从 0 到`size-1`的随机数（`size`是当前元素的数量）并返回该索引处的元素。 哈希映射将数组值存储为键，并将数组索引存储为值。

以下是详细的操作。

`insert(x)`

1.  通过进行哈希映射查找来检查`x`是否已经存在。

2.  如果不存在，则将其插入数组的末尾。

3.  同样在哈希表中添加`x`作为键，最后一个数组索引作为索引。

`remove(x)`

1.  通过执行哈希映射查找来检查`x`是否存在。

2.  如果存在，请找到其索引并将其从哈希映射中删除。

3.  将最后一个元素与此数组中的元素交换，然后删除最后一个元素。

进行交换是因为可以在`O(1)`时间内删除最后一个元素。

4.  更新哈希映射中最后一个元素的索引。

`getRandom()`

1.  生成一个从 0 到最后一个索引的随机数。

2.  返回随机生成的索引处的数组元素。

`search(x)`

在哈希映射中查找`x`。

下面是数据结构的实现。

## C++

```cpp

/* C++ program to design a DS that supports folloiwng operations 
in Theta(n) time 
a) Insert 
b) Delete 
c) Search 
d) getRandom */

#include<bits/stdc++.h> 
using namespace std; 

// class to represent the required data structure 
class myStructure 
{ 
    // A resizable array 
    vector <int> arr; 

    // A hash where keys are array elements and vlaues are 
    // indexes in arr[] 
    map <int, int> Map; 

    public: 
    // A Theta(1) function to add an element to MyDS 
    // data structure 
    void add(int x) 
    { 
        // If ekement is already present, then noting to do 
        if(Map.find(x) != Map.end()) 
            return; 

        // Else put element at the end of arr[] 
        int index = arr.size(); 
        arr.push_back(x); 

        // and hashmap also 
        Map.insert(std::pair<int,int>(x, index)); 
    } 

    // function to remove a number to DS in O(1) 
    void remove(int x) 
    { 
        // element not found then return 
        if(Map.find(x) == Map.end()) 
            return; 

        // remove element from map 
        int index = Map.at(x); 
        Map.erase(x); 

        // swap with last element in arr 
        // then remove element at back 
        int last = arr.size() - 1; 
        swap(arr[index], arr[last]); 
        arr.pop_back(); 

        // Update hash table for new index of last element 
        Map.at(arr[index]) = index; 
    } 

    // Returns index of element if element is present, otherwise null 
    int search(int x) 
    { 
        if(Map.find(x) != Map.end()) 
        return Map.at(x); 
        return -1; 
    } 

    // Returns a random element from myStructure 
    int getRandom() 
    { 
        // Find a random index from 0 to size - 1 
        srand (time(NULL)); 
        int random_index = rand() % arr.size(); 

        // Return element at randomly picked index 
        return arr.at(random_index); 
    }      
}; 

// Driver main 
int main() 
{ 
    myStructure ds; 
    ds.add(10); 
    ds.add(20); 
    ds.add(30); 
    ds.add(40); 
    cout << ds.search(30) << endl; 
    ds.remove(20); 
    ds.add(50); 
    cout << ds.search(50) << endl; 
    cout << ds.getRandom() << endl; 
} 

// This code is contributed by Aditi Sharma 

```

## Java

```java

/* Java program to design a data structure that support folloiwng operations 
   in Theta(n) time 
   a) Insert 
   b) Delete 
   c) Search 
   d) getRandom */
import java.util.*; 

// class to represent the required data structure 
class MyDS 
{ 
   ArrayList<Integer> arr;   // A resizable array 

   // A hash where keys are array elements and vlaues are 
   // indexes in arr[] 
   HashMap<Integer, Integer>  hash; 

   // Constructor (creates arr[] and hash) 
   public MyDS() 
   { 
       arr = new ArrayList<Integer>(); 
       hash = new HashMap<Integer, Integer>(); 
   } 

   // A Theta(1) function to add an element to MyDS 
   // data structure 
   void add(int x) 
   { 
      // If ekement is already present, then noting to do 
      if (hash.get(x) != null) 
          return; 

      // Else put element at the end of arr[] 
      int s = arr.size(); 
      arr.add(x); 

      // And put in hash also 
      hash.put(x, s); 
   } 

   // A Theta(1) function to remove an element from MyDS 
   // data structure 
   void remove(int x) 
   { 
       // Check if element is present 
       Integer index = hash.get(x); 
       if (index == null) 
          return; 

       // If present, then remove element from hash 
       hash.remove(x); 

       // Swap element with last element so that remove from 
       // arr[] can be done in O(1) time 
       int size = arr.size(); 
       Integer last = arr.get(size-1); 
       Collections.swap(arr, index,  size-1); 

       // Remove last element (This is O(1)) 
       arr.remove(size-1); 

       // Update hash table for new index of last element 
       hash.put(last, index); 
    } 

    // Returns a random element from MyDS 
    int getRandom() 
    { 
       // Find a random index from 0 to size - 1 
       Random rand = new Random();  // Choose a different seed 
       int index = rand.nextInt(arr.size()); 

       // Return element at randomly picked index 
       return arr.get(index); 
    } 

    // Returns index of element if element is present, otherwise null 
    Integer search(int x) 
    { 
       return hash.get(x); 
    } 
} 

// Driver class 
class Main 
{ 
    public static void main (String[] args) 
    { 
        MyDS ds = new MyDS(); 
        ds.add(10); 
        ds.add(20); 
        ds.add(30); 
        ds.add(40); 
        System.out.println(ds.search(30)); 
        ds.remove(20); 
        ds.add(50); 
        System.out.println(ds.search(50)); 
        System.out.println(ds.getRandom()); 
    } 
} 

```

## Python3

```py

''' 
Python program to design a DS that  
supports following operations 
in Theta(n) time: 
a) Insert 
b) Delete 
c) Search 
d) getRandom 
'''
import random 

# Class to represent the required  
# data structure  
class MyDS: 

    # Constructor (creates a list and a hash) 
    def __init__(self): 

        # A resizable array 
        self.arr = [] 

        # A hash where keys are lists elements  
        # and values are indexes of the list 
        self.hashd = {}  

    # A Theta(1) function to add an element  
    # to MyDS data structure 
    def add(self, x): 

        # If element is already present,  
        # then nothing has to be done 
        if x in self.hashd: 
            return

        # Else put element at 
        # the end of the list 
        s = len(self.arr) 
        self.arr.append(x) 

        # Also put it into hash 
        self.hashd[x] = s 

    # A Theta(1) function to remove an element 
    # from MyDS data structure  
    def remove(self, x): 

        # Check if element is present 
        index = self.hashd.get(x, None) 
        if index == None: 
            return

        # If present, then remove  
        # element from hash 
        del self.hashd[x] 

        # Swap element with last element  
        # so that removal from the list  
        # can be done in O(1) time 
        size = len(self.arr) 
        last = self.arr[size - 1] 
        self.arr[index], \ 
        self.arr[size - 1] = self.arr[size - 1], \ 
                             self.arr[index] 

        # Remove last element (This is O(1))  
        del self.arr[-1] 

        # Update hash table for  
        # new index of last element 
        self.hashd[last] = index 

    # Returns a random element from MyDS  
    def getRandom(self): 

        # Find a random index from 0 to size - 1 
        index = random.randrange(0, len(self.arr)) 

        # Return element at randomly picked index  
        return self.arr[index] 

    # Returns index of element 
    # if element is present,  
    # otherwise none 
    def search(self, x): 
        return self.hashd.get(x, None) 

# Driver Code 
if __name__=="__main__": 
    ds = MyDS() 
    ds.add(10) 
    ds.add(20) 
    ds.add(30) 
    ds.add(40) 
    print(ds.search(30)) 
    ds.remove(20) 
    ds.add(50) 
    print(ds.search(50)) 
    print(ds.getRandom()) 

# This code is contributed  
# by Saurabh Singh 

```

**输出**：

```
2
3
40
```

本文由 **Manish Gupta** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

