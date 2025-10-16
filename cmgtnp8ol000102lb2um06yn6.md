---
title: "Linear Search and Binary Search – A Complete Guide"
datePublished: Thu Oct 16 2025 16:50:55 GMT+0000 (Coordinated Universal Time)
cuid: cmgtnp8ol000102lb2um06yn6
slug: linear-search-and-binary-search-a-complete-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1760633368578/5411dd99-09e6-44d5-bed1-096d2c5e510c.png
tags: algorithms, data-structures, linearsearch, binary-search-algorithm, linear-search-algorithm

---

Searching is one of the most common operations in computer science. Whenever we want to find a specific element in a list, array, or dataset, we use a search algorithm. The two most common search algorithms are **Linear Search** and **Binary Search**. In this article, we will explain both in detail, their working principles, and when to use each.

## <mark>01.Linear Search</mark>

Linear Search, also called **Sequential Search**, is the simplest method of searching. It works by checking **each element of a list one by one** until the desired element (called the **key**) is found or the end of the list is reached.

Suppose we have an array and we want to find key = 9

```java
int[] arr = [3, 7, 1, 9, 5]
```

**Steps:**

1. Start at the first element (`arr[0] = 3`). Compare it with the key.
    
2. If it matches, return the index. If not, move to the next element.
    
3. Repeat step 2 until the key is found or the array ends.
    

For our example:

* Compare 3 → Not equal
    
* Compare 7 → Not equal
    
* Compare 1 → Not equal
    
* Compare 9 → Match found at index 3
    

So, the result is **index 3**.

```java
class LinearSearch {
    public static int linearSearch(int arr[], int key) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == key) {
                return i;
            }
        }
        return -1; // key not found
    }

    public static void main(String[] args) {
        int arr[] = {3, 7, 1, 9, 5};
        int key = 9;

        int result = linearSearch(arr, key);
        if (result != -1) {
            System.out.println("Element found at index " + result);
        } else {
            System.out.println("Element not found");
        }
    }
}
```

> * **Sequential checking:** Every element is compared until a match is found.
>     
> * **Works on unsorted data:** Linear search does not require sorted arrays.
>     
> * **Simple to implement:** No extra data structures are needed.
>     

### Time Complexity & Space Complexity

| Case | Time Complexity |
| --- | --- |
| Best Case | O(1) – key found at first element |
| Average Case | O(N/2) – on average, half of elements checked |
| Worst Case | O(N) – key not present or at last element |

**Space Complexity:** O(1) – no extra memory used.

In standard linear search, we check every element without considering previous searches. However, if certain elements are accessed frequently, we can optimize search performance using **two methods**:

1. Transposition
    
2. Move to Front
    

<mark>Transposition</mark>

When a key element is found, swap it with the element just before it. Over time, frequently accessed elements move closer to the start, reducing average search time.

```plaintext
arr = [2, 5, 7, 1, 6, 4, 5, 8, 3, 7]
key = 4
```

* First search: key 4 found at index 5 → swap with index 4  
    → Array becomes `[2, 5, 7, 1, 4, 6, 5, 8, 3, 7]`
    
* Next search: key 4 found at index 4 → swap with index 3  
    → Array becomes `[2, 5, 7, 4, 1, 6, 5, 8, 3, 7]`
    

**Benefits:** Frequently accessed elements move closer to the front, improving average search time.

<mark>Move to Front (or Head)</mark>

When a key element is found, move it directly to index 0. This ensures that future searches for the same element take **constant time O(1)**.

```plaintext
arr = [2, 5, 7, 1, 6, 4, 5, 8, 3, 7]
key = 4
```

* Key 4 found at index 5 → swap with index 0  
    → Array becomes `[4, 5, 7, 1, 6, 2, 5, 8, 3, 7]`
    
* Future searches for 4 take only 1 comparison.
    

## <mark>02.Binary Search</mark>

Binary Search is a faster search algorithm used for **sorted arrays**. It works by **repeatedly dividing the search space in half** and comparing the key with the middle element.

Suppose we have sorted array and we want to find key = 7

```plaintext
arr = [1, 3, 5, 7, 9, 11]
```

* Find the middle element.  
    Mid index = `(low + high)/2` → `mid = 2` → `arr[2] = 5`
    
* Compare mid with key:
    
    * If `key == mid` → return index
        
    * If `key < mid` → search left half
        
    * If `key > mid` → search right half
        
* Repeat until key is found or search space is empty.
    

<mark>Binary Search Algorithm (Iterative Method)</mark>

```java
class BinarySearchExample {
    static int binarySearch(int arr[], int x) {
        int low = 0, high = arr.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            // If x is present at mid
            if (arr[mid] == x)
                return mid;

            // If x greater, ignore left half
            if (arr[mid] < x)
                low = mid + 1;

            // If x smaller, ignore right half
            else
                high = mid - 1;
        }

        // Element not found
        return -1;
    }

    public static void main(String[] args) {
        int arr[] = {2, 3, 4, 10, 40};
        int x = 10;
        int result = binarySearch(arr, x);
        
        if (result == -1)
            System.out.println("Element not found");
        else
            System.out.println("Element found at index " + result);
    }
}
```

<mark>Recursive Binary Search Algorithm</mark>

In this version, the function calls itself until the element is found or the search range becomes empty.

```java
class BinarySearchRecursive {
    static int binarySearch(int arr[], int low, int high, int x) {
        if (high >= low) {
            int mid = low + (high - low) / 2;

            if (arr[mid] == x)
                return mid;
            if (arr[mid] > x)
                return binarySearch(arr, low, mid - 1, x);
            
            return binarySearch(arr, mid + 1, high, x);
        }
        return -1;
    }

    public static void main(String[] args) {
        int arr[] = {2, 3, 4, 10, 40};
        int x = 10;
        int result = binarySearch(arr, 0, arr.length - 1, x);

        if (result == -1)
            System.out.println("Element not found");
        else
            System.out.println("Element found at index " + result);
    }
}
```

> * **Divide and Conquer:** Each step halves the search space.
>     
> * **Requires sorted data:** Ascending or descending arrays.
>     
> * **Two approaches:** Iterative and Recursive.
>     
> * **Efficient for large datasets:** Very fast compared to linear search.
>     

### Time and Space Complexity of Binary Search

| Case | Time Complexity |
| --- | --- |
| Best Case | O(1) – element at mid |
| Average Case | O(log N) |
| Worst Case | O(log N) |

#### **Understanding log₂N**

* **log₂N** tells us **how many times we can divide the array by 2** until we reach 1 element.
    
* **Example:** Array of size 8 → `[1,3,5,7,9,11,13,15]`
    
    * Step 1: 8 → 4 elements
        
    * Step 2: 4 → 2 elements
        
    * Step 3: 2 → 1 element
        
    * Steps needed = 3 → **log₂8 = 3**
        
* Even for large arrays, log₂N grows slowly:
    
    * N = 1024 → log₂1024 = 10
        
    * N = 1,048,576 → log₂1,048,576 = 20
        

#### **Space Complexity**

* **Iterative binary search:** O(1) → uses only a few variables (`low`, `high`, `mid`).
    
* **Recursive binary search:** O(log N) → each recursive call is stored in the **stack**.
    

Searching is one of the most important operations in programming and data structures.

* **Linear search** is simple and works on unsorted arrays, but its time complexity is O(N), which makes it slower for large datasets. Improved techniques like **transposition** and **move-to-front** can optimize repeated searches by reducing average search time.
    
* **Binary search** is a highly efficient method for **sorted arrays**, with a time complexity of O(log N). By dividing the search space in half at each step, it quickly locates the target element even in very large arrays. Iterative implementations use constant space, while recursive implementations use O(log N) space due to the function call stack.
    

Choosing the right search algorithm depends on the **type and size of the dataset**. For small or unsorted data, linear search is sufficient, while binary search is ideal for large, sorted datasets.