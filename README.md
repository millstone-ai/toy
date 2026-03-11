# toy
import random

def print_intro():
    print("\n=== TREASURE HUNT ===")
    print("You are exploring a mysterious 5x5 grid.")
    print("Somewhere on the map is treasure.")
    print("But there is also a trap.")
    print("Find the treasure before you step on the trap!\n")

def get_move():
    move = input("Move (w=up, s=down, a=left, d=right, q=quit): ").strip().lower()
    while move not in ["w", "a", "s", "d", "q"]:
        move = input("Invalid move. Use w/a/s/d/q: ").strip().lower()
    return move

def show_position(x, y, size):
    print(f"\nYou are now at position ({x + 1}, {y + 1}) on the {size}x{size} map.")

def play_game():
    size = 5
    player_x, player_y = 0, 0

    # Random treasure and trap positions
    while True:
        treasure_x = random.randint(0, size - 1)
        treasure_y = random.randint(0, size - 1)
        trap_x = random.randint(0, size - 1)
        trap_y = random.randint(0, size - 1)

        # Make sure treasure/trap are not on starting square or same square
        if (treasure_x, treasure_y) != (0, 0) and (trap_x, trap_y) != (0, 0) and (treasure_x, treasure_y) != (trap_x, trap_y):
            break

    steps = 0
    print_intro()

    while True:
        show_position(player_x, player_y, size)
        move = get_move()

        if move == "q":
            print("\nYou gave up the hunt. Game over.")
            break

        if move == "w":
            if player_y > 0:
                player_y -= 1
            else:
                print("You hit the top wall.")
        elif move == "s":
            if player_y < size - 1:
                player_y += 1
            else:
                print("You hit the bottom wall.")
        elif move == "a":
            if player_x > 0:
                player_x -= 1
            else:
                print("You hit the left wall.")
        elif move == "d":
            if player_x < size - 1:
                player_x += 1
            else:
                print("You hit the right wall.")

        steps += 1

        if (player_x, player_y) == (trap_x, trap_y):
            print("\nOh no! You stepped on the trap!")
            print(f"You survived {steps} moves.")
            break

        if (player_x, player_y) == (treasure_x, treasure_y):
            print("\nYou found the treasure!")
            print(f"You won in {steps} moves.")
            break

if __name__ == "__main__":
    play_game()
