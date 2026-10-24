
graph = {
    'A': ['B', 'D', 'E'],
    'B': ['A', 'C', 'D', 'E', 'F'],
    'C': ['B', 'E', 'F'],
    'D': ['A', 'B', 'E', 'G', 'H'],
    'E': ['A', 'B', 'C', 'D', 'F', 'G', 'H', 'I'],
    'F': ['B', 'C', 'G', 'H', 'I'],
    'G': ['D', 'E', 'H', 'J'],
    'H': ['D', 'E', 'F', 'G', 'I', 'J'],
    'I': ['E', 'F', 'H', 'J'],
    'J': ['G', 'H', 'I']
}

colors = ['Red', 'Green', 'Blue', 'Yellow']
result = {}

def safe(node, color):
    for neighbor in graph[node]:
        if result.get(neighbor) == color:
            return False
    return True

def color_graph(nodes):
    if not nodes:
        return True

    node = nodes[0]

    for color in colors:
        if safe(node, color):
            result[node] = color

            if color_graph(nodes[1:]):
                return True

            del result[node]

    return False

if color_graph(list(graph)):
    for node in graph:
        print(node, ":", result[node])
else:
    print("No solution")
