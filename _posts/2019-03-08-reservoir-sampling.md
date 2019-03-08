---
layout: post
title: Reservoir Sampling
desc: Implementation in C#
categories: [algorithm]
tags: [random]
---

```C#
public class ReservoirSampling {
    public int[] SelectKItems (int[] stream, int k) {
        var random = new Random ();
        var reservoir = new int[k];
        for (int i = 0; i < k; i++) {
            reservoir[i] = stream[i];
        }
        for (int i = k; i < stream.Length; i++) {
            var p = random.Next (i + 1);
            if (p < k) {
                reservoir[p] = stream[i];
            }
        }
        return reservoir;
    }
}
```