---
layout: post
title: Priority Queue
desc: Implementation in C#
categories: [datastructure]
tags: [heap]
---

```C#
public class PriorityQueue<T> where T : IComparable {

    private IList<T> _pq;

    public PriorityQueue () {
        _pq = new List<T> ();
    }

    public bool IsEmpty () {
        return _pq.Count == 0;
    }

    public T Peek () {
        if (this.IsEmpty ()) {
            return default (T);
        }
        return _pq[0];
    }

    public T Pop () {
        if (this.IsEmpty ()) {
            return default (T);
        }
        T max = _pq[0];
        Swap (0, _pq.Count - 1);
        _pq.RemoveAt (_pq.Count - 1);
        this.SiftDown (0);
        return max;
    }

    public void Remove (T item) {
        if (this.IsEmpty ()) {
            return;
        }
        var index = _pq.IndexOf (item);
        if (index == -1) {
            return;
        }
        Swap (index, _pq.Count - 1);
        _pq.RemoveAt (_pq.Count - 1);
        this.SiftDown (index);
    }

    public void Add (T item) {
        _pq.Add (item);
        this.SiftUp (_pq.Count - 1);
    }

    private bool Less (int i, int j) {
        return _pq[i].CompareTo (_pq[j]) == -1;
    }

    private void SiftDown (int i) {
        int left = Left (i);
        int right = Right (i);
        int largest = i;
        if (left <= _pq.Count - 1 && this.Less (i, left))
            largest = left;
        if (right <= _pq.Count - 1 && this.Less (largest, right))
            largest = right;
        if (largest != i) {
            this.Swap (i, largest);
            this.SiftDown (largest);
        }
    }

    private void SiftUp (int i) {
        if (i > 0) {
            var parent = Parent (i);
            if (Less (parent, i)) {
                Swap (parent, i);
                SiftUp (parent);
            }
        }
    }

    private void Swap (int i, int j) {
        T t = _pq[i];
        _pq[i] = _pq[j];
        _pq[j] = t;
    }

    private int Parent (int i) {
        return (i - 1) / 2;
    }

    private int Left (int i) {
        return 2 * i + 1;
    }

    private int Right (int i) {
        return 2 * i + 2;
    }
}
```