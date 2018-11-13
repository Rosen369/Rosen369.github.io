---
layout: post
title: Merge sort
desc: Implementation in C#
categories: [algorithm]
tags: [sort]
---

```C#
public class MergeSort {
    public int[] Sort (int[] nums) {
        if (nums == null || nums.Length < 2) {
            return nums;
        }
        var res = new List<int> ();
        var left = new List<int> ();
        var right = new List<int> ();
        var mid = nums.Length / 2;
        for (int i = 0; i < nums.Length; i++) {
            if (i <= mid) {
                left.Add (nums[i]);
            } else {
                right.Add (nums[i]);
            }
        }
        left = Sort (left.ToArray ()).ToList ();
        right = Sort (right.ToArray ()).ToList ();
        for (int i = 0; i < nums.Length; i++) {
            if (left.Count () == 0) {
                res.AddRange (right);
                break;
            } else if (right.Count () == 0) {
                res.AddRange (left);
                break;
            } else if (left[0] < right[0]) {
                res.Add (left[0]);
                left.RemoveAt (0);
            } else {
                res.Add (right[0]);
                right.RemoveAt (0);
            }
        }
        return res.ToArray ();
    }
}
```