# 14) Merge Intervals

**When to use:**
* When you need to merge overlapping intervals.
* Problems involving scheduling or resource allocation.

## Example Problem: [Merge Intervals](https://leetcode.com/problems/merge-intervals/)

* **Input:** `intervals = [[1,3],[2,6],[8,10],[15,18]]`
* **Output:** `[[1,6],[8,10],[15,18]]`

## Solution (O(n log n) / O(n))

```python
def merge(intervals):
    if not intervals:
        return []
    
    intervals.sort(key=lambda x: x[0])
    
    merged = []
    for interval in intervals:
        if not merged or merged[-1][1] < interval[0]:
            merged.append(interval)
        else:
            merged[-1][1] = max(merged[-1][1], interval[1])
            
    return merged
```

## Complexity:

* **Time:** `O(n log n)` because of the sorting.
* **Space:** `O(n)` for the new list.

---

## Step-by-step:

1.  Sort the intervals based on their start time.
2.  Initialize an empty list `merged` to store the result.
3.  Iterate through the sorted intervals:
    *   If `merged` is empty or the current interval does not overlap with the previous one, append it to `merged`.
    *   Otherwise, there is an overlap, so merge the current and previous intervals by updating the end of the previous interval.
4.  Return `merged`.

---

## 🎯 Other Typical Problems

| Problem | Difficulty | Link |
|---|---|---|
| [Insert Interval](https://leetcode.com/problems/insert-interval/) | Medium | [Link](https://leetcode.com/problems/insert-interval/) |
| [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/) | Medium | [Link](https://leetcode.com/problems/non-overlapping-intervals/) |
| [Meeting Rooms](https://leetcode.com/problems/meeting-rooms/) | Easy | [Link](https://leetcode.com/problems/meeting-rooms/) |
| [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) | Medium | [Link](https://leetcode.com/problems/meeting-rooms-ii/) |
