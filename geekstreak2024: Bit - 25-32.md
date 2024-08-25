**Given an array of integers arr, return true if it is possible to split it in two subarrays (without reordering the elements), such that the sum of the two subarrays are equal. If it is not possible then return false.**
```
class Solution {
    public boolean canSplit(int arr[]) {
        int sum = 0;
        for(int i=0;i<arr.length;i++)
            sum += arr[i];
        int s = 0;
        for(int i=arr.length-1;i>0;i--){
            s += arr[i];
            sum -= arr[i];
            if(s==sum)
                return true;
        }
        return false;
    }
}
```
**Given an array arr[] and an integer k where k is smaller than the size of the array, the task is to find the kth smallest element in the given array. It is given that all array elements are distinct.**
```
class Solution {
    public static int kthSmallest(int[] arr, int k) {
        PriorityQueue<Integer>pq = new PriorityQueue<>(Collections.reverseOrder());
        for(int i=0;i<arr.length;i++){
            pq.add(arr[i]);
            if(pq.size()>k)
                pq.poll();
        }
        return pq.poll();
    }
}
```
**You are given an Undirected Graph having unit weight of the edges, find the shortest path from src to all the vertex and if it is unreachable to reach any vertex, then return -1 for that vertex.**
```
class Solution {
    public int[] shortestPath(int[][] edges,int n,int m ,int src) {
        List<List<Integer>> l = new ArrayList<>();
        for(int i=0;i<n;i++)
            l.add(new ArrayList<>());
        for(int e[]:edges){
            l.get(e[0]).add(e[1]);
            l.get(e[1]).add(e[0]);
        }
        int res[] = new int[n];
        Arrays.fill(res, Integer.MAX_VALUE);
        res[src]=0;
        Queue<Integer> q = new LinkedList<>();
        q.add(src);
        while(!q.isEmpty()){
            Integer node = q.remove();
            int d = res[node];
            for(Integer num:l.get(node)){
                if(res[num]>d+1){
                    res[num]=d+1;
                    q.add(num);
                }
            }
        }
        for(int i=0;i<n;i++){
            if(res[i]==Integer.MAX_VALUE)
                res[i]=-1;
        }
        return res;
    }
}
```
**Given a sorted dictionary of an alien language having N words and k starting alphabets of standard dictionary. Find the order of characters in the alien language.
Note: Many orders may be possible for a particular test case, thus you may return any valid order and output will be 1 if the order of string returned by the function is correct else 0 denoting incorrect string returned.**
```
class Solution {
    public String findOrder(String[] dict, int n, int k) {
        Map<Character,List<Character>> map=new HashMap<>();
        for(String word:dict){
            for(char ch:word.toCharArray())
                map.put(ch,new ArrayList<>());
        }
        for(int i=1;i<n;i++){
            for(int j=0;j<Math.min(dict[i-1].length(), dict[i].length());j++){
                if(dict[i-1].charAt(j)!=dict[i].charAt(j)){
                    map.get(dict[i-1].charAt(j)).add(dict[i].charAt(j));
                    break;
                }
            }
        }
        Set<Character> s = new HashSet<>();
        Stack<Character> st = new Stack<>();
        for(Character c:map.keySet()){
            if(!s.contains(c))
                topologicalSort(map, st, s, c);
        }
        String res = "";
        while(!st.isEmpty())
            res += st.pop();
        return res;
    }
    void topologicalSort(Map<Character,List<Character>> map, Stack<Character> st, Set<Character> s, char c){
        s.add(c);
        for(Character num:map.get(c)){
            if(!s.contains(num))
                topologicalSort(map, st, s, num);
        }
        st.push(c);
    }
}
```
**Given a Binary Tree, return Left view of it. Left view of a Binary Tree is set of nodes visible when tree is visited from Left side. The task is to complete the function leftView(), which accepts root of the tree as argument. If no left view is possible, return an empty tree.**
```
class Tree{
    ArrayList<Integer> leftView(Node root){
        ArrayList<Integer> res = new ArrayList<>();
        Queue<Node> q = new LinkedList<>();
        if(root==null)
            return res;
        q.add(root);
        while(!q.isEmpty()){
            res.add(q.peek().data);
            int n = q.size();
            for(int i=0;i<n;i++){
                Node temp = q.poll();
                if(temp.left!=null)
                    q.add(temp.left);
                if(temp.right!=null)
                    q.add(temp.right);
            }
        }
        return res;
    }
}
```
**You are given weights and values of items, and put these items in a knapsack of capacity W to get the maximum total value in the knapsack. Note that we have only one quantity of each item.
In other words, given two integer arrays val and wt which represent values and weights associated with items respectively. Also given an integer W which represents knapsack capacity, find out the maximum sum values subset of val[] such that the sum of the weights of the corresponding subset is smaller than or equal to W. You cannot break an item, either pick the complete item or don't pick it (0-1 property).**
```
class Solution {
    static int knapSack(int W, int wt[], int val[]) {
        int i, j;
        int n = wt.length;
        int K[][] = new int[n+1][W+1];
        for(i=0;i<=n;i++){
            for(j=0;j<=W;j++){
                if(i==0 || j==0)
                    K[i][j] = 0;
                else if(wt[i-1]<=j)
                    K[i][j] = Math.max(val[i-1]+K[i-1][j-wt[i-1]], K[i-1][j]);
                else
                    K[i][j] = K[i-1][j];
           }
       }
       return K[n][W];
    }
}
```
**Given two positive integer arrays arr and brr, find the number of pairs such that xy > yx (raised to power of) where x is an element from arr and y is an element from brr.**
```
class Solution {
    public long countPairs(int x[], int y[], int M, int N) {
        Arrays.sort(y);
        int[] z = new int[5];
        for(int i:y){
            if(i<=4)
                z[i]++;
        }
        long pairs = 0;
        for(int i:x){
            long temp = count(i, y, N, z);
            pairs += temp;
        }
        return pairs;
    }
    long count(int x, int[] a, int n, int[] z){
        if(x==0)
            return 0;
        if(x==1)
            return z[0];
        int l = 0, j = n;
        while(l<j){
            int mid = l+(j-l)/2;
            if(a[mid]<=x)
                l = mid+1;
            else
                j = mid;
        }
        long p = n-l;
        if(x==2)
            return p+z[0]+z[1]-z[3]-z[4]; 
        if(x==3)
            return p+z[0]+z[1]+z[2];
        return p+z[0]+z[1];
    } 
}
```
