def solve_maze(maze, x, y, solution):
    if x == len(maze)-1 and y == len(maze[0])-1 and maze[x][y] == 1:
        solution[x][y] = 1
        return True

    if is_safe(maze, x, y):
        if solution[x][y] == 1:
            return False  # already visited

        solution[x][y] = 1  # mark as part of the path

        # Move right
        if solve_maze(maze, x, y + 1, solution):
            return True
        # Move down
        if solve_maze(maze, x + 1, y, solution):
            return True
        # Move left
        if solve_maze(maze, x, y - 1, solution):
            return True
        # Move up
        if solve_maze(maze, x - 1, y, solution):
            return True

        solution[x][y] = 0  # backtrack
        return False
    return False

def is_safe(maze, x, y):
    return 0 <= x < len(maze) and 0 <= y < len(maze[0]) and maze[x][y] == 1

def print_solution(solution):
    for row in solution:
        print(row)

# Maze example: 1 = open path, 0 = wall
maze = [
    [1, 0, 0, 0],
    [1, 1, 0, 1],
    [0, 1, 0, 0],
    [1, 1, 1, 1]
]

solution = [[0]*len(maze[0]) for _ in range(len(maze))]

if solve_maze(maze, 0, 0, solution):
    print("Solution path (1s are the path taken):")
    print_solution(solution)
else:
    print("No path found in the maze.")
    
