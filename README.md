# Импортируем библиотеку random для выбора случайного хода
import random

# Создаем пустую доску 3 на 3
board = [[" " for _ in range(3)] for _ in range(3)]

# Определяем символы для игроков
player = "X"
computer = "O"

# Определяем функцию для вывода доски на экран
def print_board():
    print("  0 1 2")
    for i in range(3):
        print(i, end=" ")
        for j in range(3):
            print(board[i][j], end=" ")
        print()

# Определяем функцию для проверки, есть ли победитель
def check_winner():
    # Проверяем горизонтальные линии
    for i in range(3):
        if board[i][0] == board[i][1] == board[i][2] != " ":
            return board[i][0]
    # Проверяем вертикальные линии
    for j in range(3):
        if board[0][j] == board[1][j] == board[2][j] != " ":
            return board[0][j]
    # Проверяем диагональные линии
    if board[0][0] == board[1][1] == board[2][2] != " ":
        return board[0][0]
    if board[0][2] == board[1][1] == board[2][0] != " ":
        return board[0][2]
    # Проверяем, есть ли свободные клетки
    for i in range(3):
        for j in range(3):
            if board[i][j] == " ":
                return None
    # Если все клетки заняты, объявляем ничью
    return " "

# Определяем функцию для хода игрока
def player_move():
    # Запрашиваем координаты клетки от игрока
    print("Ваш ход. Введите номер строки и столбца через пробел.")
    row, col = map(int, input().split())
    # Проверяем, что координаты корректны и клетка свободна
    while not (0 <= row <= 2 and 0 <= col <= 2 and board[row][col] == " "):
        print("Неверный ход. Попробуйте еще раз.")
        row, col = map(int, input().split())
    # Заполняем клетку символом игрока
    board[row][col] = player

# Определяем функцию для хода компьютера
def computer_move():
    # Выбираем случайную свободную клетку
    print("Ход компьютера.")
    row = random.randint(0, 2)
    col = random.randint(0, 2)
    while board[row][col] != " ":
        row = random.randint(0, 2)
        col = random.randint(0, 2)
    # Заполняем клетку символом компьютера
    board[row][col] = computer

# Начинаем игру
print("Добро пожаловать в игру крестики нолики!")
print("Вы играете за X, компьютер играет за O.")
print_board()

# Повторяем ходы, пока не будет победителя или ничьи
while True:
    # Ход игрока
    player_move()
    print_board()
    # Проверяем, есть ли победитель
    winner = check_winner()
    if winner == player:
        print("Вы выиграли!")
        break
    elif winner == computer:
        print("Вы проиграли!")
        break
    elif winner == " ":
        print("Ничья!")
        break
    # Ход компьютера
    computer_move()
    print_board()
    # Проверяем, есть ли победитель
    winner = check_winner()
    if winner == player:
        print("Вы выиграли!")
        break
    elif winner == computer:
        print("Вы проиграли!")
        break
    elif winner == " ":
        print("Ничья!")
        break

