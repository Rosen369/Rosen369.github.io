---
layout: post
title: Pigeonhole sort
desc: Implementation in C#
categories: [algorithm]
tags: [sort]
---

```C#
public class PigeonholeSort {
    public int[] Sort (int[] nums) {
        if (nums == null || nums.Length < 2) {
            return nums;
        }
        var res = new List<int> ();
        var max = nums.Max ();
        var min = nums.Min ();
        var holes = new int[max - min + 1];
        for (int i = 0; i < nums.Length; i++) {
            holes[nums[i] - min]++;
        }
        for (int i = 0; i < holes.Length; i++) {
            for (int j = 0; j < holes[i]; j++) {
                res.Add (i + min);
            }
        }
        return res.ToArray ();
    }
}
```