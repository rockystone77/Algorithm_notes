## Welcome to Peter Jung's Algorithm Notes

This is a [news site](https://www.bbc.com/) that I always go to. 


## Stacks and Queues 

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

## 주식가격 

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

## 기능개발

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
## 다리를 지나는 트럭

![image](https://user-images.githubusercontent.com/88238335/135065874-3bce7aa6-2814-4827-a72e-bca887c72d55.png)


```Python
import math

def solution(bridge_length, weight, truck_weights):
    
    #Add 0s to the bridge as one unit is one second
    bridge = [0]*bridge_length
    time = 0
    finished = 0
    bridge_weight = 0
    while len(bridge) != 0:
        #finished has the weight of the truck when it crossed the bridge and is 0 if there are no trucks
        finished  = bridge.pop(0)
        #update bridge_weight
        bridge_weight -= finished
        #add a second to the clock
        time+=1
        #if there are still trucks waiting
        if truck_weights:
            #make sure the trucks does not go over the weight limit
            if bridge_weight + truck_weights[0] <= weight:
                #get the next truck in queue
                truck = truck_weights.pop(0)
                #update bridge_weight
                bridge_weight += truck
                #update trucks on the bridge
                bridge.append(truck)
            else:
                #if the bridge is full then 0 for no trucks
                bridge.append(0)
    return time
```
## 모의고사

![image](https://user-images.githubusercontent.com/88238335/135083172-5d6b802a-00c1-4523-a9dc-1960cef8d8b8.png)


```Python

def solution(answers):
    #write down the patterns in separate list
    a = [1,2,3,4,5]
    b = [2,1,2,3,2,4,2,5]
    c = [3,3,1,1,2,2,4,4,5,5]
    score = [0, 0, 0]
    result = []
    
    #go through each pattern if it matches with the answer:
    #if true +1 to score
    for idx, answer in enumerate(answers):
        if answer == a[idx%len(a)]:
            score[0] += 1
        if answer == b[idx%len(b)]:
            score[1] += 1
        if answer == c[idx%len(c)]:
            score[2] += 1
            
    #look for who correctly guessed the answers the most
    for idx, scores in enumerate(score):
        if scores == max(score):
            result.append(idx+1)

    return result
    
```

## 소수 찾기

![image](https://user-images.githubusercontent.com/88238335/135207115-f6281f4e-023e-4f7a-ad28-fe268292a167.png)

### There was probably another way than using permutations but I am not smart to do that. 

```Python
#import itertools
import itertools as it

def solution(numbers):
    primes = 0
    b = set()
    #get all possible iterations of the numbers given in "numbers"
    for i in range(1, len(numbers)+1):
        b.update((set(map(''.join, it.permutations(numbers,i)))))
    
    #Change the elements to int
    b = set(map(int, b))
    
    #Go through each number and see if they are prime number
    #If Prime number +1 to prime
    for num in b:
        ans = 0
        if int(num) <= 1:
            continue
        for i in range(1, (num+1)//2+1):
            if num % i == 0:
                ans+=1
        if ans ==1:
            primes += 1
            
    return primes
    
```
## 숫자 카드 2

![image](https://user-images.githubusercontent.com/88238335/135222429-d08c7391-38bb-469f-884a-50c574403b20.png)


```Python

#import collections for easy access to how many a certain card the person has e.g ->  {10:2, 3:2} there is 2 number 10 cards and 2 number 3 cards
#stdin for input of user

from sys import stdin
from collections import Counter

#Read through each input
_ = stdin.readline()
N = stdin.readline().split()
_ = stdin.readline()
M = stdin.readline().split()

#Counter the input
C = Counter(N)

#See if M has cards that we have and print with a space in between. 
print(' '.join(f'{C[m]}' if m in C else '0' for m in M))

    
```
## BFS 와 DFS

![image](https://user-images.githubusercontent.com/88238335/135620390-3a5abf23-303e-4e5a-9ec0-cbe5f57175de.png)

```Python
#import deque because it's O(1) not O(n)
from collections import deque

N, M, V = map(int, input().split())

#Create Graph with size N 
graph = [[0] * (N+1) for i in range(N+1)]

#Set the nodes that are connected to each other
#If they are connected node = 1
for i in range(M):
    node1, node2 = map(int, input().split())
    graph[node1][node2] = graph[node2][node1] = 1

#BFS
def bfs(v):
    found = [v]
    queue = deque()
    queue.append(v)

    while queue:
        test = queue.popleft()
        print(test, end=' ')

        for i in range(len(graph[v])):
            if graph[test][i] == 1 and (i not in found):
                found.append(i)
                queue.append(i)

#DFS
def dfs(v, found= []):
    found.append(v)
    print(v, end= ' ')

    for i in range(len(graph[v])):
        if graph[v][i] == 1 and (i not in found):
            dfs(i, found)



dfs(V)
print()
bfs(V)

    
```

## 바이러스 

![image](https://user-images.githubusercontent.com/88238335/135801475-f14e6025-8d74-4f61-a4d8-995adcae6045.png)

### The program needs to be simple in order for the test to pass (don't know why) the tester compilier probably uses lower version of python lul
```Python
#Use DFS to go through the computers that will be infected
def virus(graph, N):
    counter = 0
    visited = [ 0 for z in range(N+1)]
    stack = []
    stack.append(1)

    while(stack):
        top = stack.pop()
        for i in range(1,N+1):
            if graph[top][i] == 1 and visited[i] == 0:
                visited[i] = 1
                stack.append(i)
                counter += 1
    print(counter -1)

def main():
    N = int(input())
    M = int(input())
    
    #Make a graph for the node
    graph = [[0 for j in range(N+1)] for i in range(N+1)]

    #See if the nodes are connected
    for i in range(M):
        node1, node2  =input().split()
        node1 = int(node1)
        node2 = int(node2)
        graph[node1][node2] = 1 
        graph[node2][node1] = 1

    virus(graph, N)

if __name__ == "__main__":
    main()

    
```

## 타겟 넘버

![image](https://user-images.githubusercontent.com/88238335/135957636-a1f6ba76-123d-4510-9e9a-4310216e9dfc.png)

```Python

def solution(numbers,target):
    answer = dfs(0, numbers,target,0)
    return answer
    


def dfs(idx, numbers,target, value):
    answer = 0
    
    #if the search has gone to the limit which is idx and if the value matches the target add 1 to answer
    if idx == len(numbers):
        if value == target: return 1
        else: return 0
    
    answer += dfs(idx+1, numbers,target, value +numbers[idx])
    answer += dfs(idx+1, numbers,target, value -numbers[idx])
    return answer


    
```

## 팩토리얼 진법

![image](https://user-images.githubusercontent.com/88238335/136123568-6066142b-12e8-4aa3-b218-98f5a01f43bb.png)

### Probably could have done this better but for now it works.

```Python

def main():

    #factorial function
    def factorial(n):
        if n == 1:
            return 1
        return n * factorial(n -1)
    N = 1
    answer1 = []
    while (N != '0'):
        #get input from user
        N = str(input())
        answer = []
        j = []
        j[:0] = N
        #for each first word in N it multiplies it with the factorial of length of N going down in range. 
        for i in range(len(N),0,-1):
            k = j.pop(0)
            answer.append(int(int(k) * factorial(i)))
        if N !='0':
            answer1.append(sum(answer))
    print(*answer1, sep='\n')




if __name__ == '__main__':
    main()

    
```

## 진법 변환

![image](https://user-images.githubusercontent.com/88238335/136135305-c6cb3ef5-b940-4480-be86-fa95a423c21f.png)



```Python

def convert():
    B, N = map(str, input().split())
    answer = 0
    B_= list(B)
    #See if the letter is an alphabet and convert it to integer
    for idx, j in enumerate(B_):
        if j.isalpha():
            B_[idx] = (ord(j)-55)
    
    #Do the math 
    for idx, i in enumerate(B_):
        answer += int(i)*(int(N)**(len(B)-idx -1))
    print (answer)

if __name__ == '__main__':
    convert()


    
```

## 비밀지도

![image](https://user-images.githubusercontent.com/88238335/136136691-70a090f2-9a70-4b6b-a7fd-5653b4d97083.png)

### Probably didn't have to use numpy but oh well....
```Python

import numpy as np
def solution(n, arr1, arr2):
    a=[]
    b=[]
    d=""
    e=[]
    #Convert all integers to binary and make sure the length is "n" and fill the empty with 0 
    for i in arr1:
        a.append(list(bin(i)[2:].zfill(n)))
    for i in arr2:
        b.append(list(bin(i)[2:].zfill(n)))
    a_=(np.array(a)).astype(np.int)
    b_=(np.array(b)).astype(np.int)
    #add the two lists of binary numbers
    c = a_ + b_
    for i in c:
        for j in i:
            if j == 1 or j == 2:
                d += "#"
            else:
                d += ' '
        e.append(d)
        d=''
    return e

    
```

## Hashing

![image](https://user-images.githubusercontent.com/88238335/136302789-eca73c12-5e3a-42a7-9763-d93425c1533b.png)


```Python

def convert():
    M = int(input())
    N = str(input())
    answer = 0
    N_= list(N)
    #Change the letters to int
    for idx, j in enumerate(N_):
        N_[idx] = (ord(j)-96)
    
    #Do the Hashing
    for idx, i in enumerate(N_):
        answer += int(i) * (31 ** idx)
    print (answer % 1234567891)

if __name__ == '__main__':
    convert()


    
```

## 원주하지 못한 선수 

![image](https://user-images.githubusercontent.com/88238335/136306080-1e4abf70-cb3e-43d8-9de3-5ea1680f2a69.png)


```Python

#import counter and use the deduction function
from collections import Counter
def solution(participant, completion):
    return list((Counter(participant) - Counter(completion)).keys())[0]

    
```

##전화번호 목록

![image](https://user-images.githubusercontent.com/88238335/136306270-5de6c8b2-3397-4514-bcee-0e85bd4322ff.png)

```Python

def solution(phoneBook):
    # Sort the phonebook and See if the phone number contains the start of other phone numbers
    phoneBook = sorted(phoneBook)

    for p1, p2 in zip(phoneBook, phoneBook[1:]):
        if p2.startswith(p1):
            return False
    return True

    
```

##체육복

![image](https://user-images.githubusercontent.com/88238335/136308790-e609e384-cfef-4e37-a7cd-281508c6e1a8.png)

```Python

def solution(n, lost, reserve):
    answer = 0
    total = list()
    
    #Add students to list
    for i in range(n):
        total.append(1)
    
    #remove clothes lost
    for i in lost:
        total[i-1] -= 1
        
    #add clothes in reserve
    for i in reserve:
        total[i-1] += 1 
    
    #check if they can be lended to the person behind or the person ahead
    for i in range(len(total)):
        if total[i] == 2:
            if i-1 >= 0:
                if total[i-1] == 0:
                    total[i-1] += 1
                    total[i] -= 1
        if total[i] == 2:
            if i+1 < len(total):
                if total[i+1] == 0:
                    total[i+1] += 1
                    total[i] -= 1
    
    #count how many have sport clothes now
    for student in total:
        if student >= 1:
            answer += 1

    return answer

    
```
##괄호변환
```
1. 입력이 빈 문자열인 경우, 빈 문자열을 반환합니다. 
2. 문자열 w를 두 "균형잡힌 괄호 문자열" u, v로 분리합니다. 단, u는 "균형잡힌 괄호 문자열"로 더 이상 분리할 수 없어야 하며, v는 빈 문자열이 될 수 있습니다. 
3. 문자열 u가 "올바른 괄호 문자열" 이라면 문자열 v에 대해 1단계부터 다시 수행합니다. 
  3-1. 수행한 결과 문자열을 u에 이어 붙인 후 반환합니다. 
4. 문자열 u가 "올바른 괄호 문자열"이 아니라면 아래 과정을 수행합니다. 
  4-1. 빈 문자열에 첫 번째 문자로 '('를 붙입니다. 
  4-2. 문자열 v에 대해 1단계부터 재귀적으로 수행한 결과 문자열을 이어 붙입니다. 
  4-3. ')'를 다시 붙입니다. 
  4-4. u의 첫 번째와 마지막 문자를 제거하고, 나머지 문자열의 괄호 방향을 뒤집어서 뒤에 붙입니다. 
  4-5. 생성된 문자열을 반환합니다.
```

```Python
def solution(p):
    if p == "":
        return ""

    def isvalid(v):
        if v[0] ==")" or v[len(v) - 1] == "(":
            return False
        left = 0
        right = 0
        for i in v:
            if i == "(":
                left += 1
            else:
                right +=1
            if right > left:
                return False
        if right != left:
            return False
        return True
            

    def solve(p):
        if not p:
            return p
        u = ""
        v = ""
        left = 0
        right = 0
        for i in p:
            u += i
            if i == "(":
                left += 1
            else:
                right += 1
            if left == right:
                break
        v = p[len(u):]
        
        if isvalid(u):
            return u + solve(v)
        else:
            change = "("
            change += solve(v)
            change += ")"
            for i in u[1:len(u) -1]:
                if i == "(":
                    change += ")"
                else:
                    change += "("
            return change
    if isvalid(p):
        return p
    else:
        return solve(p)
```


## 계단 오르기 

```Python
def countWays():
    n = int(input())
    stair = [0 for i in range(n+3)]
    for i in range(n):
        stair[i] = (int(input()))
    best_way_value = [0 for i in range(n+3)]
    best_way_value[0] = stair[0]
    best_way_value[1] = max(stair[0]+stair[1], stair[1])
    best_way_value[2] = max(stair[0]+stair[2], stair[1]+stair[2])

    #Do the addition at 3 stince it can go two steps at a time and has to land on the last step (i-3)
    for i in range(3, n):
        best_way_value[i] = max(best_way_value[i-2]+stair[i], stair[i-1]+stair[i]+best_way_value[i-3])
    print(best_way_value[n-1])

if __name__ == "__main__":
    countWays()
```

## 정수 삼각형

```Python
def get_max_sum(triangle):
    for i in range(1, len(triangle)):
        for j in range(i + 1):
            #Get sum on the outer layers of the triangle
            if j==0:
                triangle[i][j] += triangle[i-1][j]
            elif j==i:
                triangle[i][j] += triangle[i-1][j-1]
            # When the triangle is in the middle get the greater number to get the greatest sum.
            else:
                triangle[i][j] += max(triangle[i-1][j-1], triangle[i-1][j])
    return(max(triangle[-1]))
```

## N 으로 표현

```Python
def solution(N, number):
    possible = [[]] + [[int(str(N) * i)] for i in range(1,9)]
    if [number] in possible:
        return possible.index([number])
    for i in range(2,9):
        for j in range(1, i):
            for num1 in possible[j]:
                for num2 in possible[i-j]:
                    possible[i].append(num1 + num2)
                    possible[i].append(num1 * num2)
                    possible[i].append(num1 - num2)
                    if num2!=0:
                        possible[i].append(num1 // num2)
        if number in possible[i]:
            return i
        possible[i] = list(set(possible[i]))
    return -1
```
## 배달

#Could have been better but who knows...
```Python
def solution(N, road, K):
    length = [float('inf')] * (N + 1)
    length[1] = 0
    towns = [1]
    answer = 0
    while (towns):
        town = towns.pop(0)
        for a, b, cost in road:
            if (a == town or b == town):
                target = b if a == town else a
                if length[target] > length[town] + cost:
                    length[target] = length[town] + cost
                    towns.append(target)

    for i in length:
        if i <= K:
            answer += 1
    return answer
```

##lifeboat

![image](https://user-images.githubusercontent.com/88238335/138837316-aec8e162-57a3-4528-a7fe-493f48b2b02f.png)

```Python
def solution(people, limit):
    no_of_lifeboats = 0
    start = 0
    end = len(people) - 1

    people.sort()

    while start <= end:
        no_of_lifeboats += 1
        if people[start] + people[end] <= limit:
            start += 1
        end -= 1
    return no_of_lifeboats
  

```

##printer

![image](https://user-images.githubusercontent.com/88238335/139002954-95369761-c99e-48ef-ab3a-e384eea37acf.png)

```Python
def solution(priorities, location):
    a = 0
    b = 0

    index = [i for i in range(len(priorities))]

    while priorities:
        first = priorities.pop(0)
        first_index = index.pop(0)
        counter = 0
        for i in range(len(priorities)):
            if priorities[i] > first:
                counter = 1
        if counter == 0:
            a += 1
            if first_index == location:
                b = a
                return b
        else:
            priorities.append(first)
            index.append(first_index)
    return b

```
