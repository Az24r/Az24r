import random
import time

class Player:
    def __init__(self, name):
        self.name = name
        self.balance = 1000
        self.in_game = True

    def play(self):
        start_time = time.time()
        while True:
            action = random.choice(['roll', 'rest', 'buy', 'sell'])
            if action == 'roll':
                roll = random.randint(1, 6) + random.randint(1, 6)
                print(f"{self.name} rolled {roll}")

                if roll == 7 or roll == 11:
                    print(f"{self.name} wins!")
                    self.balance += 500
                elif roll == 2 or roll == 3 or roll == 12:
                    print(f"{self.name} loses!")
                    self.balance -= 200
                else:
                    print(f"{self.name} gets to roll again")
                    continue

            elif action == 'rest':
                print(f"{self.name} rests for 1 second")
                time.sleep(1)

            elif action == 'buy':
                print(f"{self.name} buys an item for 100")
                self.balance -= 100

            elif action == 'sell':
                print(f"{self.name} sells an item for 50")
                self.balance += 50

            if self.balance <= 0:
                print(f"{self.name} has run out of money!")
                self.in_game = False
                break

            elapsed_time = time.time() - start_time
            if elapsed_time >= 5: # Limit game duration to 5 seconds
                break

players = [Player(f"Player {i}") for i in range(1, 6)]

while True:
    for player in players:
        if player.in_game:
            player.play()

    if not any(player.in_game for player in players):
        break
