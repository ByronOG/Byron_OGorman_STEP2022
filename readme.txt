Othello - Assignment 3

How I implemented the board, the players, the disks...

- struct player has the player's name, colour and score
-> name and colour are strings and score is an int.

- struct board_state contains the board, the player turn and their scores
-> the board is a 8x8 two dimensional character array. 
-> the player turn is an int. Where 0 = game over, 1 = black turn, 2 = white turn
-> the scores are ints

- I made both structs typedefs
- the disks are marked B, W or *. B and W are obvious, * = blank disk (not assigned a colour)

- in my main function I had several functions which initialised these components
-> startGame(2) initialised the players
-> init_board initialised the board
-> these functions are found in the initialisation c and header files

- I decided to implement these components this way as I am comfortable with structs and I believed that they would be a good implementation.


How I implemented the game logic:

- After the initialisation of the board, players, disks...

- I decided to implement a do while loop. This looped until the game was over. 
-> the game is over when board.player_turn = 0. This happens when they are no valid moves left on the board
-> this is determined by the functions next_turn and game_state which are entered after each move is made on the board.

- these functions see if either player have a valid move remaining. If not -> board.player_turn is assigned to 0 and the game is over. 

- The final board is printed to the screen. The board is updated by the function result 
-> the board state is appended to a file by the function upload_record 
-> the contents of this file are printed to the user and the program terminates


- in the do while loop in the main function: There are if/else statements to determine who's turn it is (Black or white).

- the function get_move is then entered which asks the user for their move
-> upon entering the function, the board is printed to the screen by the function print_board
-> the user enters a move from input. 
-> If it is not a legal move(letter from a to h, digit from 1 to 8), they are prompted to enter another move until the move is legal
-> the legality of the move is checked by the functions set_row and set_col. If either function return -1 the move is illegal
-> After a legal move is entered, the move is checked if it is valid - if not the user is prompted to enter another move until a valid move is entered

- the is_valid function checks if a move is valid. 
-> First it checks if the move (disk) is blank. If it isn't the function returns 0 (not valid move)
-> if it is a blank disk - a while loop is entered. This loop enters the function would_flip which checks if this disk has any bracketing disks.
-> this is checked by the function find_bracketer
-> a bracketing disk is a disk that is the same colour as the player, is on the same line as the move(disk) and has an opponent's disk inbetween.
-> if a bracketing disk is not found the move is not valid - the user has to enter another move until a bracketing disk is found
-> if a bracketing disk is found: the function make_move is entered

- make_move assigns the disk of the move to the colour of the player
-> a for loop is entered to flip all of the opponent's disks they are in line with the bracketing disk(s) by the function flip

- flip is called 8 times. This is because there are 8 possible directions that a flip can be made.
-> on each iteration a different direction is checked.
-> this is done by the use of 2 array: ROW_DIRECTIONS AND COL_DIRECTIONS.
-> these arrays contain the directions that a flip can be made and they correspond to each other.
-> (ie their first entries are [-1,0] which represents the disk that is 1 above the move)
-> if a bracketing disk is found in that direction, all of the opponent's disks that lie between the 'move' disk and the bracketing disk are flipped
-> else flip(s) are not made
-> the board is updated after each iteration which means multiple flips can be made by a single move

- once flips are done get_move is exited with the board updated.
-> next_turn is entered to check who's turn it is next
-> the do while loop (in main) ends when there are no valid moves left for either player
-> as explained earlier - the game is over and the file functions are entered.
-> the program then terminates

I decided upon this way of implementing the game logic as I drew an a3 web diagram before I started writing the code. 
This diagram helped my deicide when to branch into different directions in the program by the use of functions.
The program was not linear. By linear I mean it wasn't one set set of instructions that the program executed to manage the game.
Each 'entered' move entered different functions to determine whether the move could be made. 
Although my aproach took a large amount of code to be written, it helped me to understand what I wanted the code to do.
I made it look as neat as possible to breaking it down into modules.

