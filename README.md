# chess-move-recorder

A simple Python program that records chess moves and saves them into a file.

## Features
- Move format validation (e2e4)
- Move counter
- Saves game to chess_game.txt

```
row1_white = ["rook","knight","bishop","queen","king","bishop","knight","rook"]
row2_white = ["pawn","pawn","pawn","pawn","pawn","pawn","pawn","pawn",]
row3 = []
row4 = []
row5 = []
row6 = []
row7_black = ["pawn","pawn","pawn","pawn","pawn","pawn","pawn","pawn",]
row8_black = ["rook","knight","bishop","queen","king","bishop","knight","rook"]
board = [
    row8_black,
    row7_black,
    row6,
    row5,
    row4,
    row3,
    row2_white,
    row1_white
]

color = input("Which color are you? White/Black ")
game = True
list_gamer = []
moves = 0

while game:
   answer = input("Which move did you made? ")
   answer = answer.lower()
   if len(answer) != 4:
      print("Invalid move format! Example: e2e4")
      continue

   if answer[0] not in "abcdefgh" or answer[2] not in "abcdefgh":
      print("Columns must be between a and h!")
      continue

   if answer[1] not in "12345678" or answer[3] not in "12345678":
      print("Rows must be between 1 and 8!")
      continue
   
   if answer[0:2] == answer[2:4]:
    print("You cannot move to the same square!")
    continue

   columns = "abcdefgh"

   start_col = columns.index(answer[0])
   start_row = 8 - int(answer[1])

   end_col = columns.index(answer[2])
   end_row = 8 - int(answer[3])
   print("Start:", start_row, start_col)
   print("End:", end_row, end_col)
   
   list_gamer.append(answer)
   moves += 1
   answer2 = input("Did the game finish? yes/no ")
        
   if answer2.lower() == "yes":
      print("Your color was " + color)
      print("You have made ", moves, " moves")
      print("The moves you made:",list_gamer)
      game = False

with open("chess_game.txt", "w") as file:
    file.write("Color: " + color + "\n")
    file.write("Total moves: " + str(moves) + "\n\n")

    for i in range(0, len(list_gamer), 2):
        move_number = i // 2 + 1
        white = list_gamer[i]

        if i + 1 < len(list_gamer):
            black = list_gamer[i + 1]
            line = str(move_number) + ". " + white + " " + black + "\n"
        else:
            line = str(move_number) + ". " + white + "\n"

        file.write(line)
print("Game saved to chess_game.txt")
```
