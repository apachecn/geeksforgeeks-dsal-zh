# InfyTQ 2019:从括号不平衡的地方找位置

> 原文:[https://www . geesforgeks . org/infytq-2019-从括号不平衡的地方找到位置/](https://www.geeksforgeeks.org/infytq-2019-find-the-position-from-where-the-parenthesis-is-not-balanced/)

给定一个由[ **"("，")"、" { "、" } "、"["、"]"** ]的括号组成的字符串**。
如果**字符串**完全平衡，返回 0，否则返回发现嵌套错误的索引(从 1 开始)。
**示例:**** 

> **输入:**str = {[()]}[]"
> **输出:** 0
> **输入:**str = "[{](} "
> **输出:** 3
> **输入:** str = "}[{}]"
> **输出:** 1
> **输入:**str = {([]){ "
> **输出:【t2t**

**进场:**

1.  首先，我们正在创建 lst1 和 lst2，它们将分别有左括号和右括号
2.  现在我们将创建另一个列表 lst，它将作为 [**堆栈**](https://www.geeksforgeeks.org/stack-data-structure/) 工作，这意味着如果字符串中出现任何结束括号，那么 lst 中出现的相应开始括号将被删除
3.  如果字符串中出现任何结束括号，并且 lst 中没有相应的开始括号，那么这将是一个错误的索引，我们将返回它
4.  如果我们在遍历时到达字符串的末尾，并且 lst 的大小不等于 0，我们将返回 len(String)+1

以下是上述方法的实施

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int main()
{

    // Defining the string
    string String = "{[()]}[]";

    // Storing opening braces in list lst1
    vector<char> lst1 ={'{', '(', '['};

    // Storing closing braces in list lst2
    vector<char> lst2 ={'}', ')', ']'};

    // Creating an empty list lst
    vector<char> lst;

    int k;

    // Creating dictionary to map
    // closing braces to opening ones
    map<char,char> Dict;
    Dict.insert(pair<int, int>(')', '('));
    Dict.insert(pair<int, int>('}', '{'));
    Dict.insert(pair<int, int>(']', '['));

    int a = 0, b = 0, c = 0;

    // If first position of string contain
    // any closing braces return 1
    if(count(lst2.begin(), lst2.end(), String[0]))
    {
        cout << 1 << endl;
    }
    else
    {
        // If characters of string are opening
        // braces then append them in a list
        for(int i = 0; i < String.size(); i++)
        {
            if(count(lst1.begin(), lst1.end(), String[i]))
            {
                lst.push_back(String[i]);
                k = i + 2;
            }
            else
            {
                // When size of list is 0 and new closing
                // braces is encountered then print its
                // index starting from 1       
                if(lst.size()== 0 && (count(lst2.begin(), lst2.end(), String[i])))
                {
                    cout << (i + 1) << endl;
                    c = 1;
                    break;
                }
                else
                {
                    // As we encounter closing braces we map
                    // them with theircorresponding opening
                    // braces using dictionary and check
                    // if it is same as last opened braces
                    //(last element in list) if yes then we
                    // delete that element from list
                    if(Dict[String[i]]== lst[lst.size()-1])
                    {
                        lst.pop_back();
                    }
                    else
                    {
                        // Otherwise we return the index
                        // (starting from 1) at which
                        // nesting is found wrong
                        break;
                        cout << (i + 1) << endl;
                        a = 1;
                    }
                }
             }
        }

        // At end if the list is empty it
        // means the string is perfectly nested            
        if(lst.size() == 0 && c == 0)
        {
            cout << 0 << endl;
            b = 1;
        }

        if(a == 0 && b == 0 && c == 0)
        {
            cout << k << endl;
        }
    }

    return 0;
}

// This code is contributed by decode2207.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
public class Main
{
    public static void main(String[] args)
    {

        // Defining the string
        String string = "{[()]}[]";

        // Storing opening braces in list lst1
        char[] lst1 = {'{', '(', '['};

        // Storing closing braces in list lst2
        char[] lst2 = {'}', ')', ']'};

        // Creating an empty list lst
        Vector<Character> lst = new Vector<Character>();

        // Creating dictionary to map
        // closing braces to opening ones
        HashMap<Character, Character> Dict = new HashMap<>();
        Dict.put(')', '(');
        Dict.put('}', '{');
        Dict.put(']', '[');

        int a = 0, b = 0, c = 0;

        // If first position of string contain
        // any closing braces return 1
        if(Arrays.asList(lst2).contains(string.charAt(0)))
        {
            System.out.println(1);
        }
        else
        {
            int k = 0;

            // If characters of string are opening
            // braces then append them in a list
            for(int i = 0; i < string.length(); i++)
            {
                if(Arrays.asList(lst1).contains(string.charAt(i)))
                {
                    lst.add(string.charAt(i));
                    k = i + 2;
                }
                else
                {
                    // When size of list is 0 and new closing
                    // braces is encountered then print its
                    // index starting from 1       
                    if(lst.size()== 0 && Arrays.asList(lst2).contains(string.charAt(i)))
                    {
                        System.out.println((i + 1));
                        c = 1;
                        break;
                    }
                    else
                    {
                        // As we encounter closing braces we map
                        // them with theircorresponding opening
                        // braces using dictionary and check
                        // if it is same as last opened braces
                        //(last element in list) if yes then we
                        // delete that element from list
                        if(lst.size() > 0 && Dict.get(string.charAt(i))== lst.get(lst.size() - 1))
                        {
                            lst.remove(lst.size() - 1);
                        }
                        else
                        {
                            // Otherwise we return the index
                            // (starting from 1) at which
                            // nesting is found wrong
                            a = 1;
                            break;
                        }
                    }
                 }
            }

            // At end if the list is empty it
            // means the string is perfectly nested            
            if(lst.size() == 0 && c == 0)
            {
                System.out.println(0);
                b = 1;
            }

            if(a == 0 && b == 0 && c == 0)
            {
                System.out.println(k);
            }
        }
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Write Python3 code here

# Defining the string
string = "{[()]}[]"

# Storing opening braces in list lst1
lst1 =['{', '(', '[']

# Storing closing braces in list lst2
lst2 =['}', ')', ']']

# Creating an empty list lst
lst =[]

# Creating dictionary to map
# closing braces to opening ones
Dict ={ ')':'(', '}':'{', ']':'['}

a = b = c = 0

# If first position of string contain
# any closing braces return 1
if string[0]  in lst2:
    print(1)

else:
    # If characters of string are opening
    # braces then append them in a list
    for i in range(0, len(string)):
        if string[i] in lst1:
            lst.append(string[i])
            k = i + 2
        else:
            # When size of list is 0 and new closing
            # braces is encountered then print its
            # index starting from 1         
            if len(lst)== 0 and (string[i] in lst2):
                print(i + 1)
                c = 1
                break
            else:   
                # As we encounter closing braces we map
                # them with theircorresponding opening
                # braces using dictionary and check
                # if it is same as last opened braces
                #(last element in list) if yes then we
                # delete that element from list
                if Dict[string[i]]== lst[len(lst)-1]:
                    lst.pop()
                else:
                    # Otherwise we return the index
                    # (starting from 1) at which
                    # nesting is found wrong   
                    print(i + 1)
                    a = 1
                    break

    # At end if the list is empty it
    # means the string is perfectly nested              
    if len(lst)== 0 and c == 0:
        print(0)
        b = 1

    if a == 0 and b == 0 and c == 0:
        print(k)
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{
  static void Main()
  {

    // Defining the string
    string String = "{[()]}[]";

    // Storing opening braces in list lst1
    char[] lst1 = {'{', '(', '['};

    // Storing closing braces in list lst2
    char[] lst2 = {'}', ')', ']'};

    // Creating an empty list lst
    List<char> lst = new List<char>();

    // Creating dictionary to map
    // closing braces to opening ones
    Dictionary<char, char> Dict = new Dictionary<char, char>();
    Dict[')'] = '(';
    Dict['}'] = '{';
    Dict[']'] = '[';

    int a = 0, b = 0, c = 0;

    // If first position of string contain
    // any closing braces return 1
    if(Array.Exists(lst2, element => element == String[0]))
    {
        Console.WriteLine(1);
    }
    else
    {
        int k = 0;

        // If characters of string are opening
        // braces then append them in a list
        for(int i = 0; i < String.Length; i++)
        {
            if(Array.Exists(lst1, element => element == String[i]))
            {
                lst.Add(String[i]);
                k = i + 2;
            }
            else
            {
                // When size of list is 0 and new closing
                // braces is encountered then print its
                // index starting from 1      
                if(lst.Count== 0 && Array.Exists(lst2, element => element == String[i]))
                {
                    Console.WriteLine((i + 1));
                    c = 1;
                    break;
                }
                else
                {
                    // As we encounter closing braces we map
                    // them with theircorresponding opening
                    // braces using dictionary and check
                    // if it is same as last opened braces
                    //(last element in list) if yes then we
                    // delete that element from list
                    if(lst.Count > 0 && Dict[String[i]]== lst[lst.Count - 1])
                    {
                        lst.RemoveAt(lst.Count - 1);
                    }
                    else
                    {
                        // Otherwise we return the index
                        // (starting from 1) at which
                        // nesting is found wrong
                        a = 1;
                        break;
                    }
                }
             }
        }

        // At end if the list is empty it
        // means the string is perfectly nested           
        if(lst.Count == 0 && c == 0)
        {
            Console.WriteLine(0);
            b = 1;
        }

        if(a == 0 && b == 0 && c == 0)
        {
            Console.WriteLine(k);
        }
    }
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Defining the string
    let string = "{[()]}[]";

    // Storing opening braces in list lst1
    let lst1 =['{', '(', '['];

    // Storing closing braces in list lst2
    let lst2 =['}', ')', ']'];

    // Creating an empty list lst
    let lst =[];

    // Creating dictionary to map
    // closing braces to opening ones
    let Dict ={ ')':'(', '}':'{', ']':'['}

    let a = 0, b = 0, c = 0;

    // If first position of string contain
    // any closing braces return 1
    if(string[0]  in lst2)
    {
        document.write(1 + "</br>");
    }
    else
    {
        // If characters of string are opening
        // braces then append them in a list
        for(let i = 0; i < string.length; i++)
        {
            if(string[i] in lst1)
            {
                lst.push(string[i]);
                k = i + 2;
            }
            else
            {
                // When size of list is 0 and new closing
                // braces is encountered then print its
                // index starting from 1        
                if(lst.lengt== 0 && (string[i] in lst2))
                {
                    document.write((i + 1) + "</br>");
                    c = 1;
                    break;
                }
                else
                {
                    // As we encounter closing braces we map
                    // them with theircorresponding opening
                    // braces using dictionary and check
                    // if it is same as last opened braces
                    //(last element in list) if yes then we
                    // delete that element from list
                    if(Dict[string[i]]== lst[lst.length-1])
                    {
                        lst.pop();
                    }
                    else
                    {
                        // Otherwise we return the index
                        // (starting from 1) at which
                        // nesting is found wrong 
                        break;
                        document.write((i + 1) + "</br>");
                        a = 1;
                    }
                }
             }
        }

        // At end if the list is empty it
        // means the string is perfectly nested             
        if(lst.length == 0 && c == 0)
        {
            document.write(0 + "</br>");
            b = 1;
        }

        if(a == 0 && b == 0 && c == 0)
        {
            document.write(k + "</br>");
        }
    }

    // This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
0
```