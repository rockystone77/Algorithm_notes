## Welcome to Peter Jung's Algorithm Notes

This is a [news site](https://www.bbc.com/) that I always go to. 


### Stacks and Queues 

Stack is a container of objects that are inserted and removed according to the last-in first-out (LIFO) principle.

Queue is a container of objects (a linear collection) that are inserted and removed according to the first-in first-out (FIFO) principle.

```markdown
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

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/rockystone77/Algorithm_notes/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
