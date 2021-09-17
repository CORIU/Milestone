# My Projects

def display_board(board):
    print('   |   |')
    print(' ' + board[7] + ' | ' + board[8] + ' | ' + board[9])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[4] + ' | ' + board[5] + ' | ' + board[6])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[1] + ' | ' + board[2] + ' | ' + board[3])
    print('   |   |')
# test_board = ['#','X','O','X','O','X','O','X','O','X']
test_board = ['#',' ',' ',' ',' ',' ',' ',' ',' ',' ']

#print(display_board(test_board))

def player_input():
    marker = ''
    while not (marker == 'X'or marker == 'O'):
        marker = input("Player1:Do you want to be X or O: ").upper()

        if marker == 'X':
            return ('X','O')

        else:
            return ('O','X')

#print(player_input())


def place_marker(board,marker,position):
   board[position] = marker


#print(place_marker(test_board," ",7))
#print(display_board(test_board))


def win_check(board,mark):
    return ((board[7] == mark and board[8] == mark and board[9] == mark or
             (board[4] == mark and board[5] == mark and board[6] == mark or
              (board[1] == mark and board[2] == mark and board[3] == mark or
               (board[7] == mark and board[4] == mark and board[1] == mark or
                (board[8] == mark and board[5] == mark and board[2] == mark or
                 (board[9] == mark and board[6] == mark and board[3] == mark or
                  (board[7] == mark and board[5] == mark and board[3] == mark or
                   (board[9] == mark and board[5] == mark and board[1] == mark)))))))))
#print(win_check(test_board,'X'))




import random

def choose_first():
    if random.randint(0,1) == 0:
        return "Player 1"
    else:
        return "Player 2"
#print(choose_first())


def space_check(board,position):
    if board[position] == ' ':
        print("returning true")
        return True
    else:
        print("returning false")
        return False

#print(space_check(test_board,2))


def full_board_check(board):
    for i in range(1,10):
        if space_check(board,i):
            return False
    return True

#print(full_board_check(test_board))


def player_choice(board):
   position = 0
   while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board,position):
       position = int(input("Choose a position 1-9: "))
   return position
#print(player_choice(test_board))

def replay():
   choice = input("Do you want to play again?Enter Yes or No")
   return choice == "Yes"


print('Welcome to Tic Tac Toe!')

while True:
    # Reset the board
    theBoard = [' '] * 10
    player1_marker, player2_marker = player_input()
    turn = choose_first()
    print(turn + ' will go first.')

    play_game = input('Are you ready to play? Enter Yes or No.')

    if play_game.lower()[0] == 'y':
        game_on = True
    else:
        game_on = False

    while game_on:
        if turn == 'Player 1':
            # Player1's turn.

            display_board(theBoard)
            position = player_choice(theBoard)
            place_marker(theBoard, player1_marker, position)

            if win_check(theBoard, player1_marker):
                display_board(theBoard)
                print('Congratulations! You have won the game!')
                game_on = False
            else:
                if full_board_check(theBoard):
                    display_board(theBoard)
                    print('The game is a draw!')
                    break
                else:
                    turn = 'Player 2'

        else:
            # Player2's turn.

            display_board(theBoard)
            position = player_choice(theBoard)
            place_marker(theBoard, player2_marker, position)

            if win_check(theBoard, player2_marker):
                display_board(theBoard)
                print('Player 2 has won!')
                game_on = False
            else:
                if full_board_check(theBoard):
                    display_board(theBoard)
                    print('The game is a draw!')
                    break
                else:
                    turn = 'Player 1'

    if not replay():
        break
        

#Rock,paper, scissors

import random

def play():
    user = input("What\'s your choice? 'r', for rock,'p' for paper,'s' for scissors"'\n')
    computer = random.choice(['r','p','s'])
    if user == computer:
        return 'It\'s a tie'
    if is_win(user,computer):
        return 'you won'
    return 'you lost!'
    #r > s,s > p, p > r
def is_win(player,opponent):
    #return True if the player wins
    if (player == 'r' and opponent == 's') or (player == 's' and opponent == 'p') \
        or (player == 'p' and opponent == 'r'):
        return True

print(play())




#Hangman game

import random
from words import words
import string

def get_valid_word(words):
    word = random.choice(words)
    while '-' in word or ' ' in word:
        word = random.choice(words)
    return word

def hangman():
    word = get_valid_word(words)
    word_letters = set(word) #letters in the word
    alphabet = set(string.ascii_uppercase)
    used_letters = set() #what the user has guessed


    lives = 6

    while len(word_letters) > 0 and lives > 0:
        print('You have', lives, 'lives left and You have used these letters'.join(used_letters))
        word_list = [letter if letter in used_letters else '-' for letter in word]
        print('current word', ' '.join(word_list))


        user_letter = input('guess a letter:').upper()
        if user_letter in alphabet-used_letters:
            used_letters.add(user_letter)
            if user_letter in word_letters:
                word_letters.remove(user_letter)
            else:
                lives  = lives - 1
                print('Letter is not in the word')

        elif user_letter in used_letters:
            print('You have already used that character')

        else:
            print('Invalid character. Please try again!')
    if lives == 0:
        print('Sorry you have died')
    else:
        print('You guessed the word',word)

print(hangman())
