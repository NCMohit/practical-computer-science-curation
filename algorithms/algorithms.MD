# Algorithms

## Searching Algorithms

### Linear Search ( O ( N ) )
```python
def linear_search(value,array):
    for i in range(len(array)):
        if(array[i]==value):
            return i
    return None
```

### Binary Search ( O ( log N ) )
```python
def binary_search(value,array):     
    left = 0
    right = len(array)
    while(left < right):
        mid = int((left+right)/2)
        if(array[mid] == value):
            return mid
        if(array[mid] < value):
            left = mid + 1
        elif(array[mid] > value):
            right = mid
    return None
```

## Sorting Algorithms

### Bubble Sort ( O ( N<sup>2</sup> ) )
```python
def bubble_sort(arr):
    for j in range(len(arr)-1,0,-1):
        for i in range(j):
            if(arr[i]>arr[j]):
                temp = arr[j]
                arr[j] = arr[i]
                arr[i] = temp
    return arr
```

### Insertion Sort ( O ( N<sup>2</sup> ) )
```python
def insertion_sort(arr):
    for i in range(1,len(arr)):
        pointer = i
        while((pointer>0) & (arr[pointer]<arr[pointer-1])):
            temp = arr[pointer-1]
            arr[pointer-1] = arr[pointer]
            arr[pointer] = temp
            pointer -= 1
    return arr
```

### Selection Sort ( O ( N<sup>2</sup> ) )
```python
def selection_sort(arr):
    for i in range(1,len(arr)):
        min_index = i
        for j in range(i,len(arr)):
            if(arr[min_index]>arr[j]):
                min_index = j
        if(arr[i-1]>arr[min_index]):
            temp = arr[min_index]
            arr[min_index] = arr[i-1]
            arr[i-1] = temp
    return arr
```

### Merge Sort ( O ( N * Log(N) ) )
```python
def merge(arr1,arr2):
    i=0
    j=0
    final_arr = []
    while((i<len(arr1)) | (j<len(arr2))):
        if(i<len(arr1)):
            if(j<len(arr2)):
                if(arr1[i]<arr2[j]):
                    final_arr.append(arr1[i])
                    i+=1
                else:
                    final_arr.append(arr2[j])
                    j+=1
            else:
                final_arr.append(arr1[i])
                i+=1
        else:
            final_arr.append(arr2[j])
            j+=1
    return final_arr

def merge_sort(arr):
    if(len(arr)<=1):
        return arr
    mid = int(len(arr)/2)
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left,right)
```