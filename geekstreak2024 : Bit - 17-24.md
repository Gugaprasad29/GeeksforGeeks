**Given the head of a singly linked list, the task is to rotate the linked list anti-clockwise by k nodes, i.e., left-shift the linked list by k nodes, where k is a given positive integer smaller than or equal to length of the linked list.**
```
class Solution {
    public Node rotate(Node head, int k) {
        Node temp = head;
        for(int i=0;i<k-1;i++)
            head = head.next;
        Node curr = head.next;
        head.next = null;
        Node res = curr;
        if(curr==null)
            return temp;
        while(curr.next!=null)
            curr = curr.next;
        curr.next = temp;
        return res;
    }
}
```
**Given a set of n jobs where each jobi has a deadline and profit associated with it.**

**Each job takes 1 unit of time to complete and only one job can be scheduled at a time. We earn the profit associated with a job if and only if the job is completed by its deadline.**

**Find the number of jobs done and the maximum profit.**

**Note: Jobs will be given in the form (Jobid, Deadline, Profit) associated with that Job. Deadline of the job is the time on or before which job needs to be completed to earn the profit.**
```
class Solution{
    int[] JobScheduling(Job arr[], int n){
        Arrays.sort(arr, new Comparator<Job>(){
            public int compare(Job j1, Job j2){
                return j2.profit-j1.profit;
            }
        });
        int dl = 0;
        for(Job j:arr)
            dl = Math.max(dl, j.deadline);
        int[] res = new int[dl+1];
        Arrays.fill(res, -1);
        int count = 0;
        int total = 0;
        for(Job j:arr){
            for(int i=j.deadline;i>0;i--){
                if(res[i]==-1){
                    res[i] = j.id;
                    total += j.profit;
                    count++;
                    break;
                }
            }
        }
        return new int[]{count, total};
    }
}
```
**Given 2 sorted integer arrays arr1 and arr2 of the same size. Find the sum of the middle elements of two sorted arrays arr1 and arr2.**
```
class Solution {
    public int SumofMiddleElements(int[] arr1, int[] arr2) {
        int n = arr1.length+arr2.length;
        int mid = n/2;
        int i = 0, j = 0;
        int mid1 = 0, mid2 = 0;
        while(i+j<=mid){
            if(arr1[i]<arr2[j]){
                mid2 = mid1;
                mid1 = arr1[i];
                i++;
            }
            else{
                mid2 = mid1;
                mid1 = arr2[j];
                j++;
            }
        }
        return mid1+mid2;
    }
}
```
**Given an integer n, find the square root of n. If n is not a perfect square, then return the floor value.**

**Floor value of any number is the greatest Integer which is less than or equal to that number**
```
class Solution {
    long floorSqrt(long n) {
        return (long)(Math.sqrt(n));
    }
}
```
**You are given two strings str1 and str2. Your task is to find the length of the longest common substring among the given strings.**
```
class Solution {
    public int longestCommonSubstr(String str1, String str2) {
        int res = 0;
        int n = str1.length();
        int m = str2.length();
        int[][] dp = new int[n+1][m+1];
        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                if(str1.charAt(i-1)==str2.charAt(j-1)){
                    dp[i][j] = dp[i-1][j-1]+1;
                    res = Math.max(res, dp[i][j]);
                }   
            }
        }
        return res;
    }
}
```
**You are given a linked list where each element in the list is a node and have an integer data. You need to add 1 to the number formed by concatinating all the list node numbers together and return the head of the modified linked list.**

**Note: The head represents the first element of the given array.**
```
class Solution {
    public Node addOne(Node head) {
        if(head.next==null){
            head.data += 1;
            return head;
        }
        Node res = addOne(head.next);
        head.data += res.data/10;
        res.data = res.data%10;
        return head;
    }
}
```
