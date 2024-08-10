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
