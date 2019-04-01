#### 递归解法
```java
for(int i = start ; i <= end; i++){
            List<TreeNode> leftTree = generate(start, i-1);
            List<TreeNode> rightTree = generate(i+1, end);
            
            for(TreeNode l : leftTree){
                for(TreeNode r: rightTree){
                    TreeNode root = new TreeNode(i);
                    root.left = l;
                    root.right = r;
                    res.add(root);
                }
            }
        }
```
- 上面这段循环里， i 对应的就是root节点的选择， i == start , 左子树为空， generate(start, i-1) return [null]
i == end, 右子树为空，generate(i+1, end) return [null]
- 注意如何设计递归方法
- 题眼 Divide-and-conquer.  F(i) = G(i-1) * G(n-i)

