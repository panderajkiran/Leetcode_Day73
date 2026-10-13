# Leetcode_Day73
# Day 73: Rotate List

**LeetCode Problem:** 61. Rotate List  
**Difficulty:** Medium  
**Topic:** Linked List, Two Pointers  
**Language:** Java

## Problem Statement

Given the head of a linked list, rotate the list to the right by `k` places.

Each rotation moves the last node of the list to the beginning.

## Approach: Find Length and Adjust Pointers

I solved this problem by calculating the linked list's length and changing the links between nodes.

1. If the list is empty or contains only one node, return the head.
2. Traverse the list to find its length and last node.
3. Calculate `k % length` because rotating a list by its full length brings it back to its original position.
4. If the effective rotation count is zero, return the original list.
5. Find the new tail at position `length - k - 1`.
6. The node after the new tail becomes the new head.
7. Connect the original last node to the original head, then break the list after the new tail.

This approach rotates the list without creating a new linked list.

## Java Solution

```java
class Solution {
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || head.next == null) {
            return head;
        }

        int length = 1;
        ListNode last = head;

        while (last.next != null) {
            last = last.next;
            length++;
        }

        k = k % length;
        if (k == 0) {
            return head;
        }

        int step = length - k - 1;
        ListNode newTail = head;

        for (int i = 0; i < step; i++) {
            newTail = newTail.next;
        }

        ListNode newHead = newTail.next;
        last.next = head;
        newTail.next = null;

        return newHead;
    }
}
```

## Example

**Input:**
```text
head = [1,2,3,4,5]
k = 2
```

**Output:**
```text
[4,5,1,2,3]
```

**Explanation:**

- First rotation: `[5,1,2,3,4]`
- Second rotation: `[4,5,1,2,3]`

The last two nodes move to the beginning while preserving their relative order.

## Complexity Analysis

- **Time Complexity:** O(n) — The list is traversed to find its length and locate the new tail.
- **Space Complexity:** O(1) — Only a few pointers and variables are used.

## What I Learned

- How to rotate a linked list by changing node connections.
- Why `k % length` reduces unnecessary rotations.
- How to identify the new head and tail.
- How careful pointer manipulation can solve a problem without extra data structures.

## Takeaway

Today's problem reminded me that sometimes, we don't need to rebuild everything to change the result. We just need to understand which connections need to change.

**Day 73 complete — one more problem solved, one more step forward.**
