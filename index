"""
TASK 2: Tic-Tac-Toe AI
CODSOFT AI Internship

An unbeatable Tic-Tac-Toe AI using the Minimax algorithm with
Alpha-Beta Pruning. Demonstrates game theory and search algorithms.

Human plays as 'X', AI plays as 'O'.
"""

import math

class TicTacToe:
    def __init__(self):
        self.board = [' ' for _ in range(9)]  # 3x3 board as flat list
        self.human = 'X'
        self.ai = 'O'

    def print_board(self):
        b = self.board
        print()
        print(f" {b[0]} | {b[1]} | {b[2]} ")
        print("---+---+---")
        print(f" {b[3]} | {b[4]} | {b[5]} ")
        print("---+---+---")
        print(f" {b[6]} | {b[7]} | {b[8]} ")
        print()

    def available_moves(self):
        return [i for i, v in enumerate(self.board) if v == ' ']

    def make_move(self, pos, player):
        self.board[pos] = player

    def undo_move(self, pos):
        self.board[pos] = ' '

    def check_winner(self, player):
        b = self.board
        win_conditions = [
            [0, 1, 2], [3, 4, 5], [6, 7, 8],  # rows
            [0, 3, 6], [1, 4, 7], [2, 5, 8],  # columns
            [0, 4, 8], [2, 4, 6]              # diagonals
        ]
        return any(all(b[i] == player for i in combo) for combo in win_conditions)

    def is_draw(self):
        return ' ' not in self.board

    def is_game_over(self):
        return self.check_winner(self.human) or self.check_winner(self.ai) or self.is_draw()

    def minimax(self, depth, is_maximizing, alpha, beta):
        if self.check_winner(self.ai):
            return 10 - depth
        if self.check_winner(self.human):
            return depth - 10
        if self.is_draw():
            return 0

        if is_maximizing:
            best_score = -math.inf
            for move in self.available_moves():
                self.make_move(move, self.ai)
                score = self.minimax(depth + 1, False, alpha, beta)
                self.undo_move(move)
                best_score = max(best_score, score)
                alpha = max(alpha, best_score)
                if beta <= alpha:
                    break  # Alpha-beta pruning
            return best_score
        else:
            best_score = math.inf
            for move in self.available_moves():
                self.make_move(move, self.human)
                score = self.minimax(depth + 1, True, alpha, beta)
                self.undo_move(move)
                best_score = min(best_score, score)
                beta = min(beta, best_score)
                if beta <= alpha:
                    break  # Alpha-beta pruning
            return best_score

    def best_move(self):
        best_score = -math.inf
        move = None
        for m in self.available_moves():
            self.make_move(m, self.ai)
            score = self.minimax(0, False, -math.inf, math.inf)
            self.undo_move(m)
            if score > best_score:
                best_score = score
                move = m
        return move

    def play(self):
        print("Welcome to Tic-Tac-Toe!")
        print("You are 'X', AI is 'O'. Positions are numbered 0-8 like this:")
        print(" 0 | 1 | 2 ")
        print(" 3 | 4 | 5 ")
        print(" 6 | 7 | 8 ")

        self.print_board()

        while not self.is_game_over():
            # Human turn
            valid = False
            while not valid:
                try:
                    move = int(input("Your move (0-8): "))
                    if move in self.available_moves():
                        valid = True
                    else:
                        print("Invalid move, try again.")
                except ValueError:
                    print("Please enter a number between 0-8.")

            self.make_move(move, self.human)
            self.print_board()

            if self.is_game_over():
                break

            # AI turn
            print("AI is thinking...")
            ai_move = self.best_move()
            self.make_move(ai_move, self.ai)
            print(f"AI played position {ai_move}")
            self.print_board()

        # Result
        if self.check_winner(self.human):
            print("Congratulations! You win! (This shouldn't normally happen against optimal AI)")
        elif self.check_winner(self.ai):
            print("AI wins! Better luck next time.")
        else:
            print("It's a draw!")


if __name__ == "__main__":
    game = TicTacToe()
    game.play()
