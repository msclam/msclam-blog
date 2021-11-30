> **选择型：简单选择、堆排序**
>
> **插入型：直接插入、折半插入、希尔排序**
>
> **交换型：快速排序、冒泡排序**
>
> **分治型：归并排序**

#

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



# （二）归并排序

```c++
void merge(vector<int> &A, int l1, int r1, int l2, int r2) {
    int len = r2 - l1 + 1;
    vector<int> tmp(len, 0);
    int i = l1, j = l2, idx = 0;
    while (i <= r1 && j <= r2) {
        if (A[i] <= A[j]) {
            tmp[idx++] = A[i++];
        } else {
            tmp[idx++] = A[j++];
        }
    }
    while (i <= r1) tmp[idx++] = A[i++];
    while (j <= r2) tmp[idx++] = A[j++];

    for (int i = 0; i < idx; i ++ ) {
        A[l1 + i] = tmp[i];
    } 
}

void mergeSort(vector<int> &A, int l, int r) {
    if (l < r) {
        int mid = l + r >> 1;
        mergeSort(A, l, mid);
        mergeSort(A, mid + 1, r);
        merge(A, l, mid, mid + 1, r);
    }
}
```



# （三）堆排序

```c++
void adjustDown(vector<int> &A, int low, int high) {
    int i = low, j = 2 * i + 1;
    while (j <= high) {
        if (j + 1 <= high && A[j + 1] > A[j]) {
            j ++;
        }
        if (A[j] > A[i]) {
            swap(A[j], A[i]);
            i = j;
            j = 2 * j + 1;
        } else {
            break;
        }
    }
}

void heapSort(vector<int> &A, int n) {
    for (int i = n / 2 - 1; i >= 0; i -- ) {
        adjustDown(A, i, n - 1);
    }
    for (int i = n - 1; i > 0; i -- ) {
        swap(A[0], A[i]);
        adjustDown(A, 0, i - 1);
    }
}
```



# （四）冒泡排序

```c++
void bubbleSort(vector<int>& A, int n) {
    for (int i = 0; i < n - 1; i ++ ) {
        for (int j = 0; j < n - i - 1; j ++ ) {
            if (A[j] > A[j + 1]) {
                swap(A[j], A[j + 1]);
            }
        }
    }
}
```



# （五）选择排序

```c++
void selectSort(vector<int> &A, int n) {
    for (int i = 0; i < n - 1; i ++ ) {
        int min = i;
        for (int j = i + 1; j < n; j ++ ) {
            if (A[j] < A[min]) {
                min = j;
            }
        }
        if (min != i) {
            swap(A[min], A[i]);
        }
    }
}
```



# （六）直接插入

```c++
void insertSort(vector<int> &A, int n) {
    for (int i = 0; i < n; i ++ ) {
        int tmp = A[i], j;
        for (j = i - 1; j >= 0 && tmp < A[j]; j -- ) {
            A[j + 1] = A[j];
        }
        A[j + 1] = tmp;
    }
}
```



# （七）折半插入

```c++
void halfInsertSort(vector<int> &A, int n) {
    for (int i = 0; i < n; i ++ ) {
        int tmp = A[i], j;
        int l = 0, r = i;
        while (l < r) {
            int mid = l + r >> 1;
            if (A[mid] <= tmp) l = mid + 1;
            else r = mid;
        }
        for (j = i - 1; j >= l; j -- ) {
            A[j + 1] = A[j];
        }
        A[j + 1] = tmp;
    }
}
```



# （八）希尔排序

```c++
void shellSort(vector<int> &A, int n) {
    for (int dk = n / 2; dk >= 1; dk /= 2 ) {
        for (int i = dk; i < n; i ++ ) {
            if (A[i - dk] > A[i]) {
                int tmp = A[i], j;
                for (j = i - dk; j >= 0 && tmp < A[j]; j -= dk ) {
                    A[j + dk] = A[j];
                }
                A[j + dk] = tmp;
            }
        }
    }
}
```

