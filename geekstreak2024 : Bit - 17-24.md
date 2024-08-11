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
