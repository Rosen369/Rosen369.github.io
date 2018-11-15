---
layout: post
title: KMP Algorithm
desc: Implementation in C#
categories: [algorithm]
tags: [string]
---

Knuth–Morris–Pratt string-searching algorithm (or KMP algorithm).

__Example:__

```pseudocode
Input:
W = "ABCDABD";
S = "ABC ABCDAB ABCDABCDABDE"
Output:
15
```

```C#
public class KMP {
    public int Search (string s, string w) {
        var m = 0;
        var i = 0;
        var next = GetNext (w);
        while (m < s.Length && i < w.Length) {
            if (i == -1 || s[m] == w[i]) {
                m++;
                i++;
            } else {
                i = next[i];
            }
        }
        if (i == w.Length) {
            return m - i;
        }
        return -1;
    }

    private int[] GetNext (string w) {
        var k = -1;
        var j = 0;
        var next = new int[w.Length];
        Array.Fill (next, -1);
        while (j < w.Length - 1) {
            if (k == -1 || w[j] == w[k]) {
                ++k;
                ++j;
                next[j] = (w[j] != w[k]) ? k : next[k];
            } else {
                k = next[k];
            }
        }
        return next;
    }
}
```