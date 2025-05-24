import random

class NumberGuessingGame:
    def __init__(self):
        self.target_number = self.generate_target_number()
        self.max_attempts = 20
        self.attempts = 0
        self.guess_history = []
        self.game_won = False

    def generate_target_number(self):
        """Generate a 5-digit number with non-repetitive digits"""
        digits = list("0123456789")
        return ''.join(random.sample(digits, 5))

    def validate_input(self, guess):
        """Check if the input is valid"""
        if len(guess) != 5:
            return False, "Please enter a 5-digit number!"
        if not guess.isdigit():
            return False, "Only digits are allowed!"
        if len(set(guess)) != 5:
            return False, "All digits must be non-repetitive!"
        return True, ""

    def analyze_guess(self, guess):
        target = self.target_number
        correct_position = 0  
        correct_number = 0    
        wrong_number = 0      

        for i in range(5):
            if guess[i] == target[i]:
                correct_position += 1

        for digit in guess:
            if digit in target:
                correct_number += 1

        correct_but_wrong_position = correct_number - correct_position
        wrong_number = 5 - correct_number

        return correct_position, correct_but_wrong_position, wrong_number

    def get_feedback(self, a, b, c):
        feedback = f"{a}A{b}B{c}C"
        return feedback

    def display_welcome(self):
        print("🎮 Welcome to the 5-digit Number Guessing Game!")
        print("=" * 60)
        print("📋 Rules:")
        print("• The system has generated a 5-digit number with non-repetitive digits.")
        print("• You have 20 attempts to guess it.")
        print("• After each guess, feedback is given:")
        print("  - A: Correct digit and correct position")
        print("  - B: Correct digit but wrong position") 
        print("  - C: Digit not in the target number")
        print("• Example: 2A1B2C means 2 correct positions, 1 correct digit wrong place, 2 incorrect digits")
        print("=" * 60)
        print("🎯 Let’s begin! Enter your first guess:")
        print()

    def play_game(self):
        self.display_welcome()

        while self.attempts < self.max_attempts and not self.game_won:
            self.attempts += 1
            print(f"Attempt {self.attempts} (Remaining: {self.max_attempts - self.attempts}):")

            guess = input("Enter your 5-digit non-repetitive number: ").strip()
            is_valid, error_msg = self.validate_input(guess)
            if not is_valid:
                print(f"❌ {error_msg}")
                self.attempts -= 1  
                continue

            a, b, c = self.analyze_guess(guess)
            feedback = self.get_feedback(a, b, c)

            self.guess_history.append({
                'attempt': self.attempts,
                'guess': guess,
                'feedback': feedback,
            })

            print(f"Feedback: {feedback}")

            if a == 5:
                self.game_won = True
                print(f"🎉 Congratulations! You guessed the number in {self.attempts} attempts!")
                print(f"🎯 The correct number was: {self.target_number}")
                break

            print("-" * 60)

        if not self.game_won:
            print(f"😔 You didn't guess the number in {self.max_attempts} attempts.")
            print(f"🎯 The correct number was: {self.target_number}")

    def print_game_report(self):
        print("\n" + "=" * 60)
        print("📊 Game Report")
        print("=" * 60)
        print(f"🎯 Target Number: {self.target_number}")
        print(f"🎮 Game Result: {'Victory 🎉' if self.game_won else 'Defeat 😔'}")
        print(f"🔢 Total Attempts: {self.attempts}")
        print(f"⏱️  Attempts Used: {self.attempts}/{self.max_attempts}")

        if self.game_won:
            success_rate = (self.max_attempts - self.attempts + 1) / self.max_attempts * 100
            print(f"📈 Efficiency Score: {success_rate:.1f}%")

        print("\n📝 Guess History:")
        print("-" * 60)
        print(f"{'Try':<4} {'Guess':<8} {'Feedback':<8}")
        print("-" * 60)

        for record in self.guess_history:
            print(f"{record['attempt']:<4} {record['guess']:<8} {record['feedback']:<8}")

        print("-" * 60)

        if len(self.guess_history) > 0:
            print("\n📈 Stats:")
            total_a = sum(int(record['feedback'].split('A')[0]) for record in self.guess_history)
            total_b = sum(int(record['feedback'].split('A')[1].split('B')[0]) for record in self.guess_history)
            total_c = sum(int(record['feedback'].split('B')[1].split('C')[0]) for record in self.guess_history)

            print(f"• Total correct positions (A): {total_a}")
            print(f"• Total correct digits, wrong position (B): {total_b}")
            print(f"• Total incorrect digits (C): {total_c}")

            if self.attempts > 0:
                avg_a = total_a / self.attempts
                print(f"• Average correct positions per guess: {avg_a:.1f}")

def main():

    while True:
        game = NumberGuessingGame()
        game.play_game()
        game.print_game_report()

        while True:
            play_again = input("\n🔄 Play again? (y/n): ").strip().lower()
            if play_again in ['y', 'yes']:
                print("\n🎮 Starting a new game...\n")
                break
            elif play_again in ['n', 'no']:
                print("👋 Thanks for playing. Goodbye!")
                return
            else:
                print("❌ Please enter y or n")

if __name__ == "__main__":
    main()
