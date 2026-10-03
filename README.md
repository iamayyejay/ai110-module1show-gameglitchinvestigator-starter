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

- [ ] Describe the game's purpose.
- [ ] Detail which bugs you found.
- [ ] Explain what fixes you applied.

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

**Screenshot** *(optional)*: <!-- Insert a screenshot of your fixed, winning game here -->

## 🧪 Test Results

```
# Paste your pytest output here, e.g.:
# pytest tests/
# ========================= X passed in 0.XXs =========================
```

## 🚀 Stretch Features

- [ ] [If you choose to complete Challenge 4, describe the Enhanced UI changes here — a screenshot is optional]
