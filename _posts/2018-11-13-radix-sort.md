---
layout: post
title: Radix sort
desc: Implementation in C#
categories: [algorithm]
tags: [sort]
---

```C#
public class RadixSort {
    public int[] Sort (int[] nums) {
        if (nums == null || nums.Length < 2) {
            return nums;
        }
        var max = nums[0];
        for (int i = 1; i < nums.Length; i++) {
            max = Math.Max (max, nums[i]);
        }
        for (int exp = 1; max / exp > 0; exp *= 10) {
            var buckets = ListToBuckets (nums, exp);
            nums = BucketsToList (nums, buckets);
        }
        return nums;
    }

    private int[] BucketsToList (int[] nums, IList<IList<int>> buckets) {
        var list = new List<int> ();
        foreach (var bucket in buckets) {
            foreach (var num in bucket) {
                list.Add (num);
            }
        }
        return list.ToArray ();
    }

    private IList<IList<int>> ListToBuckets (int[] nums, int exp) {
        var buckets = new List<IList<int>> ();
        for (int i = 0; i < 10; i++) {
            buckets.Add (new List<int> ());
        }
        for (int i = 0; i < nums.Length; i++) {
            buckets[nums[i] / exp % 10].Add (nums[i]);
        }
        return buckets;
    }
}
```