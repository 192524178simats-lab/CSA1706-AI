
import heapq

graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'C': 2, 'D': 3},
    'C': {'E': 5},
    'D': {'F': 2, 'G': 8},
    'E': {'G': 3},
    'F': {'G': 1},
    'G': {}
}

h = {'A': 5, 'B': 6, 'C': 4,
     'D': 3, 'E': 3, 'F': 1, 'G': 0}

pq = [(h['A'], 0, 'A', ['A'])]
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
