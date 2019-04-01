#### 递归解法1
- 每次取中点来获取bst的root
- 通过快慢指针来获得中点， 注意corner case slow pointer 落在head处
- 通过pre pointer记录前一个 slowpoiner 的位置， 通过pre 进行截断
- 在构造树的时候注意mid == head 的base condition
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    private ListNode findMid(ListNode head){
        ListNode pre = null;
        ListNode slow = head, fast = head;
        
        while(fast != null && fast.next != null){
            pre = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        
        if(pre != null) {
            pre.next = null;
        }
        
        return slow;
        
    }
    public TreeNode sortedListToBST(ListNode head) {
        if( head == null)
            return null;
        
        ListNode mid = this.findMid(head);
        
        TreeNode node = new TreeNode(mid.val);
        
        if(head == mid) {
            return node;
        }
        
        node.left = this.sortedListToBST(head);
        node.right = this.sortedListToBST(mid.next);
        
        return node;
    }
}
```
#### 解法一微调 ， copy to a list, 
- 同样注意只有一个元素的base case
```java
class Solution {
    List<Integer> list = new ArrayList<>();
    private void copyToList(ListNode head){
        while(head != null){
            this.list.add(head.val);
            head = head.next;
        }
    }
    
    private TreeNode  convert(int left, int right){
        if(left > right)
            return null;
        int mid = (left + right) / 2;
        TreeNode node = new TreeNode(this.list.get(mid));
        if(left == right){
            return node;
        }
        node.left = convert(left, mid - 1);
        node.right = convert(mid + 1, right);
        return node;
    }
    public TreeNode sortedListToBST(ListNode head) {
        
        this.copyToList(head);
        return convert(0, this.list.size() - 1);

    }
}
```
#### 解法三中序遍历
- 利用中序遍历的思想来处理链表的遍历
- 在遍历过程中只需要一个pointer 一直移动即可， 维护这个pointer为全局的header
- 计算size 和使用位置信息的价值在于控制递归的base condition
- 注意变量的命名， 规避left right
```java
class Solution {
    ListNode head;
    
    private int findSize(ListNode head){
        ListNode p = head;
        int cn = 0;
        while(p != null){
            p = p.next;
            cn += 1;
        }
        
        return cn;
    }
    
    private TreeNode convert(int lo, int hi){
        if(lo > hi)
            return null;
        
        int mid = (lo + hi ) / 2;
        TreeNode left = this.convert(lo, mid - 1);
        TreeNode node = new TreeNode(this.head.val);
        node.left = left;
        
        this.head = this.head.next;
        
        node.right = this.convert(mid + 1, hi);
        return node;
    }
    public TreeNode sortedListToBST(ListNode head) {
        int len = this.findSize(head);
        this.head = head;
        
        return convert(0, len - 1);
    }
}
```
