---
layout: post
title: Pigeonhole sort
desc: Implementation in C#
categories: [algorithm]
tags: [sort]
---

```C#
public class PigeonholeSort {
    public void Sort (int[] nums) {
        if (nums == null || nums.Length < 2) {
            return;
        }
        var max = nums.Max ();
        var min = nums.Min ();
        var holes = new int[max - min + 1];
        for (int i = 0; i < nums.Length; i++) {
            holes[nums[i] - min]++;
        }
        var index = 0;
        for (int i = 0; i < holes.Length; i++) {
            for (int j = 0; j < holes[i]; j++) {
                nums[index++] = i + min;
            }
        }
    }
}
```