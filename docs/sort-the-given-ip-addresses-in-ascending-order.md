# 给定的 IP 地址按升序排序

> 原文:[https://www . geesforgeks . org/按升序对给定的 ip 地址进行排序/](https://www.geeksforgeeks.org/sort-the-given-ip-addresses-in-ascending-order/)

给定一个由 [IP 地址](https://www.geeksforgeeks.org/introduction-of-classful-ip-addressing/)组成的数组**arr【】**，其中每个元素都是一个 [IPv4 地址](https://www.geeksforgeeks.org/introduction-and-ipv4-datagram-header/)，任务是按照递增的顺序对给定的 IP 地址进行排序。
**举例:**

> **输入:** arr[] = {'126.255.255.255 '，' 169.255.0.0 '，' 169.253.255.255'}
> **输出:** '126.255.255.255 '，' 169.255.0.0'
> **解释:**
> 因此第三个 IP 地址将小于第三个 IP 地址。
> 169 . 255 . 0 . 0>169 . 253 . 255 . 255
> **输入:** arr[] = {'192.168.0.1 '，' 192.168.1.210 '，' 192.168.0.227'}
> **输出:** '192.168.0.1 '，' 192.168 '

**方法:**想法是使用**自定义比较器**对给定的 IP 地址进行排序。由于 IPv4 有 4 个八位字节，我们将逐八位字节比较地址。

*   检查 IP 地址的第一个八位字节，如果第一个地址有更大的第一个八位字节，则返回真以交换 IP 地址，否则返回假。
*   如果 IP 地址的第一个八位字节相同，则比较两个 IP 地址的第二个八位字节。如果第一个地址有更大的第二个二进制八位数，则返回真以交换 IP 地址，否则返回假。
*   如果 IP 地址的第二个八位字节也相同，则比较两个 IP 地址的第三个八位字节。如果第一个地址有更大的第三个二进制八位数，则返回真以交换 IP 地址，否则返回假。
*   如果 IP 地址的第三个八位字节也相同，则比较两个 IP 地址的第四个八位字节。如果第一个地址有更大的第三个二进制八位数，则返回真以交换 IP 地址，否则返回假。
*   如果第四个八位字节也相同，则两个 IP 地址相等。然后也返回 False。

以下是上述方法的实现:

## 计算机编程语言

```
# Python implementation to sort
# the array of the IP Address

from functools import cmp_to_key

# Custom Comparator to sort the
# Array in the increasing order
def customComparator(a, b):

    # Breaking into the octets
    octetsA = a.strip().split(".")
    octetsB = b.strip().split(".")

    # Condition if the IP Address
    # is same then return 0
    if octetsA == octetsB:
        return 0
    elif octetsA[0] > octetsB[0]:
        return 1
    elif octetsA[0] < octetsB[0]:
        return -1
    elif octetsA[1] > octetsB[1]:
        return 1
    elif octetsA[1] < octetsB[1]:
        return -1
    elif octetsA[2] > octetsB[2]:
        return 1
    elif octetsA[2] < octetsB[2]:
        return -1
    elif octetsA[3] > octetsB[3]:
        return 1
    elif octetsA[3] < octetsB[3]:
        return -1

# Function to sort the IP Addresses
def sortIPAdddress(arr):

    # Sort the Array using
    # Custom Comparator
    arr = sorted(arr, key = \
       cmp_to_key(customComparator))

    print(*arr)
    return arr

# Driver Code
if __name__ == "__main__":
    arr = ['192.168.0.1',
           '192.168.1.210',
           '192.168.0.227']

    # Function Call
    sortIPAdddress(arr)
```

**Output:** 

```
192.168.0.1 
192.168.0.227 
192.168.1.210
```

**时间复杂度:** O(N*logN)