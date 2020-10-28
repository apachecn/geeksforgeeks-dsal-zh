# 从给定的门票清单中查找行程

> 原文：[https://www.geeksforgeeks.org/find-itinerary-from-a-given-list-of-tickets/](https://www.geeksforgeeks.org/find-itinerary-from-a-given-list-of-tickets/)

给定票证列表，请使用给定列表按顺序查找行程。

例：

```
Input:
"Chennai" -> "Banglore"
"Bombay" -> "Delhi"
"Goa"    -> "Chennai"
"Delhi"  -> "Goa"

Output: 
Bombay->Delhi, Delhi->Goa, Goa->Chennai, Chennai->Banglore,
```

可以假设输入的票证清单不是周期性的，并且每个城市（最终目的地除外）都有一张票证。

一种解决方案是构建图形并对该图形进行[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。 该解决方案的时间复杂度为 O（n）。

我们还可以使用[散列](http://geeksquiz.com/hashing-set-1-introduction/)来避免构建图形。 这个想法是首先找到起点。 起点永远不会在票证的“靠”一侧。 一旦找到起点，我们就可以简单地遍历给定的地图以按顺序打印行程。 以下是步骤。

```
1) Create a HashMap of given pair of tickets.  Let the created 
   HashMap be 'dataset'. Every entry of 'dataset' is of the form 
   "from->to" like "Chennai" -> "Banglore"

2) Find the starting point of itinerary.
     a) Create a reverse HashMap.  Let the reverse be 'reverseMap'
        Entries of 'reverseMap' are of the form "to->form". 
        Following is 'reverseMap' for above example.
        "Banglore"-> "Chennai" 
        "Delhi"   -> "Bombay" 
        "Chennai" -> "Goa"
        "Goa"     ->  "Delhi"

     b) Traverse 'dataset'.  For every key of dataset, check if it
        is there in 'reverseMap'.  If a key is not present, then we 
        found the starting point. In the above example, "Bombay" is
        starting point.

3) Start from above found starting point and traverse the 'dataset' 
   to print itinerary.

```

以上所有步骤都需要 O（n）时间，因此总时间复杂度为 O（n）。

以下是上述想法的 Java 实现。

## Java

```java

// Java program to print itinerary in order 
import java.util.HashMap; 
import java.util.Map; 

public class printItinerary 
{ 
    // Driver function 
    public static void main(String[] args) 
    { 
        Map<String, String> dataSet = new HashMap<String, String>(); 
        dataSet.put("Chennai", "Banglore"); 
        dataSet.put("Bombay", "Delhi"); 
        dataSet.put("Goa", "Chennai"); 
        dataSet.put("Delhi", "Goa"); 

        printResult(dataSet); 
    } 

    // This function populates 'result' for given input 'dataset' 
    private static void printResult(Map<String, String> dataSet) 
    { 
        // To store reverse of given map 
        Map<String, String> reverseMap = new HashMap<String, String>(); 

        // To fill reverse map, iterate through the given map 
        for (Map.Entry<String,String> entry: dataSet.entrySet()) 
            reverseMap.put(entry.getValue(), entry.getKey()); 

        // Find the starting point of itinerary 
        String start = null; 
        for (Map.Entry<String,String> entry: dataSet.entrySet()) 
        { 
              if (!reverseMap.containsKey(entry.getKey())) 
              { 
                   start = entry.getKey(); 
                   break; 
              } 
        } 

        // If we could not find a starting point, then something wrong 
        // with input 
        if (start == null) 
        { 
           System.out.println("Invalid Input"); 
           return; 
        } 

        // Once we have starting point, we simple need to go next, next 
        // of next using given hash map 
        String to = dataSet.get(start); 
        while (to != null) 
        { 
            System.out.print(start +  "->" + to + ", "); 
            start = to; 
            to = dataSet.get(to); 
        } 
    } 
} 

```

## C++

```cpp

#include <bits/stdc++.h> 
using namespace std; 

void printItinerary(map<string, string> dataSet) 
{ 
    // To store reverse of given map 
    map<string, string> reversemap; 
    map<string, string>::iterator it; 

    // To fill reverse map, iterate through the given map 
    for (it = dataSet.begin(); it!=dataSet.end(); it++) 
        reversemap[it->second] = it->first; 

    // Find the starting point of itinerary 
    string start; 

    for (it = dataSet.begin(); it!=dataSet.end(); it++) 
    { 
        if (reversemap.find(it->first) == reversemap.end()) 
        { 
            start = it->first; 
            break; 
        } 
    } 

    // If we could not find a starting point, then something wrong with input 
     if (start.empty()) 
     { 
        cout << "Invalid Input" << endl; 
        return; 
     } 

    // Once we have starting point, we simple need to go next, 
    //next of next using given hash map 
    it = dataSet.find(start); 
    while (it != dataSet.end()) 
    { 
        cout << it->first << "->" << it->second << endl; 
        it = dataSet.find(it->second); 
    } 

} 

int main() 
{ 
    map<string, string> dataSet; 
    dataSet["Chennai"] = "Banglore"; 
    dataSet["Bombay"] = "Delhi"; 
    dataSet["Goa"] = "Chennai"; 
    dataSet["Delhi"] = "Goa"; 

    printItinerary(dataSet); 

    return 0; 
} 
// C++ implementation is contributed by Aditya Goel 

```

Output:

```
Bombay->Delhi, Delhi->Goa, Goa->Chennai, Chennai->Banglore,
```

本文由 **Rahul Jain** 编译。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

