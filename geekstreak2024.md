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
**Given a string, find the minimum number of characters to be inserted to convert it to a palindrome.**
```
class Solution{
    static int countMin(String str){
        int n = str.length();
        int[][] dp = new int[n][n];
        for(int i=2;i<=n;i++){
            for(int j=0;j<=n-i;j++){
                int k = j+i-1;
                if(str.charAt(j)==str.charAt(k))
                    dp[j][k] = dp[j+1][k-1];
                else
                    dp[j][k] = 1 + Math.min(dp[j+1][k], dp[j][k-1]);
            }
        }
        return dp[0][n-1];
    }
}
```
**Given a string str without spaces, the task is to remove all duplicate characters from it, keeping only the first occurrence.**
**Note: The original order of characters must be kept the same.**
```
class Solution {
    String removeDups(String str) {
        String s = new String();
        for(char c:str.toCharArray()){
            if(s.indexOf(c)==-1)
                s += c;
        }
        return s;
    }
}
```
**Given a boolean 2D array, consisting of only 1's and 0's, where each row is sorted. Return the 0-based index of the first row that has the most number of 1s. If no such row exists, return -1.**
```
class Solution {
    public int rowWithMax1s(int arr[][]) {
        int max = Integer.MIN_VALUE;
        int index = 0;
        for(int i=0;i<arr.length;i++){
            int count = 0;
            for(int j=0;j<arr[i].length;j++){
                if(arr[i][j]==1){
                    count++;
                }
            }
            if(count>max){
                max = count;
                index = i;
            }
        }
        if(max==0)
            return -1;
        return index;
    }
}
```
**Consider a rat placed at (0, 0) in a square matrix mat of order n* n. It has to reach the destination at (n - 1, n - 1). Find all possible paths that the rat can take to reach from source to destination. The directions in which the rat can move are 'U'(up), 'D'(down), 'L' (left), 'R' (right). Value 0 at a cell in the matrix represents that it is blocked and rat cannot move to it while value 1 at a cell in the matrix represents that rat can be travel through it.
Note: In a path, no cell can be visited more than one time. If the source cell is 0, the rat cannot move to any other cell. In case of no path, return an empty list. The driver will output "-1" automatically.**
```
class Solution {
    public ArrayList<String> findPath(int[][] mat) {
        ArrayList ans = new ArrayList<>();
        int v[][]=new int[mat.length][mat.length];
        findPath(mat,v,0,0,ans,"",mat.length);
        return ans;
    }
    public void findPath(int mat[][],int v[][],int i,int j,ArrayList<String> ans ,String s,int n){
        if(i<0 ||i>=n||j<0||j>=n || v[i][j]==1 || mat[i][j]==0)
            return;
        if(i==n-1 && j==n-1){
            ans.add(s);
            return;
        }
        v[i][j]=1;
        findPath(mat,v,i+1,j,ans,s+"D",n);
        findPath(mat,v,i-1,j,ans,s+"U",n);
        findPath(mat,v,i,j+1,ans,s+"R",n);
        findPath(mat,v,i,j-1,ans,s+"L",n);
        v[i][j]=0;
    }
}
```
**Given an array of strings arr. Return the longest common prefix among all strings present in the array. If there's no prefix common in all the strings, return "-1".**
```
class Solution {
    public String longestCommonPrefix(String arr[]) {
        if(arr == null || arr.length == 0)
            return "-1";
        String ans = arr[0];
        for(int i = 1; i < arr.length; i++){
            while(arr[i].indexOf(ans) != 0){
                ans = ans.substring(0, ans.length() - 1);
                if(ans.isEmpty())
                    return "-1";
            }
        }
        return ans;
    }
}
```
