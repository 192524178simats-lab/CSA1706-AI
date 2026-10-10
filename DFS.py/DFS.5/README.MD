graph = {
    0: [1],
    1: [3],
    2: [1],
    3: [2, 4],
    4: [5],
    5: [7],
    6: [4],
    7: [6]
}

def dfs(node, visited):
    if node not in visited:
        print(node, end=" ")
        visited.add(node)

        for neighbour in graph[node]:
            dfs(neighbour, visited)

dfs(0, set())
