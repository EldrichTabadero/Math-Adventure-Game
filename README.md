# Math-Adventure-Game

import random

def generate_problem(level):
    max_value = 10 * level

    if level == 1:
        operators = ['+', '-']
        num_operators = 1
    elif level == 2:
        operators = ['+', '-', '*']
        num_operators = 2
    else:
        operators = ['+', '-', '*', '/']
        num_operators = 3

    expression = str(random.randint(1, max_value))
    correct_answer = int(expression)

    for _ in range(num_operators):
        operator = random.choice(operators)
        next_number = random.randint(1, max_value)
        
        if operator == '/':
            next_number = correct_answer * next_number
        
        expression += f" {operator} {next_number}"
        correct_answer = eval(expression)

        correct_answer = round(correct_answer, 1)

    return expression, correct_answer

def play_game():
    print("Welcome, brave hero, to the Math Adventure Game.")
    print("Solve all the math problems to defeat the enemies and conquer each level.\n")
    print("If you succeed, a great treasure awaits you: the legendary One Piece!\n")

    score = 0
    health = 3
    rounds = 3

    for level in range(1, 4):
        level_score = 0

        if level == 1:
            print(f"--- Level {level} --- The Dark Forest ---")
        elif level == 2:
            print(f"--- Level {level} --- The Mystic Mountains ---")
        else:
            print(f"--- Level {level} --- The Dragon's Lair ---")

        print(f"Enemies grow stronger! You have {health} health points.\n")

        for i in range(1, rounds + 1):
            print(f"--- Enemy {i} ---")
            expression, correct_answer = generate_problem(level)
            print(f"Solve: {expression}")

            try:
                player_answer = float(input("Your answer: "))
            except ValueError:
                print("Invalid input! Please enter a number.\n")
                continue
          
            if player_answer == correct_answer:
                print("Correct! You defeated an enemy!")
                score += 1
                level_score += 1
            else:
                print(f"Incorrect. The correct answer was {correct_answer}.")
                health -= 1
                print(f"You've been hit! Health remaining: {health}")

            if health <= 0:
                print("\nOh no! You have fallen in battle.")
                print("Game over, Better Luck next time, brave hero!")
                return

            print()

        while True:
            print(f"\n--- Level {level} Boss Battle! ---")
            expression, correct_answer = generate_problem(level + 1)
            print(f"The Boss roars: Solve {expression} to proceed!")

            try:
                player_answer = float(input("Your answer: "))
            except ValueError:
                print("Invalid input! Please enter a number.\n")
                player_answer = None

            if player_answer == correct_answer:
                print("You defeated the Boss! Level Cleared!")
                health += 1
                level_score += 1
                break
            else:
                print(f"The Boss struck back! The correct answer was {correct_answer}.")
                health -= 2
                print(f"Health remaining: {health}")

            if health <= 0:
                print("The Boss overpowered you!... Game over!\n")
                return

        if level_score == rounds + 1:
            print("You have earned a magic potion for perfect answers! +1 Health!")
            health += 1

        print(f"Congratulations! You've conquered Level {level}!\n")

        if level < 3:
            while True:
                continue_game = input("Would you like to continue to the next level? (yes/no): ").strip().lower()
                if continue_game == 'yes':
                    break
                elif continue_game == 'no':
                    print(f"\nAdventure Complete! Your final score is {score} out of a possible {rounds * 3 + 6}.")
                    if health >= 3:
                        print("You finished strong with health to spare! A true hero!")
                    elif health > 0:
                        print("You made it through, but it was a close call! Well done!")
                    else:
                        print("You fell at the final moment, but your journey is remembered.")
                    print("Thanks for playing the Math Adventure Quest!")
                    return
                else:
                    print("Invalid input! Please enter 'yes' or 'no'.\n")

    print(f"\nAdventure complete! Your final score is {score} out of a possible {rounds * 3 + 6}.")
    if health >= 3:
        print("You finished strong with health to spare! A true hero!")
    elif health > 0:
        print("You made it through, but it was a close call! Well done!")
    else:
        print("You fell at the final moment, but your journey is remembered.")
    
    print("Thanks for playing the Math Adventure Quest!")

play_game()
