
def alpha_beta(node, alpha, beta, is_max):
    if isinstance(node, int):
        return node

    if is_max:
        best = float('-inf')

        for child in node:
            value = alpha_beta(child, alpha, beta, False)
            best = max(best, value)
            alpha = max(alpha, best)

            if alpha >= beta:
                print("Pruned remaining MAX children")
                break

        return best

    else:
        best = float('inf')

        for child in node:
            value = alpha_beta(child, alpha, beta, True)
            best = min(best, value)
            beta = min(beta, best)

            if alpha >= beta:
                print("Pruned remaining MIN children")
                break

        return best


tree = [
    [[2, 3], [5, 6]],
    [[0, 1], [7, 5]]
]

result = alpha_beta(tree, float('-inf'),
                    float('inf'), True)

print("Optimal value:", result)
