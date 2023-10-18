import tkinter as tk
from tkinter import messagebox

def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 9)

def check_winner(board, player):
    for row in board:
        if all(cell == player for cell in row):
            return True
    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True
    if all(board[i][i] == player for i in range(3)) or all(board[i][2 - i] == player for i in range(3)):
        return True
    return False

def get_empty_cells(board):
    return [(i, j) for i in range(3) for j in range(3) if board[i][j] == " "]

def minimax(board, depth, maximizing_player):
    if check_winner(board, "X"):
        return -1
    if check_winner(board, "O"):
        return 1
    if len(get_empty_cells(board)) == 0:
        return 0

    if maximizing_player:
        max_eval = float("-inf")
        for i, j in get_empty_cells(board):
            board[i][j] = "O"
            eval = minimax(board, depth + 1, False)
            board[i][j] = " "
            max_eval = max(max_eval, eval)
        return max_eval
    else:
        min_eval = float("inf")
        for i, j in get_empty_cells(board):
            board[i][j] = "X"
            eval = minimax(board, depth + 1, True)
            board[i][j] = " "
            min_eval = min(min_eval, eval)
        return min_eval

def best_move(board):
    best_score = float("-inf")
    best_move = None
    for i, j in get_empty_cells(board):
        board[i][j] = "O"
        score = minimax(board, 0, False)
        board[i][j] = " "
        if score > best_score:
            best_score = score
            best_move = (i, j)
    return best_move

def click(row, col):
    global player, board

    if board[row][col] == " " and player == "X":
        board[row][col] = "X"
        buttons[row][col].config(text="X")
        if check_winner(board, "X"):
            messagebox.showinfo("Tic-Tac-Toe", "You win!")
            reset_board()
            return
        elif len(get_empty_cells(board)) == 0:
            messagebox.showinfo("Tic-Tac-Toe", "It's a draw!")
            reset_board()
            return

        player = "O"
        ai_row, ai_col = best_move(board)
        board[ai_row][ai_col] = "O"
        buttons[ai_row][ai_col].config(text="O")

        if check_winner(board, "O"):
            messagebox.showinfo("Tic-Tac-Toe", "AI wins!")
            reset_board()
            return
        elif len(get_empty_cells(board)) == 0:
            messagebox.showinfo("Tic-Tac-Toe", "It's a draw!")
            reset_board()
            return

        player = "X"

def reset_board():
    global board
    for i in range(3):
        for j in range(3):
            board[i][j] = " "
            buttons[i][j].config(text=" ")
    player = "X"

root = tk.Tk()
root.title("Tic-Tac-Toe")

buttons = [[None, None, None], [None, None, None], [None, None, None]]
for i in range(3):
    for j in range(3):
        buttons[i][j] = tk.Button(root, text=" ", font=("normal", 20), width=6, height=2, command=lambda row=i, col=j: click(row, col))
        buttons[i][j].grid(row=i, column=j)

board = [[" " for _ in range(3)] for _ in range(3)]
player = "X"

root.mainloop()

