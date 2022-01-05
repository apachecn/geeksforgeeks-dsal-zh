# 找出两个给定集合之间的 Jaccard 索引和 Jaccard 距离

> 原文:[https://www . geesforgeks . org/find-the-JAC card-index-and-JAC card-两个给定集合之间的距离/](https://www.geeksforgeeks.org/find-the-jaccard-index-and-jaccard-distance-between-the-two-given-sets/)

给定两组整数 **s1** 和 **s2** ，任务是找到 [Jaccard 索引](https://en.wikipedia.org/wiki/Jaccard_index)和两组之间的 Jaccard 距离。

**示例:**

> **输入:** s1 = {1，2，3，4，5}，s2 = {4，5，6，7，8，9，10}
> **输出:**
> 雅克卡指数= 0.2
> 雅克卡距离= 0.8
> 
> **输入:** s1 = {1，2，3，4，5}，s2 = {4，5，6，7，8 }
> T3】输出:T5】雅克卡指数= 0.25
> 雅克卡距离= 0.75

**方法:**两组之间的 Jaccard 指数和 Jaccard 距离可以通过以下公式计算:

![ \[ Jaccard Index = \frac {| A \cap B |}{| A \cup B |} = \frac {|A \cap B |}{|A| +|B| -|A \cap B |} \] \[ Jaccard Distance = 1 - Jaccard Index \] ](img/f927aec3da9cf1f5d62153d0752c8836.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// intersection set of s1 and s2
set<int> intersection(set<int> s1, set<int> s2)
{
    set<int> intersect;

    // Find the intersection of the two sets
    set_intersection(s1.begin(), s1.end(), s2.begin(), s2.end(),
                     inserter(intersect, intersect.begin()));

    return intersect;
}

// Function to return the Jaccard index of two sets
double jaccard_index(set<int> s1, set<int> s2)
{
    // Sizes of both the sets
    double size_s1 = s1.size();
    double size_s2 = s2.size();

    // Get the intersection set
    set<int> intersect = intersection(s1, s2);

    // Size of the intersection set
    double size_in = intersect.size();

    // Calculate the Jaccard index
    // using the formula
    double jaccard_in = size_in
                        / (size_s1 + size_s2 - size_in);

    // Return the Jaccard index
    return jaccard_in;
}

// Function to return the Jaccard distance
double jaccard_distance(double jaccardIndex)
{
    // Calculate the Jaccard distance
    // using the formula
    double jaccard_dist = 1 - jaccardIndex;

    // Return the Jaccard distance
    return jaccard_dist;
}

// Driver code
int main()
{
    // Elements of the 1st set
    set<int> s1;
    s1.insert(1);
    s1.insert(2);
    s1.insert(3);
    s1.insert(4);
    s1.insert(5);

    // Elements of the 2nd set
    set<int> s2;
    s2.insert(4);
    s2.insert(5);
    s2.insert(6);
    s2.insert(7);
    s2.insert(8);
    s2.insert(9);
    s2.insert(10);

    double jaccardIndex = jaccard_index(s1, s2);

    // Print the Jaccard index and Jaccard distance
    cout << "Jaccard index = "
         << jaccardIndex << endl;
    cout << "Jaccard distance = "
         << jaccard_distance(jaccardIndex);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

# Function to return the 
# intersection set of s1 and s2 
def intersection(s1, s2) :

    # Find the intersection of the two sets 
    intersect = s1 & s2 ;

    return intersect; 

# Function to return the Jaccard index of two sets 
def jaccard_index(s1, s2) :

    # Sizes of both the sets 
    size_s1 = len(s1); 
    size_s2 = len(s2); 

    # Get the intersection set 
    intersect = intersection(s1, s2); 

    # Size of the intersection set 
    size_in = len(intersect); 

    # Calculate the Jaccard index 
    # using the formula 
    jaccard_in = size_in  / (size_s1 + size_s2 - size_in); 

    # Return the Jaccard index 
    return jaccard_in; 

# Function to return the Jaccard distance 
def jaccard_distance(jaccardIndex)  :

    # Calculate the Jaccard distance 
    # using the formula 
    jaccard_dist = 1 - jaccardIndex; 

    # Return the Jaccard distance 
    return jaccard_dist; 

# Driver code 
if __name__ == "__main__" : 

    # Elements of the 1st set 
    s1 = set(); 
    s1.add(1); 
    s1.add(2); 
    s1.add(3); 
    s1.add(4); 
    s1.add(5); 

    # Elements of the 2nd set 
    s2 = set(); 
    s2.add(4); 
    s2.add(5); 
    s2.add(6); 
    s2.add(7); 
    s2.add(8); 
    s2.add(9); 
    s2.add(10); 

    jaccardIndex = jaccard_index(s1, s2); 

    # Print the Jaccard index and Jaccard distance 
    print("Jaccard index = ",jaccardIndex); 
    print("Jaccard distance = ",jaccard_distance(jaccardIndex)); 

    # This code is contributed by AnkitRai01
```

**Output:**

```
Jaccard index = 0.2
Jaccard distance = 0.8

```