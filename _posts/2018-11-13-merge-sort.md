---
layout: post
title: Merge sort
desc: Implementation in C#
categories: [algorithm]
tags: [sort]
---

```C#
public class MergeSort {
    public void Sort (int[] nums) {
        if (nums == null || nums.Length < 2) {
            return;
        }
        MergeCore (nums, 0, nums.Length);
    }

    public void MergeCore (int[] nums, int left, int right) {
        if (right - left < 2) {
            return;
        }
        var mid = (right - left) / 2 + left;
        MergeCore (nums, left, mid);
        MergeCore (nums, mid, right);
        var temp = new int[right - left];
        var k = 0;
        var i = left;
        var j = mid;
        while (i < mid || j < right) {
            if (i == mid) {
                temp[k++] = nums[j++];
                continue;
            }
            if (j == right) {
                temp[k++] = nums[i++];
                continue;
            }
            if (nums[i] < nums[j]) {
                temp[k++] = nums[i++];
            } else {
                temp[k++] = nums[j++];
            }
        }
        for (int s = left; s < right; s++) {
            nums[s] = temp[s - left];
        }
    }
}
```