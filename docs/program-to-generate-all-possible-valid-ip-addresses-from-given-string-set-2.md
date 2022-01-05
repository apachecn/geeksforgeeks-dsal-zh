# 根据给定字符串生成所有可能的有效 IP 地址的程序|设置 2

> 原文:[https://www . geesforgeks . org/program-to-generate-all-可能-有效-IP-address-from-给定-string-set-2/](https://www.geeksforgeeks.org/program-to-generate-all-possible-valid-ip-addresses-from-given-string-set-2/)

给定一个只包含数字的字符串，通过返回所有可能的有效 IP 地址组合来恢复它。
有效的 IP 地址必须采用 **A.B.C.D** 的形式，其中 **A** 、 **B** 、 **C** 和 **D** 是从**0–255**的数字。除非编号是 **0** ，否则编号不能是 **0** 前缀。
**举例:**

> **输入:** str = "25525511135"
> **输出:**
> 255 . 255 . 11 . 135
> 255 . 255 . 111 . 35
> **输入:**str = " 1111011111 "
> **输出:**
> 111.110.11.111
> 111.110.111.11

**方法:**这个问题可以使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)解决。在每次通话中，我们有三个选项来创建有效 ip 地址的单个号码块:

1.  要么只选择一个数字，添加一个点，然后继续选择其他块(进一步的函数调用)。
2.  或者同时选择两位数字，加一个点，进一步移动。
3.  或者选择三个连续的数字并移动到下一个块。

在第四个块的末尾，如果所有的数字都已被使用，并且生成的地址是有效的 ip 地址，则将其添加到结果中，然后通过删除在前一次调用中选择的数字进行回溯。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
#include <vector>
using namespace std;

// Function to get all the valid ip-addresses
void GetAllValidIpAddress(vector<string>& result,
                          string givenString, int index,
                          int count, string ipAddress)
{

    // If index greater than givenString size
    // and we have four block
    if (givenString.size() == index && count == 4) {

        // Remove the last dot
        ipAddress.pop_back();

        // Add ip-address to the results
        result.push_back(ipAddress);
        return;
    }

    // To add one index to ip-address
    if (givenString.size() < index + 1)
        return;

    // Select one digit and call the
    // same function for other blocks
    ipAddress = ipAddress
                + givenString.substr(index, 1) + '.';
    GetAllValidIpAddress(result, givenString, index + 1,
                         count + 1, ipAddress);

    // Backtrack to generate another possible ip address
    // So we remove two index (one for the digit
    // and other for the dot) from the end
    ipAddress.erase(ipAddress.end() - 2, ipAddress.end());

    // Select two consecutive digits and call
    // the same function for other blocks
    if (givenString.size() < index + 2
        || givenString[index] == '0')
        return;
    ipAddress = ipAddress + givenString.substr(index, 2) + '.';
    GetAllValidIpAddress(result, givenString, index + 2,
                         count + 1, ipAddress);

    // Backtrack to generate another possible ip address
    // So we remove three index from the end
    ipAddress.erase(ipAddress.end() - 3, ipAddress.end());

    // Select three consecutive digits and call
    // the same function for other blocks
    if (givenString.size() < index + 3
        || stoi(givenString.substr(index, 3)) > 255)
        return;
    ipAddress += givenString.substr(index, 3) + '.';
    GetAllValidIpAddress(result, givenString, index + 3,
                         count + 1, ipAddress);

    // Backtrack to generate another possible ip address
    // So we remove four index from the end
    ipAddress.erase(ipAddress.end() - 4, ipAddress.end());
}

// Driver code
int main()
{
    string givenString = "25525511135";

    // Fill result vector with all valid ip-addresses
    vector<string> result;
    GetAllValidIpAddress(result, givenString, 0, 0, "");

    // Print all the generated ip-addresses
    for (int i = 0; i < result.size(); i++) {
        cout << result[i] << "\n";
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to get all the valid ip-addresses
def GetAllValidIpAddress(result, givenString,
                         index, count, ipAddress) :

    # If index greater than givenString size
    # and we have four block
    if (len(givenString) == index and count == 4) :

        # Remove the last dot
        ipAddress.pop();

        # Add ip-address to the results
        result.append(ipAddress);
        return;

    # To add one index to ip-address
    if (len(givenString) < index + 1) :
        return;

    # Select one digit and call the
    # same function for other blocks
    ipAddress = (ipAddress +
                 givenString[index : index + 1] + ['.']);

    GetAllValidIpAddress(result, givenString, index + 1,
                                 count + 1, ipAddress);

    # Backtrack to generate another possible ip address
    # So we remove two index (one for the digit
    # and other for the dot) from the end
    ipAddress = ipAddress[:-2];

    # Select two consecutive digits and call
    # the same function for other blocks
    if (len(givenString) < index + 2 or
            givenString[index] == '0') :
        return;

    ipAddress = ipAddress + givenString[index:index + 2] + ['.'];
    GetAllValidIpAddress(result, givenString, index + 2,
                                  count + 1, ipAddress);

    # Backtrack to generate another possible ip address
    # So we remove three index from the end
    ipAddress = ipAddress[:-3];

    # Select three consecutive digits and call
    # the same function for other blocks
    if (len(givenString)< index + 3 or
        int("".join(givenString[index:index + 3])) > 255) :
        return;
    ipAddress += givenString[index:index + 3] + ['.'];
    GetAllValidIpAddress(result, givenString,
                         index + 3, count + 1, ipAddress);

    # Backtrack to generate another possible ip address
    # So we remove four index from the end
    ipAddress = ipAddress[:-4];

# Driver code
if __name__ == "__main__" :
    givenString = list("25525511135");

    # Fill result vector with all valid ip-addresses
    result = [] ;
    GetAllValidIpAddress(result, givenString, 0, 0, []);

    # Print all the generated ip-addresses
    for i in range(len(result)) :
        print("".join(result[i]));

# This code is contributed by Ankitrai01
```

**Output:** 

```
255.255.11.135
255.255.111.35
```

**时间复杂度:** O(1)，由于 IP 地址总数不变
T3】辅助空间: O(1)