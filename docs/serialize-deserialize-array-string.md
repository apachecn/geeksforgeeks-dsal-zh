# 序列化和反序列化字符串数组

> 原文:[https://www . geeksforgeeks . org/serialize-反序列化-array-string/](https://www.geeksforgeeks.org/serialize-deserialize-array-string/)

我们给出了一个字符串数组，我们必须序列化字符串数组并反序列化序列化字符串。
**例:**

```
Input :  "geeks", "are", "awesome"
Output : Serialized String : 5~geeks3~are7~awesome
         Deserialized String : geeks are awesome

Input :  "hello", "guys", "whats", "up!!!"
Output : Serialized String : 5~hello4~guys5~whats5~up!!!
         Deserialized String : hello guys whats up!!!

```

**序列化**:扫描一个字符串中的每个元素，计算它的长度，并附加一个字符串和一个元素分隔符或分隔符(那个分隔符不应该出现在字符串中)。我们附加字符串的长度，以便知道每个元素的长度。

**反序列化函数:**找到 deliminator 的位置，然后从位置+ 1 到字长，我们把它作为单个元素存储在数组中。

```
// CPP program to serialize and
// deserialize the array of string

#include<iostream>

using namespace std;

// Function to serialized the array of string
string serialize(string str[], int ln)
{
    string temp = "";
    for (int i=0; i<ln; i++)
    {
        int ln = str[i].length();
        temp.push_back('0' + ln);
        temp = temp + "~" + str[i];
    }
    return temp;
}

// Function to deserialize the string
void deserialized(string str, string deserialize[], int ln)
{
    int len, pos=0;
    string temp = "";
    int i = 0;
    while(pos>-1)
    {
        pos = str.find("~", pos+1);
        if(pos>0)
        {
            len = str[pos-1] - 48;
            temp.append(str, pos+1, len);
            deserialize[i++] = temp;
            temp = "";
        }
    }
}

// Driver function
int main()
{
    string str[] = {"geeks", "are", "awesome"};

    int ln = sizeof(str)/sizeof(str[0]);
    string serializedstr = serialize(str, ln);

    cout << "Serialized String : " << serializedstr <<endl;

    string deserialize[ln];
    deserialized(serializedstr,deserialize,ln);

    cout << "Deserialized String : ";
    for(int i=0; i<ln; i++)
        cout << deserialize[i] << " ";

    return 0;
}
```

输出:

```
Serialized String : 5~geeks3~are7~awesome
Deserialized String : geeks are awesome

```

**参考文献:**
1。[https://stackoverflow . com/questions/13271503/Java 中的数组-字符串-字符串-返回转换](https://stackoverflow.com/questions/13271503/converting-array-string-to-string-and-back-in-java)
2。[https://www.careercup.com/question?id=5684077627703296](https://www.careercup.com/question?id=5684077627703296)

本文由**里沙布·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。