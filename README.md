import random

score = 100
count = 1
numbers = {1, 2, 3}
phrases = {"play the game","play the game!","how to play the game","how to play the game?","exit",}
original_count = count
original_score = score

leaderboard = []
def show_leaderboard(board):
    print("\n===== Leaderboard =====")
    for i, (name, score) in enumerate(board[:5], start=1):
        if i == 1:
            print(f"{i}. {name} - {score}  (highscore)")
        else:
            print(f"{i}. {name} - {score}")
    print("=======================\n")

print("#" * 50)
print(" " * 20, "Welcome!", " " * 35)
print("Choose the following option:")
print("1; Play the game!")
print("2; How to Play the game?")
print("3; Exit(T-T)")
print("#" * 50)
print(" ")

while True:
    userinput = input("Enter the number of the option you chose: ").strip().lower()
    print()

    if userinput.isdigit() and int(userinput) in numbers:
        pass
    elif userinput in phrases:
        pass
    else:
        print("Invalid input(Hint: Check for typing mistakes)\n")
        continue

    if userinput == "1" or userinput == "play the game" or userinput == "play the game!":
        random_integer = random.randint(1, 100)

        while True:
            userinput1 = input(f"Attempt {count}: ").strip().lower()
            if userinput1 == "exit":
                print("Game exited\n")
                break

            elif not userinput1.isdigit():
                print("Invalid input(Hint: Enter only numbers in numbers not in words)")
            else:
                guess = int(userinput1)
                if guess < 1 or guess > 100:
                    print("Invalid input(Hint: Type the number within 1 and 100)")
                elif guess > random_integer:
                    print("Go lower")
                    count += 1
                elif guess < random_integer:
                    print("Go higher")
                    count += 1
                else:
                    score = 100 - 5*count
                    print("YOU WON!")
                    print(f"Your Score: {score}, Total Attempts: {count}")
                    count = original_count

                    name = input("Enter your name for the leaderboard: ").strip()
                    if name == "":
                        name = "Anonymous"
                    leaderboard.append((name, score))
                    leaderboard = sorted(leaderboard, key=lambda x: x[1], reverse=True)

                    show_leaderboard(leaderboard)
                    print()
                    score = original_score
                    break

    elif userinput == "2" or userinput == "how to play the game" or userinput == "how to play the game?":
        print("The computer chooses a number at random and you have to guess it.")
        print("After each guess, you'll be told 'Go higher' or 'Go lower'.")
        print("You start with 100 points. Each wrong guess loses 5 points.")
        print("Type 'exit' at any time to quit the game.")
        print("BEST OF LUCK!!!\n")

    elif userinput == "3" or userinput == "exit":
        print("Thank you for playing!")
        break

