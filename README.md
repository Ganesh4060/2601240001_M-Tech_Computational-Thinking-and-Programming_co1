# Divide and Conquer

## 5. Merge Two Sorted Data Sources

Two departments have separately sorted employee lists. You need one completely sorted list.

### Question

How can the merge step of Merge Sort be useful in this scenario?

### Solution

According to the scenario, the merge step of Merge Sort can be used to combine two separately sorted employee lists into one completely sorted list.

### Merge Step of Merge Sort

The merge step compares the elements of two sorted lists and selects the smaller element one by one.

Since both lists are already sorted, there is no need to sort them again. We simply compare the current elements of both lists and add the smaller one to the result.

### Example

Imagine that two departments have separately sorted employee IDs.

**Department A:**

101, 105, 120, 150

**Department B:**

103, 110, 130, 140

We need to combine both lists into one completely sorted employee list.

### 1. Initialize

Create an empty result list and two pointers.

```text
result = []

i = 0
j = 0
```

Here:

* `i` points to the current element of Department A.
* `j` points to the current element of Department B.

**Department A:**

101, 105, 120, 150
↑
i

**Department B:**

103, 110, 130, 140
↑
j

### 2. Compare

Compare the first elements.

**A[i] = 101**

**B[j] = 103**

Since:

**101 < 103**

Therefore, add `101` to the result.

```text
result = [101]
```

Move `i` to the next element.

---

Now compare:

**105 and 103**

Since:

**103 < 105**

Add `103`.

```text
result = [101, 103]
```

Move `j` to the next element.

---

Again compare:

**105 and 110**

Since:

**105 < 110**

Add `105`.

```text
result = [101, 103, 105]
```

Move `i`.

---

Again compare:

**120 and 110**

Since:

**110 < 120**

Add `110`.

```text
result = [101, 103, 105, 110]
```

Move `j`.

---

### 3. Continue

Continue comparing the current elements.

**120 and 130**

Since:

**120 < 130**

Add `120`.

```text
result = [101, 103, 105, 110, 120]
```

---

**150 and 130**

Since:

**130 < 150**

Add `130`.

```text
result = [101, 103, 105, 110, 120, 130]
```

---

**150 and 140**

Since:

**140 < 150**

Add `140`.

```text
result = [101, 103, 105, 110, 120, 130, 140]
```

---

### 4. Add Remaining Element

Now Department B has no remaining elements.

Department A still has:

```text
150
```

So, add `150` to the result.

```text
result = [101, 103, 105, 110, 120, 130, 140, 150]
```

Therefore:

**101, 103, 105, 110, 120, 130, 140, 150**

is the completely sorted employee list.

# Algorithm

### Input

* Sorted list `a`
* Sorted list `b`

### Steps

1. Create an empty list `result`.
2. Set `i = 0`.
3. Set `j = 0`.
4. While both lists have elements:

   * Compare `a[i]` and `b[j]`.
   * If `a[i] < b[j]`, add `a[i]` to `result`.
   * Increase `i` by 1.
   * Otherwise, add `b[j]` to `result`.
   * Increase `j` by 1.
5. Add all remaining elements of `a` to `result`.
6. Add all remaining elements of `b` to `result`.
7. Return the completely sorted list.

# Python Implementation

```python
def merge_lists(a, b):
    result = []
    i = 0
    j = 0

    while i < len(a) and j < len(b):
        if a[i] < b[j]:
            result.append(a[i])
            i += 1
        else:
            result.append(b[j])
            j += 1

    result.extend(a[i:])
    result.extend(b[j:])

    return result


# Two sorted employee lists
a = [101, 105, 120, 150]
b = [103, 110, 130, 140]

result = merge_lists(a, b)

print(result)
```

# Output

```text
[101, 103, 105, 110, 120, 130, 140, 150]
```

# Time Complexity

### Worst Case

**O(n + m)**

Where:

* `n` = number of elements in list `a`
* `m` = number of elements in list `b`

Every element from both lists is processed once.

### Best Case

**O(n + m)**

The merge operation still needs to process the elements of the two lists.

# Space Complexity

**O(n + m)**

The `result` list stores all elements from both input lists.

# Why This is Divide and Conquer

Merge Sort uses the following approach:

```text
Divide
   ↓
Sort the smaller parts
   ↓
Merge the sorted parts
   ↓
One completely sorted list
```

In this scenario, the two departments have **already sorted lists**, so we directly use the **merge step** to combine them efficiently.

```text
Department A          Department B
[101,105,120,150]    [103,110,130,140]
         \                  /
          \                /
               Merge
                 ↓
[101,103,105,110,120,130,140,150]
```

