# 根据给定字符串生成所有可能的有效 IP 地址的程序

> 原文:[https://www . geesforgeks . org/program-generate-可能-有效-IP-address-给定-string/](https://www.geeksforgeeks.org/program-generate-possible-valid-ip-addresses-given-string/)

给定一个只包含数字的字符串，通过返回所有可能的有效 IP 地址组合来恢复它。
有效的 IP 地址必须采用 A.B.C.D 的形式，其中 A、B、C 和 D 是 0-255 之间的数字。除非数字是 0，否则不能以 0 为前缀。

**示例:**

```
Input: 25525511135
Output: [“255.255.11.135”, “255.255.111.35”]
Explanation:
These are the only valid possible
IP addresses.

Input: "25505011535"
Output: []
Explanation: 
We cannot generate a valid IP
address with this string.
```

首先，我们将在给定的字符串中放置 3 个点，然后尝试这 3 个点的所有可能组合。
有效性的角例:

```
For string "25011255255"
25.011.255.255 is not valid as 011 is not valid.
25.11.255.255 is not valid either as you are not
allowed to change the string.
250.11.255.255 is valid.
```

**方法:**用“.”分割字符串然后检查所有角落的箱子。在进入循环之前，检查字符串的大小。使用循环字符串生成所有可能的组合。如果发现 IP 有效，则返回 IP 地址，否则只返回空列表。
以下是上述办法的实施情况:

## C++

```
// C++ program to generate all possible
// valid IP addresses from given string
#include <bits/stdc++.h>
using namespace std;

// Function checks whether IP digits
// are valid or not.
int is_valid(string ip)
{
    // Splitting by "."
    vector<string> ips;
    string ex = "";
    for (int i = 0; i < ip.size(); i++) {
        if (ip[i] == '.') {
            ips.push_back(ex);
            ex = "";
        }
        else {
            ex = ex + ip[i];
        }
    }
    ips.push_back(ex);

    // Checking for the corner cases
    // cout << ip << endl;
    for (int i = 0; i < ips.size(); i++) {
        // cout << ips[i] <<endl;
        if (ips[i].length() > 3
            || stoi(ips[i]) < 0
            || stoi(ips[i]) > 255)
            return 0;

        if (ips[i].length() > 1
            && stoi(ips[i]) == 0)
            return 0;

        if (ips[i].length() > 1
            && stoi(ips[i]) != 0
            && ips[i][0] == '0')
            return 0;
    }
    return 1;
}

// Function converts string to IP address
void convert(string ip)
{
    int l = ip.length();

    // Check for string size
    if (l > 12 || l < 4) {
        cout << "Not Valid IP Address";
    }

    string check = ip;
    vector<string> ans;

    // Generating different combinations.
    for (int i = 1; i < l - 2; i++) {
        for (int j = i + 1; j < l - 1; j++) {
            for (int k = j + 1; k < l; k++) {
                check = check.substr(0, k) + "."
                        + check.substr(k);
                check
                    = check.substr(0, j) + "."
                      + check.substr(j);
                check
                    = check.substr(0, i) + "."
                      + check.substr(i);

                // cout<< check <<endl;
                // Check for the validity of combination
                if (is_valid(check)) {
                    ans.push_back(check);
                    std::cout << check << '\n';
                }
                check = ip;
            }
        }
    }
}

// Driver code
int main()
{
    string A = "25525511135";
    string B = "25505011535";

    convert(A);
    convert(B);

    return 0;
}

// This code is contributed by Harshit
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to generate all possible
// valid IP addresses from given string
import java.util.*;

class GFG {

    // Function to restore Ip Addresses
    public static ArrayList<String>
    restoreIpAddresses(String A)
    {
        if (A.length() < 3 || A.length() > 12)
            return new ArrayList<>();
        return convert(A);
    }

    private static ArrayList<String>
    convert(String s)
    {
        ArrayList<String> l = new ArrayList<>();
        int size = s.length();

        String snew = s;

        for (int i = 1; i < size - 2;
             i++) {
            for (int j = i + 1;
                 j < size - 1; j++) {
                for (int k = j + 1;
                     k < size; k++) {
                    snew
                        = snew.substring(0, k) + "."
                          + snew.substring(k);
                    snew
                        = snew.substring(0, j) + "."
                          + snew.substring(j);
                    snew
                        = snew.substring(0, i) + "."
                          + snew.substring(i);

                    if (isValid(snew)) {
                        l.add(snew);
                    }
                    snew = s;
                }
            }
        }

        Collections.sort(l, new Comparator<String>() {
            public int compare(String o1, String o2)
            {
                String a1[] = o1.split("[.]");
                String a2[] = o2.split("[.]");

                int result = -1;
                for (int i = 0; i < 4
                                && result != 0;
                     i++) {
                    result = a1[i].compareTo(a2[i]);
                }
                return result;
            }
        });
        return l;
    }

    private static boolean isValid(String ip)
    {
        String a[] = ip.split("[.]");
        for (String s : a) {
            int i = Integer.parseInt(s);
            if (s.length() > 3 || i < 0 || i > 255) {
                return false;
            }
            if (s.length() > 1 && i == 0)
                return false;
            if (s.length() > 1 && i != 0
                && s.charAt(0) == '0')
                return false;
        }

        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        System.out.println(
            restoreIpAddresses(
                "25525511135")
                .toString());
    }
}

// This code is contributed by Nidhi Hooda.
```

## 蟒蛇 3

```
# Python3 code to check valid possible IP

# Function checks whether IP digits
# are valid or not.
def is_valid(ip):

    # Splitting by "."
    ip = ip.split(".")

    # Checking for the corner cases
    for i in ip:
        if (len(i) > 3 or int(i) < 0 or
                          int(i) > 255):
            return False
        if len(i) > 1 and int(i) == 0:
            return False
        if (len(i) > 1 and int(i) != 0 and
            i[0] == '0'):
            return False

    return True

# Function converts string to IP address
def convert(s):

    sz = len(s)

    # Check for string size
    if sz > 12:
        return []
    snew = s
    l = []

    # Generating different combinations.
    for i in range(1, sz - 2):
        for j in range(i + 1, sz - 1):
            for k in range(j + 1, sz):
                snew = snew[:k] + "." + snew[k:]
                snew = snew[:j] + "." + snew[j:]
                snew = snew[:i] + "." + snew[i:]

                # Check for the validity of combination
                if is_valid(snew):
                    l.append(snew)

                snew = s

    return l

# Driver code        
A = "25525511135"
B = "25505011535"

print(convert(A))
print(convert(B))
```

**Output**

```
255.255.11.135
255.255.111.35

```

**复杂度分析:**

*   **时间复杂度:** O(n^3)，其中 n 是字符串的长度
    需要字符串的三次嵌套遍历，其中 n 总是小于 12。
*   **辅助空间:** O(n)。
    只要需要额外的空间。

**另一种有效的方法(动态规划):**对于这个问题存在一种 dp 方法，可以在时间复杂度 O(n*4*3)=O(12n)=O(n)和空间复杂度 O(4n)上求解。

**方法:**我们知道 IP 只有 4 个部分。我们从字符串的末尾开始迭代，一直到字符串的开头。我们创建一个大小为(4 x N)的 dp 2D 阵列。dp 数组中只能有 2 个值，即 1(真)或 0(假)。dp[0][i]告诉我们是否可以从 I 开始到字符串末尾的子字符串创建 IP 的 1 部分。类似地，dp[1][i]告诉我们是否可以从从 I 开始到字符串结束的子字符串创建 IP 的 2 个部分。

创建 dp 阵列后，我们开始创建有效的 IP 地址。我们从 2D dp 阵列的左下角开始。我们只迭代 12 次(最坏的情况)，但这些也将是有效的 IP 地址，因为我们只形成有效的 IP 地址。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to generate all possible
// valid IP addresses from given string
import java.util.*;

class GFG
{
    public static ArrayList<String> list;

    // Function to restore Ip Addresses
    public static ArrayList<String>
    restoreIpAddresses(String s)
    {
        int n = s.length();
        list = new ArrayList<>();
        if (n < 4 || n > 12)
            return list;

         // initialize the dp array
        int dp[][] = new int[4][n];
        for (int i = 0; i < 4; i++)
        {
            for (int j = n - 1; j >= 0; j--)
            {
                if (i == 0)
                {
                    // take the substring
                    String sub = s.substring(j);
                    if (isValid(sub))
                    {
                        dp[i][j] = 1;
                    }
                    else if (j < n - 3)
                    {
                        break;
                    }
                }
                else
                {
                    if (j <= n - i)
                    {
                        for (int k = 1;
                             k <= 3 && j + k <= n;
                             k++)
                        {
                            String temp
                                = s.substring(j, j + k);
                            if (isValid(temp))
                            {
                                if (j + k < n
                                    && dp[i - 1][j + k]
                                           == 1)
                                {
                                    dp[i][j] = 1;
                                    break;
                                }
                            }
                        }
                    }
                }
            }
        }

        if (dp[3][0] == 0)
            return list;

        // Call function createfromDp
        createIpFromDp(dp, 3, 0, s, "");
        return list;
    }

    public static void createIpFromDp(int dp[][],
                                      int r,
                                      int c, String s,
                                      String ans)
    {
        if (r == 0)
        {
            ans += s.substring(c);
            list.add(ans);
            return;
        }
        for (int i = 1;
             i <= 3 && c + i < s.length();
             i++)
        {
            if (isValid(s.substring(c, c + i))
                && dp[r - 1] == 1)
            {
                createIpFromDp(dp, r - 1, c + i, s,
                               ans +
                               s.substring(c, c + i)
                               + ".");
            }
        }
    }

    private static boolean isValid(String ip)
    {
        String a[] = ip.split("[.]");
        for (String s : a)
        {
            int i = Integer.parseInt(s);
            if (s.length() > 3 || i < 0 || i > 255)
            {
                return false;
            }
            if (s.length() > 1 && i == 0)
                return false;
            if (s.length() > 1 && i != 0
                && s.charAt(0) == '0')
                return false;
        }

        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Function call
        System.out.println(
            restoreIpAddresses("25525511135").toString());
    }
}

// This code is contributed by Nidhi Hooda.
```

**Output**

```
[255.255.11.135, 255.255.111.35]

```

**复杂度分析:**

*   **时间复杂度** : O(n)，其中 n 为字符串的长度。dp 数组的创建需要 O(4*n*3) = O(12n) = O(n)。从 dp 阵列创建有效的 IP 需要 O(n)。
*   **辅助空间** : O(n)。因为 dp 数组有额外的空间大小(4 x n)。意思是 O(4n)。

**<u>另一种方法:</u>(使用递归)**

## C++

```
#include <iostream>
#include <vector>
using namespace std;

void solve(string s, int i, int j, int level, string temp,
           vector<string>& res)
{
    if (i == (j + 1) && level == 5) {
        res.push_back(temp.substr(1));
    }

    // Digits of a number ranging 0-255 can lie only between
    // 0-3
    for (int k = i; k < i + 3 && k <= j; k++) {
        string ad = s.substr(i, k - i + 1);

        // Return if sting starting with '0' or it is
        // greater than 255.
        if (s[i] == '0' || stol(ad) > 255)
            return;

        // Recursively call for another level.
        solve(s, k + 1, j, level + 1, temp + '.' + ad, res);
    }
}

int main()
{
    string s = "25525511135";
    int n = s.length();

    vector<string> ans;

    solve(s, 0, n - 1, 1, "", ans);

    for (string s : ans)
        cout << s << endl;

    return 0;
}
```

**Output**

```
255.255.11.135
255.255.111.35

```