#Had Had Had - 200
Eve and Eva were in class. They both tried to describe a man that was once sick. Eve said "The man had a cold." Eva said "The man had had a cold." According to English grammar, Eva was correct.

Now imagine their two teachers, Bill and Bob: Bob was a little off, and said that "Eve, while Eva had had 'had had', had had 'had'; 'had' had had the better grammar." Bill corrected him, saying "Eva, while Eve had had 'had', had had 'had had'; 'had had' had had the better grammar."

Continuing this pattern, the knowledgeable supervisor would note that "Bill, while Bob had had 'had had had had had had had had had had', had had 'had had had had had had had had had had had'; 'had had had had had had had had had had had' had had the better grammar."

Continuing this, how many 'had's would be in the incorrect 100th iteration?

```python
incorrect_had=0
correct_had=0
had_i=1
had_c=2
x=0
while x<99:
    incorrect_had=had_i*2+had_c+6
    correct_had=had_c*2+had_i+6
    had_i=incorrect_had
    had_c=correct_had
    x+=1
print incorrect_had
print correct_had
```

flag: 773066281098016996554691694648431909053161282998

