
import heapq

graph = {
    'P': [('R', 4), ('C', 4), ('A', 4)],
    'R': [('E', 5)],
    'C': [('R', 2), ('U', 3), ('M', 6)],
    'E': [('U', 5), ('S', 5)],
    'A': [('M', 3)],
    'M': [('U', 5), ('L', 2)],
    'U': [('S', 4), ('N', 5)],
    'L': [('N', 5)],
    'N': [('S', 6)],
    'S': []
}

h = {
    'P': 10, 'R': 8, 'C': 6, 'E': 3,
    'A': 11, 'M': 9, 'U': 4, 'L': 9,
    'N': 6, 'S': 0
}

def astar(start, goal):
    pq = [(h[start], 0, start)]
    cost = {start: 0}
    parent = {start: None}
    closed = set()

    while pq:
        f, g, node = heapq.heappop(pq)

        if node in closed:
            continue

        if node == goal:
            path = []
            while node is not None:
                path.append(node)
                node = parent[node]

            path.reverse()
            print("Path:", " -> ".join(path))
            print("Total cost:", g)
            return

        closed.add(node)

        for neighbor, weight in graph[node]:
            new_cost = g + weight

            if new_cost < cost.get(neighbor, float('inf')):
                cost[neighbor] = new_cost
                parent[neighbor] = node
                heapq.heappush(
                    pq, (new_cost + h[neighbor],
                         new_cost, neighbor)
                )

    print("Path not found")

astar('P', 'S')
