# Sorting-Algorithms-in-Python

## 1. MergeSort O(nlogn) (Divide & conquer)
### arr = [2,8,5,3,9,4,1,7] 
### Divide & conquer, excute recursively, first devide then merge

![4](https://user-images.githubusercontent.com/37478093/88377323-89ae9380-cdd1-11ea-8490-d7035f8ac3e9.png)
![5](https://user-images.githubusercontent.com/37478093/88377324-8adfc080-cdd1-11ea-9aa6-97b6ce056f2e.png)

```
def mergesort(arr):
    if(len(arr) <= 1): # already divide in to one element
        return arr # return itself
    mid = int(len(arr)/2) # otherwise devide from middle
    left = mergesort(arr[:mid]) # continue deviding left
    right = mergesort(arr[mid:]) # continue deviding right
    return merge(left, right) # when completely divide, finally merge them

def merge(arr1, arr2):
    i = 0
    j = 0
    arr = []
    print(arr1, arr2)
    while(i<len(arr1) and j<len(arr2)):
        if(arr1[i] < arr2[j]):
            arr.append(arr1[i])
            i+=1
        else:
            arr.append(arr2[j])
            j+=1
    arr += arr1[i:] # when arr2 is finished, attach remain of arr1 if exists
    arr += arr2[j:] # when arr1 is finished, attach remain of arr2 if exists
    return arr

arr = [2,8,5,3,9,4,1,7]     
print(mergesort(arr))

# merge
# [2] [8]
# [5] [3]
# [2, 8] [3, 5] # merge these two array: exam them from index 0, find smaller 2, append
# it, only increment i, compare 8>3, them increment j, compare 8>5, then increment j, 
# now arr2 is finished, attach remain of arr1, which is 8
# [9] [4]
# [1] [7]
# [4, 9] [1, 7]
# [2, 3, 5, 8] [1, 4, 7, 9]
# [1, 2, 3, 4, 5, 7, 8, 9]
```

## 2. QuickSort Worst: O(n^2) Average: O(nlogn)
### arr = [4,1,7,8,3,5,9] 
### Method: Pivot element: items on the left are smaller, items on the right are larger. Set first element to pivot, then use partition function to put pivot to correct position.

![6](https://user-images.githubusercontent.com/37478093/88377847-7ea83300-cdd2-11ea-8fc8-8ed6a121623c.png)

```
def quicksort(arr):
    quicksort2(arr, 0, len(arr)-1)
    return arr

def quicksort2(arr, left, right):
    if(left < right): # if more than two element
        pivotIndex = partition(arr, left, right)
        quicksort2(arr, left, pivotIndex - 1)
        quicksort2(arr, pivotIndex + 1, right)
        print(arr)
    
def partition(arr, left, right): # the process to find position of pivot element
    border = left # border is last element of left partition
    pivot = arr[border] # choose first element to pivot 
    for i in range(left+1,right+1):
        if(arr[i] > pivot):
            continue
        else:
            border+=1
            arr[border], arr[i] = arr[i], arr[border]
    arr[border], arr[left] = arr[left], arr[border]
    return border

arr = [4,1,7,8,3,5,9]  
quicksort(arr)

# [3, 1, 4, 8, 7, 5, 9] # after first partition, pivot is 4
# [1, 3, 4, 8, 7, 5, 9] # after partition left side, pivot is 3
# [1, 3, 4, 5, 7, 8, 9] # after partition right side, pivot is 8
# [1, 3, 4, 5, 7, 8, 9] # left side is done, partition [5, 7]
# [1, 3, 4, 5, 7, 8, 9] # done
```
```
# see how does partition work?
arr = [4,1,7,8,3,5,9]    
def partition(arr, left, right):
    border = left # border is last element of left partition
    pivot = arr[border] # choose first element 4 to pivot 
    for i in range(left+1,right+1):
        print(i, arr)
        if(arr[i] > pivot):
            continue
        else:
            border+=1
            arr[border], arr[i] = arr[i], arr[border]
    arr[border], arr[left] = arr[left], arr[border] # put pivot to border position
    return border # index of pivot

partition(arr, 0, 6)
print(arr)

# 1 [4, 1, 7, 8, 3, 5, 9] 1<pivot, border=1, 1 swap with arr[border]=1,self
# 2 [4, 1, 7, 8, 3, 5, 9] 7>pivot, do nothing
# 3 [4, 1, 7, 8, 3, 5, 9] 8>pivot, do nothing
# 4 [4, 1, 7, 8, 3, 5, 9] 3<pivot, border=2, 3 swap with arr[border]=7
# 5 [4, 1, 3, 8, 7, 5, 9] 5>pivot, do nothing
# 6 [4, 1, 3, 8, 7, 5, 9] 9>pivot, do nothing
# [3, 1, 4, 8, 7, 5, 9]
```

## 3. Selection sort O(n^2)
### arr = [2,5,1,8,9,4]
### Method: Select min element on right side of i, if min is smaller than arr[i] then swap the min with arr[i], else arr[i] is in correct position

```
def selectionSort(arr):
    n = len(arr)
    for i in range(n-1):
        print(i, arr)
        indexOfMin = i
        for j in range(i+1, n):
            if arr[j] < arr[indexOfMin]:
                indexOfMin = j
        arr[indexOfMin], arr[i] = arr[i], arr[indexOfMin] # swap
    return arr

arr = [2,5,1,8,9,4]
selectionSort(arr)

# 0 [2, 5, 1, 8, 9, 4] i=0, find min from [5,1,8,9,4], find 1<2, swap 1 with arr[0]=2
# 1 [1, 5, 2, 8, 9, 4] i=1, find min from [2,8,9,4] find 2<5, swap 2 with arr[1]=5
# 2 [1, 2, 5, 8, 9, 4] i=2, find min from [8,9,4] find 4<5, swap 5 with arr[2]=5
# 3 [1, 2, 4, 8, 9, 5] i=3, find min from [9,5] find 5<8, swap
# 4 [1, 2, 4, 5, 9, 8] i=4, find min from [8] find 8<9, swap

# [1, 2, 4, 5, 8, 9]
```

## 4. Bubble sort O(n^2)
### arr = [2,5,1,8,9,4]
### Bubble: Bubble(largest value float to right side)
```
# do following one time one bubble will float to the end
# for k in range(n-1):
#     if arr[i] > arr[i+1]:
#         # swap
#         arr[k], arr[k+1] = arr[k+1], arr[k] 

# O(n^2)
arr = [2, 5, 1, 8, 9, 4]
def bubbleSort(arr):
    n = len(arr)
    for i in range(n-1):
        for k in range(n-i-1):
            if arr[k] > arr[k+1]:
                # swap
                arr[k], arr[k+1] = arr[k+1], arr[k] 
        print(i, arr)
bubbleSort(arr)
# [2, 5, 1, 8, 9, 4] push 9 to the end
# [2, 1, 5, 8, 4, 9] push 8 in front of 9
# [1, 2, 5, 4, 8, 9] push 5 in front of 8
# [1, 2, 4, 5, 8, 9] already sorted
```

