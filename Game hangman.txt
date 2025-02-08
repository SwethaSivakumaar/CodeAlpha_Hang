import random

# List of words to choose from
word_list = ['python', 'hangman', 'developer', 'computer', 'programming', 'keyboard', 'algorithm', 'debugging']

# Function to select a random word from the list
def select_word():
    return random.choice(word_list)

# Function to display the current state of the word (with guessed letters and underscores)
def display_word(word, guessed_letters):
    displayed_word = ''.join([letter if letter in guessed_letters else '_' for letter in word])
    return displayed_word

# Function to play the Hangman game
def play_hangman():
    word = select_word()  # Select a random word
    guessed_letters = []  # List of guessed letters
    incorrect_guesses = 0  # Track the number of incorrect guesses
    max_incorrect_guesses = 6  # Set the limit on the number of incorrect guesses allowed

    print("Welcome to Hangman!")
    print("Try to guess the word, one letter at a time.")
    
    # Game loop
    while incorrect_guesses < max_incorrect_guesses:
        print("\nWord:", display_word(word, guessed_letters))
        print("Guessed Letters:", ', '.join(guessed_letters))
        print("Incorrect Guesses Left:", max_incorrect_guesses - incorrect_guesses)
        
        guess = input("Guess a letter: ").lower()

        # Check if the input is a valid letter
        if not guess.isalpha() or len(guess) != 1:
            print("Please enter a valid single letter.")
            continue

        if guess in guessed_letters:
            print("You already guessed that letter!")
            continue
        
        guessed_letters.append(guess)

        # Check if the guessed letter is in the word
        if guess in word:
            print(f"Good guess! The letter '{guess}' is in the word.")
        else:
            incorrect_guesses += 1
            print(f"Oops! The letter '{guess}' is not in the word.")
        
        # Check if the player has guessed all letters
        if all(letter in guessed_letters for letter in word):
            print(f"\nCongratulations! You guessed the word '{word}' correctly!")
            break
    else:
        print(f"\nSorry, you've run out of guesses! The word was '{word}'.")

# Start the game
play_hangman()
