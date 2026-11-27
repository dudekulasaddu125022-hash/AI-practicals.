# Practical 6 — Constraint satisfaction: map colouring and 8-Queens
# Run:  python P6_csp.py
# Library: none. Only plain Python 3.
 
REGIONS = ["A", "B", "C", "D", "E"]
NEIGHBOURS = {
    "A": ["B", "C"],
    "B": ["A", "C", "D"],
    "C": ["A", "B", "D", "E"],
    "D": ["B", "C", "E"],
    "E": ["C", "D"],
}
COLOURS = ["Red", "Green", "Blue"]
 
 
def colour_ok(region, colour, assign):
    # Consistency check: a neighbour must not already have this colour.
    for other in NEIGHBOURS[region]:
        if assign.get(other) == colour:
            return False
    return True
 
 
def colour_map():
    assign = {}
 
    def backtrack():
        if len(assign) == len(REGIONS):
            return True                    # every region has a colour
        region = next(r for r in REGIONS if r not in assign)
        for colour in COLOURS:
            if colour_ok(region, colour, assign):
                assign[region] = colour    # try
                if backtrack():
                    return True
                del assign[region]         # undo = backtrack
        return False
 
    ok = backtrack()
    return ok, assign
 
 
def queens_ok(cols, row, col):
    # No shared column and no shared diagonal with earlier queens.
    for r, c in enumerate(cols):
        if c == col or abs(c - col) == abs(r - row):
            return False
    return True
 
 
def nqueens(n=8):
    cols = []
 
    def backtrack(row):
        if row == n:
            return True                    # one queen in every row
        for col in range(n):
            if queens_ok(cols, row, col):
                cols.append(col)           # try
                if backtrack(row + 1):
                    return True
                cols.pop()                 # undo = backtrack
        return False
 
    backtrack(0)
    return cols
 
 
if __name__ == "__main__":
    print("PRACTICAL 6  |  CSP backtracking")
    ok, assign = colour_map()
    print("Map colouring (neighbours must differ):")
    for region, colour in assign.items():
        print("  Region", region, "->", colour)
    print("Solved?", ok)
 
    sol = nqueens(8)
    print()
    print("8-Queens (column of the queen in each row):", sol)
    print("Board (Q = queen):")
    for r in range(8):
        print(" ", "".join(" Q" if sol[r] == c else " ." for c in range(8)))

