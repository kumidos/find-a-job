- lc 333 largest-bst-subtree
- 这道题关键是知道判断bst 和 中序遍历的关系， 掌握了这个， public方法的核心通过后序遍历来解决
```java
public int largestBSTSubtree(TreeNode root) {
        if(root == null) return 0;
        int l = largestBSTSubtree(root.left);
        int r = largestBSTSubtree(root.right);
        if(isBST(root))
            return l + r + 1;
        else
            return Math.max(l , r);
    }
```
- 971. Flip Binary Tree To Match Preorder Traversal
- 典型中序遍历 ， 数组按序访问即可， 其中一个test case挂掉表明， 需要检查左子树是否挂掉来确定下一步。
```java
List<Integer> er = new ArrayList<>();
    List<Integer> res = new ArrayList<>();
    int index = 0;
    public List<Integer> flipMatchVoyage(TreeNode root, int[] voyage) {
        flip(root, voyage);
        
        if(index == voyage.length  && er.size() == 0)
            return res;
        else{
            return er;
        }
    }
    
    private void flip(TreeNode node, int[] voyage){
        if(node == null) 
            return;
        if(index < voyage.length && node.val != voyage[index]){
            er.add(-1);
            return;
        }
        index ++;
        if(node.left != null && node.right != null){
            TreeNode l = node.left, r = node.right;
            if(index < voyage.length && l.val != voyage[index] && r.val == voyage[index]){
                node.left = r;
                node.right = l;
                res.add(node.val);
            }
        }
        flip(node.left, voyage);
        if(er.size() != 0)
            return;
        flip(node.right, voyage);
            
            
    }
```
