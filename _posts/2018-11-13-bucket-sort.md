---
layout: post
title: Bucket sort
desc: Implementation in C#
categories: [algorithm]
tags: [sort]
---

```C#
public class BucketSort {
    public int[] Sort (int[] nums, int bucketSize) {
        if (nums == null || nums.Length < 2) {
            return nums;
        }
        var res = new List<int> ();
        var max = nums.Max ();
        var min = nums.Min ();
        // Initialise buckets
        var bucketCount = (max - min) / bucketSize + 1;
        var buckets = new List<IList<int>> ();
        for (int i = 0; i < bucketCount; i++) {
            buckets.Add (new List<int> ());
        }
        // Distribute input array values into buckets
        for (int i = 0; i < nums.Length; i++) {
            buckets[(nums[i] - min) / bucketSize].Add (nums[i]);
        }
        // Sort each bucket
        foreach (var bucket in buckets) {
            var arr = bucket.ToArray ();
            Array.Sort (arr);
            for (int i = 0; i < arr.Length; i++) {
                res.Add (arr[i]);
            }
        }
        return res.ToArray ();
    }
}
```