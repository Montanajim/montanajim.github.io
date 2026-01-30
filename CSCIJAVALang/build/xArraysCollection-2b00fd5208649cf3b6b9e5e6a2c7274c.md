# Arrays Collection



The `java.util.Arrays` class is a utility class that provides numerous static methods for working with arrays in Java. These methods help with common operations such as sorting, searching, comparing, and filling arrays. Below is an overview of the most commonly used methods, along with code examples that demonstrate how they work.

------

## 1. `toString()` and `deepToString()`

### `Arrays.toString()`

- **Purpose**: Returns a string representation of the contents of a one-dimensional array.
- **Usage**: Works on arrays of any reference or primitive type (e.g., `int[]`, `String[]`).

**Example**:

```java
import java.util.Arrays;

public class ToStringExample {
    public static void main(String[] args) {
        int[] intArray = {1, 2, 3, 4, 5};
        System.out.println(Arrays.toString(intArray));
        // Output: [1, 2, 3, 4, 5]
    }
}
```

### `Arrays.deepToString()`

- **Purpose**: Returns a string representation of the contents of a multi-dimensional array (e.g., `int[][]` or `String[][]`).
- **Usage**: Recursive approach that handles nested arrays.

**Example**:

```java
import java.util.Arrays;

public class DeepToStringExample {
    public static void main(String[] args) {
        int[][] int2DArray = {
            {1, 2, 3},
            {4, 5, 6}
        };
        System.out.println(Arrays.deepToString(int2DArray));
        // Output: [[1, 2, 3], [4, 5, 6]]
    }
}
```

------

## 2. `sort()`

- **Purpose**: Sorts the array into ascending order based on natural ordering.
- **Overloads**: There are multiple overloads of `sort()` for different data types (`int[]`, `double[]`, `Object[]`, etc.), as well as range-based sorts (e.g., `sort(array, fromIndex, toIndex)`).

**Example (Primitive array sort)**:

```java
import java.util.Arrays;

public class SortExample {
    public static void main(String[] args) {
        int[] numbers = {5, 2, 8, 1, 3};
        Arrays.sort(numbers);
        System.out.println(Arrays.toString(numbers));
        // Output: [1, 2, 3, 5, 8]
    }
}
```

**Example (Object array sort)**:

```java
import java.util.Arrays;

public class SortStrings {
    public static void main(String[] args) {
        String[] fruits = {"Apple", "Mango", "Banana", "Cherry"};
        Arrays.sort(fruits);
        System.out.println(Arrays.toString(fruits));
        // Output: [Apple, Banana, Cherry, Mango]
    }
}
```

**Example (Range-based sort)**:

```java
import java.util.Arrays;

public class RangeSortExample {
    public static void main(String[] args) {
        int[] numbers = {5, 2, 8, 1, 3, 10, 7};
        // Sort only the subarray from index 1 (inclusive) to index 4 (exclusive).
        Arrays.sort(numbers, 1, 4);
        System.out.println(Arrays.toString(numbers));
        // Output: [5, 1, 2, 8, 3, 10, 7]
    }
}
```

------

## 3. `binarySearch()`

- **Purpose**: Searches a sorted array for a given element using the binary search algorithm.

- **Precondition**: The array **must be sorted** for binary search to work correctly.

- Return value

  :

  - If the element is found, returns its index.
  - Otherwise, returns a negative value (the “insertion point” - 1).

**Example**:

```java
import java.util.Arrays;

public class BinarySearchExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 5, 8, 10};
        // Must be sorted before calling binarySearch
        int index = Arrays.binarySearch(numbers, 5);
        System.out.println("Index of 5: " + index);
        // Output: Index of 5: 3

        int missingIndex = Arrays.binarySearch(numbers, 7);
        System.out.println("Index of 7: " + missingIndex);
        // Output: Index of 7: -5 (negative number indicating "insertion point" - 1)
    }
}
```

------

## 4. `fill()`

- **Purpose**: Assigns the specified value to each element of the array (or subrange).
- **Overloads**: Similar to `sort()`, there are multiple overloads to handle different data types and subranges.

**Example**:

```java
import java.util.Arrays;

public class FillExample {
    public static void main(String[] args) {
        int[] numbers = new int[5];
        Arrays.fill(numbers, 10);
        System.out.println(Arrays.toString(numbers));
        // Output: [10, 10, 10, 10, 10]

        // Fill a subrange
        Arrays.fill(numbers, 1, 4, 7);
        System.out.println(Arrays.toString(numbers));
        // Output: [10, 7, 7, 7, 10]
    }
}
```

------

## 5. `copyOf()` and `copyOfRange()`

### `Arrays.copyOf()`

- **Purpose**: Copies the specified array, truncating or padding with default values (if necessary) so the copy has the specified length.

**Example**:

```java
import java.util.Arrays;

public class CopyOfExample {
    public static void main(String[] args) {
        int[] original = {1, 2, 3, 4, 5};
        int[] copy = Arrays.copyOf(original, 3);
        System.out.println(Arrays.toString(copy));
        // Output: [1, 2, 3]
    }
}
```

### `Arrays.copyOfRange()`

- **Purpose**: Copies the specified range of the original array into a new array.
- **Usage**: `Arrays.copyOfRange(originalArray, from, to)` where `from` is inclusive and `to` is exclusive.

**Example**:

```java
import java.util.Arrays;

public class CopyOfRangeExample {
    public static void main(String[] args) {
        int[] original = {1, 2, 3, 4, 5, 6};
        int[] copyRange = Arrays.copyOfRange(original, 2, 5);
        System.out.println(Arrays.toString(copyRange));
        // Output: [3, 4, 5]
    }
}
```

------

## 6. `equals()` and `deepEquals()`

### `Arrays.equals()`

- **Purpose**: Compares two arrays (one-dimensional) for equality. Returns `true` if both arrays have the same length and all corresponding elements are equal.
- **Note**: For objects, it checks using the `.equals()` method on each element. For primitives, it checks their values.

**Example**:

```java
import java.util.Arrays;

public class EqualsExample {
    public static void main(String[] args) {
        int[] arr1 = {1, 2, 3};
        int[] arr2 = {1, 2, 3};
        int[] arr3 = {1, 2, 4};

        System.out.println(Arrays.equals(arr1, arr2)); // true
        System.out.println(Arrays.equals(arr1, arr3)); // false
    }
}
```

### `Arrays.deepEquals()`

- **Purpose**: Compares two multi-dimensional arrays for equality. It checks each element at every nesting level.
- **Usage**: For nested arrays, it recursively checks each nested level.

**Example**:

```java
import java.util.Arrays;

public class DeepEqualsExample {
    public static void main(String[] args) {
        int[][] arr1 = {
            {1, 2, 3},
            {4, 5, 6}
        };
        int[][] arr2 = {
            {1, 2, 3},
            {4, 5, 6}
        };
        int[][] arr3 = {
            {1, 2, 3},
            {4, 5, 7}
        };

        System.out.println(Arrays.deepEquals(arr1, arr2)); // true
        System.out.println(Arrays.deepEquals(arr1, arr3)); // false
    }
}
```

------

## 7. `setAll()` and `parallelSetAll()` (Java 8+)

- **Purpose**: Populates an array by calling the provided generator function for each index. `parallelSetAll()` does this in parallel.
- **Usage**: Useful for programmatically generating array content.

**Example (`setAll`)**:

```java
import java.util.Arrays;
import java.util.function.IntUnaryOperator;

public class SetAllExample {
    public static void main(String[] args) {
        int[] nums = new int[5];
        Arrays.setAll(nums, index -> index * 2);
        System.out.println(Arrays.toString(nums));
        // Output: [0, 2, 4, 6, 8]
    }
}
```

**Example (`parallelSetAll`)**:

```java
import java.util.Arrays;

public class ParallelSetAllExample {
    public static void main(String[] args) {
        int[] nums = new int[5];
        Arrays.parallelSetAll(nums, index -> index * 3);
        System.out.println(Arrays.toString(nums));
        // Output: [0, 3, 6, 9, 12]
    }
}
```

------

## 8. `parallelSort()` (Java 8+)

- **Purpose**: Sorts large arrays in parallel using multiple threads, potentially faster on multi-core systems.
- **Usage**: Similar to `Arrays.sort()` but may improve performance for very large arrays.

**Example**:

```java
import java.util.Arrays;

public class ParallelSortExample {
    public static void main(String[] args) {
        int[] numbers = {5, 2, 8, 1, 3};
        Arrays.parallelSort(numbers);
        System.out.println(Arrays.toString(numbers));
        // Output: [1, 2, 3, 5, 8]
    }
}
```

------

## Summary

- **`Arrays.toString()` / `deepToString()`**: Convert arrays to a readable string.
- **`Arrays.sort()`**: Sort arrays (various overloads, including range sorts).
- **`Arrays.binarySearch()`**: Quickly locate an element in a sorted array.
- **`Arrays.fill()`**: Fill array (or subrange) with a specific value.
- **`Arrays.copyOf()` / `copyOfRange()`**: Create new arrays from existing arrays.
- **`Arrays.equals()` / `deepEquals()`**: Compare arrays for equality (single or multi-dimensional).
- **`Arrays.setAll()` / `parallelSetAll()`**: Programmatically set array elements.
- **`Arrays.parallelSort()`**: Parallel version of sorting, potentially faster on multi-core systems.

The `java.util.Arrays` class offers a robust set of utility methods that streamline many common operations on arrays. Familiarity with these methods can significantly reduce the amount of boilerplate code you need to write and can make your code more efficient and expressive.