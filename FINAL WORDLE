########################################
# Name: Gabriella Weis
# Collaborators (if any): Shouvik, Landon Mead, Elliot Lew
# GenAI Transcript (if any): Asked chatgpt how to streamline the show message part of my check_answer() function
# Estimated time spent (hr): 7
# Description of any added extensions:
########################################

from WordleGraphics import *  # WordleGWindow, N_ROWS, N_COLS, CORRECT_COLOR, PRESENT_COLOR, MISSING_COLOR, UNKNOWN_COLOR
from english import * # ENGLISH_WORDS, is_english_word
import random

def wordle():
    #answer = random_five_letter()
    # The main function to play the Wordle game.
    row_counter = []

    def enter_action():
        # What should happen when RETURN/ENTER is pressed.
        row = gw.get_current_row()
        check_answer(row, answer)
        
    def word_from_row(row:int) -> str:
        user_word = ""
        gw.get_current_row()
        for i in range(N_COLS):
            user_word += gw.get_square_letter(row, i)
        return(user_word)

    gw = WordleGWindow()
    gw.add_enter_listener(enter_action)

    def check_answer(row, answer):
        remaining_letters = list(answer)
        guess = word_from_row(row).lower()
        if not is_english_word(guess):
            gw.show_message("Please enter a valid English word.")
            return
        if guess in row_counter:
            gw.show_message("You already guessed that word!")
            return
        row_counter.append(guess)
        if guess == answer:
            gw.show_message("You did it!")
        else:
            if len(row_counter) < 6:
                gw.show_message("Not quite. Keep guessing!")
            else:
                gw.show_message(f"Oops! The word was actually {answer}.")

    
        # green
        for i in range(N_COLS):
            if guess[i] == answer[i]:
                gw.set_square_color(row, i, CORRECT_COLOR)
                remaining_letters[remaining_letters.index(guess[i])] = None

        # yellow + grey
        for i in range(N_COLS):
            if guess[i] == answer[i]:
                continue
            elif guess[i] in remaining_letters:
                gw.set_square_color(row, i, PRESENT_COLOR)
                remaining_letters[remaining_letters.index(guess[i])] = None
            else:
                gw.set_square_color(row, i, MISSING_COLOR)
        color_keys(row)
        gw.set_current_row(row + 1)

    # color keys accordingly
    def color_keys(row):
        guess = word_from_row(row).lower()
        for i in range(N_COLS):
            square_color = gw.get_square_color(row, i)
            key_color = gw.get_key_color(guess[i])
            if square_color == CORRECT_COLOR:
                gw.set_key_color(guess[i], CORRECT_COLOR)
            elif square_color == PRESENT_COLOR and key_color != CORRECT_COLOR:
                gw.set_key_color(guess[i], PRESENT_COLOR)
            elif key_color != CORRECT_COLOR and key_color is not PRESENT_COLOR:
                gw.set_key_color(guess[i], MISSING_COLOR)

    def random_five_letter():
        five_letters = []
        for word in ENGLISH_WORDS:
            if len(word) == 5:
                five_letters.append(word)
        answer = random.choice(five_letters)
        return answer
    answer = random_five_letter()

# Startup boilerplate
if __name__ == "__main__":
    wordle()
