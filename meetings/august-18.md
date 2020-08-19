# Problem Strings: Making Anagrams

[Link to the problem](https://www.hackerrank.com/challenges/ctci-making-anagrams/)


## Approach using python

**Data Structure used:** Dictionary

**Complexity:** O(n)

**Explanation:**

We had to loop over two strings of sizes **l** and **w** to create the dictionaries. This process takes O(l) + O(w) of computing time.

After that we had to loop over both dictionaries which in the worst case has the size of the whole alphabetic. Adding more O(l) and O(w) to the ending time complexity.

Resulting:
> O(n) = 2O(l) + 2O(w) + O(1)

Disclaimer:

The data access to retrieve the occurence is considered constant O(1)

```py
def make_dict(a):
    chars = {}
    for l in a:
        if l in chars:
            chars[l] += 1
        else:
            chars[l] = 1
    
    return chars

# Complete the makeAnagram function below.
def makeAnagram(a, b):
    chars_a = make_dict(a)
    chars_b = make_dict(b)
    deletions = 0
    
    for key in chars_a:
        if key in chars_b:
            deletions += abs(chars_a[key] - chars_b[key])
        else:
            #exists in a but not in b
            deletions += chars_a[key]

    for key in chars_b:
        if key not in chars_a:
            #exists in b but not in a
            deletions += chars_b[key]

    return deletions
```

## Approach using go

**Data Structure used:** Array

**Complexity:** O(n)

**Explanation:**

We had to loop over two strings of sizes **l** and **w** to create arrays of ascii representation. This process takes O(l) + O(w) of computing time.

After that we had to loop over both arrays **at the same time** which has the fixed size of 127 (ASCII[a-z]).

Resulting:
> O(n) = O(l) + O(w) + O(127) + O(1)

Disclaimer:

The data access to retrieve the occurence is considered constant O(1).

```go
func makeAnagram(a string, b string) int32 {
    count_a := make([]int, 127)
    count_b := make([]int, 127)
    var r int32

    for _, d := range(a) {
        count_a[int(d)] +=1
    }

    for _, e := range(b) {
        count_b[int(e)] +=1
    }

    for i:= 0; i < 127; i++ {
        r += int32(math.Abs(float64(count_a[i]) - float64(count_b[i])))
    }

    return r
}
```