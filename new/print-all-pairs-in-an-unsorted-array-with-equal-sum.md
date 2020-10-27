# 以相等的总和在未排序的数组中打印所有对

给定一个未排序的数组 A []。 任务是以相等的总和打印未排序数组中的所有**个唯一对**。
**注意**：以以下示例所示的格式打印结果。
**范例：** [

```
Input: A[] = { 6, 4, 12, 10, 22, 54, 32, 42, 21, 11}
Output:
Pairs : ( 4, 12) ( 6, 10)  have sum : 16
Pairs : ( 10, 22) ( 21, 11)  have sum : 32
Pairs : ( 12, 21) ( 22, 11)  have sum : 33
Pairs : ( 22, 21) ( 32, 11)  have sum : 43
Pairs : ( 32, 21) ( 42, 11)  have sum : 53
Pairs : ( 12, 42) ( 22, 32)  have sum : 54
Pairs : ( 10, 54) ( 22, 42)  have sum : 64

Input:A[]= { 4, 23, 65, 67, 24, 12, 86}
Output:
Pairs : ( 4, 86) ( 23, 67) have sum : 90

```

这个想法是在 C ++ STL 中使用[映射，以避免重复的元素对。](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 

*   创建一个键，键为整数的[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)，值的整数作为整数，以存储所有唯一的元素对及其对应的总和。
*   遍历数组并生成所有可能的对，并将这些对及其对应的和存储在第一张地图上。
*   创建第二个映射，键为整数，值作为对的[向量，以存储所有具有相应总和的元素对的列表。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
*   最后，遍历第二张地图，对于具有多于一对的和，请打印所有对，然后按上述示例所示的格式打印相应的和。

下面是上述方法的实现：

## C ++

```

// C++ program to print all pairs 
// with equal sum 

#include <bits/stdc++.h> 
using namespace std; 

// Function to print all pairs 
// with equal sum 
void pairWithEqualSum(int A[], int n) 
{ 

    map<int, vector<pair<int, int> > > mp; 

    // Insert all unique pairs and their 
    // corresponding sum in the map 
    for (int i = 0; i < n - 1; i++) { 
        for (int j = i + 1; j < n; j++) { 
            pair<int, int> p = make_pair(A[i], A[j]); 

            mp[A[i] + A[j]].push_back(p); 
        } 
    } 

    // Traverse the map mp, and for sum 
    // with more than one pair, print all pairs 
    // and the corresponding sum 
    for (auto itr = mp.begin(); itr != mp.end(); itr++) { 
        if (itr->second.size() > 1) { 
            cout << "Pairs : "; 

            for (int i = 0; i < itr->second.size(); i++) { 
                cout << "( " << itr->second[i].first << ", "
                     << itr->second[i].second << ") "; 
            } 

            cout << " have sum : " << itr->first << endl; 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    int A[] 
        = { 6, 4, 12, 10, 22, 54, 32, 42, 21, 11, 8, 2 }; 

    int n = sizeof(A) / sizeof(A[0]); 

    pairWithEqualSum(A, n); 

    return 0; 
}

```

## 爪哇

```

// Java program to print all pairs 
// with equal sum 
import java.util.*; 

class GFG { 
    static class pair { 
        int first, second; 
        public pair(int first, int second) 
        { 
            this.first = first; 
            this.second = second; 
        } 
    } 

    // Function to print all pairs 
    // with equal sum 
    static void pairWithEqualSum(int A[], int n) 
    { 

        Map<Integer, Vector<pair> > mp = new HashMap<>(); 

        // Insert all unique pairs and their 
        // corresponding sum in the map 
        for (int i = 0; i < n - 1; i++) { 
            for (int j = i + 1; j < n; j++) { 
                pair p = new pair(A[i], A[j]); 
                Vector<pair> pp = new Vector<pair>(); 
                if (mp.containsKey(A[i] + A[j])) 
                    pp.addAll(mp.get(A[i] + A[j])); 
                pp.add(p); 
                mp.put(A[i] + A[j], pp); 
            } 
        } 

        // Traverse the map mp, and for sum 
        // with more than one pair, print all pairs 
        // and the corresponding sum 
        for (Map.Entry<Integer, Vector<pair> > itr : 
             mp.entrySet()) { 
            if (itr.getValue().size() > 1) { 
                System.out.print("Pairs : "); 

                for (int i = 0; i < itr.getValue().size(); 
                     i++) { 
                    System.out.print( 
                        "( " + itr.getValue().get(i).first 
                        + ", "
                        + itr.getValue().get(i).second 
                        + ") "); 
                } 

                System.out.print( 
                    " have sum : " + itr.getKey() + "\n"); 
            } 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int A[] = { 6,  4,  12, 10, 22, 54, 
                    32, 42, 21, 11, 8,  2 }; 

        int n = A.length; 

        pairWithEqualSum(A, n); 
    } 
} 

// This code is contributed by Rajput-Ji

```

## Python3

```

# Python implementation of the 
# approach 

# Function to print all pairs 
# with equal sum 

def pairWithEqualSum(A, n): 
    mp = {} 

    # Insert all unique pairs and their 
    # corresponding sum in the map 

    for i in range(n): 
        for j in range(i+1, n): 
            if A[i]+A[j] in mp: 
                mp[A[i]+A[j]].append((A[i], A[j])) 
            else: 
                mp[A[i]+A[j]] = [(A[i], A[j])] 

    # Traverse the map mp, and for sum 
    # with more than one pair, print all pairs 
    # and the corresponding sum 

    for itr in mp: 
        if len(mp[itr]) > 1: 
            print("Pairs : ", end="") 
            for i in range(0, len(mp[itr])): 
                print("(", mp[itr][i][0], ",", 
                      mp[itr][i][1], ")", end=" ") 

            print("have sum :", itr) 

# Driver Code 
if __name__ == "__main__": 

    A = [6, 4, 12, 10, 22, 54, 
         32, 42, 21, 11, 8, 2] 
    n = len(A) 

    pairWithEqualSum(A, n) 

```

## C＃

```

// C# program to print all pairs 
// with equal sum 
using System; 
using System.Collections.Generic; 

class GFG { 
    class pair { 
        public int first, second; 
        public pair(int first, int second) 
        { 
            this.first = first; 
            this.second = second; 
        } 
    } 

    // Function to print all pairs 
    // with equal sum 
    static void pairWithEqualSum(int[] A, int n) 
    { 

        Dictionary<int, List<pair> > mp 
            = new Dictionary<int, List<pair> >(); 

        // Insert all unique pairs and their 
        // corresponding sum in the map 
        for (int i = 0; i < n - 1; i++) { 
            for (int j = i + 1; j < n; j++) { 
                pair p = new pair(A[i], A[j]); 
                List<pair> pp = new List<pair>(); 
                if (mp.ContainsKey(A[i] + A[j])) 
                    pp = AddAll(mp[A[i] + A[j]]); 
                pp.Add(p); 
                if (mp.ContainsKey(A[i] + A[j])) 
                    mp[A[i] + A[j]] = pp; 
                else
                    mp.Add(A[i] + A[j], pp); 
            } 
        } 

        // Traverse the map mp, and for sum 
        // with more than one pair, print all pairs 
        // and the corresponding sum 
        foreach(KeyValuePair<int, List<pair> > itr in mp) 
        { 
            if (itr.Value.Count > 1) { 
                Console.Write("Pairs : "); 

                for (int i = 0; i < itr.Value.Count; i++) { 
                    Console.Write( 
                        "( " + itr.Value[i].first + ", "
                        + itr.Value[i].second + ") "); 
                } 

                Console.Write(" have sum : " + itr.Key 
                              + "\n"); 
            } 
        } 
    } 
    static List<pair> AddAll(List<pair> list) 
    { 
        List<pair> l = new List<pair>(); 
        foreach(pair p in list) l.Add(p); 
        return l; 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        int[] A = { 6,  4,  12, 10, 22, 54, 
                    32, 42, 21, 11, 8,  2 }; 

        int n = A.Length; 

        pairWithEqualSum(A, n); 
    } 
} 

// This code is contributed by Rajput-Ji

```

**Output**

```
Pairs : ( 6, 4) ( 8, 2)  have sum : 10
Pairs : ( 4, 8) ( 10, 2)  have sum : 12
Pairs : ( 6, 8) ( 4, 10) ( 12, 2)  have sum : 14
Pairs : ( 6, 10) ( 4, 12)  have sum : 16
Pairs : ( 6, 12) ( 10, 8)  have sum : 18
Pairs : ( 12, 11) ( 21, 2)  have sum : 23
Pairs : ( 10, 22) ( 21, 11)  have sum : 32
Pairs : ( 12, 21) ( 22, 11)  have sum : 33
Pairs : ( 12, 22) ( 32, 2)  have sum : 34
Pairs : ( 22, 21) ( 32, 11)  have sum : 43
Pairs : ( 12, 32) ( 42, 2)  have sum : 44
Pairs : ( 32, 21) ( 42, 11)  have sum : 53
Pairs : ( 12, 42) ( 22, 32)  have sum : 54
Pairs : ( 10, 54) ( 22, 42)  have sum : 64

```

使用一个单一映射的上述方法的另一种实现。

## 爪哇

```

// Java program for the above approach 
import java.io.*; 
import java.util.HashMap; 
import java.util.Map; 

class GFG{ 

// Function to find pairs 
public void findPairs(int arr[]){ 

    Map<Integer, 
        Integer> map = new HashMap<Integer,  
                                   Integer>(); 

    int sum = 0, element = 0; 

    // Iterate from 0 to arr.length 
    for(int i = 0; i < arr.length; i++)  
    { 

      // Iterate from i+1 to arr.length 
      for(int j = i + 1; j < arr.length; j++)  
      { 
          sum = arr[i] + arr[j]; 

          // If sum is found in map 
          if(map.get(sum) != null)  
          { 

            // To find the first array 
            // element whose of the sum pair 
            element = map.get(sum); 

            // Print the output 
            System.out.println("Pairs:(" + arr[i] + 
                             "," + arr[j] + ") (" + 
                                    element + "," +  
                                  (sum - element) + 
                              ") have sum:" + sum); 
          }  
          else
          { 
            // Else put map[sum] = arr[i] 
            map.put(sum, arr[i]); 
          } 
      } 
    } 
} 

  // Driver Code 
  public static void main(String[] args)  
  { 
    int arr[] = {6, 4, 12, 10, 22, 54,  
                 32, 42, 21, 11, 8, 2}; 

    GFG obj = new GFG(); 

    // Function Call 
    obj.findPairs(arr); 
  } 
} 

```

**Output**

```
Pairs:(4,12) (6,10)  have sum:16
Pairs:(4,10) (6,8)  have sum:14
Pairs:(12,2) (6,8)  have sum:14
Pairs:(10,8) (6,12)  have sum:18
Pairs:(10,2) (4,8)  have sum:12
Pairs:(22,32) (12,42)  have sum:54
Pairs:(22,42) (10,54)  have sum:64
Pairs:(22,11) (12,21)  have sum:33
Pairs:(32,11) (22,21)  have sum:43
Pairs:(32,2) (12,22)  have sum:34
Pairs:(42,11) (32,21)  have sum:53
Pairs:(42,2) (12,32)  have sum:44
Pairs:(21,11) (10,22)  have sum:32
Pairs:(21,2) (12,11)  have sum:23
Pairs:(8,2) (6,4)  have sum:10

```

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。