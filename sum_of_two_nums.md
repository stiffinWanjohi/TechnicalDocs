# Two Sum (LeetCode Problem #1)

## Problem Statement:

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example:

```
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

Easy peasy, right? Well, let's dive into the solution approach!

## The Solution Strategy

Fear not, intrepid problem-solver! We have a clever strategy to conquer this challenge. It's time to unleash the power of hash tables (or dictionaries, if you prefer).

Here's the step-by-step plan:

1. Initialize an empty dictionary called `complement_dict`.
2. Iterate through the array `nums`.
3. For each element `num` in `nums`:
   - Calculate the complement `target - num`.
   - Check if the complement exists in `complement_dict`.
     - If it does, we've found our pair! Return the indices of `num` and its complement.
   - If the complement does not exist, store `num` in `complement_dict` with its index as the value.
4. If no solution is found, return an empty list (because we're sad pandas).

Now, let's put this plan into action with some Python magic!

```python
def two_sum(nums, target):
    complement_dict = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in complement_dict:
            return [complement_dict[complement], i]
        complement_dict[num] = i
    return []
```

Let's walk through an example to see this solution in action:

```
Input: nums = [2, 7, 11, 15], target = 9
```

1. Initialize an empty dictionary `complement_dict = {}`.
2. Iterate through the array `nums`:
   - For `num = 2`, the complement `target - num = 9 - 2 = 7` is not in `complement_dict`. Store `2` in `complement_dict` with its index `0`: `complement_dict = {2: 0}`.
   - For `num = 7`, the complement `target - num = 9 - 7 = 2` is in `complement_dict`. Return the indices `[complement_dict[2], i] = [0, 1]`.

And just like that, we've solved the "Two Sum" problem! The output is `[0, 1]`.

## Complexity Analysis

Now, let's analyze the efficiency of our solution:

- Time complexity: O(n), where n is the length of the input array `nums`. We iterate through the array once, and the dictionary operations (get and set) have amortized constant time complexity.
- Space complexity: O(n), where n is the length of the input array `nums`. In the worst case, we need to store all elements in the dictionary.

This solution is efficient, with linear time and space complexity, and it handles the case where the same element cannot be used twice. It's a solid approach for solving the "Two Sum" problem on LeetCode, and it's sure to impress your coding peers!
