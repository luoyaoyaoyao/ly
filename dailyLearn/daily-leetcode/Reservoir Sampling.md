[398. Random Pick Index](https://leetcode.com/problems/random-pick-index/)

```java
int[] nums = new int[] {1,2,3,3,3};
Solution solution = new Solution(nums);

// pick(3) should return either index 2, 3, or 4 randomly. Each index should have equal probability of returning.
solution.pick(3);

// pick(1) should return 0. Since in the array only nums[0] is equal to 1.
solution.pick(1);
```

```java
class Solution {
    int[] nums;
    public Solution(int[] nums) {
        this.nums = nums;
    }
    public int pick(int target) {
        int res = 0;
        Random rnd = new Random();
        int count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == target) {
                if (rnd.nextInt(++count) == 0) {
                    res = i;
                }
            }
        }
        return res;
    }
}
```

[382. Linked List Random Node](https://leetcode.com/problems/linked-list-random-node/)

```java
// Init a singly linked list [1,2,3].
ListNode head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
Solution solution = new Solution(head);

// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
solution.getRandom();
```

```java
class Solution {

    ListNode head;
    Random random;
    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    public Solution(ListNode head) {
        this.head = head;
        random = new Random();
    }
    /** Returns a random node's value. */
    public int getRandom() {
        ListNode c = head;
        int r = c.val;
        for(int i=1;c.next != null;i++){
            c = c.next;
            if(random.nextInt(i + 1) == i) r = c.val;                        
        }
        return r;
    }
}

```