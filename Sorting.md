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

## QuickSort

```java
void quicksort(int[] nums, int start, int end) {
    if (start >= end) {return;}
    
    int pIndex = Partition(nums, start, end);
    quicksort(nums, start, pIndex -1);
    quicksort(nums, pIndex + 1, end);
}

int partition(int[] nums, int start, int end) {
    pivot = nums[end];
    pIndex = start;

    for (i = start; i < end; i++) {
        if (nums[i] <= pivot) {
            swap(nums[i], nums[pIndex])
            pIndex++;
        }
    }

    swap(A[pIndex], A[end]);
    return pIndex;
}

void swap(int a, int b, int[] nums) {
      int temp = nums[a];
      nums[a] = nums[b];
      nums[b] = temp;
}
```

## QuickSelect

```java

    public int findKthLargest(int[] nums, int k) {
        return quickSelect(nums, k, 0, nums.length - 1);
    }
   
    public int quickSelect(int[] nums, int k, int low, int high) {
        int pIndex = partition(nums,low, high);
         
        if (k -1 == pIndex) {
            return nums[k-1];
        } else if (k -1 < pIndex) {
            return quickSelect(nums, k, low, pIndex - 1);
        } else {
            return quickSelect(nums, k, pIndex + 1, high);
        }   
    }
    
    public int partition(int[] nums, int low, int high) {
        int pivot = nums[high];
        int pIndex = low;
        
        for (int i = low; i < high; i++) {
            if (nums[i] > pivot) {
                swap(nums, i, pIndex);
                pIndex++;
            } 
        }
        
        swap(nums, pIndex, high);
        return pIndex; 
    }
    
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;   
    }

```

## Counting Sort / Radix Sort
      
      Used to sort numbers within a specific range
      Runtime: O(n + k)

### Counting Sort for chars

```java

 void sort(char arr[]) { 
        int n = arr.length; 
  
        // The output character array that will have sorted arr 
        char output[] = new char[n]; 
  
        // Create a count array to store count of inidividul 
        // characters and initialize count array as 0 
        int count[] = new int[256]; 
        for (int i=0; i<256; ++i) 
            count[i] = 0; 
  
        // store count of each character 
        for (int i=0; i<n; ++i) 
            ++count[arr[i]]; 
  
        // Change count[i] so that count[i] now contains actual 
        // position of this character in output array 
        for (int i=1; i<=255; ++i) 
            count[i] += count[i-1]; 
  
        // Build the output character array 
        // Iterate BACKWARDS on original array, updating position-- in count each time 
        // To make it stable we are operating in reverse order. 
        for (int i = n-1; i>=0; i--) { 
            output[count[arr[i]]-1] = arr[i]; 
            count[arr[i]]--; 
        } 
  
        // Copy the output array to arr, so that arr now 
        // contains sorted characters 
        for (int i = 0; i<n; ++i) 
            arr[i] = output[i]; 
    } 

```

### Counting sort for ints with min/max/negative numbers

```java
static void countSort(int[] arr)  { 
        int max = Arrays.stream(arr).max().getAsInt(); 
        int min = Arrays.stream(arr).min().getAsInt(); 
        int range = max - min + 1; 
        int count[] = new int[range]; 
        int output[] = new int[arr.length]; 
        
        for (int i = 0; i < arr.length; i++) 
            count[arr[i] - min]++; 
  
        for (int i = 1; i < count.length; i++)  
            count[i] += count[i - 1]; 
     
        for (int i = arr.length - 1; i >= 0; i--)  { 
            output[count[arr[i] - min] - 1] = arr[i]; 
            count[arr[i] - min]--; 
        } 
  
        for (int i = 0; i < arr.length; i++) 
            arr[i] = output[i];   
    } 

```

### Radix Sort

      Just like counting sort but for each digit, starting with least significant digit
      Run time = O(d(n + b)), where d = digits, b = base

## Bucket Sort

      Algorithm:
      Set up an array of initially empty "buckets".
      Scatter: Go over the original array, putting each object in its bucket.
      Sort each non-empty bucket.
      Gather: Visit the buckets in order and put all elements back into the original array.
      
      Time Complexity: Assuming N^2 sorting algorithm and uniformlly distriubted data : O(n), see wikipedia for proof,
      Worst case = O(N^2), all data is distributed into one bucket
      

```java

function bucketSort(array, k) is
  buckets ← new array of k empty lists
  M ← the maximum key value in the array
  for i = 1 to length(array) do
    insert array[i] into buckets[floor(k * array[i] / M)]
  for i = 1 to k do
    nextSort(buckets[i])
  return the concatenation of buckets[1], ...., buckets[k]

```
