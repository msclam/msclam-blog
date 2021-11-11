# （一）快速排序

> 版本一

~~~c++
void quickSort(vector<int>& A, int l, int r) {
    if (l >= r) return;
    int i = l, j = r, x = A[l + r >> 1];
    while (i < j) {
        while (A[i] < x) i ++;
        while (A[j] > x) j --;
        if (i <= j) {
            swap(A[i], A[j]);
            i ++;
            j --;
        }
    }
    if (l < j) quickSort(A, l, j);
    if (i < r) quickSort(A, i, r);
}
~~~

> 版本二

```c++
int partition(vector<int>& A, int l, int r) {
    int x = A[l];
    while (l < r) {
        while (l < r && A[r] > x) r --;
        A[l] = A[r];
        while (l < r && A[l] <= x) l ++;
        A[r] = A[l]; 
    }
    A[l] = x;
    return l;
}

void quick_sort(vector<int>& A, int l, int r) {
    if (l < r) {
        int pos = partition(A, l, r);
        quick_sort(A, l, pos - 1);
        quick_sort(A, pos + 1, r);
    }
}
```

