---
title: "Binary Search 模板"
description: "Binary Search 模板总结"
categories: [Algorithm]
tags: [algorithm]
toc: true
math: true
mermaid: false
---

# 题目
以
[LeetCode 33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)
为例，这题最适合的模板是 `while left <= right` 这种写法。首先以 `mid` 区分哪半边是有序的，对有序的那一半区间进行二分。

**Example 1:**
> Input: nums = [4,5,6,7,0,1,2], target = 0
>
> Output: 4

**Example 2:**
> Input: nums = [4,5,6,7,0,1,2], target = 3
>
> Output: -1

**Example 3:**
> Input: nums = [1,3,5], target = 1
>
> Output: 0

## Solution
```python
def search(self, nums: list[int], target: int) -> int:
        n = len(nums)
        left, right = 0, n-1
        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target: return mid

            # 先判断哪边有序
            if nums[0] <= nums[mid]:
                # 左边有序
                if nums[0] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            else:
                # 右边有序
                if nums[mid] < target <= nums[-1]:
                    left = mid + 1
                else:
                    right = mid - 1
        
        return -1
```