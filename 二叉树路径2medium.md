# 113. 路径总和 II
## medium
## 题目描述
给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

## 标准输入
[5,4,8,11,null,13,4,7,2,null,null,5,1]
22
## 标准输出
[[5,4,11,2],[5,8,4,5]]
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
        self.res = []
        
        def dfs(root,tmp,sum):
            if not root: return 
            
            if not root.left and not root.right and root.val == sum:
                tmp += [root.val]
                self.res.append(tmp)
            
            dfs(root.left,tmp + [root.val], sum - root.val)
            dfs(root.right,tmp + [root.val], sum - root.val)
            
            

        dfs(root, [], sum)
        return self.res
```
## 执行结果：
通过
显示详情执行用时 :52 ms, 在所有 Python3 提交中击败了74.37%的用户

内存消耗 :19 MB, 在所有 Python3 提交中击败了11.11%的用户