**Given a sorted array. Convert it into a Height Balanced Binary Search Tree (BST). Return the root of the BST.**
**Height-balanced BST means a binary tree in which the depth of the left subtree and the right subtree of every node never differ by more than 1.**
```
class Solution {
    public Node sortedArrayToBST(int[] nums) {
        if(nums.length == 0)
            return null;
        return tree(nums, 0, nums.length -1);
    }
    public Node tree(int[] nums, int start, int end){
        if(start>end)
            return null;
           
        int mid = (start+end)/2;
        Node node = new Node(nums[mid]);
        node.left = tree(nums, start, mid-1);
        node.right = tree(nums, mid+1, end);
       
        return node;
    }
}
```
**Given a string str and an integer k, return true if the string can be changed into a pangram after at most k operations, else return false.**
**A single operation consists of swapping an existing alphabetic character with any other alphabetic character.**
```
class Solution {
    boolean kPangram(String str, int k) {
        if(str.length()<26)
            return false;
        int[] arr = new int[26];
        for(char c: str.toCharArray()){
            if(97<=c && c<126)
                arr[c-'a']++;
        }
        int emp = 0;
        int more = 0;
        for(int i:arr){
            if(i==0)
                emp++;
            else if(i>1)
                more += i-1;
        }
        if(emp==0)
            return true;
        else if(emp<=k && more>=emp)
            return true;
        return false;
    }
}
```
