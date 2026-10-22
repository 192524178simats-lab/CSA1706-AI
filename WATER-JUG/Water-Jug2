from collections import deque

def water_jug():
    start = (12, 0, 0)
    goal = (6, 6, 0)
    q = deque([(start, [])])
    visited = {start}

    while q:
        state, path = q.popleft()

        if state == goal:
            for s in path + [state]:
                print(s)
            return

        for i in range(3):
            for j in range(3):
                if i != j:
                    a = list(state)
                    amount = min(a[i], [12, 8, 5][j] - a[j])
                    if amount > 0:
                        a[i] -= amount
                        a[j] += amount
                        nxt = tuple(a)

                        if nxt not in visited:
                            visited.add(nxt)
                            q.append((nxt, path + [state]))

water_jug()
