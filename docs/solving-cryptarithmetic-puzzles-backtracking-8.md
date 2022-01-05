# 解决密码学难题|回溯-8

> 原文:[https://www . geeksforgeeks . org/solving-cryptarithmetic-拼图-回溯-8/](https://www.geeksforgeeks.org/solving-cryptarithmetic-puzzles-backtracking-8/)

报纸和杂志通常有以下形式的加密算术谜题:

```
  SEND
+ MORE
--------
 MONEY
-------- 
```

这里的目标是给每个字母分配一个从 0 到 9 的数字，以便算术运算正确。规则是，一个字母的所有出现都必须分配相同的数字，任何数字都不能分配给多个字母。

*   首先，创建一个列表，列出需要分配给求解的所有字符
*   如果指定了所有角色，如果解谜则返回 true，否则返回 false
*   否则，考虑第一个未分配的字符
*   for (every possible choice among the digits not in use)

    做出选择，然后递归尝试分配剩余的字符
    如果递归成功，返回真
    如果！成功，取消分配并尝试另一个数字

*   如果所有的数字都尝试过了，但没有成功，返回 false 触发回溯

```
/* ExhaustiveSolve
* ---------------
* This is the "not-very-smart" version of cryptarithmetic solver. It takes
* the puzzle itself (with the 3 strings for the two addends and sum) and a
* string of letters as yet unassigned. If no more letters to assign
* then we've hit a base-case, if the current letter-to-digit mapping solves
* the puzzle, we're done, otherwise we return false to trigger backtracking
* If we have letters to assign, we take the first letter from that list, and
* try assigning it the digits from 0 to 9 and then recursively working
* through solving puzzle from here. If we manage to make a good assignment
* that works, we've succeeded, else we need to unassign that choice and try
* another digit. This version is easy to write, since it uses a simple
* approach (quite similar to permutations if you think about it) but it is
* not so smart because it doesn't take into account the structure of the
* puzzle constraints (for example, once the two digits for the addends have
* been assigned, there is no reason to try anything other than the correct
* digit for the sum) yet it tries a lot of useless combos regardless
*/
bool ExhaustiveSolve(puzzleT puzzle, string lettersToAssign)
{
    if (lettersToAssign.empty()) // no more choices to make
        return PuzzleSolved(puzzle); // checks arithmetic to see if works
    for (int digit = 0; digit <= 9; digit++)   // try all digits
    {
        if (AssignLetterToDigit(lettersToAssign[0], digit))
        {
            if (ExhaustiveSolve(puzzle, lettersToAssign.substr(1)))
                return true;
            UnassignLetterFromDigit(lettersToAssign[0], digit);
        }
    }
    return false;  // nothing worked, need to backtrack
}
```

上面的算法实际上与置换算法有很多共同之处，它基本上只是创建了从字符到数字的映射的所有排列，并尝试每种排列，直到一种排列成功或者所有排列都被成功尝试。对于一个大难题，这可能需要一段时间。
更聪明的算法可以考虑到谜题的结构，避免走上死胡同。例如，如果我们从一个人的位置开始分配角色，并向左移动，在每个阶段，我们可以在继续之前验证到目前为止我们所拥有的东西的正确性。这无疑使代码变得复杂，但却极大地提高了效率，使得解决大型难题变得更加可行。

下面的伪代码，在这种情况下，有更多的特殊情况，但同样的一般设计

*   首先检查最上面一行最右边的数字，进位为 0
*   如果我们超出了拼图最左边的数字，如果没有进位，则返回 true，否则返回 false
*   如果我们当前试图在其中一个加数
    中分配一个字符，如果已经分配了字符，只需在这个加数下面的行上重复一次，将值加到总和
    中。如果没有分配，那么
    *   对于(未使用的数字中的每一个可能的选择)
        做出那个选择，然后在这个下面的行上，如果成功，返回 true
        if！成功，取消分配并尝试另一个数字
    *   如果没有赋值触发回溯，则返回 false
*   否则，如果试图在总和中指定一个字符
*   如果分配的字符和匹配正确，
    用进位在左边的下一列重复出现，如果成功返回真，
*   如果分配的字符&不匹配，返回 false
*   如果已使用未赋值的正确数字，则返回 false
*   如果字符未赋值&正确数字未被使用，
    赋值并在左下一列用进位重复，如果成功返回真
*   返回 false 以触发回溯

**来源:**