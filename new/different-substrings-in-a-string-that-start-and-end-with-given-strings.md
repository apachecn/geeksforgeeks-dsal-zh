# 字符串中以给定字符串开头和结尾的不同子字符串

给定一个字符串 s 和其他两个字符串的开头和结尾，请找到该字符串中以给定的 begin 和 end 字符串开头和结尾的不同子字符串的数量。

**示例：**

```
Input : s = "geeksforgeeks"
        begin = "geeks"
        end = "for"
Output : 1

Input : s = "vishakha"
        begin = "h"
        end = "a"
Output : 2
Two different sub-strings are "ha" and "hakha".

```

**方法：**查找出现的所有字符串开头和结尾。 将每个字符串的索引存储在两个不同的数组中。 之后遍历整个字符串，并在每次迭代中向已看到的子字符串添加一个符号，然后将新字符串映射到一些非负整数。 由于字符串的开头和结尾以及长度相等的不同字符串被映射为不同的数字（并且相等的字符串被相等地映射），因此只需计算一定长度的必要子字符串的数目即可。

## C ++

```

// Cpp program to find number of 
// different sub stings 
#include <bits/stdc++.h> 
using namespace std; 

// function to return number of different  
// sub-strings 
int numberOfDifferentSubstrings(string s, string a,  
                                          string b) 
{ 
    // initially our answer is zero. 
    int ans = 0; 

    // find the length of given strings 
    int ls = s.size(), la = a.size(), lb = b.size(); 

    // currently make array and initially put zero. 
    int x[ls] = { 0 }, y[ls] = { 0 }; 

    // find occurrence of "a" and "b" in string "s" 
    for (int i = 0; i < ls; i++) { 
        if (s.substr(i, la) == a) 
            x[i] = 1; 
        if (s.substr(i, lb) == b) 
            y[i] = 1; 
    } 

    // We use a hash to make sure that same  
    // substring is not counted twice. 
    unordered_set<string> hash;     

    // go through all the positions to find  
    // occurrence of "a" first. 
    string curr_substr = ""; 
    for (int i = 0; i < ls; i++) { 

        // if we found occurrence of "a". 
        if (x[i]) { 

            // then go through all the positions 
            // to find occurrence of "b". 
            for (int j = i; j < ls; j++) { 

                // if we do found "b" at index 
                // j then add it to already 
                // existed substring. 
                if (!y[j]) 
                    curr_substr += s[j]; 

                // if we found occurrence of "b". 
                if (y[j]) { 

                    // now add string "b" to  
                    // already existed substing. 
                    curr_substr += s.substr(j, lb); 

                    // If current substring is not 
                    // included already. 
                    if (hash.find(curr_substr) == hash.end()) 
                        ans++; 

                    // put any non negative  
                    // integer to make this 
                    // string as already  
                    // existed. 
                    hash.insert(curr_substr); 
                } 
            } 

            // make substring null. 
            curr_substr = ""; 
        } 
    } 

    // return answer. 
    return ans; 
} 

// Driver program for above function. 
int main() 
{ 
    string s = "codecppforfood"; 
    string begin = "c"; 
    string end = "d"; 
    cout << numberOfDifferentSubstrings(s, begin, end)  
        << endl; 
    return 0; 
} 

```

## 爪哇

```

// Java program to find number of  
// different sub stings 
import java.util.HashSet; 

class GFG 
{ 

// function to return number of  
// different sub-strings 
static int numberOfDifferentSubstrings(String s,  
                                       char a, char b)  
{ 

    // initially our answer is zero. 
    int ans = 0; 

    // find the length of given strings 
    int ls = s.length(); 

    // currently make array and  
    // initially put zero. 
    int[] x = new int[ls]; 
    int[] y = new int[ls]; 

    // find occurrence of "a" and "b"  
    // in string "s" 
    for (int i = 0; i < ls; i++) 
    { 
        if (s.charAt(i) == a) 
            x[i] = 1; 
        if (s.charAt(i) == b) 
            y[i] = 1; 
    } 

    // We use a hash to make sure that same 
    // substring is not counted twice. 
    HashSet<String> hash = new HashSet<>(); 

    // go through all the positions to find 
    // occurrence of "a" first. 
    String curr_substr = ""; 
    for (int i = 0; i < ls; i++)  
    { 

        // if we found occurrence of "a". 
        if (x[i] != 0)  
        { 

            // then go through all the positions 
            // to find occurrence of "b". 
            for (int j = i; j < ls; j++)  
            { 

                // if we do found "b" at index 
                // j then add it to already 
                // existed substring. 
                if (y[j] == 0) 
                    curr_substr += s.charAt(i); 

                // if we found occurrence of "b". 
                if (y[j] != 0)  
                { 

                    // now add string "b" to 
                    // already existed substing. 
                    curr_substr += s.charAt(j); 

                    // If current substring is not 
                    // included already. 
                    if (!hash.contains(curr_substr)) 
                        ans++; 

                    // put any non negative 
                    // integer to make this 
                    // string as already 
                    // existed. 
                    hash.add(curr_substr); 
                } 
            } 

            // make substring null. 
            curr_substr = ""; 
        } 
    } 

    // return answer. 
    return ans; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    String s = "codecppforfood"; 
    char begin = 'c'; 
    char end = 'd'; 
    System.out.println( 
           numberOfDifferentSubstrings(s, begin, end)); 
} 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```

# Python 3 program to find number of 
# different sub stings 

# function to return number of different  
# sub-strings 
def numberOfDifferentSubstrings(s, a, b): 

    # initially our answer is zero. 
    ans = 0

    # find the length of given strings 
    ls = len(s) 
    la = len(a) 
    lb = len(b) 

    # currently make array and initially 
    # put zero. 
    x = [0] * ls 
    y = [0] * ls 

    # find occurrence of "a" and "b" in string "s" 
    for i in range(ls): 

        if (s[i: la + i] == a): 
            x[i] = 1
        if (s[i: lb + i] == b): 
            y[i] = 1

    # We use a hash to make sure that same  
    # substring is not counted twice. 
    hash = []  

    # go through all the positions to find  
    # occurrence of "a" first. 
    curr_substr = "" 
    for i in range(ls): 

        # if we found occurrence of "a". 
        if (x[i]): 

            # then go through all the positions 
            # to find occurrence of "b". 
            for j in range( i, ls): 

                # if we do found "b" at index 
                # j then add it to already 
                # existed substring. 
                if (not y[j]): 
                    curr_substr += s[j] 

                # if we found occurrence of "b". 
                if (y[j]): 

                    # now add string "b" to  
                    # already existed substing. 

                    curr_substr += s[j: lb + j] 

                    # If current substring is not 
                    # included already. 
                    if curr_substr not in hash: 
                        ans += 1

                    # put any non negative integer  
                    # to make this string as already  
                    # existed. 
                    hash.append(curr_substr) 

            # make substring null. 
            curr_substr = "" 

    # return answer. 
    return ans 

# Driver Code 
if __name__ == "__main__": 

    s = "codecppforfood"
    begin = "c"
    end = "d"
    print(numberOfDifferentSubstrings(s, begin, end)) 

# This code is contributed by ita_c 

```

## C＃

```

// C# program to find number of  
// different sub stings 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

// function to return number of  
// different sub-strings 
static int numberOfDifferentSubstrings(String s,  
                                    char a, char b)  
{ 

    // initially our answer is zero. 
    int ans = 0; 

    // find the length of given strings 
    int ls = s.Length; 

    // currently make array and  
    // initially put zero. 
    int[] x = new int[ls]; 
    int[] y = new int[ls]; 

    // find occurrence of "a" and "b"  
    // in string "s" 
    for (int i = 0; i < ls; i++) 
    { 
        if (s[i] == a) 
            x[i] = 1; 
        if (s[i] == b) 
            y[i] = 1; 
    } 

    // We use a hash to make sure that same 
    // substring is not counted twice. 
    HashSet<String> hash = new HashSet<String>(); 

    // go through all the positions to find 
    // occurrence of "a" first. 
    String curr_substr = ""; 
    for (int i = 0; i < ls; i++)  
    { 

        // if we found occurrence of "a". 
        if (x[i] != 0)  
        { 

            // then go through all the positions 
            // to find occurrence of "b". 
            for (int j = i; j < ls; j++)  
            { 

                // if we do found "b" at index 
                // j then add it to already 
                // existed substring. 
                if (y[j] == 0) 
                    curr_substr += s[i]; 

                // if we found occurrence of "b". 
                if (y[j] != 0)  
                { 

                    // now add string "b" to 
                    // already existed substing. 
                    curr_substr += s[j]; 

                    // If current substring is not 
                    // included already. 
                    if (!hash.Contains(curr_substr)) 
                        ans++; 

                    // put any non negative 
                    // integer to make this 
                    // string as already 
                    // existed. 
                    hash.Add(curr_substr); 
                } 
            } 

            // make substring null. 
            curr_substr = ""; 
        } 
    } 

    // return answer. 
    return ans; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    String s = "codecppforfood"; 
    char begin = 'c'; 
    char end = 'd'; 
    Console.WriteLine( 
        numberOfDifferentSubstrings(s, begin, end)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
3

```

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。