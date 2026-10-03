# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
**When I first ran the game, I guessed the number 100 and it said it was    "TOO HIGH" and to "GO HIGHER!". I also had to hit "Submit Guess" twice whenever Iwanted to submit a number to guess.** 


**Bug Reproduction Log**

Document at least 3 bugs you found. Add rows as needed.

**Bug 1: Incorrect “Go Higher” / “Go Lower” Feedback**
**Expected:** The “Go Higher” and “Go Lower” messages should accurately indicate whether the user’s guess is above or below the correct number.

**Actual:** The game displays “Go Higher” after every guess, even when the user’s guess is incorrect in the opposite direction.

**Bug 2: “New Game” Does Not Properly Reset the Game**
**Expected:** Selecting “New Game” should reset the current game and give the user the designated number of attempts again.

**Actual:** After selecting “New Game” and entering another guess, the “Game over.” message continues to appear instead of starting a fresh game.

**Bug 3: Incorrect Attempts Remaining Display**
**Expected:** The number shown next to “Attempts Left:” should accurately reflect how many guesses the user has remaining.

**Actual:** When the display shows “Attempts left: 1,” the game immediately outputs “Out of attempts!” instead of allowing the user to use their final attempt.

**Bug 4: Missing/Incorrect Number Range**
**Expected:** The range shown on the left panel should clearly identify the numbers that the user can choose from when making a guess.

**Actual:** The range does not properly communicate the valid range of numbers available to the user.


## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)? **Claude Code**
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result). **Claude suggested that the "Guess a number between 1 and 100" message is hardcoded and ignores the difficulty range. So I changed the difficulty and the number range did not change**
- Give one example of an AI suggestion you did not accept as written (including what the AI suggested, why you rejected or changed it, and how you verified your version). It does not have to be a suggestion that was wrong: over-engineered, out of scope, harder to read, or a poor fit for this codebase all count. **Sometimes Claude would suggest the same changes twice but just worded differently and I would hgave to catch it before it over-corrected it self or changed code after it had already fixed it.**

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed? **If I ran it in the browser and it was no longer broken, I was sure it was fixed.**
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code. **I ran pytest and it showed that the four NotImplementedError stubs in logic_utils.py needed to be replaced with the real functions from app.py.**
- Did AI help you design or understand any tests? How? **Yes, Claude helped me design a test that would give it a wrong guess and guess something that wasn't a number such as "abc".**

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit? **Streamlit is kind of like a website that rebuilds itself everytime you interact with it. When you click a button or enter text, Streamlit runs the Python script from the beginning again.** 

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects? **One habit that I want to reuse in the future is to ask Claude to make test for me to run with pytest because sometimes it is hard to think of paramters to test.**
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task? **One thing I would do differently is not depend so much on Claude to code.**
- In one or two sentences, describe how this project changed the way you think about AI generated code. **This project makes me think more highly of AI generated code and makes me believe it will be more reliable in the future.** 
