# 空间之树–锁定和解锁 N 元树

> 原文:[https://www . geesforgeks . org/空间之树-锁定和解锁-n-ary-tree/](https://www.geeksforgeeks.org/tree-of-space-locking-and-unlocking-n-ary-tree/)

给定由 **N** 节点和[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **查询【】**组成的[通用 M 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)形式的世界地图，任务是实现给定树的功能**锁定**、**解锁**和**升级**。对于**查询[]** 中的每个查询，当操作执行成功时，函数返回**真**，否则返回**假**。这些功能定义如下:

**X:** 树中节点的名称，并且将是唯一的
**uid:** 访问节点 X 的人的用户 id

**1。锁(X，uid):** 锁独占访问根子树。

*   一旦**锁定(X，uid)** 成功，那么**锁定(A，任何用户)**应该会失败，其中 **A** 是 **X** 的后代。
*   **锁定(B .任何用户)**在 **X** 是 **B** 的后代的情况下应该失败。
*   **锁定**操作不能在已经锁定的节点上执行。

**2。解锁(X，uid):** 解锁锁定的节点。

*   **解锁**恢复**锁定**操作。
*   只能在同一个**上调用，由同一个 **uid** 解锁**。

**3。升级锁(X，uid):** 用户 uid 可以将他们的**锁**升级到祖先节点。

*   只有当任何祖先节点仅被同一用户 **uid** 锁定**时才有可能。**
*   **如果有任何节点被下面的某个其他节点 **uid** **Y** 锁定**的话，**升级**应该会失败。****

****示例:****

> ****输入:** N = 7，M = 2，节点= ['世界'，'亚洲'，'非洲'，'中国'，'印度'，'南非'，'埃及']，
> 查询= ['1 中国 9 '，' 1 印度 9 '，' 3 亚洲 9 '，' 2 印度 9 '，' 2 亚洲 9 ']
> T4】输出:真真假假真**
> 
> ****输入:** N = 3，M = 2，节点= ['World '，' China '，' India']，
> 查询= ['3 India 1 '，' 1 World 9 ']
> T4】输出:假真**

**下面是上述方法的实现:**

## **蟒蛇 3**

```
# Python Implementation

# Locking function
def lock(name):
    ind = nodes.index(name)+1
    c1 = ind * 2
    c2 = ind * 2 + 1
    if status[name] == 'lock' \
            or status[name] == 'fail':
        return 'false'
    else:
        p = ind//2
        status[nodes[p-1]] = 'fail'
        status[name] = 'lock'
        return 'true'

# Unlocking function
def unlock(name):
    if status[name] == 'lock':
        status[name] = 'unlock'
        return 'true'
    else:
        return 'false'

# Upgrade function
def upgrade(name):
    ind = nodes.index(name)+1

    # left child of ind
    c1 = ind * 2

    # right child of ind
    c2 = ind * 2 + 1
    if c1 in range(1, n) and c2 in range(1, n):
        if status[nodes[c1-1]] == 'lock' \
            and status[nodes[c2-1]] == 'lock':
            status[nodes[c1-1]] = 'unlock'
            status[nodes[c2-1]] = 'unlock'
            status[nodes[ind-1]] = 'lock'
            return 'true'
        else:
            return 'false'

# Precomputation
def precompute(queries):
  d = []

  # Traversing the queries
  for j in queries:
      i = j.split()
      d.append(i[1])
      d.append(int(i[0]))

  status = {}
  for j in range(0, len(d)-1, 2):
      status[d[j]] = 0
  return status, d

# Function to perform operations
def operation(name, code):
    result = 'false'

    # Choose operation to perform
    if code == 1:
        result = lock(name)
    elif code == 2:
        result = unlock(name)
    elif code == 3:
        result = upgrade(name)
    return result

# Driver Code
if __name__ == '__main__':

      # Given Input
    n = 7;m = 2
    apis = 5
    nodes = ['World', 'Asia', \
            'Africa', 'China', \
            'India', 'SouthAfrica', 'Egypt']
    queries = ['1 China 9', '1 India 9', \
             '3 Asia 9', '2 India 9', '2 Asia 9']

    # Precomputation
    status, d = precompute(queries)

    # Function Call
    for j in range(0, len(d) - 1, 2):
        print(operation(d[j], d[j + 1]), end = ' ')
```

****Output:** 

```
true true true false true
```** 

*****时间复杂度:**O(LogN)*
T5**辅助空间:** O(N)**