# Sorting


## Merge Sort

```java
void mergesort(int[] nums) {
      n = A.length;
      if (n < 2) return;
      mid = n/2;

      left = new int[mid];
      right = new int[n - mid];

      for (int i = 0; i < mid; i++) 
          left[i] = nums[i];

      for (int i = mid; i < n; i++) 
          right[i - mid] = nums[i];

      mergesort(left);
      mergesort(right);
      merge(left, right, nums)
    }
}

void merge(int[] L,  int[] R, int[] nums) {
    int i = j = k = 0;

    while (i < L.length && j < R.length) {
        if (L[i] < R[j]) {
            nums[k++] = L[i++];
        } else {
            nums[k++] = R[j++];
        }
    }

    while (i < L.length) nums[k++] = L[i++];
    while (j < R.length) nums[k++] = R[j++];  
}

```
