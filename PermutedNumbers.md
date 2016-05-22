#Permuted Numbers - 200
For any odd number p, 2 to the power of n mod p is a different value for each n that is at most p-1 and at least 1 (the value of “x mod y” is the same as the remained of x divided by y and is sometimes expressed as “x%y”). The values range from 1 to p - 1. 
For example, when p is 5:
when n is 1: (2 ^ 1) % 5 = 2
when n is 2: (2 ^ 2) % 5 = 4
when n is 3: (2 ^ 3) % 5 = 3
when n is 4: (2 ^ 4) % 5 = 1

This function is called a permutation on (1,2,3,4) as it can be seen as an assignment of each of these numbers to another unique number within the set (ordered as (2, 4, 3, 1) in this case). A permutation can be used for encoding list of integers by running it on each value in the list. We’ve encoded the flag by transforming the character into numbers by their place in the alphabet ( a -> 1, b -> 2, c -> 3, and so on), with “ ” going to 27, and “_” going to 28. We then used the above method with p set to 29.

(23, 24, 2, 23, 1, 10, 2, 26, 28, 23, 1, 5, 3, 13, 11, 1, 24, 2, 13, 16, 1, 23, 27, 1, 4, 13, 3, 2, 18, 1, 2, 6, 23, 3, 13, 1, 2, 7, 7)

```python
n=1
poo=""
a=list()
while n<30:
    a.append(2**n)
    n+=1
b=(23, 24, 2, 23, 1, 10, 2, 26, 28, 23, 1, 5, 3, 13, 11, 1, 24, 2, 13, 16, 1, 23, 27, 1, 4, 13, 3, 2, 18, 1, 2, 6, 23, 3, 13, 1, 2, 7, 7)
n=0
while n<len(b):
    x=0
    while x<len(a) and a[x]%29!=b[n]:
        x+=1
    if x+1!=27 and x+1!=28:   
        poo+=chr(x+97)
    elif x+1==27:
        poo+= " "
    elif x+1==28:
        poo+= "_"
    n+=1
print poo
```

flag: that_wasnt_very_hard_to_break_after_all
