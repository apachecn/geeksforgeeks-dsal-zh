# 查找以投票代表候选人姓名的选举的获胜者

在选举中给出一系列候选人姓名。 数组中的候选人名称代表对候选人的投票。 打印获得 Max 投票的候选人姓名。 如果有平局，则按字典顺序打印较小的名称。

例子：

```
Input :  votes[] = {"john", "johnny", "jackie", 
                    "johnny", "john", "jackie", 
                    "jamie", "jamie", "john",
                    "johnny", "jamie", "johnny", 
                    "john"};
Output : John
We have four Candidates with name as 'John', 
'Johnny', 'jamie', 'jackie'. The candidates
John and Johny get maximum votes. Since John
is alphabetically smaller, we print it.

```

**简单解决方案**是运行两个循环并计算每个单词的出现次数。 该解决方案的时间复杂度为 O（n * n * MAX_WORD_LEN）。

**有效解决方案**是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。 我们将所有选票插入哈希图中，并跟踪不同名称的计数。 最后，我们遍历地图并打印出最高票数的人。

## CPP

```

// C++++ program to find winner in an election. 
#include "bits/stdc++.h" 
using namespace std; 

    /* We have four Candidates with name as 'John', 
      'Johnny', 'jamie', 'jackie'. 
       The votes in String array are as per the 
       votes casted. Print the name of candidates 
       received Max vote. */
    void findWinner(vector<string>& votes) 
    { 

        // Insert all votes in a hashmap 
        map<string,int> mapObj ; 
        for (auto& str : votes) 
        { 
            mapObj[str]++; 
        } 

        // Traverse through map to find the candidate 
        // with maximum votes. 
        int maxValueInMap = 0; 
        string winner; 
        for (auto& entry : mapObj) 
        { 
            string key  = entry.first; 
            int val = entry.second; 
            if (val > maxValueInMap) 
            { 
                maxValueInMap = val; 
                winner = key; 
            } 

            // If there is a tie, pick lexicographically 
            // smaller. 
            else if (val == maxValueInMap && 
                winner>key) 
                winner = key; 
        } 
        cout << winner << endl; 
    } 

    // Driver code 
    int main() 
    { 
       vector<string> votes = { "john", "johnny", "jackie", 
                         "johnny", "john", "jackie", 
                         "jamie", "jamie", "john", 
                         "johnny", "jamie", "johnny", 
                         "john" }; 

       findWinner(votes); 
       return 0; 
    } 

```

## 爪哇

```

// Java program to find winner in an election. 
import java.util.*; 

public class ElectoralVotingBallot 
{ 
    /* We have four Candidates with name as 'John', 
      'Johnny', 'jamie', 'jackie'. 
       The votes in String array are as per the 
       votes casted. Print the name of candidates 
       received Max vote. */
    public static void findWinner(String votes[]) 
    { 
        // Insert all votes in a hashmap 
        Map<String,Integer> map = 
                    new HashMap<String, Integer>(); 
        for (String str : votes) 
        { 
            if (map.keySet().contains(str)) 
                map.put(str, map.get(str) + 1); 
            else
                map.put(str, 1); 
        } 

        // Traverse through map to find the candidate 
        // with maximum votes. 
        int maxValueInMap = 0; 
        String winner = ""; 
        for (Map.Entry<String,Integer> entry : map.entrySet()) 
        { 
            String key  = entry.getKey(); 
            Integer val = entry.getValue(); 
            if (val > maxValueInMap) 
            { 
                maxValueInMap = val; 
                winner = key; 
            } 

            // If there is a tie, pick lexicographically 
            // smaller.  
            else if (val == maxValueInMap && 
                winner.compareTo(key) > 0) 
                winner = key; 
        } 
        System.out.println(winner); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
       String[] votes = { "john", "johnny", "jackie", 
                         "johnny", "john", "jackie", 
                         "jamie", "jamie", "john", 
                         "johnny", "jamie", "johnny", 
                         "john" }; 

       findWinner(votes); 
    } 
} 

```

## C＃

```

// C# program to find winner in an election. 
using System; 
using System.Collections.Generic; 

public class ElectoralVotingBallot 
{ 
    /* We have four Candidates with name as 'John', 
    'Johnny', 'jamie', 'jackie'. 
    The votes in String array are as per the 
    votes casted. Print the name of candidates 
    received Max vote. */
    public static void findWinner(String []votes) 
    { 
        // Insert all votes in a hashmap 
        Dictionary<String,int> map = 
                    new Dictionary<String, int>(); 
        foreach (String str in votes) 
        { 
            if (map.ContainsKey(str)) 
                map[str] = map[str] + 1; 
            else
                map.Add(str, 1); 
        } 

        // Traverse through map to find the candidate 
        // with maximum votes. 
        int maxValueInMap = 0; 
        String winner = ""; 
        foreach(KeyValuePair<String, int> entry in map) 
        { 
            String key = entry.Key; 
            int val = entry.Value; 
            if (val > maxValueInMap) 
            { 
                maxValueInMap = val; 
                winner = key; 
            } 

            // If there is a tie, pick lexicographically 
            // smaller.  
            else if (val == maxValueInMap && 
                winner.CompareTo(key) > 0) 
                winner = key; 
        } 
        Console.WriteLine(winner); 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        String[] votes = { "john", "johnny", "jackie", 
                            "johnny", "john", "jackie", 
                            "jamie", "jamie", "john", 
                            "johnny", "jamie", "johnny", 
                            "john" }; 

        findWinner(votes); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
John

```

另一个有效的解决方案是使用 [Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 。 请参阅字符串数组中最常用的词。

本文由 **Ishfaq Ramzan Nagoo** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。