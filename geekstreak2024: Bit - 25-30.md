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
