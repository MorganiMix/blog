---
title: 'Writing an algorithm to determine if a number is happy using Python'
author: Morgan Ho
date: '2025-06-13'
---

# Leetcode
Leetcode is an interview question bank for coding, which appears in varius tech companies. Today I will share how I tackle one of the questions. 

# The question
The question asks me to write an algorithm to determine if a number is happy. A happy number is a number defines by the following process:

1. Starting with any positive integer, replace the number by the sum of the squares of its digits.
2. Repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1.
3. Those numbers for which this process ends in 1 are happy.

In short, write some code that returns true if n is a happy number, and false if not.

Example 1:
    Input: n = 19
    Output: true
    Explanation:
    1^2 + 9^2 = 82
    8^2 + 2^2 = 68
    6^2 + 8^2 = 100
    1^2 + 0^2 + 0^2 = 1

Example 2:
    Input n = 2
    Output: false

# My approach to the problem
Let's start out with something easy. First, I create a variable 'total' to calculate the sum of the squares of its digits for 1 iteration.

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        total = 0
        # find the number of digits of a number.
        length = len(str(n)) 
        # do a for loop for the amount of times equal to the digits a number has.
        for i in range (length):
            # a number with modulus 10 is the last digit. Square it.
            total += (n%10)**2
            # integer division by 10 to find the second last digit, third last and so on.
            n = n//10
        n = total
```

I have used 'total' to store the first process of summation of squaring all the digits. However, we need to repeat the process. Using another for loop to repeat it 10 times first and view the results using print(). It will be changed to while loop after conditions of breaking the loop is set.

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        # repeat 10 times as placeholder
        for j in range(10):
            total = 0
            # find the number of digits of a number.
            length = len(str(n)) 
            # do a for loop for the amount of times equal to the digits a number has.
            for i in range (length):
                # a number with modulus 10 is the last digit. Square it.
                total += (n%10)**2
                # integer division by 10 to find the second last digit, third last and so on.
                 = n//10
            # repeat the same process with previous result 
            n = total
            print(total)
```

Then, I add a flag to show if a number is happy number. It starts with False and change to true if total equals to 1. 

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        ishappynumber = False
        # repeat 10 times as placeholder
        for j in range(10):
            total = 0
            # find the number of digits of a number.
            length = len(str(n)) 
            # do a for loop for the amount of times equal to the digits a number has.
            for i in range (length):
                # a number with modulus 10 is the last digit. Square it.
                total += (n%10)**2
                # integer division by 10 to find the second last digit, third last and so on.
                 = n//10
            # repeat the same process with previous result
            n = total
            print(total)
            if total == 1:
                ishappynumber = True
                break
        return ishappynumber
```

Writing a break condition if a number is not happy is more challenging. Most online solutions will use an if statement for n<10 because only 1 or 7 will return happy number. To me, the code should be making calculation for any number 'n', not just hardcoding logic for all numbers under 10. Therefore, my method will check if the number (not equal to 1) has appeared on the list of totals repeatedly. If so, the number is unhappy and the while loop is broken.

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        ishappynumber = False
        # initialise the list of totals 
        recordtotal = []
        # repeat 10 times as placeholder
        for j in range(10):
            total = 0
            # find the number of digits of a number.
            length = len(str(n)) 
            # do a for loop for the amount of times equal to the digits a number has.
            for i in range (length):
                # a number with modulus 10 is the last digit. Square it.
                total += (n%10)**2
                # integer division by 10 to find the second last digit, third last and so on.
                 = n//10
            # repeat the same process with previous result
            n = total
            print(total)
            if total == 1:
                ishappynumber = True
                break
            if total in recordtotal:
                break
            recordtotal.append(total)
        return ishappynumber
```

Although it is slower for the program to calculate if a number is happy, it is less hard coded and shows results based on calculation.