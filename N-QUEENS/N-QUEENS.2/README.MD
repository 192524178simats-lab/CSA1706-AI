
N = 8
board = [-1] * N

def is_safe(row, col):
    for i in range(row):
        if board[i] == col:
            return False
        if abs(board[i] - col) == abs(i - row):
            return False
    return True

def solve(row):
    if row == N:
        for r in range(N):
            print(" ".join(
                "Q" if board[r] == c else "."
                for c in range(N)
            ))
        return True

    for col in range(N):
        if is_safe(row, col):
            board[row] = col

            if solve(row + 1):
                return True

            board[row] = -1

    return False

if not solve(0):
    print("No solution")
