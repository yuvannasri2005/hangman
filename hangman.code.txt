import random
hangman_stages = [
    """
       ------
       |    |
            |
            |
            |
            |
    """,
    """
       ------
       |    |
       O    |
            |
            |
            |
    """,
    """
       ------
       |    |
       O    |
       |    |
            |
            |
    """,
    """
       ------
       |    |
       O    |
      /|    |
            |
            |
    """,
    """
       ------
       |    |
       O    |
      /|\\   |
            |
            |
    """,
    """
       ------
       |    |
       O    |
      /|\\   |
      /     |
            |
    """,
    """
       ------
       |    |
       O    |
      /|\\   |
      / \\   |
            |
    """
]

def get_word():
    """Select a word from a predefined list."""
    words = ["python", "hangman", "challenge", "programming", "developer"]
    return random.choice(words)

def display_progress(word, guessed_letters):
    """Display the current progress of the guessed word."""
    return ' '.join(letter if letter in guessed_letters else '_' for letter in word)

def get_guess():
    """Get a valid letter guess from the player."""
    while True:
        guess = input("Guess a letter: ").strip().lower()
        if len(guess) != 1 or not guess.isalpha():
            print("Invalid input. Please enter a single letter.")
        else:
            return guess

def play_game():
    """Play a game of Hangman."""
    print("Welcome to Hangman!")
    
    word = get_word()
    guessed_letters = set()
    attempts_remaining = len(hangman_stages) - 1
    
    while attempts_remaining >= 0:
        print(hangman_stages[len(hangman_stages) - 1 - attempts_remaining])
        print("\nWord to guess: ", display_progress(word, guessed_letters))
        print(f"Remaining attempts: {attempts_remaining}")
        
        guess = get_guess()
        
        if guess in guessed_letters:
            print("You've already guessed that letter.")
            continue
        
        guessed_letters.add(guess)
        
        if guess in word:
            print("Good guess!")
        else:
            print("Wrong guess!")
            attempts_remaining -= 1
        
        if set(word) <= guessed_letters:
            print("Congratulations! You've guessed the word:", word)
            break
        
        if attempts_remaining < 0:
            print(hangman_stages[-1])
            print(f"Game over! The word was: {word}")
            break

    if input("Do you want to play again? (yes/no): ").strip().lower() == 'yes':
        play_game()

if __name__ == "__main__":
    play_game()
