# 简化目录路径(像 Unix 一样)

> 原文:[https://www . geesforgeks . org/simplify-directory-path-UNIX-like/](https://www.geeksforgeeks.org/simplify-directory-path-unix-like/)

给定一个文件的绝对路径(Unix 风格)，简化它。请注意，绝对路径总是以“/”(根目录)开头，路径中的一个点代表当前目录，双点代表父目录。
示例:

```
"/a/./"   --> means stay at the current directory 'a'
"/a/b/.." --> means jump to the parent directory
              from 'b' to 'a'
"////"    --> consecutive multiple '/' are a  valid  
              path, they are equivalent to single "/".

Input : /home/
Output : /home

Input : /a/./b/../../c/
Output : /c

Input : /a/..
Output:/

Input : /a/../
Output : /

Input : /../../../../../a
Output : /a

Input : /a/./b/./c/./d/
Output : /a/b/c/d

Input : /a/../.././../../.
Output:/

Input : /a//b//c//////d
Output : /a/b/c/d
```

**注意:**给定的输入将始终具有有效的绝对路径。

**方法 1:**
通过查看示例，我们可以看到上面的简化过程就像一个**堆栈**一样。每当我们遇到任何文件名时，我们只需将其推入堆栈。当我们遇到。我们什么都不做。当我们找到“..”在我们的路径中，我们只需弹出最上面的元素，因为我们必须跳回父目录。
当我们看到多个“////”时，我们只是忽略它们，因为它们相当于一个单独的“/”。迭代整个字符串后，堆栈中剩余的元素就是我们简化的绝对路径。我们必须创建另一个堆栈来反转存储在原始堆栈中的元素，然后将结果存储在字符串中。

## C++

```
/* C++ program to simplify a Unix
   styled absolute path of a file */
#include <bits/stdc++.h>
using namespace std;

// function to simplify a Unix - styled
// absolute path
string simplify(string A)
{
    // stack to store the file's names.
    stack<string> st;

    // temporary string which stores the extracted
    // directory name or commands("." / "..")
    // Eg. "/a/b/../."
    // dir will contain "a", "b", "..", ".";
    string dir;

    // contains resultant simplifies string.
    string res;

    // every string starts from root directory.
    res.append("/");

    // stores length of input string.
    int len_A = A.length();

    for (int i = 0; i < len_A; i++) {

        // we will clear the temporary string
        // every time to accommodate new directory
        // name or command.
        dir.clear();

        // skip all the multiple '/' Eg. "/////""
        while (A[i] == '/')
            i++;

        // stores directory's name("a", "b" etc.)
        // or commands("."/"..") into dir
        while (i < len_A && A[i] != '/') {
            dir.push_back(A[i]);
            i++;
        }

        // if dir has ".." just pop the topmost
        // element if the stack is not empty
        // otherwise ignore.
        if (dir.compare("..") == 0) {
            if (!st.empty())
                st.pop();           
        }

        // if dir has "." then simply continue
        // with the process.
        else if (dir.compare(".") == 0)
            continue;

        // pushes if it encounters directory's
        // name("a", "b").
        else if (dir.length() != 0)
            st.push(dir);       
    }

    // a temporary stack  (st1) which will contain
    // the reverse of original stack(st).
    stack<string> st1;
    while (!st.empty()) {
        st1.push(st.top());
        st.pop();
    }

    // the st1 will contain the actual res.
    while (!st1.empty()) {
        string temp = st1.top();

        // if it's the last element no need
        // to append "/"
        if (st1.size() != 1)
            res.append(temp + "/");
        else
            res.append(temp);

        st1.pop();
    }

    return res;
}

// Driver code.
int main()
{
    // absolute path which we have to simplify.
    string str("/a/./b/../../c/");
    string res = simplify(str);
    cout << res;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to simplify a Unix
styled absolute path of a file */
import java.io.*;
import java.util.*;

class GFG
{
    public static void main(String []args)
    {
        // absolute path which we have to simplify.
        String str = new String("/a/./b/../../c/");
        String res = simplify(str);
        System.out.println(res);
    }

    // function to simplify a Unix - styled
    // absolute path
    static String simplify(String A)
    {
        // Stack to store the file's names.
        Stack<String> st = new Stack<String>();

        // temporary String which stores the extracted
        // directory name or commands("." / "..")
        // Eg. "/a/b/../."

        // contains resultant simplifies String.
        String res = "";

        // every String starts from root directory.
        res += "/";

        // stores length of input String.
        int len_A = A.length();

        for (int i = 0; i < len_A; i++)
        {

            // we will clear the temporary String
            // every time to accommodate new directory
            // name or command.
            // dir will contain "a", "b", "..", ".";
            String dir = "";

            // skip all the multiple '/' Eg. "/////""
            while (i < len_A && A.charAt(i) == '/')
                i++;

            // stores directory's name("a", "b" etc.)
            // or commands("."/"..") into dir
            while (i < len_A && A.charAt(i) != '/')
            {
                dir += A.charAt(i);
                i++;
            }

            // if dir has ".." just pop the topmost
            // element if the Stack is not empty
            // otherwise ignore.
            if (dir.equals("..") == true)
            {
                if (!st.empty())
                    st.pop();    
            }

            // if dir has "." then simply continue
            // with the process.
            else if (dir.equals(".") == true)
                continue;

            // pushes if it encounters directory's
            // name("a", "b").
            else if (dir.length() != 0)
                st.push(dir);
        }

        // a temporary Stack (st1) which will contain
        // the reverse of original Stack(st).
        Stack<String> st1 = new Stack<String>();
        while (!st.empty())
        {

            st1.push(st.pop());
            // st.pop();
        }

        // the st1 will contain the actual res.
        while (!st1.empty())
        {

            // if it's the last element no need
            // to append "/"
            if (st1.size() != 1)
                res += (st1.pop() + "/");
            else
                res += st1.pop();

            // st1.pop();
        }
        return res;
    }

}

// This code is contributed by ankush_953
```

## 蟒蛇 3

```
# Python program to simplify a Unix
# styled absolute path of a file

# function to simplify a Unix - styled
# absolute path

def simplify(A):
    # stack to store the file's names.
    st = []

    # temporary string which stores the extracted
    # directory name or commands("." / "..")
    # Eg. "/a/b/../."
    # dir will contain "a", "b", "..", ".";
    dir = ""

    # contains resultant simplifies string.
    res = ""

    # every string starts from root directory.
    res += "/"

    # stores length of input string.
    len_A = len(A)
    i = 0
    while i < len_A:

        # we will clear the temporary string
        # every time to accommodate new directory
        # name or command.
        dir_str = ""

        # skip all the multiple '/' Eg. "##/""
        while (i < len_A and A[i] == '/'):
            i += 1

        # stores directory's name("a", "b" etc.)
        # or commands("."/"..") into dir
        while (i < len_A and A[i] != '/'):
            dir_str += A[i]
            i += 1

        # if dir has ".." just pop the topmost
        # element if the stack is not empty
        # otherwise ignore.
        if dir_str == "..":
            if len(st):
                st.pop()

        # if dir has "." then simply continue
        # with the process.
        elif dir_str == '.':
            continue

        # pushes if it encounters directory's
        # name("a", "b").
        elif len(dir_str) > 0:
            st.append(dir_str)

        i += 1

    # a temporary stack (st1) which will contain
    # the reverse of original stack(st).
    st1 = []
    while len(st):
        st1.append(st[-1])
        st.pop()

    # the st1 will contain the actual res.
    while len(st1):
        temp = st1[-1]

        # if it's the last element no need
        # to append "/"
        if (len(st1) != 1):
            res += (temp + "/")
        else:
            res += temp
        st1.pop()

    return res

# Driver code.

# absolute path which we have to simplify.
string = "/a/./b/../../c/"
res = simplify(string)
print(res)

# This code is contributed by ankush_953
```

## C#

```
// C# program to simplify a Unix
// styled absolute path of a file
using System;
using System.Collections.Generic;

class GFG
{
    public static void Main(String []args)
    {
        // absolute path which we have to simplify.
        String str = ("/a/./b/../../c/");
        String res = simplify(str);
        Console.WriteLine(res);
    }

    // function to simplify a Unix - styled
    // absolute path
    static String simplify(String A)
    {
        // Stack to store the file's names.
        Stack<String> st = new Stack<String>();

        // temporary String which stores the extracted
        // directory name or commands("." / "..")
        // Eg. "/a/b/../."

        // contains resultant simplifies String.
        String res = "";

        // every String starts from root directory.
        res += "/";

        // stores length of input String.
        int len_A = A.Length;

        for (int i = 0; i < len_A; i++)
        {

            // we will clear the temporary String
            // every time to accommodate new directory
            // name or command.
            // dir will contain "a", "b", "..", ".";
            String dir = "";

            // skip all the multiple '/' Eg. "/////""
            while (i < len_A && A[i] == '/')
                i++;

            // stores directory's name("a", "b" etc.)
            // or commands("."/"..") into dir
            while (i < len_A && A[i] != '/')
            {
                dir += A[i];
                i++;
            }

            // if dir has ".." just pop the topmost
            // element if the Stack is not empty
            // otherwise ignore.
            if (dir.Equals("..") == true)
            {
                if (st.Count!=0)
                    st.Pop();    
            }

            // if dir has "." then simply continue
            // with the process.
            else if (dir.Equals(".") == true)
                continue;

            // pushes if it encounters directory's
            // name("a", "b").
            else if (dir.Length != 0)
                st.Push(dir);
        }

        // a temporary Stack (st1) which will contain
        // the reverse of original Stack(st).
        Stack<String> st1 = new Stack<String>();
        while (st.Count!=0)
        {

            st1.Push(st.Pop());
            // st.pop();
        }

        // the st1 will contain the actual res.
        while (st1.Count!=0)
        {

            // if it's the last element no need
            // to append "/"
            if (st1.Count!= 1)
                res += (st1.Pop() + "/");
            else
                res += st1.Pop();

            // st1.pop();
        }
        return res;
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to simplify a Unix
    // styled absolute path of a file

    // function to simplify a Unix - styled
    // absolute path
    function simplify(A)
    {
        // Stack to store the file's names.
        let st = [];

        // temporary String which stores the extracted
        // directory name or commands("." / "..")
        // Eg. "/a/b/../."

        // contains resultant simplifies String.
        let res = "";

        // every String starts from root directory.
        res += "/";

        // stores length of input String.
        let len_A = A.length;

        for (let i = 0; i < len_A; i++)
        {

            // we will clear the temporary String
            // every time to accommodate new directory
            // name or command.
            // dir will contain "a", "b", "..", ".";
            let dir = "";

            // skip all the multiple '/' Eg. "/////""
            while (i < len_A && A[i] == '/')
                i++;

            // stores directory's name("a", "b" etc.)
            // or commands("."/"..") into dir
            while (i < len_A && A[i] != '/')
            {
                dir += A[i];
                i++;
            }

            // if dir has ".." just pop the topmost
            // element if the Stack is not empty
            // otherwise ignore.
            if (dir == "..")
            {
                if (st.length!=0)
                    st.pop();   
            }

            // if dir has "." then simply continue
            // with the process.
            else if (dir == ".")
                continue;

            // pushes if it encounters directory's
            // name("a", "b").
            else if (dir.length != 0)
                st.push(dir);
        }

        // a temporary Stack (st1) which will contain
        // the reverse of original Stack(st).
        let st1 = [];
        while (st.length!=0)
        {

            st1.push(st[st.length - 1]);
            st.pop();
        }

        // the st1 will contain the actual res.
        while (st1.length!=0)
        {

            // if it's the last element no need
            // to append "/"
            if (st1.length!= 1)
            {
                res += (st1[st1.length - 1] + "/");
                st.pop();
            }
            else
            {
                res += st1[st1.length - 1];
                st1.pop();
            }
        }
        return res;
    }

    // absolute path which we have to simplify.
    let str = ("/a/./b/../../c/");
    let res = simplify(str);
    document.write(res);

    // This code is contributed by divyesh072019.
</script>
```

**Output**

```
/c
```