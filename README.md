<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name: Harsshitha lakshmanan     </h3>
<h3>Register Number:  212223230075        </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>








``````
// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)

``````

<hr>
<h2>Sample Graph I</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

<hr>
<h2>Sample Input</h2>
<hr>
10 14 <br>
A B 6 <br>
A F 3 <br>
B D 2 <br>
B C 3 <br>
C D 1 <br>
C E 5 <br>
D E 8 <br>
E I 5 <br>
E J 5 <br>
F G 1 <br>
G I 3 <br>
I J 3 <br>
F H 7 <br>
I H 2 <br>
A 10 <br>
B 8 <br>
C 5 <br>
D 7 <br>
E 3 <br>
F 6 <br>
G 5 <br>
H 3 <br>
I 1 <br>
J 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
Path found: ['A', 'F', 'G', 'I', 'J']


<hr>
<h2>Sample Graph II</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)


<hr>
<h2>Sample Input</h2>
<hr>
6 6 <br>
A B 2 <br>
B C 1 <br>
A E 3 <br>
B G 9 <br>
E D 6 <br>
D G 1 <br>
A 11 <br>
B 6 <br>
C 99 <br>
E 7 <br>
D 1 <br>
G 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
Path found: ['A', 'E', 'D', 'G']


Program:

~~~

from collections import defaultdict

class Node:
    def __init__(self, name, parent=None, g=0, h=0):
        self.name = name
        self.parent = parent
        self.g = g
        self.h = h
        self.f = g + h

def a_star(graph, heuristics, start, goal):
    open_list = []
    closed_list = []

    start_node = Node(start, None, 0, heuristics[start])
    open_list.append(start_node)

    while open_list:
        # Node with minimum f value
        current = min(open_list, key=lambda x: x.f)
        open_list.remove(current)
        closed_list.append(current)

        if current.name == goal:
            path = []
            while current:
                path.append(current.name)
                current = current.parent
            return path[::-1]

        for neighbor, cost in graph[current.name]:
            g = current.g + cost
            h = heuristics[neighbor]
            f = g + h

            # Skip if better node exists in OPEN
            if any(n.name == neighbor and n.f <= f for n in open_list):
                continue

            # Skip if better node exists in CLOSED
            if any(n.name == neighbor and n.f <= f for n in closed_list):
                continue

            open_list.append(Node(neighbor, current, g, h))

    return None

# -------- Driver Code --------
graph = defaultdict(list)

v, e = map(int, input().split())
for _ in range(e):
    u, v1, w = input().split()
    graph[u].append((v1, int(w)))
    graph[v1].append((u, int(w)))

heuristics = {}
for _ in range(len(graph)):
    n, h = input().split()
    heuristics[n] = int(h)

start = list(heuristics.keys())[0]
goal = min(heuristics, key=lambda x: heuristics[x])

path = a_star(graph, heuristics, start, goal)
print("Path found:", path)



~~~








Output:


<img width="561" height="539" alt="image" src="https://github.com/user-attachments/assets/2e474f5d-8391-4719-8c08-35963cd491c6" />




<img width="443" height="289" alt="image" src="https://github.com/user-attachments/assets/b8149101-6aad-4f9d-bf85-c579cf43a88e" />





RESULT:
Thus the given code is executed succesfully.


