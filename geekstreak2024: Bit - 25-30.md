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
