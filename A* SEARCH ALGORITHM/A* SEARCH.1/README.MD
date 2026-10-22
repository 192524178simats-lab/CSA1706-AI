
import heapq

graph = {
    'S': {'A': 3, 'D': 4},
    'A': {'B': 4, 'D': 5},
    'B': {'C': 4, 'E': 5},
    'C': {},
    'D': {'E': 2},
    'E': {'F': 4},
    'F': {'G': 3.5},
    'G': {}
}

h = {'S': 11.5, 'A': 10.1, 'B': 5.8,
     'C': 3.4, 'D': 9.2, 'E': 7.1,
     'F': 3.5, 'G': 0}

pq = [(h['S'], 0, 'S', ['S'])]
best = {}

while pq:
    f, cost, node, path = heapq.heappop(pq)

    if node in best and best[node] <= cost:
        continue
    best[node] = cost

    if node == 'G':
        print("Path:", " -> ".join(path))
        print("Total cost:", cost)
        break

    for nxt, w in graph[node].items():
        new_cost = cost + w
        heapq.heappush(
            pq, (new_cost + h[nxt], new_cost,
                 nxt, path + [nxt])
        )
