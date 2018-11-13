---
layout: post
title: Counting sort
desc: Implementation in C#
categories: [algorithm]
tags: [sort]
---

```C#
public class CountingSort {
    public int[] Sort (int[] nums) {
        if (nums == null || nums.Length < 2) {
            return nums;
        }
        var res = new List<int> ();
        var max = nums.Max ();
        var count = new int[max + 1];
        for (int i = 0; i < nums.Length; i++) {
            count[nums[i]]++;
        }
        for (int i = 0; i < max; i++) {
            for (int j = 0; j < count[i]; j++) {
                res.Add (i);
            }
        }
        return res.ToArray ();
    }
}
```