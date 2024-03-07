import random
import numpy as np
import matplotlib.pyplot as plt


DIFFICULTY = 0.7  # MAX = 0.753, At least 20 numbers given.


def isValid(i, j, key, board):
    """判断填入的数字是否合法"""
    # 检查行是否合法
    for col in range(len(board)):
        if board[i][col] == key:
            return False

    # 检查列是否合法
    for row in range(len(board)):
        if board[row][j] == key:
            return False

    # 检查3*3小格子是否合法
    box_row = (i // 3) * 3
    box_col = (j // 3) * 3
    for row in range(box_row, box_row + 3):
        for col in range(box_col, box_col + 3):
            if board[row][col] == key:
                return False

    return True


def backtracking(board):
    """回溯算法"""
    board_size = len(board)
    for i in range(board_size):
        for j in range(board_size):
            if board[i][j] == 0:
                for key in range(1, 10):
                    if isValid(i, j, key, board):
                        board[i][j] = key
                        result = backtracking(board)
                        if result:
                            return True
                        board[i][j] = 0
                return False
    return True


def generate_sudoku(difficulty):
    """生成一个数独题"""
    # 创建一个空的数独板
    board = [[0] * 9 for _ in range(9)]

    # 填充对角线上的3*3子格
    for i in range(0, 9, 3):
        nums = [1, 2, 3, 4, 5, 6, 7, 8, 9]
        random.shuffle(nums)
        for j in range(3):
            board[i + j][i + j] = nums[j]

    # 使用 backtracking 函数填充数独板
    backtracking(board)

    # 计算需要挖去的单元格数量
    empty_cells = int(difficulty * 81)
    empty_cells = 81 - max(81 - empty_cells, 20)  # 控制挖去的范围，最少保留20个数字

    # 随机挖空数独板中的数字，保证数独有唯一解
    empty_cells = random.sample(range(81), empty_cells)
    for cell in empty_cells:
        row = cell // 9
        col = cell % 9
        board[row][col] = 0

    return board


def draw_sudoku(board, completed=False):
    """画出数独"""
    fig, ax = plt.subplots()
    ax.set_xlim([0, 9])
    ax.set_ylim([0, 9])
    ax.set_aspect('equal', adjustable='box')

    # 绘制数独格子
    for i in range(10):
        if i % 3 == 0:
            ax.axhline(i, color='black', linewidth=2)
            ax.axvline(i, color='black', linewidth=2)
        else:
            ax.axhline(i, color='gray')
            ax.axvline(i, color='gray')

    # 填充数独数字
    for i in range(9):
        for j in range(9):
            if board[i][j] != 0:
                ax.text(j + 0.5, i + 0.5, str(board[i][j]),
                        fontsize=12, ha='center', va='center')

    # 设置标题
    title = "One Answer" if completed else "Problem"
    plt.title(title)

    plt.xticks([])
    plt.yticks([])
    plt.savefig(title + ".png")
    plt.show()


# 示例数独
# sudoku_board = [
#     [5, 3, 0, 0, 7, 0, 0, 0, 0],
#     [6, 0, 0, 1, 9, 5, 0, 0, 0],
#     [0, 9, 8, 0, 0, 0, 0, 6, 0],
#     [8, 0, 0, 0, 6, 0, 0, 0, 3],
#     [4, 0, 0, 8, 0, 3, 0, 0, 1],
#     [7, 0, 0, 0, 2, 0, 0, 0, 6],
#     [0, 6, 0, 0, 0, 0, 2, 8, 0],
#     [0, 0, 0, 4, 1, 9, 0, 0, 5],
#     [0, 0, 0, 0, 8, 0, 0, 7, 9]
# ]


if __name__ == "__main__":
    sudoku_board = generate_sudoku(difficulty=DIFFICULTY)
    draw_sudoku(sudoku_board)

    backtracking(sudoku_board)
    draw_sudoku(sudoku_board, completed=True)
