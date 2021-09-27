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

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
