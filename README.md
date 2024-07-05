# LEETCODE-Linked-List-2058
Sure, let's go through a dry run of the given code step by step. Here is the class and method we're examining:

```java
class Solution {
  public int[] nodesBetweenCriticalPoints(ListNode head) {
    int minDistance = Integer.MAX_VALUE;
    int firstMaIndex = -1;
    int prevMaIndex = -1;
    int index = 1;
    ListNode prev = head;      // Point to the index 0.
    ListNode curr = head.next; // Point to the index 1.

    while (curr.next != null) {
      if ((curr.val > prev.val && curr.val > curr.next.val) ||
          (curr.val < prev.val && curr.val < curr.next.val)) {
        if (firstMaIndex == -1) // Only assign once.
          firstMaIndex = index;
        if (prevMaIndex != -1)
          minDistance = Math.min(minDistance, index - prevMaIndex);
        prevMaIndex = index;
      }
      prev = curr;
      curr = curr.next;
      ++index;
    }

    if (minDistance == Integer.MAX_VALUE)
      return new int[] {-1, -1};
    return new int[] {minDistance, prevMaIndex - firstMaIndex};
  }
}
```

Let's assume we have the following linked list:
```
1 -> 3 -> 2 -> 4 -> 1 -> 5
```

Here’s how the method would process this list:

1. Initialize variables:
   - `minDistance = Integer.MAX_VALUE`
   - `firstMaIndex = -1`
   - `prevMaIndex = -1`
   - `index = 1`
   - `prev` points to the node with value `1`
   - `curr` points to the node with value `3`

2. Enter the `while` loop:
   - `curr` is `3`, `prev` is `1`, `curr.next` is `2`
   - Check if `curr` is a local maximum or minimum:
     - `curr.val > prev.val` (3 > 1) and `curr.val > curr.next.val` (3 > 2) is true.
   - `firstMaIndex` is `-1`, so set `firstMaIndex = 1`
   - `prevMaIndex` is `-1`, so skip the `minDistance` update.
   - Set `prevMaIndex = 1`
   - Move `prev` to `3`, `curr` to `2`, increment `index` to `2`

3. Next iteration:
   - `curr` is `2`, `prev` is `3`, `curr.next` is `4`
   - Check if `curr` is a local maximum or minimum:
     - `curr.val < prev.val` (2 < 3) and `curr.val < curr.next.val` (2 < 4) is true.
   - `firstMaIndex` is `1`, so skip setting `firstMaIndex`.
   - `prevMaIndex` is `1`, so update `minDistance = Math.min(minDistance, 2 - 1) = 1`
   - Set `prevMaIndex = 2`
   - Move `prev` to `2`, `curr` to `4`, increment `index` to `3`

4. Next iteration:
   - `curr` is `4`, `prev` is `2`, `curr.next` is `1`
   - Check if `curr` is a local maximum or minimum:
     - `curr.val > prev.val` (4 > 2) and `curr.val > curr.next.val` (4 > 1) is true.
   - `firstMaIndex` is `1`, so skip setting `firstMaIndex`.
   - `prevMaIndex` is `2`, so update `minDistance = Math.min(minDistance, 3 - 2) = 1`
   - Set `prevMaIndex = 3`
   - Move `prev` to `4`, `curr` to `1`, increment `index` to `4`

5. Next iteration:
   - `curr` is `1`, `prev` is `4`, `curr.next` is `5`
   - Check if `curr` is a local maximum or minimum:
     - `curr.val < prev.val` (1 < 4) and `curr.val < curr.next.val` (1 < 5) is true.
   - `firstMaIndex` is `1`, so skip setting `firstMaIndex`.
   - `prevMaIndex` is `3`, so update `minDistance = Math.min(minDistance, 4 - 3) = 1`
   - Set `prevMaIndex = 4`
   - Move `prev` to `1`, `curr` to `5`, increment `index` to `5`

6. The `while` loop exits because `curr.next` is `null`.

7. Check if `minDistance` is `Integer.MAX_VALUE`:
   - It’s not, so return `[minDistance, prevMaIndex - firstMaIndex]` which is `[1, 4 - 1]` or `[1, 3]`.

Therefore, the output for this linked list would be `[1, 3]`.
