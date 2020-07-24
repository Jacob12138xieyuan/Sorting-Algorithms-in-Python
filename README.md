# Sorting-Algorithms-in-Python

# MergeSort O(nlogn) (Divide & conquer)
### arr = [2,8,5,3,9,4,1,7] 
### Divide & conquer, excute recursively, first devide then merge

`
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
`
