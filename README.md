# XO-game
# XO-game for homework (FPW-64 SkillFactory)


BOARD = {1: '_', 2: '_', 3: '_', 4: '_', 5: '_', 6: '_', 7: '_', 8: '_', 9: '_'}  # - Игровое поле 

PLAYERS = {
    'X': [],  # - значки - X
    'O': []   # - значки - O
}

WIN_RULES = (
    (1, 2, 3),  # - верхняя горизонтальная линия
    (4, 5, 6),  # - средняя горизонтальная линия
    (7, 8, 9),  # - нижняя горизонтальная линия
    (1, 4, 7),  # - левая вертикальная линия
    (2, 5, 8),  # - средняя вертикальная линия
    (3, 6, 9),  # - правая вертикальная линия
    (1, 5, 9),  # - \ диагональная линия 
    (3, 5, 7)   # - / диагональная линия
)


def print_board():
    print(f'{BOARD[1]} {BOARD[2]} {BOARD[3]}')
    print(f'{BOARD[4]} {BOARD[5]} {BOARD[6]}')
    print(f'{BOARD[7]} {BOARD[8]} {BOARD[9]}')


def win_check(sign):
    board_mask = set(PLAYERS[sign])
    winner = bool([True for rule in WIN_RULES if len(board_mask.intersection(rule)) == 3])
    return winner


def set_cell(cell, sign):
    BOARD[cell] = sign
    PLAYERS[sign].append(cell)


def start():
    sign = 'X'  # - current sign
    step = 1    # - current step
    while True:
        # - print current game board
        print_board()

        # - wait & check user input
        cell = input(f'\nCurrent {sign}, Type cell [1-9] or 0 for exit game: ')

        # - if 0 - exit
        if cell == '0':
            break

        # - if in range [1-9] proceed game process
        elif cell in list(map(str, range(1, 10))):
            # - If cell is not busy then set current sign to it
            if BOARD[int(cell)] == '_':
                set_cell(int(cell), sign)
            else:
                print(f'\nCell is busy... repeat input')
                continue
            # - Winner check
            if win_check(sign):
                print(f'\nSign {sign} winner!!!')
                print_board()
                break
            else:
                # - If no winner, check steps
                if step == 9:
                    print(f'\nNo more steps!!! GAME OVER')
                    print_board()
                    break
                else:
                    step += 1
            # - Replace current sign
            sign = 'O' if sign == 'X' else 'X'

        # - if otherwise print a warning and continue
        else:
            print('\nWrong input: Must be [1-9] for select cell, or 0 for exit game')
            continue


if __name__ == '__main__':
    print(f'\nWelcome to XO-game. Game play step by step, from X to O sign.')
    print(f'Use Numpad for select cell. Good luck!!!\n')
    start()
