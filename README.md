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

Exercises:
#Display Fibonacci series up to 10 terms

 def Fibonacci(n):
     fibs = [0,1]
     for i in range(2,n):
         fibs.append(fibs[i - 1] + fibs[i - 2])
     return fibs
 
 #Write a loop to find the factorial of any number    
    def factorial_num(num):
    factorial = 1
    for i in range(1,num + 1):
        factorial = factorial * i  #why factorial becomes 2??
         print("The number", num,"is",factorial)
print(factorial_num(5))

#Write a Python program that accepts a string and calculate the number of digits and letters.
def dig_let():
   str = input("Enter a string: ")
   digit = 0
   letters = 0
   for i in str:
      if i.isdigit():
         digit += 1
      elif i.isalpha():
         letters +=1
      else:
         pass
   print("The number of digit: ",digit)
   print("The number of letters: ",letters)
print(dig_let())


#Write a Python program to check whether an alphabet is a vowel or consonant.
def alphabet():
   ch = input("Input a letter from the alphabet: ")
   if(ch == 'A' or ch == 'a' or ch == 'E' or ch == 'e' or ch == 'I'or ch == 'i' or ch == 'O' or ch == 'o'
      or ch == 'U'or ch == 'u'):
      print(ch,"is a vowel")
   else:
      print(ch,"is a consonant")
print(alphabet())


#You are driving a little too fast, and a police officer stops you. Write code to compute the result,
# encoded as an int value: 0=no ticket, 1=small ticket, 2=big ticket. If speed is 60 or less, the result is 0.
# If speed is between 61 and 80 inclusive, the result is 1. If speed is 81 or more, the result is 2. Unless it is your birthday
# -- on that day, your speed can be 5 higher in all cases.
def caught_speeding(speed,is_birthday):
   while not is_birthday:
      if speed <= 60:

         return 0
      elif speed > 60 and speed < 81:
         return 1
      elif speed > 81:
         return 2
      elif is_birthday:
         return 5
   return caught_speeding(speed - 5,False)
print(caught_speeding(60,False))
print(caught_speeding(65,False))
print(caught_speeding(65,True))

# Given two strings, return True if either of the strings appears at the very end of the other string, ignoring
# # upper/lower case differences (in other words, the computation should not be "case sensitive").
# # Note: s.lower() returns the lowercase version of a string.
def end_other(a,b):
   a = a.lower()
   b = b.lower()
   return a.endswith(b) or b.endswith(a)
print(end_other('Hiabc','abc'))
print(end_other('AbC','HiaBc'))
print(end_other('abc', 'abXabc'))

# #Return the sum of the numbers in the array, except ignore sections of numbers
# # starting with a 6 and extending to the next 7 (every 6 will be followed by at least one 7). Return 0 for no numbers.
def sum67(nums):
    total = 0
    skyp = True
    for num in nums:
        if num == 6:
            skyp = False
        if skyp:
            total += num
        if num == 7:
            skyp = True
    return total

print(sum67([1,2,2]))
print(sum67([1,2,2,6,99,99,7]))
print(sum67([1,1,2,6,7,1]))


# #Create a function that takes a list of numbers between 1 and 10 (excluding one number) and returns the missing number.
def missing_number(lst):
   total = 0
   for num in range(0, len(lst)):
      total += lst[num]
   mylist = range(1,11)
   all_total = sum(mylist)
   return all_total - total

print(missing_number([1, 2, 3, 4, 6, 7, 8, 9, 10]))
print(missing_number([6, 4, 5, 8, 2, 1, 10, 7, 9]))
print(missing_number([10, 5, 1, 2, 4, 6, 8, 3, 9]))


# #An isogram is a word that has no duplicate letters.
# # Create a function that takes a string and returns either True or False depending on whether or not it's an "isogram".
def is_isogram(txt):
   for char in txt:
      if txt.upper().count(char.upper()) >= 2:
         return False


   return True




print(is_isogram('Algoritm'))
print(is_isogram('modem'))


# #Create a function that returns the list of numbers from a given range. But for multiples of three, return “Eda”
# # instead of the number and for the multiples of five, return “Bit”.
# # For numbers which are multiples of both three and five, return “EdaBit”.
def eda_bit(start,end):
   l = []
   for i in range(start, end + 1):
      if i % 5 == 0 and i % 3 == 0:
         l.append('EdaBit')
      elif i % 3 == 0:
         l.append('Eda')
      elif i % 5 == 0:
         l.append('Bit')
      else:
         l.append(i)
   return l
print(eda_bit(0,10))
print(eda_bit(14,20))
print(eda_bit(99,106))


def count_palindromes(num1,num2):
   count = 0
   for i in range(num1,num2 + 1):
      if str(i) == str(i)[::-1]:
         count +=1
   return count






print(count_palindromes(1,10))
print(count_palindromes(555,556))
print(count_palindromes(878,898))


# #In this exercise you will have to:
#
# Take a list of names.
# Add "Hello" to every name.
# Make one big string with all greetings.
# The solution should be one string with a comma in between every "Hello (Name)".

def greet_people(names):
   if len(names) == 1:
      return ', '.join(['Hello ' +name for name in names])
   elif len(names) == 2:
      return ', '.join(['Hello ' + name for name in names])
   elif len(names) >= 2:
      return ', '.join(['Hello '+ name for name in names])
print(greet_people(['Joe']))
print(greet_people(['Angela','Joe']))
print(greet_people(["Frank", "Angela", "Joe"]))


# #Create a function which returns a list of booleans, from a given number.
# # Iterating through the number one digit at a time, append True if the digit is 1 and False if it is 0.
def integer_boolean(txt):
   my_list = []
   for i in txt:
      if i == '1':
         my_list.append(True)
      elif i == '0':
         my_list.append(False)

   return my_list
print(integer_boolean("100101"))
print(integer_boolean("10"))
print(integer_boolean("001"))


# #Create a function that returns True if the first list is a subset of the second. Return False otherwise.
def is_subset(lst1,lst2):
   x = set(lst1)
   y = set(lst2)
   if x.issubset(y):
      return True
   else:
      return False
print(is_subset([3,2,5],[5,3,7,9,2]))
print(is_subset([8, 9], [7, 1, 9, 8, 4, 5, 6]))
print(is_subset([1, 2], [3, 5, 9, 1]))


def ternary(a,b):
   x = "both" if a and b else "neither" and "first" if a else "second"

   return x
print(ternary(False,True))


# #Given an unsorted list, create a function that returns the nth smallest integer
# #(the smallest integer is the first smallest, the second smallest integer is the second smallest, etc).

def nth_smallest(lst,n):
   count = 0
   l = sorted(lst)
   for i in l:
      count += 1
      if n == count:
         return i
print(nth_smallest([100, 2000, 30000, 4000000], 2))
print(nth_smallest([4, 2, 7, 6],2))
print(nth_smallest( [500, 600, 3, 652, 56, 45], 3))

#Create a function that takes an integer and returns a list from 1 to the given number, where:
#
# # # If the number can be divided evenly by 4, amplify it by 10 (i.e. return 10 times the number).
# # # If the number cannot be divided evenly by 4, simply return the number.

def amplify(num):
  l = []
  for i in range(1,num + 1):
     if i % 4 == 0:
        l.append(i * 10)
     else:
        l.append(i)
  return l


print(amplify(4))
print(amplify(3))
print(amplify(25))


# #Create a function that takes a list of numbers and return the number that's unique
def unique(lst):
  count = dict()
  for num in lst:
     if str(num) not in count:
        count[str(num)] = 1
     else:
        count[str(num)] += 1
  for i in count:
     if count[i] == 1:
        return i

  return count
print(unique([3,3,3,7,3,3]))
print(unique([0, 0, 0.77, 0, 0]))
print(unique([0, 1, 1, 1, 1, 1, 1, 1]))

# #Create a function that moves all capital letters to the front of a word
def cap_to_front(s):
   upper_case = ''
   lower_case = ''
   for i in s:
      if i.isupper():
         upper_case += i
      elif i.islower():
         lower_case += i
   return upper_case + lower_case
print(cap_to_front('hApPy'))
print(cap_to_front('moveMENT'))
print(cap_to_front('shOrtCAKE'))

# # The first and last characters must be a consonant.
# # The character in the middle must be a vowel.
def vowel_sandwich(txt):
    vowels = ['a','e','i','o','u']
    consonants = ['b','c','d','f','g',"h", "j", "k", "l", "m", "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z"]
    if len(txt) >=4:
        return False
    elif txt[0] not in consonants or txt[2] not in consonants:
       return True
    for i in vowels:
        if i == txt[1]:
            return True

    return False


print(vowel_sandwich('cat'))
print(vowel_sandwich('ear'))
print(vowel_sandwich('bake'))
print(vowel_sandwich('try'))


# #Write a function that retrieves the last n elements from a list.
def last(lst,n):
   if n == 0:
      return []

   if n <= len(lst):
      return lst[-n:]
   else:
      n > len(lst)
      return 'Invalid'


print(last([1,2,3,4,5],1))
print(last([4, 3, 9, 9, 7, 6], 3))
print(last([1, 2, 3, 4, 5], 7))
print(last([1, 2, 3, 4, 5], 2))
print(last([1, 2, 4, 5, 6, 7], 3))
print(last([1,2,3],0))

# #Write a function that takes a string, breaks it up and returns it with vowels first,
# # consonants second. For any character that's not a vowel
# # (like special characters or spaces), treat them like consonants.
def is_vowel(x):
   if x in 'aeiou':
      return True
   return False
def split(txt):
   count = 0
   lst = list(txt)
   for i in txt:
      if is_vowel(i):
         lst.pop(lst.index(i,count))
         lst.insert(count,i)
         count += 1
   return ''.join(lst)


# #Create a function that takes damage and speed (attacks per second) and returns the amount of damage after a given time

def damage(damage,speed,time):
   while damage and speed > 0:
      if time == 'second':
         return damage * speed
      elif time == 'minute':
         return damage * speed * 60
      elif time == 'hour':
         return damage * speed * 3600
   return 'Invalid'
print(damage(40,5,'second'))
print(damage(100,1,'minute'))
print(damage(2,100,'hour'))
print(damage(-4,-244,'minute'))

# Write two functions:
#
# to_list(), which converts a number to an integer list of its digits.
# to_number(), which converts a list of integers back to its number.
def to_list(num):
   res = [int(x) for x in str(num)]
   return res
def to_number(lst):
   s = [str(i) for i in (lst)]
   return ''.join(s)


print(to_list(235))
print(to_list(0))
print(to_number([2,3,5]))



# #Given a list, return True if there are more odd numbers than even numbers, otherwise return False.
def odd_even(lst):
   a = []
   b = []
   for i in lst:
      if i % 2 == 0:
         a.append(i)
      else:
         b.append(i)
   return len(b) > len(a)


print(odd_even([1, 2, 3, 4, 5, 6, 7, 8, 9]))
print(odd_even([1]))
print(odd_even([13452394823795273847528572346]))


