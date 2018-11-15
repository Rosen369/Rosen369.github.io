---
layout: post
title: Quick sort
desc: Implementation in C#
categories: [algorithm]
tags: [sort]
---

```C#
public class QuickSort {
    public void Sort (int[] nums) {
        if (nums == null || nums.Length < 2) {
            return;
        }
        Partition (nums, 0, nums.Length - 1);
    }

    private void Partition (int[] nums, int low, int high) {
        if (low >= high) {
            return;
        }
        var curr = nums[low];
        var i = low;
        var j = high;
        while (i < j) {
            while (nums[j] > curr && i < j) {
                j--;
            }
            nums[i] = nums[j];
            while (nums[i] < curr && i < j) {
                i++;
            }
            nums[j] = nums[i];
        }
        nums[i] = curr;
        Partition (nums, low, j - 1);
        Partition (nums, j + 1, high);
    }
}
```