---
layout: post
title: "Advent of code"
categories: journal
---

### Attempt at Advent of code
#### Day 1 :
Check the two numbers that add up to 2020 and then return their product
initial thoughts are that to use to do a search of the whole list and to find two numbers that add up to 2020 to manually find their product But i do think there is a better way to do this
The method i opted was to go over the list twice to find the number that add up to 2020 and break the loop.
I saved the data provided to a file and then processed this file using python and this was fairly simple if you are familiar with file operations. 
```python
with open('./adventcode') as f:
        #rstip to remove the white spaces and splitlines to remove the /n 
        read_data = f.read().rstrip().splitlines()
        for num in read_data:
            for num1 in read_data:
                    if int(num) + int(num1) == 2020:
                            print(int(num)*int(num1))
                            break
```
#### Day 2:
calculate the number of valid passwords that are present in the corpus.
String manipulation is required to complete the task
```python
with open('./input.txt') as f:
    valid_pass = 0
    for line in f:
        length , letter, word = line.split()
        count = word.count(letter[0])
        left , right = length.split('-')
        if (count>=int(left)) & (count<=int(right)):
            valid_pass+=1
print(valid_pass)
```
learning operator precedence matters a lot and i got a wrong answer because of this which i then figured out the reason

##### Task2 :
Just a slight modification on the previous algorithm . Just taking the index to check the position


#### Day3:
Given the task of calculating the trees it was simple enough to implement the below code

```python
    with open('./input.txt') as f:
        #to go down one line at a time
        for line in f:
            y = y%(len(line)-1)
            if line[y]== "#":
                trees+=1
            #go left 3 positions
            y+=3
```
For the part two it was just running this multiple lines over different combination of slopes 

```python
count=1
    slopes = [(1,1),(3,1),(5,1),(7,1),(1,2)]
    #Open the file stored as input 
    for y_i , x_i in slopes:
        trees=0
        y=0
        i=0
        with open('./input.txt') as f:
            #to go down one line at a time
            for line in f:
                if x_i == 2:
                    if i%x_i!=0:
                        i+=1
                        continue
                    i+=1
                y = y%(len(line)-1)
                if line[y]== "#":
                    trees+=1
                #go left 3 positions
                y+=y_i
        count*= trees
```
#### Day4:

The first part of the passport processing was thinking about how to store all the data from the input file and then processing it. This was rather simple compared to the second task.
I do believe theres a better way to do this.
For the task two however i had to employ regular expressions and this took some time to study them and see how they work in python and i was still struggling with the right terminologies.

I had to reiterate the code multiple times to get the right output. 
Had to clear the confusion about the atmost and atleast concepts 

After all the effort i still was not able to get the write answer and took the help of the reddit community. This was where i kind enough person found out there was  a bug in the code i was parsing the in and cm but not checking the case where they are completely missing .

#### Day5:

This was a brezze compared to the mess of day4 , i just had to think about two functions that calculated the row and col number and then repeatadly passing in the values i got the id

For the function i did take some iterations to get it right. I am still skepticall as to how this works(edge cases) but it sure does work.

#### Day5:

Both the tasks were simple once i thought of a way to process them and bless the fuction intersections in the data structure sets (python) with out this it would be a complicated task


### Day 7:
Well this was one challege as i had never worked on regression and looking at the problem i kinda knew i needed recurssion but i so wish i didnt as i am not confident with it . BUt this gave me an oputunity to work on my skills of recurssio which it so desperately needed.

The first thing was trying to understand the problem and to think of a way to represent the data that was presented and then i finally seleteled at a dict with in a dict approach which basically ment that i have a dictionaty to represent the different bags that are presetn the outermost bag and then repersent inner bags wihtin this bag as a dict with keys as the name and number of bags as  a value , i used regular expressions to filter out what was required and i dont know what i would do with out the regular expressioins.

After the first task of representing the data as required it was really important to think how will i find the way to counnt all the occurance to do so.

This finally came up to using regressions and this was the only way out.

Inital thought was to to go through the list and if the dict didnt have the bag go through the dicts of the bags within one by one , basically getting a false everytime unless the bag was found then it would return a true

```python
def countCal(currentbag, bags):
    if currentbag in bags.keys():
        if "shiny gold" in bags[currentbag].keys():
            return True
        else :
            for bag in bags[currentbag].keys():
                if countCal(bag, bags):
                    return True
    else:
        return False
```