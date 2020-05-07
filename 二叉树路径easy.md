# 112. 路径总和 
## easy
## 题目描述
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:
Given the below binary tree and sum = 22,
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.
              

## 标准输入：
[5,4,8,11,null,13,4,7,2,null,null,null,1]
22
## 标准输出：
true

思路一——递归思路
用深度优先搜索（DFS）遍历所有可能的从根到叶的路径
如果没有输入根节点，输出False，
如果输入的是叶子节点，判断sum的值是否符合要求。符合则输出True否则输出False
否则判断该节点的左子树或右子树是否满足该条件。
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        if not root:
            return False
        if not root.left and not root.right:
            return True if sum == root.val else False
        else:
            return self.hasPathSum(root.left, sum-root.val) or self.hasPathSum(root.right, sum-root.val)
```
执行结果：
通过
显示详情
执行用时 :60 ms, 在所有 Python3 提交中击败了40.29%的用户
内存消耗 :15.6 MB, 在所有 Python3 提交中击败了6.67%的用户

思路二——DFS的非递归实现，用栈实现。
新建一个数组stack，只要里面还有数值，就将其pop出来赋值给node和tmp_sum
如果当前节点存在，且为叶子节点，且其数值等于tmp_sum则输出true
否则将该节点的左右子树节点和减去当前节点的值加入到stack数组中。
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        stack = [(root, sum)]
        while len(stack) > 0:
            node, tmp_sum = stack.pop()
            if node:
                if not node.left and not node.right and node.val == tmp_sum:
                    return True
                stack.append((node.right, tmp_sum-node.val))
                stack.append((node.left, tmp_sum-node.val))
        return False
```
执行结果：
通过
显示详情
执行用时 :56 ms, 在所有 Python3 提交中击败了55.30%的用户
内存消耗 :15.7 MB, 在所有 Python3 提交中击败了6.67%的用户

