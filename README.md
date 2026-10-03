# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation

You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 

- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup

1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission

1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

- [x] Describe the game's purpose.

  **Purpose:** Glitchy Guesser is a number-guessing game built with Streamlit. The game picks a secret number in a range set by the difficulty (Easy 1–20, Normal 1–100, Hard 1–50). The player has a limited number of attempts to find it, and after each guess the game says "Go HIGHER" or "Go LOWER". Points are awarded for winning quickly and deducted for wrong guesses.

  The project is also a debugging exercise. The original AI-generated version was full of bugs: hints that lied, a secret that changed, and scoring that made no sense. The goal is to find those bugs, fix them, and move the game logic into `logic_utils.py` so it can be tested with `pytest`.

- [x] Detail which bugs you found.

  1. **Lying hints:** on every even attempt `app.py` converted the secret to a string before calling `check_guess`, so the comparison fell into a string-comparison fallback and gave wrong "Higher/Lower" hints.
  2. **New Game ignored the difficulty:** it always picked a secret from 1–100, and it didn't reset the score, status or history, so a finished game couldn't be replayed.
  3. **Secret didn't match the range:** changing the difficulty kept the old secret, which could be outside the new range.
  4. **Hardcoded range message:** the prompt always said "between 1 and 100", whatever the difficulty.
  5. **Off-by-one attempts:** the attempt counter started at 1, so "Attempts left" was one too low and players lost an attempt.
  6. **Invalid input cost an attempt:** blank or non-numeric guesses were counted as attempts.
  7. **Odd scoring:** a "Too High" guess gave +5 points on even attempts, and a win scored `100 - 10 * (attempt + 1)`, which over-penalised.

- [x] Explain what fixes you applied.

  1. **Refactor:** moved `get_range_for_difficulty`, `parse_guess`, `check_guess` and `update_score` from `app.py` into `logic_utils.py`; `app.py` now imports them.
  2. **Hints:** removed the string-comparison fallback in `check_guess` and always pass the secret as an int, so hints are consistent.
  3. **New game:** added a `start_new_game()` helper that uses the selected difficulty's range and resets the secret, attempts, score, status and history. It runs on first load, when New Game is clicked, and when the difficulty changes.
  4. **Range message:** the prompt now shows the real `low` and `high`.
  5. **Attempts:** the counter starts at 0 and only increases on a valid guess.
  6. **Scoring:** "Too High" always costs 5 points, and a win scores `100 - 10 * attempt` (minimum 10).
  7. **Tests:** updated `tests/test_game_logic.py` to unpack the `(outcome, message)` tuple that `check_guess` returns, and checked the fixes by playing through the app.

## 📸 Demo Walkthrough

A sample game on **Normal** difficulty (range 1–100, 8 attempts), where the secret number is 55:

1. The game starts with "Guess a number between 1 and 100. Attempts left: 8" and a score of 0.
2. The user enters `abc`. The game shows "That is not a number." and the attempt is not used (still 8 left).
3. The user enters `40`. The game shows "📈 Go HIGHER!" (Too Low). The score drops to -5 and 7 attempts are left.
4. The user enters `70`. The game shows "📉 Go LOWER!" (Too High). The score drops to -10 and 6 attempts are left.
5. The user enters `55`. The game shows "🎉 Correct!", balloons appear, and the score becomes 60 (100 - 10 × 3 = 70 points for winning on attempt 3, added to -10).
6. The game ends: further guesses show "You already won. Start a new game to play again."
7. The user clicks **New Game**. The score, attempts and history reset, and a new secret is chosen within the current difficulty's range.
8. Switching to **Easy** also starts a fresh game, and the message changes to "Guess a number between 1 and 20."

**Screenshot**: a winning game on Normal difficulty.

![Fixed, winning game](Game%20Glitch%20Success.png)

## 🧪 Test Results

==================================================== test session starts ====================================================
platform win32 -- Python 3.11.9, pytest-9.1.1, pluggy-1.6.0
rootdir: C:\Users\inthe\Desktop\AI110\ai110-module1show-gameglitchinvestigator-starter
configfile: pytest.ini
testpaths: tests
plugins: anyio-4.15.1
collected 3 items                                                                                                            

tests\test_game_logic.py ...                                                                                           [100%]

===================================================== 3 passed in 0.02s =====================================================


## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
