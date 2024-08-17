**Given two strings str1 and str2. Return the minimum number of operations required to convert str1 to str2.
The possible operations are permitted:**

**1.Insert a character at any position of the string.**

**2.Remove any character from the string.**

**3.Replace any character from the string with any other character.**
```
class Solution {
    public int editDistance(String str1, String str2) {
        int m = str1.length();
        int n = str2.length();
        int dp[][] = new int[m+1][n+1];
        for(int i=0;i<=m;i++)
            dp[i][0] = i;
        for(int j=0;j<=n;j++)
            dp[0][j] = j;
        for(int i=1;i<=m;i++){
            for(int j=1;j<=n; j++){
                if(str1.charAt(i-1) == str2.charAt(j-1)) 
                    dp[i][j] = dp[i-1][j-1];
                else
                    dp[i][j] = 1 + Math.min(Math.min(dp[i][j-1], dp[i-1][j]), dp[i-1][j-1]);
            }
        }
        return dp[m][n];
    }
}
```
**A celebrity is a person who is known to all but does not know anyone at a party. A party is being organized by some people.  A square matrix mat is used to represent people at the party such that if an element of row i and column j is set to 1 it means ith person knows jth person. You need to return the index of the celebrity in the party, if the celebrity does not exist, return -1.**
```
class Solution {
    public int celebrity(int mat[][]) {
       List<Integer> celb = new ArrayList<>();
        for(int i = 0; i < mat.length; i++) {
            boolean isCeleb = true;
            for(int j = 0; j < mat[i].length; j++) {
                if(i != j && mat[i][j] == 1)
                    isCeleb = false;
            }
            if(isCeleb)
                celb.add(i);
        }
        for(int i = 0; i < mat[0].length; i++) {
            boolean isCeleb = true;
            for(int j = 0; j < mat.length; j++) {
                if(i != j && mat[j][i] == 0)
                    isCeleb = false;
            }
            if(!isCeleb)
                celb.remove((Integer) i);
        }
        if(celb.isEmpty())
            return -1;
        return celb.get(0);
    }
}
```
**You are given timings of n meetings in the form of (start[i], end[i]) where start[i] is the start time of meeting i and end[i] is the finish time of meeting i. Return the maximum number of meetings that can be accommodated in a single meeting room, when only one meeting can be held in the meeting room at a particular time.**

**Note: The start time of one chosen meeting can't be equal to the end time of the other chosen meeting.**
```
class Solution {
    public int maxMeetings(int n, int start[], int end[]) {
        ArrayList<int[]> l = new ArrayList<>();
        for(int i=0;i<n;i++){
            l.add(new int[]{start[i],end[i]});
        }
        Collections.sort(l, new Comparator<int[]>() {
            @Override
            public int compare(int[] a, int[] b) {
                int compareEnd = Integer.compare(a[1], b[1]);
                if (compareEnd != 0) {
                    return compareEnd;
                }
                return Integer.compare(b[0], a[0]);
            }
        });
        int count = 0;
        for(int i=0;i<n;){
            int limit = l.get(i)[1];
            count++;
            while(i<n&&l.get(i)[0]<=limit){
                i++;
            }   
        }
        return count;
    }
}
```
**Given a binary tree, return an array where elements represent the bottom view of the binary tree from left to right.**

**Note: If there are multiple bottom-most nodes for a horizontal distance from the root, then the latter one in the level traversal is considered.**
```
class Solution{
    int maxLeft=0;
    int maxRight=0;
    public ArrayList <Integer> bottomView(Node root){
        ArrayList<Integer> bv = new ArrayList<>();
        if(root == null)
            return bv;
        HashMap<Integer,int[]> map = new HashMap<>();
        solve(root, 0, 0, map);
        while(maxLeft<=maxRight)
            bv.add(map.get(maxLeft++)[1]);
        return bv;
    }
    void solve(Node root, int n, int m, HashMap<Integer,int[]> map){
        if(root==null)
            return;
        maxLeft=Math.min(maxLeft, n);
        maxRight=Math.max(maxRight, n);
        if(map.get(n)==null || map.get(n)[0]<=m)
        map.put(n, new int[]{m, root.data});
        solve(root.left,n-1, m+1, map);
        solve(root.right,n+1, m+1, map);
    }
}
```
**You are given a string str in the form of an IPv4 Address. Your task is to validate an IPv4 Address, if it is valid return true otherwise return false.**

**IPv4 addresses are canonically represented in dot-decimal notation, which consists of four decimal numbers, each ranging from 0 to 255, separated by dots.**

**A valid IPv4 Address is of the form x1.x2.x3.x4 where 0 <= (x1, x2, x3, x4) <= 255. Thus, we can write the generalized form of an IPv4 address as (0-255).(0-255).(0-255).(0-255)**

**Note: Here we are considering numbers only from 0 to 255 and any additional leading zeroes will be considered invalid.**
```
class Solution {
    public boolean isValid(String str) {
        String[] arr=str.split("\\.");
        if(arr.length!=4)
            return false;
        for(int i=0;i<arr.length;i++){
            int l=arr[i].length();
            if(l>1 && arr[i].charAt(0)=='0')
                return false;
            if(arr[i].isEmpty() || arr[i].length()>3 || Integer.parseInt(arr[i])<0  || Integer.parseInt(arr[i])>255)
                return false;
        }
        return true;
    }
}
```
**Given two sorted arrays arr1 and arr2 and an element k. The task is to find the element that would be at the kth position of the combined sorted array.**
```
class Solution {
    public long kthElement(int k, int arr1[], int arr2[]) {
        int a = arr1.length;
        int b = arr2.length;
        int[] arr = new int[a+b];
        for(int i=0;i<a;i++)
            arr[i] = arr1[i];
        for(int i=0;i<b;i++)
            arr[a + i] = arr2[i];
        Arrays.sort(arr);
        long res = arr[k-1];
        return res;
    }
}
```
**Given a Binary Tree. Check for the Sum Tree for every node except the leaf node. Return true if it is a Sum Tree otherwise, return false.**

**A SumTree is a Binary Tree where the value of a node is equal to the sum of the nodes present in its left subtree and right subtree. An empty tree is also a Sum Tree as the sum of an empty tree can be considered to be 0. A leaf node is also considered a Sum Tree.**
```
class Solution {
    boolean isSumTree(Node root) {
        return sum(root) != 0;
    }
    int sum(Node root){
        if(root == null)
            return 0;
        if(root.left == root.right)
            return root.data;
        int left = sum(root.left);
        int right = sum(root.right);
        if(root.data != left+right)
            return 0;
        return root.data+left+right;
    }
}
```
**Given an array arr of n integers. Task is to write a program to find the maximum value of ∑arr[i]xi, where i = 0, 1, 2,., n-1. You are allowed to rearrange the elements of the array.**
```
class Solution {
    int Maximize(int arr[]) {
        int mod = 1000000007;
        Arrays.sort(arr);
        long sum = 0;
        for(int i=0;i<arr.length;i++)
            sum = (sum+(long)arr[i]*i)%mod;
        return (int)sum;
    }
}
```
