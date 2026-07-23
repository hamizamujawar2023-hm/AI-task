from collections import deque import 
heapq 
# ----------------------------------------------------
# Graph (Edge Costs in km) 
# ---------------------------------------------------- graph 
= { 
 "College": [("Junction A", 2), ("Market", 4)], 
 "Junction A": [("Signal B", 2)], 
 "Market": [("Park", 3)], 
 "Signal B": [("Flyover C", 2), ("Park", 2)], 
 "Park": [("Flyover C", 2)], 
 "Flyover C": [("Home", 2.5)], 
 "Home": [] 
} 
# ----------------------------------------------------
# Heuristic Values (Estimated distance to Home) 
# ----------------------------------------------------
heuristic = { "College": 8.5, "Junction A": 6.5, 
 "Market": 5.5, 
 "Signal B": 4.5, 
 "Park": 3.5, 
 "Flyover C": 2.5, 
 "Home": 0 
} 
# ----------------------------------------------------
# Display Graph 
# ----------------------------------------------------
print("\n========== GRAPH ==========") for 
node in graph: 
 print(node, "->", graph[node]) 
print("\n========== HEURISTIC VALUES ==========") for 
node in heuristic: 
 print(node, ":", heuristic[node]) 
# ----------------------------------------------------
# Breadth First Search (BFS) 
# ----------------------------------------------------
def bfs(start, goal): queue = 
deque([(start, [start], 0)]) visited = set() 
explored = 0 
 while queue: 
 node, path, cost = queue.popleft() 
 if node not in visited: 
visited.add(node) explored 
+= 1 
 if node == goal: 
 print("\n===== Breadth First Search (BFS) =====") 
print("Path :", " -> ".join(path)) print("Total Path 
Cost :", cost, "km") print("Nodes Explored :", 
explored) return 
 for neighbor, weight in graph[node]: queue.append((neighbor, path + [neighbor], cost + weight)) 
# ----------------------------------------------------
# Depth First Search (DFS) 
# ----------------------------------------------------
def dfs(start, goal): stack = [(start, 
[start], 0)] visited = set() explored = 
0 
 while stack: 
 node, path, cost = stack.pop() 
 if node not in visited: 
visited.add(node) explored 
+= 1 
 if node == goal: 
 print("\n===== Depth First Search (DFS) =====") 
print("Path :", " -> ".join(path)) print("Total Path 
Cost :", cost, "km") print("Nodes Explored :", 
explored) return 
 for neighbor, weight in reversed(graph[node]): 
 stack.append((neighbor, path + [neighbor], cost + weight)) # -----------------------
-----------------------------
# Uniform Cost Search (UCS) 
# ---------------------------------------------------- def 
ucs(start, goal): 
 pq = [(0, start, [start])] 
visited = {} explored 
= 0 
 while pq: 
 cost, node, path = heapq.heappop(pq) 
 if node in visited: 
 continue 
 visited[node] = cost 
 explored += 1 if node == goal: 
 print("\n===== Uniform Cost Search (UCS) =====") 
print("Path :", " -> ".join(path)) print("Total Path Cost 
:", cost, "km") print("Nodes Explored :", explored) 
return 
 for neighbor, weight in graph[node]: 
 heapq.heappush(pq, (cost + weight, neighbor, path + [neighbor])) 
# ----------------------------------------------------
# Greedy Best First Search 
# ---------------------------------------------------- def 
greedy(start, goal): 
 pq = [(heuristic[start], start, [start], 0)] 
visited = set() explored = 0 
 while pq: 
 h, node, path, cost = heapq.heappop(pq) 
 if node in visited: 
 continue 
 visited.add(node) 
explored += 1 
 if node == goal: 
 print("\n===== Greedy Best First Search =====") 
print("Path :", " -> ".join(path)) print("Total Path 
Cost :", cost, "km") print("Nodes Explored :", 
explored) return 
 for neighbor, weight in graph[node]: 
 heapq.heappush( 
 pq, 
 (heuristic[neighbor], neighbor, path + [neighbor], cost + weight) 
 ) 
# ----------------------------------------------------
# A* Search # ---------------------------------------------------- def 
astar(start, goal): 
 pq = [(heuristic[start], 0, start, [start])] 
visited = {} explored = 0 
 while pq: 
 f, g, node, path = heapq.heappop(pq) 
 if node in visited: 
 continue 
 visited[node] = g 
explored += 1 
 if node == goal: 
 print("\n===== A* Search =====") 
print("Source :", start) 
print("Destination :", goal) print("Path 
Found :", " -> ".join(path)) print("Total 
Cost (Distance) :", g, "km") 
print("Nodes Explored :", explored) 
return 
 for neighbor, weight in graph[node]: 
new_g = g + weight 
 new_f = new_g + heuristic[neighbor] 
 heapq.heappush( 
 pq, 
 (new_f, new_g, neighbor, path + [neighbor]) 
 ) 
# ----------------------------------------------------
# Main Program 
# ----------------------------------------------------
source = "College" destination = "Home" 
bfs(source, destination) dfs(source, 
destination) ucs(source, 
destination) greedy(source, destination) astar(source, 
destination) 
