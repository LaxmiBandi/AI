import random

def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 5)

def check_winner(board, player):
    # Check rows, columns, and diagonals
    for i in range(3):
        if all(cell == player for cell in board[i]) or \
           all(row[i] == player for row in board):
            return True
    if all(board[i][i] == player for i in range(3)) or \
       all(board[i][2 - i] == player for i in range(3)):
        return True
    return False

def is_draw(board):
    return all(cell in ['X', 'O'] for row in board for cell in row)

def get_available_moves(board):
    return [(i, j) for i in range(3) for j in range(3) if board[i][j] not in ['X', 'O']]

def minimax(board, depth, is_maximizing):
    if check_winner(board, 'O'):
        return 1
    if check_winner(board, 'X'):
        return -1
    if is_draw(board):
        return 0

    if is_maximizing:
        best_score = -float("inf")
        for (i, j) in get_available_moves(board):
            board[i][j] = 'O'
            score = minimax(board, depth + 1, False)
            board[i][j] = str(i * 3 + j + 1)
            best_score = max(score, best_score)
        return best_score
    else:
        best_score = float("inf")
        for (i, j) in get_available_moves(board):
            board[i][j] = 'X'
            score = minimax(board, depth + 1, True)
            board[i][j] = str(i * 3 + j + 1)
            best_score = min(score, best_score)
        return best_score

def computer_move(board):
    best_score = -float("inf")
    move = None
    for (i, j) in get_available_moves(board):
        board[i][j] = 'O'
        score = minimax(board, 0, False)
        board[i][j] = str(i * 3 + j + 1)
        if score > best_score:
            best_score = score
            move = (i, j)
    if move:
        board[move[0]][move[1]] = 'O'

def human_move(board):
    while True:
        try:
            move = int(input("Enter your move (1-9): "))
            if move < 1 or move > 9:
                raise ValueError
            row, col = (move - 1) // 3, (move - 1) % 3
            if board[row][col] in ['X', 'O']:
                print("Cell already taken. Try again.")
            else:
                board[row][col] = 'X'
                break
        except ValueError:
            print("Invalid input. Enter a number from 1 to 9.")

def play_game():
    board = [[str(i * 3 + j + 1) for j in range(3)] for i in range(3)]
    print("Welcome to Tic-Tac-Toe!")
    print("You are X, computer is O.")
    print_board(board)

    while True:
        human_move(board)
        print_board(board)
        if check_winner(board, 'X'):
            print("You win!")
            break
        if is_draw(board):
            print("It's a draw!")

            break

        print("Computer's move:")
        computer_move(board)
        print_board(board)
        if check_winner(board, 'O'):
            print("Computer wins!")
            break
        if is_draw(board):
            print("It's a draw!")
            break

if __name__ == "__main__":
    play_game()
