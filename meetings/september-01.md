# Problem Strings: Sherlock and the Valid String

[Link to the problem](https://www.hackerrank.com/challenges/sherlock-and-valid-string/)


## Approach using python

**Data Structure used:** Dictionary and List

**Complexity:** O(n)

**Explanation:**

We had a few different scenarios, the easiest one is that the letters' frequency of appearance are all the same. So we should return YES. 

The second one it's when the difference between the highest and the lowest number of ocurrency is 1 and there is only one letter with the highest number. It means there is only one extra letter, so we return YES.

The third and last scenario it's when the diffent that we spoke is one, then remove this letter, and check whether all the other counts are the same, if so we return YES, otherwise we return NO.



```py
def create_dictionay(collection):
    dic_result = {}
    for element in collection:
        if element in dic_result:
            dic_result[element] = dic_result[element] + 1 
        else:
            dic_result[element] = 1
    return dic_result

# Complete the isValid function below.
def isValid(s):
    
    count_occ = create_dictionay(s)
    freq = list(count_occ.values())

    if(max(freq) - min(freq) == 0): return "YES"
    
    if(max(freq) - min(freq) == 1 and freq.count(max(freq)) == 1):
        return "YES"

    if(freq.count(min(freq)) == 1):
        freq.remove(min(freq))
        
        if(max(freq) - min(freq) ==0):
            return "YES
        else:
            return "NO"
    else:
        return "NO"

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