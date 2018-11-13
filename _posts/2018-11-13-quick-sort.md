---
layout: post
title: Quick sort
desc: Implementation in C#
categories: [algorithm]
tags: [sort]
---

```C#
public class QuickSort {
    public int[] Sort (int[] nums) {
        if (nums == null || nums.Length < 2) {
            return nums;
        }
        var res = new List<int> ();
        var mid = nums.Length / 2;
        var left = new List<int> ();
        var right = new List<int> ();
        for (int i = 0; i < nums.Length; i++) {
            if (i == mid) {
                continue;
            }
            if (nums[i] < nums[mid]) {
                left.Add (nums[i]);
            } else {
                right.Add (nums[i]);
            }
        }
        left = Sort (left.ToArray ()).ToList ();
        right = Sort (right.ToArray ()).ToList ();
        res.AddRange (left);
        res.Add (nums[mid]);
        res.AddRange (right);
        return res.ToArray ();
    }
}
```