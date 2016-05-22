#Wondrous Numbers - 200
Legend has it that, given an infinite number of steps, you can reduce any given number 'n' to 1 by repeating the following steps:
- If the number is even, divide by two.
- If the number is odd, multiply it by three and add one.
What number between 1 and 100 requires the largest amount of these steps before 1 is reached?

```python
x=2
maxint=0
maxsteps=0
steps=0
while x<100:
    temp=x
    while temp!=1:
        if temp%2==0:
          temp=temp/2
        else:
            temp=3*temp+1
        steps+=1
    if steps> maxsteps:
        maxint=x
        maxsteps=steps
    steps=0
    x+=1
print maxint
```

flag: 97
