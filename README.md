## Welcome to Peter Jung's Algorithm Notes

This is a [news site](https://www.bbc.com/) that I always go to. 


### Stacks and Queues 

Stack is a container of objects that are inserted and removed according to the last-in first-out (LIFO) principle.

Queue is a container of objects (a linear collection) that are inserted and removed according to the first-in first-out (FIFO) principle.

```Python
#using python 

class Stack(list):
    push = list.append
    def peek(self):
        return self[-1]
    #pop is already a built in function in python

class Queue(list):
    put = list.append
    def peek(self):
        return self[0]
    def get(self):
        return self.pop(0)
```

### 주식가격 

![image](https://user-images.githubusercontent.com/88238335/134834037-7fb286ca-8c5a-4fca-bb31-cbbd28f99a0d.png)

```Python
#using python 

def solution(prices):

    #add zeros to results
    
    result=[0 for x in range(len(prices))]
    
    #go through each element and the one after to see if there was a drop in prices
    #if there was a drop break if not add more seconds to result
    
    for i in range(len(prices)):
        for j in range(i+1,len(prices)):
            if prices[i]<=prices[j]:
                result[i]+=1
            else:
                result[i]+=1
                break
    return result
```

### 기능개발

![image](https://user-images.githubusercontent.com/88238335/134906335-438873f7-2f7d-4b49-94d4-baf5e0557367.png)

```Python
import math

def solution(progresses, speeds):
    result = []
    timeleft = []
    counter = 1
    
    #Appends the time needed to finish the progress to timeleft
    
    for i in range(len(progresses)):
        timeleft.append(math.ceil(  (100 - progresses[i] ) / speeds[i]))
        
    # pop the list of timeleft and see if the time after has less time to completion and add 1 to counter
    
    first = timeleft.pop(0)
    
    while len(timeleft) > 0:
        if first >= timeleft[0]:
            counter += 1
            timeleft.pop(0)
        else:
            result.append(counter)
            first = timeleft.pop(0)
            counter = 1
    result.append(counter)
    return result
```
