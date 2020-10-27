# 序列

中第二重复的单词

给定一个字符串序列，任务是找出给定序列中倒数第二个（或频繁出现）的字符串（考虑到两个单词都不是倒数第二个，总是会有一个单词）。

例子：

```
Input : {"aaa", "bbb", "ccc", "bbb", 
         "aaa", "aaa"}
Output : bbb

Input : {"geeks", "for", "geeks", "for", 
          "geeks", "aaa"}
Output : for

```

在询问：亚马逊

1.  将所有单词存储在地图中，将单词的出现作为关键字并将其出现作为值。
2.  在地图上找到第二个最大值。
3.  再次遍历该映射，并返回出现值等于第二个最大值的单词。

## C ++

```

// C++ program to find out the second 
// most repeated word 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the word 
string secMostRepeated(vector<string> seq) 
{ 

    // Store all the words with its occurrence 
    unordered_map<string, int> occ; 
    for (int i = 0; i < seq.size(); i++) 
        occ[seq[i]]++; 

    // find the second largest occurrence 
    int first_max = INT_MIN, sec_max = INT_MIN; 
    for (auto it = occ.begin(); it != occ.end(); it++) { 
        if (it->second > first_max) { 
            sec_max = first_max; 
            first_max = it->second; 
        } 

        else if (it->second > sec_max &&  
                 it->second != first_max) 
            sec_max = it->second; 
    } 

    // Return string with occurrence equals 
    // to sec_max 
    for (auto it = occ.begin(); it != occ.end(); it++) 
        if (it->second == sec_max) 
            return it->first; 
} 

// Driver program 
int main() 
{ 
    vector<string> seq = { "ccc", "aaa", "ccc", 
                          "ddd", "aaa", "aaa" }; 
    cout << secMostRepeated(seq); 
    return 0; 
} 

```

## 爪哇

```

// Java program to find out the second 
// most repeated word 

import java.util.*; 

class GFG  
{ 
    // Method to find the word 
    static String secMostRepeated(Vector<String> seq) 
    { 
        // Store all the words with its occurrence 
        HashMap<String, Integer> occ = new HashMap<String,Integer>(seq.size()){ 
            @Override
            public Integer get(Object key) { 
                 return containsKey(key) ? super.get(key) : 0; 
            } 
        }; 

        for (int i = 0; i < seq.size(); i++) 
            occ.put(seq.get(i), occ.get(seq.get(i))+1); 

        // find the second largest occurrence 
       int first_max = Integer.MIN_VALUE, sec_max = Integer.MIN_VALUE; 

       Iterator<Map.Entry<String, Integer>> itr = occ.entrySet().iterator(); 
       while (itr.hasNext())  
       { 
           Map.Entry<String, Integer> entry = itr.next(); 
           int v = entry.getValue(); 
           if( v > first_max) { 
                sec_max = first_max; 
                first_max = v; 
            } 

            else if (v > sec_max &&  
                     v != first_max) 
                sec_max = v; 
       } 

       // Return string with occurrence equals 
        // to sec_max 
       itr = occ.entrySet().iterator(); 
       while (itr.hasNext())  
       { 
           Map.Entry<String, Integer> entry = itr.next(); 
           int v = entry.getValue(); 
           if (v == sec_max) 
                return entry.getKey(); 
       } 

       return null; 
    } 

    // Driver method 
    public static void main(String[] args)  
    { 
        String arr[] = { "ccc", "aaa", "ccc", 
                         "ddd", "aaa", "aaa" }; 
        List<String> seq =  Arrays.asList(arr); 

        System.out.println(secMostRepeated(new Vector<>(seq))); 
    }     
} 
// This program is contributed by Gaurav Miglani 

```

## C＃

```

// C# program to find out the second 
// most repeated word 
using System; 
using System.Collections.Generic; 

class GFG  
{ 
    // Method to find the word 
    static String secMostRepeated(List<String> seq) 
    { 
        // Store all the words with its occurrence 
        Dictionary<String, int> occ =  
        new Dictionary<String, int>(); 

        for (int i = 0; i < seq.Count; i++) 
            if(occ.ContainsKey(seq[i])) 
                occ[seq[i]] = occ[seq[i]] + 1; 
            else
                occ.Add(seq[i], 1); 

        // find the second largest occurrence 
        int first_max = int.MinValue,  
            sec_max = int.MinValue; 

        foreach(KeyValuePair<String, int> entry in occ) 
        { 
            int v = entry.Value; 
            if( v > first_max)  
            { 
                sec_max = first_max; 
                first_max = v; 
            } 

            else if (v > sec_max &&  
                    v != first_max) 
                sec_max = v; 
        } 

        // Return string with occurrence equals 
        // to sec_max 
        foreach(KeyValuePair<String, int> entry in occ) 
        { 
            int v = entry.Value; 
            if (v == sec_max) 
                return entry.Key; 
        } 

        return null; 
    } 

    // Driver method 
    public static void Main(String[] args)  
    { 
        String []arr = { "ccc", "aaa", "ccc", 
                        "ddd", "aaa", "aaa" }; 
        List<String> seq = new List<String>(arr); 

        Console.WriteLine(secMostRepeated(seq)); 
    }  
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
ccc

```

**参考：**
[https://www.careercup.com/question?id=5748104113422336](https://www.careercup.com/question?id=5748104113422336)

本文由 **[Sahil Chhabra](https://www.facebook.com/sahil.chhabra.965)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。