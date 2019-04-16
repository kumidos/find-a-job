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
- lc 971 Flip Binary Tree To Match Preorder Traversal
- 典型中序遍历 ， 数组按序访问即可， 其中一个test case挂掉表明， 需要检查左子树是否挂掉来确定下一步。
```java
    class Solution {
    
    List<Integer> res = new ArrayList<>();
    int index = 0;
    public List<Integer> flipMatchVoyage(TreeNode root, int[] voyage) {
        boolean check = flip(root, voyage);
        if(check){
            return res;
        } else {
            return Arrays.asList(new Integer[] {-1});
        }
        
    }
    
    private boolean flip(TreeNode node, int[] voyage){
        if(node == null) 
            return true;
        if(index < voyage.length && node.val != voyage[index]){
           
            return false;
        }
        index ++;
        TreeNode l = node.left, r = node.right;
        if(l != null && r != null ){
           
            if(index < voyage.length && l.val != voyage[index] && r.val == voyage[index]){
                node.left = r;
                node.right = l;
                res.add(node.val);
            }
        }
        
        return flip(node.left, voyage) && flip(node.right, voyage);
         
            
    }
}
```
