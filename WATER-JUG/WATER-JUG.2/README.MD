from collections import deque

def water_jug():
    cap = (3, 5, 8)
    start = (0, 0, 8)
    goal = (0, 4, 4)
    q = deque([(start, [start])])
    visited = {start}

    while q:
        state, path = q.popleft()

        if state == goal:
            for s in path:
                print(s)
            return

        for i in range(3):
            for j in range(3):
                a = list(state)
                x = min(a[i], cap[j] - a[j])

                if i != j and x > 0:
                    a[i] -= x
                    a[j] += x
                    nxt = tuple(a)

                    if nxt not in visited:
                        visited.add(nxt)
                        q.append((nxt, path + [nxt]))

water_jug()
